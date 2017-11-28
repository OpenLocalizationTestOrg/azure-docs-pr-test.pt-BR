---
title: "aaaCreate um aplicativo web no Azure que se conecta tooMongoDB em execução em uma máquina virtual"
description: "Um tutorial que ensina como toouse Git toodeploy um tooAzure do aplicativo ASP.NET do serviço de aplicativo, conectadas tooMongoDB em uma máquina Virtual do Azure."
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
ms.openlocfilehash: 1f5f42c28c3c294d92c9ebf1499374931d47c010
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-in-azure-that-connects-toomongodb-running-on-a-virtual-machine"></a><span data-ttu-id="f3010-103">Criar um aplicativo web no Azure que se conecta tooMongoDB em execução em uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="f3010-103">Create a web app in Azure that connects tooMongoDB running on a virtual machine</span></span>
<span data-ttu-id="f3010-104">Usando o Git, você pode implantar um aplicativo de ASP.NET tooAzure aplicativos de Web do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f3010-104">Using Git, you can deploy an ASP.NET application tooAzure App Service Web Apps.</span></span> <span data-ttu-id="f3010-105">Neste tutorial, você criará um front-end ASP.NET MVC simples aplicativo de lista de tarefas que se conecta o banco de dados do MongoDB tooa executado em uma máquina virtual no Azure.</span><span class="sxs-lookup"><span data-stu-id="f3010-105">In this tutorial, you will build a simple front-end ASP.NET MVC task list application that connects tooa MongoDB database running on a virtual machine in Azure.</span></span>  <span data-ttu-id="f3010-106">[O MongoDB][MongoDB] é um popular banco de dados NoSQL de código-fonte aberto e de alto desempenho.</span><span class="sxs-lookup"><span data-stu-id="f3010-106">[MongoDB][MongoDB] is a popular open source, high performance NoSQL database.</span></span> <span data-ttu-id="f3010-107">Depois de executar e testar Olá ASP.NET aplicativo no computador de desenvolvimento, você fará o upload Olá aplicativo tooApp aplicativos Web do serviço usando o Git.</span><span class="sxs-lookup"><span data-stu-id="f3010-107">After running and testing hello ASP.NET application on your development computer, you will upload hello application tooApp Service Web Apps using Git.</span></span>

> [!NOTE]
> <span data-ttu-id="f3010-108">Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f3010-108">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="f3010-109">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="f3010-109">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="background-knowledge"></a><span data-ttu-id="f3010-110">Conhecimento prévio</span><span class="sxs-lookup"><span data-stu-id="f3010-110">Background knowledge</span></span>
<span data-ttu-id="f3010-111">Conhecimento da seguinte Olá é útil para este tutorial, no entanto, não é necessário:</span><span class="sxs-lookup"><span data-stu-id="f3010-111">Knowledge of hello following is useful for this tutorial, though not required:</span></span>

