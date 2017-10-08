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
# <a name="create-a-web-app-in-azure-that-connects-toomongodb-running-on-a-virtual-machine"></a>Criar um aplicativo web no Azure que se conecta tooMongoDB em execução em uma máquina virtual
Usando o Git, você pode implantar um aplicativo de ASP.NET tooAzure aplicativos de Web do serviço de aplicativo. Neste tutorial, você criará um front-end ASP.NET MVC simples aplicativo de lista de tarefas que se conecta o banco de dados do MongoDB tooa executado em uma máquina virtual no Azure.  [O MongoDB][MongoDB] é um popular banco de dados NoSQL de código-fonte aberto e de alto desempenho. Depois de executar e testar Olá ASP.NET aplicativo no computador de desenvolvimento, você fará o upload Olá aplicativo tooApp aplicativos Web do serviço usando o Git.

> [!NOTE]
> Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo. Nenhum cartão de crédito é exigido, sem compromissos.
> 
> 

## <a name="background-knowledge"></a>Conhecimento prévio
Conhecimento da seguinte Olá é útil para este tutorial, no entanto, não é necessário:

* driver de saudação c# para o MongoDB. Para obter mais informações sobre como desenvolver aplicativos c# contra MongoDB, consulte Olá MongoDB [Center de linguagem CSharp][MongoC#LangCenter]. 
* estrutura de aplicativo web do ASP .NET Hello. Você pode aprender tudo sobre ele no hello [site ASP.net][ASP.NET].
* estrutura de aplicativo web do ASP .NET MVC Hello. Você pode aprender tudo sobre ele no hello [site ASP.NET MVC][MVCWebSite].
* Azure. Você pode começar lendo em [Azure][WindowsAzure].

## <a name="prerequisites"></a>Pré-requisitos
* [Visual Studio Express 2013 para Web][VSEWeb] ou [Visual Studio 2013][VSUlt]
* [SDK do Azure para .NET](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409)
* Uma assinatura ativa do Microsoft Azure

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<a id="virtualmachine"></a> 

## <a name="create-a-virtual-machine-and-install-mongodb"></a>Criar uma máquina virtual e instalar MongoDB
Este tutorial supõe que você tenha criado uma máquina virtual no Azure. Depois de criar a máquina virtual de saudação é necessário tooinstall MongoDB na máquina virtual de saudação:

* toocreate uma máquina virtual do Windows e instale o MongoDB, consulte [MongoDB instalar em uma máquina virtual executando o Windows Server no Azure][InstallMongoOnWindowsVM].

Depois que você criou a máquina virtual de saudação no Azure e instalado o MongoDB, ser se tooremember Olá nome DNS da máquina virtual de saudação ("testlinuxvm.cloudapp.net", por exemplo) e a porta externa Olá para o MongoDB que você especificou no ponto de extremidade de saudação.  Você precisará dessas informações posteriormente no tutorial de saudação.

<a id="createapp"></a>

## <a name="create-hello-application"></a>Criar um aplicativo hello
Nesta seção você criará um aplicativo ASP.NET chamado "Minha lista de tarefas" usando o Visual Studio e executar uma implantação inicial de tooAzure aplicativos de Web do serviço de aplicativo. Você executará aplicativo hello localmente, mas ele se conectará tooyour máquina virtual do Azure e usar a instância do MongoDB Olá que você criou nele.

1. No Visual Studio, clique em **Novo Projeto**.
   
    ![Iniciar página Novo Projeto][StartPageNewProject]
2. Em Olá **novo projeto** janela, no painel esquerdo hello, selecione **Visual C#**e, em seguida, selecione **Web**. No painel do meio hello, selecione **aplicativo Web ASP.NET**. Na parte inferior do hello, nomeie o projeto "MyTaskListApp" e, em seguida, clique em **Okey**.
   
    ![Caixa de diálogo Novo Projeto][NewProjectMyTaskListApp]
3. Em Olá **novo projeto ASP.NET** caixa de diálogo, selecione **MVC**e, em seguida, clique em **Okey**.
   
    ![Selecionar modelo do MVC][VS2013SelectMVCTemplate]
4. Se você não tiver entrado no Microsoft Azure, será solicitado toosign no. Siga Olá prompts toosign no Azure.
5. Depois de se conectar, você poderá começar a configurar seu aplicativo Web do Serviço de Aplicativo. Especificar Olá **nome do aplicativo Web**, **plano de serviço de aplicativo**, **grupo de recursos**, e **região**, em seguida, clique em **criar**.
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSConfigureWebAppSettings.png)
6. Depois de concluir a criação do projeto hello, aguarde Olá web aplicativo toobe criado no serviço de aplicativo do Azure, conforme indicado no hello **atividade de serviço de aplicativo do Azure** janela. Em seguida, clique em **MyTaskListApp publicar toothis aplicativo Web agora**.
7. Clique em **Publicar**.
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSPublishWeb.png)
   
    Depois que o aplicativo do ASP.NET padrão é publicado tooAzure aplicativos de Web do serviço de aplicativo, ele será iniciado no navegador de saudação.

## <a name="install-hello-mongodb-c-driver"></a>Instalar Olá MongoDB c# driver
MongoDB oferece suporte a cliente c# aplicativos por meio de um driver, que é necessário tooinstall em seu computador de desenvolvimento local. Olá c# driver está disponível através do NuGet.

Olá tooinstall MongoDB c# driver:

1. Em **Gerenciador de soluções**, Olá atalho **MyTaskListApp** do projeto e selecione **NuGetPackages gerenciar**.
   
    ![Gerenciar Pacotes NuGet][VS2013ManageNuGetPackages]