* <span data-ttu-id="f3010-112">driver de saudação c# para o MongoDB.</span><span class="sxs-lookup"><span data-stu-id="f3010-112">hello C# driver for MongoDB.</span></span> <span data-ttu-id="f3010-113">Para obter mais informações sobre como desenvolver aplicativos c# contra MongoDB, consulte Olá MongoDB [Center de linguagem CSharp][MongoC#LangCenter].</span><span class="sxs-lookup"><span data-stu-id="f3010-113">For more information on developing C# applications against MongoDB, see hello MongoDB [CSharp Language Center][MongoC#LangCenter].</span></span> 
* <span data-ttu-id="f3010-114">estrutura de aplicativo web do ASP .NET Hello.</span><span class="sxs-lookup"><span data-stu-id="f3010-114">hello ASP .NET web application framework.</span></span> <span data-ttu-id="f3010-115">Você pode aprender tudo sobre ele no hello [site ASP.net][ASP.NET].</span><span class="sxs-lookup"><span data-stu-id="f3010-115">You can learn all about it at hello [ASP.net website][ASP.NET].</span></span>
* <span data-ttu-id="f3010-116">estrutura de aplicativo web do ASP .NET MVC Hello.</span><span class="sxs-lookup"><span data-stu-id="f3010-116">hello ASP .NET MVC web application framework.</span></span> <span data-ttu-id="f3010-117">Você pode aprender tudo sobre ele no hello [site ASP.NET MVC][MVCWebSite].</span><span class="sxs-lookup"><span data-stu-id="f3010-117">You can learn all about it at hello [ASP.NET MVC website][MVCWebSite].</span></span>
* <span data-ttu-id="f3010-118">Azure.</span><span class="sxs-lookup"><span data-stu-id="f3010-118">Azure.</span></span> <span data-ttu-id="f3010-119">Você pode começar lendo em [Azure][WindowsAzure].</span><span class="sxs-lookup"><span data-stu-id="f3010-119">You can get started reading at [Azure][WindowsAzure].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f3010-120">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f3010-120">Prerequisites</span></span>
* <span data-ttu-id="f3010-121">[Visual Studio Express 2013 para Web][VSEWeb] ou [Visual Studio 2013][VSUlt]</span><span class="sxs-lookup"><span data-stu-id="f3010-121">[Visual Studio Express 2013 for Web][VSEWeb] or [Visual Studio 2013][VSUlt]</span></span>
* [<span data-ttu-id="f3010-122">SDK do Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="f3010-122">Azure SDK for .NET</span></span>](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409)
* <span data-ttu-id="f3010-123">Uma assinatura ativa do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="f3010-123">An active Microsoft Azure subscription</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<a id="virtualmachine"></a> 

## <a name="create-a-virtual-machine-and-install-mongodb"></a><span data-ttu-id="f3010-124">Criar uma máquina virtual e instalar MongoDB</span><span class="sxs-lookup"><span data-stu-id="f3010-124">Create a virtual machine and install MongoDB</span></span>
<span data-ttu-id="f3010-125">Este tutorial supõe que você tenha criado uma máquina virtual no Azure.</span><span class="sxs-lookup"><span data-stu-id="f3010-125">This tutorial assumes you have created a virtual machine in Azure.</span></span> <span data-ttu-id="f3010-126">Depois de criar a máquina virtual de saudação é necessário tooinstall MongoDB na máquina virtual de saudação:</span><span class="sxs-lookup"><span data-stu-id="f3010-126">After creating hello virtual machine you need tooinstall MongoDB on hello virtual machine:</span></span>

* <span data-ttu-id="f3010-127">toocreate uma máquina virtual do Windows e instale o MongoDB, consulte [MongoDB instalar em uma máquina virtual executando o Windows Server no Azure][InstallMongoOnWindowsVM].</span><span class="sxs-lookup"><span data-stu-id="f3010-127">toocreate a Windows virtual machine and install MongoDB, see [Install MongoDB on a virtual machine running Windows Server in Azure][InstallMongoOnWindowsVM].</span></span>

<span data-ttu-id="f3010-128">Depois que você criou a máquina virtual de saudação no Azure e instalado o MongoDB, ser se tooremember Olá nome DNS da máquina virtual de saudação ("testlinuxvm.cloudapp.net", por exemplo) e a porta externa Olá para o MongoDB que você especificou no ponto de extremidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="f3010-128">After you have created hello virtual machine in Azure and installed MongoDB, be sure tooremember hello DNS name of hello virtual machine ("testlinuxvm.cloudapp.net", for example) and hello external port for MongoDB that you specified in hello endpoint.</span></span>  <span data-ttu-id="f3010-129">Você precisará dessas informações posteriormente no tutorial de saudação.</span><span class="sxs-lookup"><span data-stu-id="f3010-129">You will need this information later in hello tutorial.</span></span>

<a id="createapp"></a>

## <a name="create-hello-application"></a><span data-ttu-id="f3010-130">Criar um aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="f3010-130">Create hello application</span></span>
<span data-ttu-id="f3010-131">Nesta seção você criará um aplicativo ASP.NET chamado "Minha lista de tarefas" usando o Visual Studio e executar uma implantação inicial de tooAzure aplicativos de Web do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f3010-131">In this section you will create an ASP.NET application called "My Task List" by using Visual Studio and perform an initial deployment tooAzure App Service Web Apps.</span></span> <span data-ttu-id="f3010-132">Você executará aplicativo hello localmente, mas ele se conectará tooyour máquina virtual do Azure e usar a instância do MongoDB Olá que você criou nele.</span><span class="sxs-lookup"><span data-stu-id="f3010-132">You will run hello application locally, but it will connect tooyour virtual machine on Azure and use hello MongoDB instance that you created there.</span></span>