2. Em Olá **gerenciar pacotes NuGet** no painel esquerdo do hello, clique em **Online**. Em Olá **Pesquisar Online** em saudação à direita, digite "mongodb.driver".  Clique em **instalar** tooinstall driver de saudação.
   
    ![Procurar o driver do C# para MongoDB][SearchforMongoDBCSharpDriver]
3. Clique em **aceito** tooaccept Olá 10gen, Inc. termos de licença.
4. Clique em **fechar** depois Olá driver instalado.
    ![Driver do C# para MongoDB instalado][MongoDBCsharpDriverInstalled]

Olá MongoDB c# driver agora está instalado.  Referências toohello **MongoDB.Bson**, **MongoDB.Driver**, e **MongoDB.Driver.Core** bibliotecas foram adicionadas toohello projeto.

![Referências do driver do C# para MongoDB][MongoDBCSharpDriverReferences]

## <a name="add-a-model"></a>Adicionar um modelo
Em **Solution Explorer**, Olá do botão direito do mouse *modelos* pasta e **adicionar** um novo **classe** e nomeie-o *TaskModel.cs* .  Em *TaskModel.cs*, substitua código existente Olá Olá código a seguir:

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

## <a name="add-hello-data-access-layer"></a>Adicionar camada de acesso a dados Olá
Em **Solution Explorer**, Olá do botão direito do mouse *MyTaskListApp* projeto e **adicionar** um **nova pasta** chamado *DAL*.  Saudação de atalho *DAL* pasta e **adicionar** um novo **classe**. Arquivo de nome de classe Olá *Dal.cs*.  Em *Dal.cs*, substitua código existente Olá Olá código a seguir:

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

## <a name="add-a-controller"></a>Adicionar um controlador
Olá abrir *Controllers\HomeController.cs* arquivo **Gerenciador de soluções** e substitua código existente Olá pelo seguinte Olá:

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

## <a name="set-up-hello-styles"></a>Configurar estilos Olá
título de saudação do toochange na parte superior de Olá da página hello, abra Olá *exibições \ compartilhadas\\cshtml* do arquivo em **Solution Explorer** e substitua o "Nome do aplicativo" no cabeçalho da barra de navegação de saudação com a tarefa"My Lista de aplicativos"para que fique assim:

     @Html.ActionLink("My Task List Application", "Index", "Home", null, new { @class = "navbar-brand" })

Em ordem tooset menu da lista de tarefas de hello, abra Olá *\Views\Home\Index.cshtml* arquivo e substitua código existente Olá Olá código a seguir:

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


tooadd Olá capacidade toocreate uma nova tarefa, clique com botão direito Olá *Views\Home\\*  pasta e **adicionar** um **exibição**.  Nome de exibição Olá *criar*. Substitua o código de saudação pelo seguinte hello:

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

**Gerenciador de soluções** deve ser assim:

![Gerenciador de Soluções][SolutionExplorerMyTaskListApp]

## <a name="set-hello-mongodb-connection-string"></a>Saudação de conjunto de cadeia de conexão do MongoDB
Em **Solution Explorer**, abra Olá *DAL/Dal.cs* arquivo. Localize Olá linha de código a seguir:

    private string connectionString = "mongodb://<vm-dns-name>";

Substituir `<vm-dns-name>` com o nome DNS de saudação da máquina virtual de saudação executando MongoDB criado no hello [criar uma máquina virtual e instale o MongoDB] [ Create a virtual machine and install MongoDB] etapa deste tutorial.  nome DNS Olá toofind de sua máquina virtual, vá toohello Portal do Azure, selecione **máquinas virtuais**e encontrar **nome DNS**.

Se o nome DNS de saudação da máquina virtual de saudação for "testlinuxvm.cloudapp.net" e MongoDB está escutando na porta padrão de saudação 27017, Olá linha de cadeia de caracteres de conexão de código será semelhante:

    private string connectionString = "mongodb://testlinuxvm.cloudapp.net";

Se o ponto de extremidade de máquina virtual de saudação especifica uma porta externa diferente para o MongoDB, você pode especificar porta de saudação na cadeia de caracteres de conexão de saudação:

     private string connectionString = "mongodb://testlinuxvm.cloudapp.net:12345";

Para obter mais informações sobre cadeias de conexão de MongoDB, consulte [Conexões][MongoConnectionStrings].

## <a name="test-hello-local-deployment"></a>Implantação de local de saudação do teste
toorun seu aplicativo no computador de desenvolvimento, selecione **iniciar depuração** de saudação **depurar** menu ou pressione **F5**. O IIS Express é iniciado e um navegador é aberto e inicia a página inicial do aplicativo hello.  Você pode adicionar uma nova tarefa, adicionaremos o banco de dados do MongoDB toohello com sua máquina virtual no Azure.

![Aplicativo Minha Lista de Tarefas][TaskListAppBlank]

## <a name="publish-tooazure-app-service-web-apps"></a>Publicar aplicativos de Web do serviço de aplicativo tooAzure
Nesta seção, você publicará o tooAzure alterações aplicativos de Web do serviço de aplicativo.

1. No Gerenciador de Soluções, clique novamente com o botão direito do mouse em **MyTaskListApp** e clique em **Publicar**.
2. Clique em **Publicar**.
   
    Agora você deve ver o aplicativo web em execução no serviço de aplicativo do Azure e acessar o banco de dados do MongoDB Olá em máquinas virtuais do Azure.

## <a name="summary"></a>Resumo
Agora você ter implantado com êxito seu aplicativo de ASP.NET tooAzure aplicativos de Web do serviço de aplicativo. Olá tooview o aplicativo web:

1. Faça logon no hello Portal do Azure.
2. Clique em **Aplicativos Web**. 
3. Selecione o aplicativo web no hello **aplicativos Web** lista.

Para obter mais informações sobre como desenvolver aplicativos do C# para MongoDB, consulte a [Central da linguagem CSharp][MongoC#LangCenter]. 

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