1. <span data-ttu-id="f3010-133">No Visual Studio, clique em **Novo Projeto**.</span><span class="sxs-lookup"><span data-stu-id="f3010-133">In Visual Studio, click **New Project**.</span></span>
   
    ![Iniciar página Novo Projeto][StartPageNewProject]
2. <span data-ttu-id="f3010-135">Em Olá **novo projeto** janela, no painel esquerdo hello, selecione **Visual C#**e, em seguida, selecione **Web**.</span><span class="sxs-lookup"><span data-stu-id="f3010-135">In hello **New Project** window, in hello left pane, select **Visual C#**, and then select **Web**.</span></span> <span data-ttu-id="f3010-136">No painel do meio hello, selecione **aplicativo Web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="f3010-136">In hello middle pane, select **ASP.NET  Web Application**.</span></span> <span data-ttu-id="f3010-137">Na parte inferior do hello, nomeie o projeto "MyTaskListApp" e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="f3010-137">At hello bottom, name your project "MyTaskListApp," and then click **OK**.</span></span>
   
    ![Caixa de diálogo Novo Projeto][NewProjectMyTaskListApp]
3. <span data-ttu-id="f3010-139">Em Olá **novo projeto ASP.NET** caixa de diálogo, selecione **MVC**e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="f3010-139">In hello **New ASP.NET Project** dialog box, select **MVC**, and then click **OK**.</span></span>
   
    ![Selecionar modelo do MVC][VS2013SelectMVCTemplate]
4. <span data-ttu-id="f3010-141">Se você não tiver entrado no Microsoft Azure, será solicitado toosign no.</span><span class="sxs-lookup"><span data-stu-id="f3010-141">If you aren't already signed into Microsoft Azure, you will be prompted toosign in.</span></span> <span data-ttu-id="f3010-142">Siga Olá prompts toosign no Azure.</span><span class="sxs-lookup"><span data-stu-id="f3010-142">Follow hello prompts toosign into Azure.</span></span>
5. <span data-ttu-id="f3010-143">Depois de se conectar, você poderá começar a configurar seu aplicativo Web do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f3010-143">Once you are signed in, you can start configuring your App Service web app.</span></span> <span data-ttu-id="f3010-144">Especificar Olá **nome do aplicativo Web**, **plano de serviço de aplicativo**, **grupo de recursos**, e **região**, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="f3010-144">Specify hello **Web App name**, **App Service plan**, **Resource group**, and **Region**, then click **Create**.</span></span>
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSConfigureWebAppSettings.png)
6. <span data-ttu-id="f3010-145">Depois de concluir a criação do projeto hello, aguarde Olá web aplicativo toobe criado no serviço de aplicativo do Azure, conforme indicado no hello **atividade de serviço de aplicativo do Azure** janela.</span><span class="sxs-lookup"><span data-stu-id="f3010-145">After hello project creation completes, wait for hello web app toobe created in Azure App Service as indicated in hello **Azure App Service Activity** window.</span></span> <span data-ttu-id="f3010-146">Em seguida, clique em **MyTaskListApp publicar toothis aplicativo Web agora**.</span><span class="sxs-lookup"><span data-stu-id="f3010-146">Then, click **Publish MyTaskListApp toothis Web App now**.</span></span>
7. <span data-ttu-id="f3010-147">Clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="f3010-147">Click **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSPublishWeb.png)
   
    <span data-ttu-id="f3010-148">Depois que o aplicativo do ASP.NET padrão é publicado tooAzure aplicativos de Web do serviço de aplicativo, ele será iniciado no navegador de saudação.</span><span class="sxs-lookup"><span data-stu-id="f3010-148">Once your default ASP.NET application is published tooAzure App Service Web Apps, it will be launched in hello browser.</span></span>

## <a name="install-hello-mongodb-c-driver"></a><span data-ttu-id="f3010-149">Instalar Olá MongoDB c# driver</span><span class="sxs-lookup"><span data-stu-id="f3010-149">Install hello MongoDB C# driver</span></span>
<span data-ttu-id="f3010-150">MongoDB oferece suporte a cliente c# aplicativos por meio de um driver, que é necessário tooinstall em seu computador de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="f3010-150">MongoDB offers client-side support for C# applications through a driver, which you need tooinstall on your local development computer.</span></span> <span data-ttu-id="f3010-151">Olá c# driver está disponível através do NuGet.</span><span class="sxs-lookup"><span data-stu-id="f3010-151">hello C# driver is available through NuGet.</span></span>

<span data-ttu-id="f3010-152">Olá tooinstall MongoDB c# driver:</span><span class="sxs-lookup"><span data-stu-id="f3010-152">tooinstall hello MongoDB C# driver:</span></span>

1. <span data-ttu-id="f3010-153">Em **Gerenciador de soluções**, Olá atalho **MyTaskListApp** do projeto e selecione **NuGetPackages gerenciar**.</span><span class="sxs-lookup"><span data-stu-id="f3010-153">In **Solution Explorer**, right-click hello **MyTaskListApp** project and select **Manage NuGetPackages**.</span></span>
   
    ![Gerenciar Pacotes NuGet][VS2013ManageNuGetPackages]
2. <span data-ttu-id="f3010-155">Em Olá **gerenciar pacotes NuGet** no painel esquerdo do hello, clique em **Online**.</span><span class="sxs-lookup"><span data-stu-id="f3010-155">In hello **Manage NuGet Packages** window, in hello left pane, click **Online**.</span></span> <span data-ttu-id="f3010-156">Em Olá **Pesquisar Online** em saudação à direita, digite "mongodb.driver".</span><span class="sxs-lookup"><span data-stu-id="f3010-156">In hello **Search Online** box on hello right, type "mongodb.driver".</span></span>  <span data-ttu-id="f3010-157">Clique em **instalar** tooinstall driver de saudação.</span><span class="sxs-lookup"><span data-stu-id="f3010-157">Click **Install** tooinstall hello driver.</span></span>
   
    ![Procurar o driver do C# para MongoDB][SearchforMongoDBCSharpDriver]
3. <span data-ttu-id="f3010-159">Clique em **aceito** tooaccept Olá 10gen, Inc. termos de licença.</span><span class="sxs-lookup"><span data-stu-id="f3010-159">Click **I Accept** tooaccept hello 10gen, Inc. license terms.</span></span>
4. <span data-ttu-id="f3010-160">Clique em **fechar** depois Olá driver instalado.</span><span class="sxs-lookup"><span data-stu-id="f3010-160">Click **Close** after hello driver has installed.</span></span>
    <span data-ttu-id="f3010-161">![Driver do C# para MongoDB instalado][MongoDBCsharpDriverInstalled]</span><span class="sxs-lookup"><span data-stu-id="f3010-161">![MongoDB C# Driver Installed][MongoDBCsharpDriverInstalled]</span></span>

<span data-ttu-id="f3010-162">Olá MongoDB c# driver agora está instalado.</span><span class="sxs-lookup"><span data-stu-id="f3010-162">hello MongoDB C# driver is now installed.</span></span>  <span data-ttu-id="f3010-163">Referências toohello **MongoDB.Bson**, **MongoDB.Driver**, e **MongoDB.Driver.Core** bibliotecas foram adicionadas toohello projeto.</span><span class="sxs-lookup"><span data-stu-id="f3010-163">References toohello **MongoDB.Bson**, **MongoDB.Driver**, and **MongoDB.Driver.Core**  libraries have been added toohello project.</span></span>

![Referências do driver do C# para MongoDB][MongoDBCSharpDriverReferences]

## <a name="add-a-model"></a><span data-ttu-id="f3010-165">Adicionar um modelo</span><span class="sxs-lookup"><span data-stu-id="f3010-165">Add a model</span></span>
<span data-ttu-id="f3010-166">Em **Solution Explorer**, Olá do botão direito do mouse *modelos* pasta e **adicionar** um novo **classe** e nomeie-o *TaskModel.cs* .</span><span class="sxs-lookup"><span data-stu-id="f3010-166">In **Solution Explorer**, right-click hello *Models* folder and **Add** a new **Class** and name it *TaskModel.cs*.</span></span>  <span data-ttu-id="f3010-167">Em *TaskModel.cs*, substitua código existente Olá Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="f3010-167">In *TaskModel.cs*, replace hello existing code with hello following code:</span></span>

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

## <a name="add-hello-data-access-layer"></a><span data-ttu-id="f3010-168">Adicionar camada de acesso a dados Olá</span><span class="sxs-lookup"><span data-stu-id="f3010-168">Add hello data access layer</span></span>
<span data-ttu-id="f3010-169">Em **Solution Explorer**, Olá do botão direito do mouse *MyTaskListApp* projeto e **adicionar** um **nova pasta** chamado *DAL*.</span><span class="sxs-lookup"><span data-stu-id="f3010-169">In **Solution Explorer**, right-click hello *MyTaskListApp* project and **Add** a **New Folder** named *DAL*.</span></span>  <span data-ttu-id="f3010-170">Saudação de atalho *DAL* pasta e **adicionar** um novo **classe**.</span><span class="sxs-lookup"><span data-stu-id="f3010-170">Right-click hello *DAL* folder and **Add** a new **Class**.</span></span> <span data-ttu-id="f3010-171">Arquivo de nome de classe Olá *Dal.cs*.</span><span class="sxs-lookup"><span data-stu-id="f3010-171">Name hello class file *Dal.cs*.</span></span>  <span data-ttu-id="f3010-172">Em *Dal.cs*, substitua código existente Olá Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="f3010-172">In *Dal.cs*, replace hello existing code with hello following code:</span></span>

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

            // toodo: update hello connection string with hello DNS name
            // or IP address of your server. 
            //For example, "mongodb://testlinux.cloudapp.net"
            private string connectionString = "mongodb://mongodbsrv20151211.cloudapp.net";

            // This sample uses a database named "Tasks" and a 
            //collection named "TasksList".  hello database and collection 
            //will be automatically created if they don't already exist.
            private string dbName = "Tasks";
            private string collectionName = "TasksList";

            // Default constructor.        
            public Dal()
            {
            }

            // Gets all Task items from hello MongoDB server.        
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

            // Creates a Task and inserts it into hello collection in MongoDB.
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

## <a name="add-a-controller"></a><span data-ttu-id="f3010-173">Adicionar um controlador</span><span class="sxs-lookup"><span data-stu-id="f3010-173">Add a controller</span></span>
<span data-ttu-id="f3010-174">Olá abrir *Controllers\HomeController.cs* arquivo **Gerenciador de soluções** e substitua código existente Olá pelo seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="f3010-174">Open hello *Controllers\HomeController.cs* file in **Solution Explorer** and replace hello existing code with hello following:</span></span>

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

## <a name="set-up-hello-styles"></a><span data-ttu-id="f3010-175">Configurar estilos Olá</span><span class="sxs-lookup"><span data-stu-id="f3010-175">Set up hello styles</span></span>
<span data-ttu-id="f3010-176">título de saudação do toochange na parte superior de Olá da página hello, abra Olá *exibições \ compartilhadas\\cshtml* do arquivo em **Solution Explorer** e substitua o "Nome do aplicativo" no cabeçalho da barra de navegação de saudação com a tarefa"My Lista de aplicativos"para que fique assim:</span><span class="sxs-lookup"><span data-stu-id="f3010-176">toochange hello title at hello top of hello page, open hello *Views\Shared\\_Layout.cshtml* file in **Solution Explorer** and replace "Application name" in hello navbar header with "My Task List Application" so that it looks like this:</span></span>

     @Html.ActionLink("My Task List Application", "Index", "Home", null, new { @class = "navbar-brand" })

<span data-ttu-id="f3010-177">Em ordem tooset menu da lista de tarefas de hello, abra Olá *\Views\Home\Index.cshtml* arquivo e substitua código existente Olá Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="f3010-177">In order tooset up hello Task List menu, open hello *\Views\Home\Index.cshtml* file and replace hello existing code with hello following code:</span></span>

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


<span data-ttu-id="f3010-178">tooadd Olá capacidade toocreate uma nova tarefa, clique com botão direito Olá *Views\Home\\*  pasta e **adicionar** um **exibição**.</span><span class="sxs-lookup"><span data-stu-id="f3010-178">tooadd hello ability toocreate a new task, right-click hello *Views\Home\\* folder and **Add** a **View**.</span></span>  <span data-ttu-id="f3010-179">Nome de exibição Olá *criar*.</span><span class="sxs-lookup"><span data-stu-id="f3010-179">Name hello view *Create*.</span></span> <span data-ttu-id="f3010-180">Substitua o código de saudação pelo seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="f3010-180">Replace hello code with hello following:</span></span>

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

<span data-ttu-id="f3010-181">**Gerenciador de soluções** deve ser assim:</span><span class="sxs-lookup"><span data-stu-id="f3010-181">**Solution Explorer** should look like this:</span></span>

![Gerenciador de Soluções][SolutionExplorerMyTaskListApp]

## <a name="set-hello-mongodb-connection-string"></a><span data-ttu-id="f3010-183">Saudação de conjunto de cadeia de conexão do MongoDB</span><span class="sxs-lookup"><span data-stu-id="f3010-183">Set hello MongoDB connection string</span></span>
<span data-ttu-id="f3010-184">Em **Solution Explorer**, abra Olá *DAL/Dal.cs* arquivo.</span><span class="sxs-lookup"><span data-stu-id="f3010-184">In **Solution Explorer**, open hello *DAL/Dal.cs* file.</span></span> <span data-ttu-id="f3010-185">Localize Olá linha de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="f3010-185">Find hello following line of code:</span></span>

    private string connectionString = "mongodb://<vm-dns-name>";

<span data-ttu-id="f3010-186">Substituir `<vm-dns-name>` com o nome DNS de saudação da máquina virtual de saudação executando MongoDB criado no hello [criar uma máquina virtual e instale o MongoDB] [ Create a virtual machine and install MongoDB] etapa deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="f3010-186">Replace `<vm-dns-name>` with hello DNS name of hello virtual machine running MongoDB you created in hello [Create a virtual machine and install MongoDB][Create a virtual machine and install MongoDB] step of this tutorial.</span></span>  <span data-ttu-id="f3010-187">nome DNS Olá toofind de sua máquina virtual, vá toohello Portal do Azure, selecione **máquinas virtuais**e encontrar **nome DNS**.</span><span class="sxs-lookup"><span data-stu-id="f3010-187">toofind hello DNS name of your virtual machine, go toohello Azure Portal, select **Virtual Machines**, and find **DNS Name**.</span></span>

<span data-ttu-id="f3010-188">Se o nome DNS de saudação da máquina virtual de saudação for "testlinuxvm.cloudapp.net" e MongoDB está escutando na porta padrão de saudação 27017, Olá linha de cadeia de caracteres de conexão de código será semelhante:</span><span class="sxs-lookup"><span data-stu-id="f3010-188">If hello DNS name of hello virtual machine is "testlinuxvm.cloudapp.net" and MongoDB is listening on hello default port 27017, hello connection string line of code will look like:</span></span>

    private string connectionString = "mongodb://testlinuxvm.cloudapp.net";

<span data-ttu-id="f3010-189">Se o ponto de extremidade de máquina virtual de saudação especifica uma porta externa diferente para o MongoDB, você pode especificar porta de saudação na cadeia de caracteres de conexão de saudação:</span><span class="sxs-lookup"><span data-stu-id="f3010-189">If hello virtual machine endpoint specifies a different external port for MongoDB, you can specifiy hello port in hello connection string:</span></span>

     private string connectionString = "mongodb://testlinuxvm.cloudapp.net:12345";

<span data-ttu-id="f3010-190">Para obter mais informações sobre cadeias de conexão de MongoDB, consulte [Conexões][MongoConnectionStrings].</span><span class="sxs-lookup"><span data-stu-id="f3010-190">For more information on MongoDB connection strings, see [Connections][MongoConnectionStrings].</span></span>

## <a name="test-hello-local-deployment"></a><span data-ttu-id="f3010-191">Implantação de local de saudação do teste</span><span class="sxs-lookup"><span data-stu-id="f3010-191">Test hello local deployment</span></span>
<span data-ttu-id="f3010-192">toorun seu aplicativo no computador de desenvolvimento, selecione **iniciar depuração** de saudação **depurar** menu ou pressione **F5**.</span><span class="sxs-lookup"><span data-stu-id="f3010-192">toorun your application on your development computer, select **Start Debugging** from hello **Debug** menu or hit **F5**.</span></span> <span data-ttu-id="f3010-193">O IIS Express é iniciado e um navegador é aberto e inicia a página inicial do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="f3010-193">IIS Express starts and a browser opens and launches hello application's home page.</span></span>  <span data-ttu-id="f3010-194">Você pode adicionar uma nova tarefa, adicionaremos o banco de dados do MongoDB toohello com sua máquina virtual no Azure.</span><span class="sxs-lookup"><span data-stu-id="f3010-194">You can add a new task, which will be added toohello MongoDB database running on your virtual machine in Azure.</span></span>

![Aplicativo Minha Lista de Tarefas][TaskListAppBlank]

## <a name="publish-tooazure-app-service-web-apps"></a><span data-ttu-id="f3010-196">Publicar aplicativos de Web do serviço de aplicativo tooAzure</span><span class="sxs-lookup"><span data-stu-id="f3010-196">Publish tooAzure App Service Web Apps</span></span>
<span data-ttu-id="f3010-197">Nesta seção, você publicará o tooAzure alterações aplicativos de Web do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f3010-197">In this section you will publish your changes tooAzure App Service Web Apps.</span></span>

1. <span data-ttu-id="f3010-198">No Gerenciador de Soluções, clique novamente com o botão direito do mouse em **MyTaskListApp** e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="f3010-198">In Solution Explorer, right-click **MyTaskListApp** again and click **Publish**.</span></span>
2. <span data-ttu-id="f3010-199">Clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="f3010-199">Click **Publish**.</span></span>
   
    <span data-ttu-id="f3010-200">Agora você deve ver o aplicativo web em execução no serviço de aplicativo do Azure e acessar o banco de dados do MongoDB Olá em máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="f3010-200">You should now see your web app running in Azure App Service and accessing hello MongoDB database in Azure Virtual Machines.</span></span>

## <a name="summary"></a><span data-ttu-id="f3010-201">Resumo</span><span class="sxs-lookup"><span data-stu-id="f3010-201">Summary</span></span>
<span data-ttu-id="f3010-202">Agora você ter implantado com êxito seu aplicativo de ASP.NET tooAzure aplicativos de Web do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f3010-202">You have now successfully deployed your ASP.NET application tooAzure App Service Web Apps.</span></span> <span data-ttu-id="f3010-203">Olá tooview o aplicativo web:</span><span class="sxs-lookup"><span data-stu-id="f3010-203">tooview hello web app:</span></span>

1. <span data-ttu-id="f3010-204">Faça logon no hello Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f3010-204">Log into hello Azure Portal.</span></span>
2. <span data-ttu-id="f3010-205">Clique em **Aplicativos Web**.</span><span class="sxs-lookup"><span data-stu-id="f3010-205">Click **Web apps**.</span></span> 
3. <span data-ttu-id="f3010-206">Selecione o aplicativo web no hello **aplicativos Web** lista.</span><span class="sxs-lookup"><span data-stu-id="f3010-206">Select your web app in hello **Web Apps** list.</span></span>

<span data-ttu-id="f3010-207">Para obter mais informações sobre como desenvolver aplicativos do C# para MongoDB, consulte a [Central da linguagem CSharp][MongoC#LangCenter].</span><span class="sxs-lookup"><span data-stu-id="f3010-207">For more information on developing C# applications against MongoDB, see [CSharp Language Center][MongoC#LangCenter].</span></span> 

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
[Create and run hello My Task List ASP.NET application on your development computer]: #createapp
[Create an Azure web site]: #createwebsite
[Deploy hello ASP.NET application toohello web site using Git]: #deployapp
