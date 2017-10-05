---
title: Criar uma API REST no Azure com ASP.NET e uma BD SQL | Microsoft Docs
description: Um tutorial que ensina como implantar um aplicativo que usa a API Web ASP.NET em um aplicativo Web do Azure usando o Visual Studio.
services: app-service\web
documentationcenter: .net
author: Rick-Anderson
writer: Rick-Anderson
manager: erikre
editor: 
ms.assetid: f4916fc0-ea08-41f7-846b-73e41bc88149
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/29/2016
ms.author: riande
ms.openlocfilehash: 64c18f2cfabbb7af6ffd89b4c2a9095fca1cf799
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-rest-service-using-aspnet-web-api-and-sql-database-in-azure-app-service"></a><span data-ttu-id="97611-103">Criar um serviço REST usando a API Web ASP.NET e o Banco de Dados SQL no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="97611-103">Create a REST service using ASP.NET Web API and SQL Database in Azure App Service</span></span>
<span data-ttu-id="97611-104">Este tutorial mostra como implantar um aplicativo Web do ASP.NET em um [Serviço de Aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) usando o assistente de Publicação na Web no Visual Studio 2013 ou no Visual Studio 2013 Community Edition.</span><span class="sxs-lookup"><span data-stu-id="97611-104">This tutorial shows how to deploy an ASP.NET web app to an [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by using the Publish Web wizard in Visual Studio 2013 or Visual Studio 2013 Community Edition.</span></span> 

<span data-ttu-id="97611-105">É possível abrir uma conta do Azure gratuitamente e, se você ainda não tiver o Visual Studio 2013, o SDK instalará automaticamente o Visual Studio 2013 para o Web Express.</span><span class="sxs-lookup"><span data-stu-id="97611-105">You can open an Azure account for free, and if you don't already have Visual Studio 2013, the SDK automatically installs Visual Studio 2013 for Web Express.</span></span> <span data-ttu-id="97611-106">Portanto, você pode começar a desenvolver para o Azure de maneira totalmente gratuita.</span><span class="sxs-lookup"><span data-stu-id="97611-106">So you can start developing for Azure entirely for free.</span></span>

<span data-ttu-id="97611-107">Este tutorial pressupõe que você não tem nenhuma experiência anterior com o Azure.</span><span class="sxs-lookup"><span data-stu-id="97611-107">This tutorial assumes that you have no prior experience using Azure.</span></span> <span data-ttu-id="97611-108">Ao concluir este tutorial, você terá um aplicativo Web simples em funcionamento na nuvem.</span><span class="sxs-lookup"><span data-stu-id="97611-108">On completing this tutorial, you'll have a simple web app up and running in the cloud.</span></span>

<span data-ttu-id="97611-109">Você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="97611-109">You'll learn:</span></span>

* <span data-ttu-id="97611-110">Como habilitar seu computador para desenvolvimento do Azure ao instalar o SDK do Azure.</span><span class="sxs-lookup"><span data-stu-id="97611-110">How to enable your machine for Azure development by installing the Azure SDK.</span></span>
* <span data-ttu-id="97611-111">Como criar um projeto MVC 5 do Visual Studio ASP.NET e publicá-lo em um aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="97611-111">How to create a Visual Studio ASP.NET MVC 5 project and publish it to an Azure app.</span></span>
* <span data-ttu-id="97611-112">Como usar a API Web ASP.NET para habilitar chamadas à API Restful.</span><span class="sxs-lookup"><span data-stu-id="97611-112">How to use the ASP.NET Web API to enable Restful API calls.</span></span>
* <span data-ttu-id="97611-113">Como usar um banco de dados SQL para armazenar dados no Azure.</span><span class="sxs-lookup"><span data-stu-id="97611-113">How to use a SQL database to store data in Azure.</span></span>
* <span data-ttu-id="97611-114">Como publicar atualizações de aplicativo no Azure.</span><span class="sxs-lookup"><span data-stu-id="97611-114">How to publish application updates to Azure.</span></span>

<span data-ttu-id="97611-115">Você criará um aplicativo Web de lista de contatos simples desenvolvido no ASP.NET MVC 5 e que usa o ADO.NET Entity Framework para acesso ao banco de dados.</span><span class="sxs-lookup"><span data-stu-id="97611-115">You'll build a simple contact list web application that is built on ASP.NET MVC 5 and uses the ADO.NET Entity Framework for database access.</span></span> <span data-ttu-id="97611-116">A ilustração a seguir mostra o aplicativo concluído:</span><span class="sxs-lookup"><span data-stu-id="97611-116">The following illustration shows the completed application:</span></span>

![captura de tela do site][intro001]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

### <a name="create-the-project"></a><span data-ttu-id="97611-118">Criar o projeto</span><span class="sxs-lookup"><span data-stu-id="97611-118">Create the project</span></span>
1. <span data-ttu-id="97611-119">Inicie o Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="97611-119">Start Visual Studio 2013.</span></span>
2. <span data-ttu-id="97611-120">No menu **Arquivo**, clique em **Novo Projeto**.</span><span class="sxs-lookup"><span data-stu-id="97611-120">From the **File** menu click **New Project**.</span></span>
3. <span data-ttu-id="97611-121">Na caixa de diálogo **Novo Projeto**, expanda **Visual C#**, escolha **Web** e, em seguida, **Aplicativo Web ASP .NET**.</span><span class="sxs-lookup"><span data-stu-id="97611-121">In the **New Project** dialog box, expand **Visual C#** and select **Web**  and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="97611-122">Nomeie o aplicativo **ContactManager** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="97611-122">Name the application **ContactManager** and click **OK**.</span></span>
   
    ![Caixa de diálogo Novo Projeto](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr4.png)
4. <span data-ttu-id="97611-124">Na caixa de diálogo **Novo Projeto ASP.NET**, escolha o modelo **MVC**, marque **API Web** e clique em **Alterar Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="97611-124">In the **New ASP.NET Project** dialog box, select the **MVC** template, check **Web API** and then click **Change Authentication**.</span></span>
5. <span data-ttu-id="97611-125">Na caixa de diálogo **Alterar Autenticação**, clique em **Sem Autenticação** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="97611-125">In the **Change Authentication** dialog box, click **No Authentication**, and then click **OK**.</span></span>
   
    ![Sem Autenticação](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/GS13noauth.png)
   
    <span data-ttu-id="97611-127">O aplicativo de exemplo que você está criando não possui recursos que exijam que os usuários façam logon.</span><span class="sxs-lookup"><span data-stu-id="97611-127">The sample application you're creating won't have features that require users to log in.</span></span> <span data-ttu-id="97611-128">Para obter informações sobre como implementar recursos de autenticação e autorização, consulte a seção [Próximas Etapas](#nextsteps) no final deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="97611-128">For information about how to implement authentication and authorization features, see the [Next Steps](#nextsteps) section at the end of this tutorial.</span></span> 
6. <span data-ttu-id="97611-129">Na caixa de diálogo **Novo Projeto ASP.NET**, verifique se a opção **Hospedar na Nuvem** está marcada e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="97611-129">In the **New ASP.NET Project** dialog box, make sure the **Host in the Cloud** is checked and click **OK**.</span></span>

<span data-ttu-id="97611-130">Se você não entrou anteriormente no Azure, será solicitado que você entre.</span><span class="sxs-lookup"><span data-stu-id="97611-130">If you have not previously signed in to Azure, you will be prompted to sign in.</span></span>

1. <span data-ttu-id="97611-131">O assistente de configuração sugerirá um nome exclusivo com base em *ContactManager* (consulte a imagem abaixo).</span><span class="sxs-lookup"><span data-stu-id="97611-131">The configuration wizard will suggest a unique name based on *ContactManager* (see the image below).</span></span> <span data-ttu-id="97611-132">Selecione uma região perto de você.</span><span class="sxs-lookup"><span data-stu-id="97611-132">Select a region near you.</span></span> <span data-ttu-id="97611-133">É possível utilizar o [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") para localizar o data center de latência mais baixa.</span><span class="sxs-lookup"><span data-stu-id="97611-133">You can use [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") to find the lowest latency data center.</span></span> 
2. <span data-ttu-id="97611-134">Se você não criou um servidor de banco de dados antes, selecione **Criar novo servidor**, digite um nome de usuário de banco de dados e uma senha.</span><span class="sxs-lookup"><span data-stu-id="97611-134">If you haven't created a database server before, select **Create new server**, enter a database user name and password.</span></span>
   
    ![Configurar o site do Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configAz.PNG)

<span data-ttu-id="97611-136">Se você tiver um servidor de banco de dados, use isso para criar um novo banco de dados.</span><span class="sxs-lookup"><span data-stu-id="97611-136">If you have a database server, use that to create a new database.</span></span> <span data-ttu-id="97611-137">Os servidores de banco de dados são um recurso precioso e você geralmente deseja criar vários bancos de dados no mesmo servidor de teste e desenvolvimento em vez de criar um servidor de banco de dados por banco de dados.</span><span class="sxs-lookup"><span data-stu-id="97611-137">Database servers are a precious resource, and you generally want to create multiple databases on the same server for testing and development rather than creating a database server per database.</span></span> <span data-ttu-id="97611-138">Certifique-se de que o seu site e banco de dados estejam na mesma região.</span><span class="sxs-lookup"><span data-stu-id="97611-138">Make sure your web site and database are in the same region.</span></span>

![Configurar o site do Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configWithDB.PNG)

### <a name="set-the-page-header-and-footer"></a><span data-ttu-id="97611-140">Configurar o cabeçalho e o rodapé da página</span><span class="sxs-lookup"><span data-stu-id="97611-140">Set the page header and footer</span></span>
1. <span data-ttu-id="97611-141">No **Gerenciador de Soluções**, expanda a pasta *Views\Shared* e abra o arquivo *_Layout.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="97611-141">In **Solution Explorer**, expand the *Views\Shared* folder and open the *_Layout.cshtml* file.</span></span>
   
    ![_Layout.cshtml no Gerenciador de Soluções][newapp004]
2. <span data-ttu-id="97611-143">Substitua o conteúdo do arquivo *Views\Shared_Layout.cshtml* pelo seguinte código:</span><span class="sxs-lookup"><span data-stu-id="97611-143">Replace the contents of the *Views\Shared_Layout.cshtml* file with the following code:</span></span>

        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="utf-8" />
            <title>@ViewBag.Title - Contact Manager</title>
            <link href="~/favicon.ico" rel="shortcut icon" type="image/x-icon" />
            <meta name="viewport" content="width=device-width" />
            @Styles.Render("~/Content/css")
            @Scripts.Render("~/bundles/modernizr")
        </head>
        <body>
            <header>
                <div class="content-wrapper">
                    <div class="float-left">
                        <p class="site-title">@Html.ActionLink("Contact Manager", "Index", "Home")</p>
                    </div>
                </div>
            </header>
            <div id="body">
                @RenderSection("featured", required: false)
                <section class="content-wrapper main-content clear-fix">
                    @RenderBody()
                </section>
            </div>
            <footer>
                <div class="content-wrapper">
                    <div class="float-left">
                        <p>&copy; @DateTime.Now.Year - Contact Manager</p>
                    </div>
                </div>
            </footer>
            @Scripts.Render("~/bundles/jquery")
            @RenderSection("scripts", required: false)
        </body>
        </html>

<span data-ttu-id="97611-144">A marcação acima altera o nome do aplicativo de "My ASP.NET App" para "Contact Manager" e remove os links para **Página Inicial**, **Sobre** e **Contato**.</span><span class="sxs-lookup"><span data-stu-id="97611-144">The markup above changes the app name from "My ASP.NET App" to "Contact Manager", and it removes the links to **Home**, **About** and **Contact**.</span></span>

### <a name="run-the-application-locally"></a><span data-ttu-id="97611-145">Executar o aplicativo localmente</span><span class="sxs-lookup"><span data-stu-id="97611-145">Run the application locally</span></span>
1. <span data-ttu-id="97611-146">Pressione CTRL+F5 para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="97611-146">Press CTRL+F5 to run the application.</span></span>
   <span data-ttu-id="97611-147">A home page do aplicativo é exibida no navegador padrão.</span><span class="sxs-lookup"><span data-stu-id="97611-147">The application home page appears in the default browser.</span></span>
    <span data-ttu-id="97611-148">![Home page da lista de tarefas pendentes](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)</span><span class="sxs-lookup"><span data-stu-id="97611-148">![To Do List home page](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)</span></span>

<span data-ttu-id="97611-149">Isso é tudo o que você precisa fazer por enquanto para criar o aplicativo que você implantará no Azure.</span><span class="sxs-lookup"><span data-stu-id="97611-149">This is all you need to do for now to create the application that you'll deploy to Azure.</span></span> <span data-ttu-id="97611-150">Posteriormente, você adicionará a funcionalidade do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="97611-150">Later you'll add database functionality.</span></span>

## <a name="deploy-the-application-to-azure"></a><span data-ttu-id="97611-151">Implantar o aplicativo no Azure</span><span class="sxs-lookup"><span data-stu-id="97611-151">Deploy the application to Azure</span></span>
1. <span data-ttu-id="97611-152">No Visual Studio, clique com o botão direito do mouse no projeto no **Gerenciador de Soluções** e selecione **Publicar** no menu de contexto.</span><span class="sxs-lookup"><span data-stu-id="97611-152">In Visual Studio, right-click the project in **Solution Explorer** and select **Publish** from the context menu.</span></span>
   
    ![Publicar no menu de contexto do projeto][PublishVSSolution]
   
    <span data-ttu-id="97611-154">O assistente de **Publicar Web** é aberto.</span><span class="sxs-lookup"><span data-stu-id="97611-154">The **Publish Web** wizard opens.</span></span>
2. <span data-ttu-id="97611-155">Clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="97611-155">Click **Publish**.</span></span>

![Guia Configurações](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/pw.png)

<span data-ttu-id="97611-157">O Visual Studio inicia o processo de cópia dos arquivos no servidor do Azure.</span><span class="sxs-lookup"><span data-stu-id="97611-157">Visual Studio begins the process of copying the files to the Azure server.</span></span> <span data-ttu-id="97611-158">A janela **Saída** mostra quais ações de implantação foram executadas e os relatórios da conclusão com êxito da implantação.</span><span class="sxs-lookup"><span data-stu-id="97611-158">The **Output** window shows what deployment actions were taken and reports successful completion of the deployment.</span></span>

1. <span data-ttu-id="97611-159">O navegador padrão abre automaticamente a URL do site implantado.</span><span class="sxs-lookup"><span data-stu-id="97611-159">The default browser automatically opens to the URL of the deployed site.</span></span>
   
   <span data-ttu-id="97611-160">O aplicativo que você criou agora está em execução na nuvem.</span><span class="sxs-lookup"><span data-stu-id="97611-160">The application you created is now running in the cloud.</span></span>
   
   ![A home page da lista de tarefas pendentes em execução no Azure][rxz2]

## <a name="add-a-database-to-the-application"></a><span data-ttu-id="97611-162">Adicionar um banco de dados ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="97611-162">Add a database to the application</span></span>
<span data-ttu-id="97611-163">Em seguida, você atualizará o aplicativo MVC para adicionar a habilidade de exibir e atualizar contatos e armazenar os dados em um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="97611-163">Next, you'll update the MVC application to add the ability to display and update contacts and store the data in a database.</span></span> <span data-ttu-id="97611-164">O aplicativo usará o Entity Framework para criar o banco de dados e ler e atualizar dados no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="97611-164">The application will use the Entity Framework to create the database and to read and update data in the database.</span></span>

### <a name="add-data-model-classes-for-the-contacts"></a><span data-ttu-id="97611-165">Adicionar classes de modelo de dados aos contatos</span><span class="sxs-lookup"><span data-stu-id="97611-165">Add data model classes for the contacts</span></span>
<span data-ttu-id="97611-166">Você começa criando um modelo de dados simples no código.</span><span class="sxs-lookup"><span data-stu-id="97611-166">You begin by creating a simple data model in code.</span></span>

1. <span data-ttu-id="97611-167">No **Gerenciador de Soluções**, clique com o botão direito do mouse na pasta Modelos e clique em **Adicionar**. Em seguida, clique em **Classe**.</span><span class="sxs-lookup"><span data-stu-id="97611-167">In **Solution Explorer**, right-click the Models folder, click **Add**, and then **Class**.</span></span>
   
    ![Adicionar Classe no menu de contexto da pasta Modelos][adddb001]
2. <span data-ttu-id="97611-169">Na caixa de diálogo **Adicionar Novo Item**, nomeie o novo arquivo de classe *Contact.cs* e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="97611-169">In the **Add New Item** dialog box, name the new class file *Contact.cs*, and then click **Add**.</span></span>
   
    ![Caixa de diálogo Adicionar Novo Item][adddb002]
3. <span data-ttu-id="97611-171">Substitua o conteúdo do arquivo Contacts.cs pelo código a seguir.</span><span class="sxs-lookup"><span data-stu-id="97611-171">Replace the contents of the Contacts.cs file with the following code.</span></span>
   
        using System.Globalization;
        namespace ContactManager.Models
        {
            public class Contact
               {
                public int ContactId { get; set; }
                public string Name { get; set; }
                public string Address { get; set; }
                public string City { get; set; }
                public string State { get; set; }
                public string Zip { get; set; }
                public string Email { get; set; }
                public string Twitter { get; set; }
                public string Self
                {
                    get { return string.Format(CultureInfo.CurrentCulture,
                         "api/contacts/{0}", this.ContactId); }
                    set { }
                }
            }
        }

<span data-ttu-id="97611-172">A classe **Contact** define os dados que você armazenará para cada contato, além de uma chave primária, ContactID, que é necessária para o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="97611-172">The **Contact** class defines the data that you will store for each contact, plus a primary key, ContactID, that is needed by the database.</span></span> <span data-ttu-id="97611-173">Você pode obter mais informações sobre modelos de dados na seção [Próximas etapas](#nextsteps) ao final deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="97611-173">You can get more information about data models in the [Next Steps](#nextsteps) section at the end of this tutorial.</span></span>

### <a name="create-web-pages-that-enable-app-users-to-work-with-the-contacts"></a><span data-ttu-id="97611-174">Criar as páginas da Web que permitem que os usuários do aplicativo trabalhem com os contatos</span><span class="sxs-lookup"><span data-stu-id="97611-174">Create web pages that enable app users to work with the contacts</span></span>
<span data-ttu-id="97611-175">No ASP.NET MVC, o recurso de scaffolding pode gerar automaticamente o código que executa as ações CRUD (criar, ler, atualizar e excluir).</span><span class="sxs-lookup"><span data-stu-id="97611-175">The ASP.NET MVC the scaffolding feature can automatically generate code that performs create, read, update, and delete (CRUD) actions.</span></span>

## <a name="add-a-controller-and-a-view-for-the-data"></a><span data-ttu-id="97611-176">Adicionar um controlador e uma exibição para os dados</span><span class="sxs-lookup"><span data-stu-id="97611-176">Add a Controller and a view for the data</span></span>
1. <span data-ttu-id="97611-177">No **Gerenciador de Soluções**, expanda a pasta Controllers.</span><span class="sxs-lookup"><span data-stu-id="97611-177">In **Solution Explorer**, expand the Controllers folder.</span></span>
2. <span data-ttu-id="97611-178">Compile o projeto **(Ctrl+Shift+B)**.</span><span class="sxs-lookup"><span data-stu-id="97611-178">Build the project **(Ctrl+Shift+B)**.</span></span> <span data-ttu-id="97611-179">(Você deve compilar o projeto antes de usar o mecanismo de scaffolding.)</span><span class="sxs-lookup"><span data-stu-id="97611-179">(You must build the project before using scaffolding mechanism.)</span></span> 
3. <span data-ttu-id="97611-180">Clique com o botão direito do mouse na pasta Controladores e clique em **Adicionar** e em **Controlador**.</span><span class="sxs-lookup"><span data-stu-id="97611-180">Right-click the Controllers folder and click **Add**, and then click **Controller**.</span></span>
   
    ![Adicionar Controlador no menu de contexto da pasta Controladores][addcode001]
4. <span data-ttu-id="97611-182">Na caixa de diálogo **Adicionar Scaffold**, escolha **Controlador MVC com exibições, usando o Entity Framework** e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="97611-182">In the **Add Scaffold** dialog box, select **MVC Controller with views, using Entity Framework** and click **Add**.</span></span>
   
   ![Adicionar controlador](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rrAC.png)
5. <span data-ttu-id="97611-184">Defina o nome do controlador como **HomeController**.</span><span class="sxs-lookup"><span data-stu-id="97611-184">Set the controller name to **HomeController**.</span></span> <span data-ttu-id="97611-185">Selecione **Contato** como a classe de modelo.</span><span class="sxs-lookup"><span data-stu-id="97611-185">Select **Contact** as your model class.</span></span> <span data-ttu-id="97611-186">Clique no botão **Novo contexto de dados** e aceite o padrão "ContactManager.Models.ContactManagerContext" para o **Novo tipo de contexto de dados**.</span><span class="sxs-lookup"><span data-stu-id="97611-186">Click the **New data context** button and accept the default "ContactManager.Models.ContactManagerContext" for the **New data context type**.</span></span> <span data-ttu-id="97611-187">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="97611-187">Click **Add**.</span></span>

    <span data-ttu-id="97611-188">Uma caixa de diálogo avisará: "Já existe um arquivo com o nome HomeController.</span><span class="sxs-lookup"><span data-stu-id="97611-188">A dialog box will prompt you: "A file with the name HomeController already exits.</span></span> <span data-ttu-id="97611-189">Deseja substituí-lo?".</span><span class="sxs-lookup"><span data-stu-id="97611-189">Do you want to replace it?".</span></span> <span data-ttu-id="97611-190">Clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="97611-190">Click **Yes**.</span></span> <span data-ttu-id="97611-191">Estamos substituindo o controlador inicial que foi criado com o novo projeto.</span><span class="sxs-lookup"><span data-stu-id="97611-191">We are overwriting the Home Controller that was created with the new project.</span></span> <span data-ttu-id="97611-192">Usaremos o novo controlador inicial para nossa lista de contatos.</span><span class="sxs-lookup"><span data-stu-id="97611-192">We will use the new Home Controller for our contact list.</span></span>

    <span data-ttu-id="97611-193">O Visual Studio cria métodos do controlador e modos de exibição para as operações de banco de dados CRUD para objetos **Contact** .</span><span class="sxs-lookup"><span data-stu-id="97611-193">Visual Studio creates controller methods and views for CRUD database operations for **Contact** objects.</span></span>

## <a name="enable-migrations-create-the-database-add-sample-data-and-a-data-initializer"></a><span data-ttu-id="97611-194">Habilitar migrações, criar o banco de dados, adicionar dados de exemplo e um inicializador de dados</span><span class="sxs-lookup"><span data-stu-id="97611-194">Enable Migrations, create the database, add sample data and a data initializer</span></span>
<span data-ttu-id="97611-195">A próxima tarefa é habilitar o recurso [Codificar Primeiras Migrações](http://curah.microsoft.com/55220) para criar o banco de dados com base no modelo de dados criado.</span><span class="sxs-lookup"><span data-stu-id="97611-195">The next task is to enable the [Code First Migrations](http://curah.microsoft.com/55220) feature in order to create the database based on the data model you created.</span></span>

1. <span data-ttu-id="97611-196">No menu **Ferramentas**, escolha **Gerenciador de Pacotes de Biblioteca** e, em seguida, **Console do Gerenciador de Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="97611-196">In the **Tools** menu, select **Library Package Manager** and then **Package Manager Console**.</span></span>
   
    ![Console do Gerenciador de Pacotes no menu Ferramentas][addcode008]
2. <span data-ttu-id="97611-198">Na janela **Console do Gerenciador de Pacotes** , digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="97611-198">In the **Package Manager Console** window, enter the following command:</span></span>
   
        enable-migrations 
   
    <span data-ttu-id="97611-199">O comando **enable-migrations** cria a pasta *Migrações* e coloca nessa pasta um arquivo *Configuration.cs*, que pode ser editado para configurar Migrações.</span><span class="sxs-lookup"><span data-stu-id="97611-199">The **enable-migrations** command creates a *Migrations* folder and it puts in that folder a *Configuration.cs* file that you can edit to configure Migrations.</span></span> 
3. <span data-ttu-id="97611-200">Na janela **Console do Gerenciador de Pacotes** , digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="97611-200">In the **Package Manager Console** window, enter the following command:</span></span>
   
        add-migration Initial
   
    <span data-ttu-id="97611-201">O comando **add-migration Initial** gera uma classe denominada **&lt;date_stamp&gt;Initial**, que cria o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="97611-201">The **add-migration Initial** command generates a class named **&lt;date_stamp&gt;Initial** that creates the database.</span></span> <span data-ttu-id="97611-202">O primeiro parâmetro ( *Initial* ) é arbitrário e é usado para criar o nome do arquivo.</span><span class="sxs-lookup"><span data-stu-id="97611-202">The first parameter ( *Initial* ) is arbitrary and used to create the name of the file.</span></span> <span data-ttu-id="97611-203">Você pode ver os novos arquivos de classe no **Gerenciador de Soluções**.</span><span class="sxs-lookup"><span data-stu-id="97611-203">You can see the new class files in **Solution Explorer**.</span></span>
   
    <span data-ttu-id="97611-204">Na classe **Inicial**, o método **Up** cria a tabela Contatos e o método **Down** (usado quando você deseja retornar ao estado anterior) a descarta.</span><span class="sxs-lookup"><span data-stu-id="97611-204">In the **Initial** class, the **Up** method creates the Contacts table, and the **Down** method (used when you want to return to the previous state) drops it.</span></span>
4. <span data-ttu-id="97611-205">Abra o arquivo *Migrations\Configuration.cs*.</span><span class="sxs-lookup"><span data-stu-id="97611-205">Open the *Migrations\Configuration.cs* file.</span></span> 
5. <span data-ttu-id="97611-206">Adicione os seguintes namespaces.</span><span class="sxs-lookup"><span data-stu-id="97611-206">Add the following namespaces.</span></span> 
   
         using ContactManager.Models;
6. <span data-ttu-id="97611-207">Substitua o método *Seed* pelo seguinte código:</span><span class="sxs-lookup"><span data-stu-id="97611-207">Replace the *Seed* method with the following code:</span></span>
   
        protected override void Seed(ContactManager.Models.ContactManagerContext context)
        {
            context.Contacts.AddOrUpdate(p => p.Name,
               new Contact
               {
                   Name = "Debra Garcia",
                   Address = "1234 Main St",
                   City = "Redmond",
                   State = "WA",
                   Zip = "10999",
                   Email = "debra@example.com",
                   Twitter = "debra_example"
               },
                new Contact
                {
                    Name = "Thorsten Weinrich",
                    Address = "5678 1st Ave W",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "thorsten@example.com",
                    Twitter = "thorsten_example"
                },
                new Contact
                {
                    Name = "Yuhong Li",
                    Address = "9012 State st",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "yuhong@example.com",
                    Twitter = "yuhong_example"
                },
                new Contact
                {
                    Name = "Jon Orton",
                    Address = "3456 Maple St",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "jon@example.com",
                    Twitter = "jon_example"
                },
                new Contact
                {
                    Name = "Diliana Alexieva-Bosseva",
                    Address = "7890 2nd Ave E",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "diliana@example.com",
                    Twitter = "diliana_example"
                }
                );
        }
   
    <span data-ttu-id="97611-208">O código acima inicializa o banco de dados com as informações de contato.</span><span class="sxs-lookup"><span data-stu-id="97611-208">This code above will initialize the database with the contact information.</span></span> <span data-ttu-id="97611-209">Para obter mais informações sobre a propagação do banco de dados, consulte [Depurando BDs do Entity Framework (EF) (a página pode estar em inglês)](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).</span><span class="sxs-lookup"><span data-stu-id="97611-209">For more information on seeding the database, see [Debugging Entity Framework (EF) DBs](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).</span></span>
7. <span data-ttu-id="97611-210">Em **Console do Gerenciador de Pacotes** , digite o comando:</span><span class="sxs-lookup"><span data-stu-id="97611-210">In the **Package Manager Console** enter the command:</span></span>
   
        update-database
   
    ![Comandos do Console do Gerenciador de Pacotes][addcode009]
   
    <span data-ttu-id="97611-212">O **update-database** executa a primeira migração que cria o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="97611-212">The **update-database** runs the first migration which creates the database.</span></span> <span data-ttu-id="97611-213">Por padrão, o banco de dados é criado como um banco de dados LocalDB do SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="97611-213">By default, the database is created as a SQL Server Express LocalDB database.</span></span>
8. <span data-ttu-id="97611-214">Pressione CTRL+F5 para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="97611-214">Press CTRL+F5 to run the application.</span></span> 

<span data-ttu-id="97611-215">O aplicativo mostra os dados de semente e fornece links de edição, detalhes e exclusão.</span><span class="sxs-lookup"><span data-stu-id="97611-215">The application shows the seed data and provides edit, details and delete links.</span></span>

![Exibição do MVC de dados][rxz3]

## <a name="edit-the-view"></a><span data-ttu-id="97611-217">Editar a exibição</span><span class="sxs-lookup"><span data-stu-id="97611-217">Edit the View</span></span>
1. <span data-ttu-id="97611-218">Abra o arquivo *Views\Home\Index.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="97611-218">Open the *Views\Home\Index.cshtml* file.</span></span> <span data-ttu-id="97611-219">Na próxima etapa, substituiremos a marcação gerada pelo código que usa [jQuery](http://jquery.com/) e [Knockout.js](http://knockoutjs.com/).</span><span class="sxs-lookup"><span data-stu-id="97611-219">In the next step, we will replace the generated markup with code that uses [jQuery](http://jquery.com/) and [Knockout.js](http://knockoutjs.com/).</span></span> <span data-ttu-id="97611-220">Esse novo código recupera a lista de contatos do uso da API Web e do JSON e associa os dados de contato à interface do usuário usando knockout.js.</span><span class="sxs-lookup"><span data-stu-id="97611-220">This new code retrieves the list of contacts from using web API and JSON and then binds the contact data to the UI using knockout.js.</span></span> <span data-ttu-id="97611-221">Para obter mais informações, consulte a seção [Próximas Etapas](#nextsteps) no final deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="97611-221">For more information, see the [Next Steps](#nextsteps) section at the end of this tutorial.</span></span> 
2. <span data-ttu-id="97611-222">Substitua o conteúdo do arquivo pelo código a seguir.</span><span class="sxs-lookup"><span data-stu-id="97611-222">Replace the contents of the file with the following code.</span></span>
   
        @model IEnumerable<ContactManager.Models.Contact>
        @{
            ViewBag.Title = "Home";
        }
        @section Scripts {
            @Scripts.Render("~/bundles/knockout")
            <script type="text/javascript">
                function ContactsViewModel() {
                    var self = this;
                    self.contacts = ko.observableArray([]);
                    self.addContact = function () {
                        $.post("api/contacts",
                            $("#addContact").serialize(),
                            function (value) {
                                self.contacts.push(value);
                            },
                            "json");
                    }
                    self.removeContact = function (contact) {
                        $.ajax({
                            type: "DELETE",
                            url: contact.Self,
                            success: function () {
                                self.contacts.remove(contact);
                            }
                        });
                    }
   
                    $.getJSON("api/contacts", function (data) {
                        self.contacts(data);
                    });
                }
                ko.applyBindings(new ContactsViewModel());    
        </script>
        }
        <ul id="contacts" data-bind="foreach: contacts">
            <li class="ui-widget-content ui-corner-all">
                <h1 data-bind="text: Name" class="ui-widget-header"></h1>
                <div><span data-bind="text: $data.Address || 'Address?'"></span></div>
                <div>
                    <span data-bind="text: $data.City || 'City?'"></span>,
                    <span data-bind="text: $data.State || 'State?'"></span>
                    <span data-bind="text: $data.Zip || 'Zip?'"></span>
                </div>
                <div data-bind="if: $data.Email"><a data-bind="attr: { href: 'mailto:' + Email }, text: Email"></a></div>
                <div data-bind="ifnot: $data.Email"><span>Email?</span></div>
                <div data-bind="if: $data.Twitter"><a data-bind="attr: { href: 'http://twitter.com/' + Twitter }, text: '@@' + Twitter"></a></div>
                <div data-bind="ifnot: $data.Twitter"><span>Twitter?</span></div>
                <p><a data-bind="attr: { href: Self }, click: $root.removeContact" class="removeContact ui-state-default ui-corner-all">Remove</a></p>
            </li>
        </ul>
        <form id="addContact" data-bind="submit: addContact">
            <fieldset>
                <legend>Add New Contact</legend>
                <ol>
                    <li>
                        <label for="Name">Name</label>
                        <input type="text" name="Name" />
                    </li>
                    <li>
                        <label for="Address">Address</label>
                        <input type="text" name="Address" >
                    </li>
                    <li>
                        <label for="City">City</label>
                        <input type="text" name="City" />
                    </li>
                    <li>
                        <label for="State">State</label>
                        <input type="text" name="State" />
                    </li>
                    <li>
                        <label for="Zip">Zip</label>
                        <input type="text" name="Zip" />
                    </li>
                    <li>
                        <label for="Email">E-mail</label>
                        <input type="text" name="Email" />
                    </li>
                    <li>
                        <label for="Twitter">Twitter</label>
                        <input type="text" name="Twitter" />
                    </li>
                </ol>
                <input type="submit" value="Add" />
            </fieldset>
        </form>
3. <span data-ttu-id="97611-223">Clique com o botão direito do mouse na pasta Content e clique em **Adicionar** e em **Novo Item...**.</span><span class="sxs-lookup"><span data-stu-id="97611-223">Right-click the Content folder and click **Add**, and then click **New Item...**.</span></span>
   
    ![Adicionar folha de estilos no menu de contexto da pasta Content][addcode005]
4. <span data-ttu-id="97611-225">Na caixa de diálogo **Adicionar Novo Item**, digite **Estilo** na caixa de pesquisa na parte superior direita e escolha **Folha de Estilos**.</span><span class="sxs-lookup"><span data-stu-id="97611-225">In the **Add New Item** dialog box, enter **Style** in the upper right search box and then select **Style Sheet**.</span></span>
    <span data-ttu-id="97611-226">![Caixa de diálogo Adicionar Novo Item][rxStyle]</span><span class="sxs-lookup"><span data-stu-id="97611-226">![Add New Item dialog box][rxStyle]</span></span>
5. <span data-ttu-id="97611-227">Nomeie o arquivo *Contacts.css* e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="97611-227">Name the file *Contacts.css* and click **Add**.</span></span> <span data-ttu-id="97611-228">Substitua o conteúdo do arquivo pelo código a seguir.</span><span class="sxs-lookup"><span data-stu-id="97611-228">Replace the contents of the file with the following code.</span></span>
   
        .column {
            float: left;
            width: 50%;
            padding: 0;
            margin: 5px 0;
        }
        form ol {
            list-style-type: none;
            padding: 0;
            margin: 0;
        }
        form li {
            padding: 1px;
            margin: 3px;
        }
        form input[type="text"] {
            width: 100%;
        }
        #addContact {
            width: 300px;
            float: left;
            width:30%;
        }
        #contacts {
            list-style-type: none;
            margin: 0;
            padding: 0;
            float:left;
            width: 70%;
        }
        #contacts li {
            margin: 3px 3px 3px 0;
            padding: 1px;
            float: left;
            width: 300px;
            text-align: center;
            background-image: none;
            background-color: #F5F5F5;
        }
        #contacts li h1
        {
            padding: 0;
            margin: 0;
            background-image: none;
            background-color: Orange;
            color: White;
            font-family: Trebuchet MS, Tahoma, Verdana, Arial, sans-serif;
        }
        .removeContact, .viewImage
        {
            padding: 3px;
            text-decoration: none;
        }
   
    <span data-ttu-id="97611-229">Usaremos esta folha de estilos no layout, nas cores e nos estilos usados no aplicativo do gerenciador de contatos.</span><span class="sxs-lookup"><span data-stu-id="97611-229">We will use this style sheet for the layout, colors and styles used in the contact manager app.</span></span>
6. <span data-ttu-id="97611-230">Abra o arquivo *AppStart\BundleConfig.cs*.</span><span class="sxs-lookup"><span data-stu-id="97611-230">Open the *App_Start\BundleConfig.cs* file.</span></span>
7. <span data-ttu-id="97611-231">Adicione o código a seguir para registrar o plug-in [Knockout](http://knockoutjs.com/index.html "KO") .</span><span class="sxs-lookup"><span data-stu-id="97611-231">Add the following code to register the [Knockout](http://knockoutjs.com/index.html "KO") plugin.</span></span>
   
        bundles.Add(new ScriptBundle("~/bundles/knockout").Include(
                    "~/Scripts/knockout-{version}.js"));
    <span data-ttu-id="97611-232">Este exemplo usa o knockout para simplificar o código JavaScript dinâmico que lida com os modelos de tela.</span><span class="sxs-lookup"><span data-stu-id="97611-232">This sample using knockout to simplify dynamic JavaScript code that handles the screen templates.</span></span>
8. <span data-ttu-id="97611-233">Modifique a entrada contents/css para registrar a folha de estilos de *contacts.css* .</span><span class="sxs-lookup"><span data-stu-id="97611-233">Modify the contents/css entry to register the *contacts.css* style sheet.</span></span> <span data-ttu-id="97611-234">Altere a linha a seguir:</span><span class="sxs-lookup"><span data-stu-id="97611-234">Change the following line:</span></span>
   
                 bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/site.css"));
   <span data-ttu-id="97611-235">Para:</span><span class="sxs-lookup"><span data-stu-id="97611-235">To:</span></span>
   
        bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/contacts.css",
                   "~/Content/site.css"));
9. <span data-ttu-id="97611-236">No Console do Gerenciador de Pacotes, execute o comando a seguir para instalar o Knockout.</span><span class="sxs-lookup"><span data-stu-id="97611-236">In the Package Manager Console, run the following command to install Knockout.</span></span>
   
        Install-Package knockoutjs

## <a name="add-a-controller-for-the-web-api-restful-interface"></a><span data-ttu-id="97611-237">Adicionar um controlador para a interface da API Web Restful</span><span class="sxs-lookup"><span data-stu-id="97611-237">Add a controller for the Web API Restful interface</span></span>
1. <span data-ttu-id="97611-238">No **Gerenciador de Soluções**, clique com o botão direito do mouse em Controllers, clique em **Adicionar** e, em seguida, em **Controlador...**</span><span class="sxs-lookup"><span data-stu-id="97611-238">In **Solution Explorer**, right-click Controllers and click **Add** and then **Controller....**</span></span> 
2. <span data-ttu-id="97611-239">Na caixa de diálogo **Adicionar Scaffold**, insira **Controlador da Web API 2 com ações, usando o Entity Framework** e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="97611-239">In the **Add Scaffold** dialog box, enter **Web API 2 Controller with actions, using Entity Framework** and then click **Add**.</span></span>
   
    ![Adicionar a API do controlador](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt1.png)
3. <span data-ttu-id="97611-241">Na caixa de diálogo **Adicionar Controlador** , insira "ContactsController" como o nome do controlador.</span><span class="sxs-lookup"><span data-stu-id="97611-241">In the **Add Controller** dialog box, enter "ContactsController" as your controller name.</span></span> <span data-ttu-id="97611-242">Selecione "Contato (ContactManager.Models)" para a **Classe do modelo**.</span><span class="sxs-lookup"><span data-stu-id="97611-242">Select "Contact (ContactManager.Models)" for the **Model class**.</span></span>  <span data-ttu-id="97611-243">Mantenha o valor padrão para o **Classe de contexto de dados**.</span><span class="sxs-lookup"><span data-stu-id="97611-243">Keep the default value for the **Data context class**.</span></span> 
4. <span data-ttu-id="97611-244">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="97611-244">Click **Add**.</span></span>

### <a name="run-the-application-locally"></a><span data-ttu-id="97611-245">Executar o aplicativo localmente</span><span class="sxs-lookup"><span data-stu-id="97611-245">Run the application locally</span></span>
1. <span data-ttu-id="97611-246">Pressione CTRL+F5 para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="97611-246">Press CTRL+F5 to run the application.</span></span>
   
    ![Página de índice][intro001]
2. <span data-ttu-id="97611-248">Digite um contato e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="97611-248">Enter a contact and click **Add**.</span></span> <span data-ttu-id="97611-249">O aplicativo retorna para a home page e exibe o contato que você inseriu.</span><span class="sxs-lookup"><span data-stu-id="97611-249">The app returns to the home page and displays the contact you entered.</span></span>
   
    ![Página de índice com itens da lista de tarefas pendentes][addwebapi004]
3. <span data-ttu-id="97611-251">No navegador, acrescente **/api/contacts** à URL.</span><span class="sxs-lookup"><span data-stu-id="97611-251">In the browser, append **/api/contacts** to the URL.</span></span>
   
    <span data-ttu-id="97611-252">A URL resultante será semelhante a http://localhost:1234/api/contacts.</span><span class="sxs-lookup"><span data-stu-id="97611-252">The resulting URL will resemble http://localhost:1234/api/contacts.</span></span> <span data-ttu-id="97611-253">A API Web RESTful que você adicionou retorna os contatos armazenados.</span><span class="sxs-lookup"><span data-stu-id="97611-253">The RESTful web API you added returns the stored contacts.</span></span> <span data-ttu-id="97611-254">O Firefox e o Chrome exibirão os dados em formato XML.</span><span class="sxs-lookup"><span data-stu-id="97611-254">Firefox and Chrome will display the data in XML format.</span></span>
   
    ![Página de índice com itens da lista de tarefas pendentes][rxFFchrome]

    <span data-ttu-id="97611-256">O IE solicitará que você abra ou salve os contatos.</span><span class="sxs-lookup"><span data-stu-id="97611-256">IE will prompt you to open or save the contacts.</span></span>

    ![Caixa de diálogo Salvar API Web][addwebapi006]


    <span data-ttu-id="97611-258">Você pode abrir os contatos retornados no bloco de notas ou em um navegador.</span><span class="sxs-lookup"><span data-stu-id="97611-258">You can open the returned contacts in notepad or a browser.</span></span>

    <span data-ttu-id="97611-259">Essa saída pode ser consumida por outro aplicativo, como um aplicativo ou uma página da web móvel.</span><span class="sxs-lookup"><span data-stu-id="97611-259">This output can be consumed by another application such as mobile web page or application.</span></span>

    ![Caixa de diálogo Salvar API Web][addwebapi007]

    <span data-ttu-id="97611-261">**Aviso de Segurança**: neste ponto, o aplicativo não é seguro e está vulnerável a ataques CSRF.</span><span class="sxs-lookup"><span data-stu-id="97611-261">**Security Warning**: At this point, your application is insecure and vulnerable to CSRF attack.</span></span> <span data-ttu-id="97611-262">Mais à frente no tutorial, removeremos essa vulnerabilidade.</span><span class="sxs-lookup"><span data-stu-id="97611-262">Later in the tutorial we will remove this vulnerability.</span></span> <span data-ttu-id="97611-263">Para obter mais informações, confira [Evitando ataques de solicitação intersite forjada (CSRF)][prevent-csrf-attacks].</span><span class="sxs-lookup"><span data-stu-id="97611-263">For more information see [Preventing Cross-Site Request Forgery (CSRF) Attacks][prevent-csrf-attacks].</span></span>
## <a name="add-xsrf-protection"></a><span data-ttu-id="97611-264">Adicionar proteção XSRF</span><span class="sxs-lookup"><span data-stu-id="97611-264">Add XSRF Protection</span></span>
<span data-ttu-id="97611-265">A solicitação entre sites forjada (também conhecida como XSRF ou CSRF) é um ataque contra aplicativos web hospedados, no qual um site mal-intencionado pode influenciar a interação entre um navegador cliente e um site confiável para esse navegador.</span><span class="sxs-lookup"><span data-stu-id="97611-265">Cross-site request forgery (also known as XSRF or CSRF) is an attack against web-hosted applications whereby a malicious website can influence the interaction between a client browser and a website trusted by that browser.</span></span> <span data-ttu-id="97611-266">Esses ataques são possibilitados porque os navegadores da web enviarão tokens de autenticação automaticamente com toda solicitação para um site.</span><span class="sxs-lookup"><span data-stu-id="97611-266">These attacks are made possible because web browsers will send authentication tokens automatically with every request to a website.</span></span> <span data-ttu-id="97611-267">O exemplo canônico é um cookie de autenticação, como o tíquete de autenticação de formulários do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="97611-267">The canonical example is an authentication cookie, such as ASP.NET's Forms Authentication ticket.</span></span> <span data-ttu-id="97611-268">No entanto, os sites que usam qualquer mecanismo de autenticação persistente (como a autenticação do Windows, Basic e assim por diante) podem ser alvos desses ataques.</span><span class="sxs-lookup"><span data-stu-id="97611-268">However, websites which use any persistent authentication mechanism (such as Windows Authentication, Basic, and so forth) can be targeted by these attacks.</span></span>

<span data-ttu-id="97611-269">Um ataque XSRF é diferente de um ataque de phishing.</span><span class="sxs-lookup"><span data-stu-id="97611-269">An XSRF attack is distinct from a phishing attack.</span></span> <span data-ttu-id="97611-270">Os ataques de phishing exigem a interação da vítima.</span><span class="sxs-lookup"><span data-stu-id="97611-270">Phishing attacks require interaction from the victim.</span></span> <span data-ttu-id="97611-271">Em um ataque de phishing, um site mal-intencionado imita o site de destino e a vítima é levada a fornecer informações confidenciais ao invasor.</span><span class="sxs-lookup"><span data-stu-id="97611-271">In a phishing attack, a malicious website will mimic the target website, and the victim is fooled into providing sensitive information to the attacker.</span></span> <span data-ttu-id="97611-272">Em um ataque XSRF, normalmente não é necessária nenhuma interação da vítima.</span><span class="sxs-lookup"><span data-stu-id="97611-272">In an XSRF attack, there is often no interaction necessary from the victim.</span></span> <span data-ttu-id="97611-273">Em vez disso, o invasor conta com que o navegador envie automaticamente todos os cookies relevantes ao site de destino.</span><span class="sxs-lookup"><span data-stu-id="97611-273">Rather, the attacker is relying on the browser automatically sending all relevant cookies to the destination website.</span></span>

<span data-ttu-id="97611-274">Para saber mais, confira [Open Web Application Security Project](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).</span><span class="sxs-lookup"><span data-stu-id="97611-274">For more information, see the [Open Web Application Security Project](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).</span></span>

1. <span data-ttu-id="97611-275">No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto **ContactManager**, clique em **Adicionar** e em **Classe**.</span><span class="sxs-lookup"><span data-stu-id="97611-275">In **Solution Explorer**, right **ContactManager** project and click **Add** and then click **Class**.</span></span>
2. <span data-ttu-id="97611-276">Nomeie o arquivo como *ValidateHttpAntiForgeryTokenAttribute.cs* e adicione o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="97611-276">Name the file *ValidateHttpAntiForgeryTokenAttribute.cs* and add the following code:</span></span>
   
        using System;
        using System.Collections.Generic;
        using System.Linq;
        using System.Net;
        using System.Net.Http;
        using System.Web.Helpers;
        using System.Web.Http.Controllers;
        using System.Web.Http.Filters;
        using System.Web.Mvc;
        namespace ContactManager.Filters
        {
            public class ValidateHttpAntiForgeryTokenAttribute : AuthorizationFilterAttribute
            {
                public override void OnAuthorization(HttpActionContext actionContext)
                {
                    HttpRequestMessage request = actionContext.ControllerContext.Request;
                    try
                    {
                        if (IsAjaxRequest(request))
                        {
                            ValidateRequestHeader(request);
                        }
                        else
                        {
                            AntiForgery.Validate();
                        }
                    }
                    catch (HttpAntiForgeryException e)
                    {
                        actionContext.Response = request.CreateErrorResponse(HttpStatusCode.Forbidden, e);
                    }
                }
                private bool IsAjaxRequest(HttpRequestMessage request)
                {
                    IEnumerable<string> xRequestedWithHeaders;
                    if (request.Headers.TryGetValues("X-Requested-With", out xRequestedWithHeaders))
                    {
                        string headerValue = xRequestedWithHeaders.FirstOrDefault();
                        if (!String.IsNullOrEmpty(headerValue))
                        {
                            return String.Equals(headerValue, "XMLHttpRequest", StringComparison.OrdinalIgnoreCase);
                        }
                    }
                    return false;
                }
                private void ValidateRequestHeader(HttpRequestMessage request)
                {
                    string cookieToken = String.Empty;
                    string formToken = String.Empty;
                    IEnumerable<string> tokenHeaders;
                    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
                    {
                        string tokenValue = tokenHeaders.FirstOrDefault();
                        if (!String.IsNullOrEmpty(tokenValue))
                        {
                            string[] tokens = tokenValue.Split(':');
                            if (tokens.Length == 2)
                            {
                                cookieToken = tokens[0].Trim();
                                formToken = tokens[1].Trim();
                            }
                        }
                    }
                    AntiForgery.Validate(cookieToken, formToken);
                }
            }
        }
3. <span data-ttu-id="97611-277">Adicione a instrução *using* a seguir ao controlador de contratos, de forma que você tenha acesso ao atributo **[ValidateHttpAntiForgeryToken]** .</span><span class="sxs-lookup"><span data-stu-id="97611-277">Add the following *using* statement to the contracts controller so you have access to the **[ValidateHttpAntiForgeryToken]** attribute.</span></span>
   
        using ContactManager.Filters;
4. <span data-ttu-id="97611-278">Adicione o atributo **[ValidateHttpAntiForgeryToken]** aos métodos Post do **ContactsController** para protegê-lo contra ameaças XSRF.</span><span class="sxs-lookup"><span data-stu-id="97611-278">Add the **[ValidateHttpAntiForgeryToken]** attribute to the Post methods of the **ContactsController** to protect it from XSRF threats.</span></span> <span data-ttu-id="97611-279">Você o adicionará aos métodos de ação "PutContact", "PostContact" e **DeleteContact**.</span><span class="sxs-lookup"><span data-stu-id="97611-279">You will add it to the "PutContact",  "PostContact" and **DeleteContact** action methods.</span></span>
   
        [ValidateHttpAntiForgeryToken]
            public IHttpActionResult PutContact(int id, Contact contact)
            {
5. <span data-ttu-id="97611-280">Atualize a seção *Scripts* do arquivo *Views\Home\Index.cshtml* de modo a incluir o código para obtenção de tokens XSRF.</span><span class="sxs-lookup"><span data-stu-id="97611-280">Update the *Scripts* section of the *Views\Home\Index.cshtml* file to include code to get the XSRF tokens.</span></span>
   
         @section Scripts {
            @Scripts.Render("~/bundles/knockout")
            <script type="text/javascript">
                @functions{
                   public string TokenHeaderValue()
                   {
                      string cookieToken, formToken;
                      AntiForgery.GetTokens(null, out cookieToken, out formToken);
                      return cookieToken + ":" + formToken;                
                   }
                }
   
               function ContactsViewModel() {
                  var self = this;
                  self.contacts = ko.observableArray([]);
                  self.addContact = function () {
   
                     $.ajax({
                        type: "post",
                        url: "api/contacts",
                        data: $("#addContact").serialize(),
                        dataType: "json",
                        success: function (value) {
                           self.contacts.push(value);
                        },
                        headers: {
                           'RequestVerificationToken': '@TokenHeaderValue()'
                        }
                     });
   
                  }
                  self.removeContact = function (contact) {
                     $.ajax({
                        type: "DELETE",
                        url: contact.Self,
                        success: function () {
                           self.contacts.remove(contact);
                        },
                        headers: {
                           'RequestVerificationToken': '@TokenHeaderValue()'
                        }
   
                     });
                  }
   
                  $.getJSON("api/contacts", function (data) {
                     self.contacts(data);
                  });
               }
               ko.applyBindings(new ContactsViewModel());
            </script>
         }

## <a name="publish-the-application-update-to-azure-and-sql-database"></a><span data-ttu-id="97611-281">Publicar a atualização do aplicativo no Azure e no Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="97611-281">Publish the application update to Azure and SQL Database</span></span>
<span data-ttu-id="97611-282">Para publicar o aplicativo, repita o procedimento seguido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="97611-282">To publish the application, you repeat the procedure you followed earlier.</span></span>

1. <span data-ttu-id="97611-283">No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto e escolha **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="97611-283">In **Solution Explorer**, right click the project and select **Publish**.</span></span>
   
    ![Publicar][rxP]
2. <span data-ttu-id="97611-285">Clique na guia **Configurações** .</span><span class="sxs-lookup"><span data-stu-id="97611-285">Click the **Settings** tab.</span></span>
3. <span data-ttu-id="97611-286">Em **ContactsManagerContext(ContactsManagerContext)**, clique no ícone **v** para alterar *Cadeia de conexão remota* para a cadeia de conexão do banco de dados de contato.</span><span class="sxs-lookup"><span data-stu-id="97611-286">Under **ContactsManagerContext(ContactsManagerContext)**, click the **v** icon to change *Remote connection string* to the connection string for the contact database.</span></span> <span data-ttu-id="97611-287">Clique em **ContactDB**.</span><span class="sxs-lookup"><span data-stu-id="97611-287">Click **ContactDB**.</span></span>
   
    ![Configurações](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt5.png)
4. <span data-ttu-id="97611-289">Marque a caixa de seleção de **Executar Codificar Migrações Iniciais (executado na inicialização do aplicativo)**.</span><span class="sxs-lookup"><span data-stu-id="97611-289">Check the box for **Execute Code First Migrations (runs on application start)**.</span></span>
5. <span data-ttu-id="97611-290">Clique em **Avançar** e, em seguida, em **Visualizar**.</span><span class="sxs-lookup"><span data-stu-id="97611-290">Click **Next** and then click **Preview**.</span></span> <span data-ttu-id="97611-291">O Visual Studio exibe uma lista dos arquivos que serão adicionados ou atualizados.</span><span class="sxs-lookup"><span data-stu-id="97611-291">Visual Studio displays a list of the files that will be added or updated.</span></span>
6. <span data-ttu-id="97611-292">Clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="97611-292">Click **Publish**.</span></span>
   <span data-ttu-id="97611-293">Depois que a implantação for concluída, o navegador será aberto na home page do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="97611-293">After the deployment completes, the browser opens to the home page of the application.</span></span>
   
    ![Página de índice sem contatos][intro001]
   
    <span data-ttu-id="97611-295">O processo de publicação do Visual Studio configurou automaticamente a cadeia de conexão no arquivo *Web.config* implantado para apontar para o banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="97611-295">The Visual Studio publish process automatically configured the connection string in the deployed *Web.config* file to point to the SQL database.</span></span> <span data-ttu-id="97611-296">Ele também configurou Codificar Migrações Iniciais para atualizar automaticamente o banco de dados para a versão mais recente na primeira vez em que o aplicativo acessar o banco de dados após a implantação.</span><span class="sxs-lookup"><span data-stu-id="97611-296">It also configured Code First Migrations to automatically upgrade the database to the latest version the first time the application accesses the database after deployment.</span></span>
   
    <span data-ttu-id="97611-297">Como resultado dessa configuração, o Código Primeiro criou o banco de dados executando o código na classe **Initial** que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="97611-297">As a result of this configuration, Code First created the database by running the code in the **Initial** class that you created earlier.</span></span> <span data-ttu-id="97611-298">Ele fez isso na primeira vez que o aplicativo tentou acessar o banco de dados após a implantação.</span><span class="sxs-lookup"><span data-stu-id="97611-298">It did this the first time the application tried to access the database after deployment.</span></span>
7. <span data-ttu-id="97611-299">Insira um contato como quando você executou o aplicativo localmente para verificar se a implantação do banco de dados teve êxito.</span><span class="sxs-lookup"><span data-stu-id="97611-299">Enter a contact as you did when you ran the app locally, to verify that database deployment succeeded.</span></span>

<span data-ttu-id="97611-300">Ao ver que o item inserido foi salvo e exibido na página do gerenciador de contatos, você sabe que ele foi armazenado no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="97611-300">When you see that the item you enter is saved and appears on the contact manager page, you know that it has been stored in the database.</span></span>

![Página de índice com contatos][addwebapi004]

<span data-ttu-id="97611-302">O aplicativo agora está sendo executado na nuvem, usando o Banco de dados SQL para armazenar seus dados.</span><span class="sxs-lookup"><span data-stu-id="97611-302">The application is now running in the cloud, using SQL Database to store its data.</span></span> <span data-ttu-id="97611-303">Depois de concluir o teste do aplicativo no Azure, exclua-o.</span><span class="sxs-lookup"><span data-stu-id="97611-303">After you finish testing the application in Azure, delete it.</span></span> <span data-ttu-id="97611-304">O aplicativo é público e não tem um mecanismo para limitar o acesso.</span><span class="sxs-lookup"><span data-stu-id="97611-304">The application is public and doesn't have a mechanism to limit access.</span></span>

> [!NOTE]
> <span data-ttu-id="97611-305">Se você deseja começar com o Serviço de Aplicativo do Azure antes de se inscrever em uma conta do Azure, acesse [Experimentar o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/), em que você pode criar imediatamente um aplicativo Web inicial de curta duração no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="97611-305">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="97611-306">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="97611-306">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="97611-307">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="97611-307">Next Steps</span></span>
<span data-ttu-id="97611-308">Outra maneira de armazenar dados em um aplicativo do Azure é usar o Armazenamento do Azure, que fornece armazenamento de dados não relacionais na forma de blobs e tabelas.</span><span class="sxs-lookup"><span data-stu-id="97611-308">Another way to store data in an Azure application is to use Azure storage, which provide non-relational data storage in the form of blobs and tables.</span></span> <span data-ttu-id="97611-309">Os links a seguir fornecem mais informações sobre a API Web, o ASP.NET MVC e o Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="97611-309">The following links provide more information on Web API, ASP.NET MVC and Window Azure.</span></span>

* <span data-ttu-id="97611-310">[Introdução ao Entity Framework usando MVC][EFCodeFirstMVCTutorial]</span><span class="sxs-lookup"><span data-stu-id="97611-310">[Getting Started with Entity Framework using MVC][EFCodeFirstMVCTutorial]</span></span>
* [<span data-ttu-id="97611-311">Introdução ao ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="97611-311">Intro to ASP.NET MVC 5</span></span>](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [<span data-ttu-id="97611-312">Sua primeira API Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="97611-312">Your First ASP.NET Web API</span></span>](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)
* [<span data-ttu-id="97611-313">Depurando WAWS</span><span class="sxs-lookup"><span data-stu-id="97611-313">Debugging WAWS</span></span>](web-sites-dotnet-troubleshoot-visual-studio.md)

<span data-ttu-id="97611-314">Este tutorial e o aplicativo de exemplo foram escritos por [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [@RickAndMSFT](https://twitter.com/RickAndMSFT)) com a ajuda de Tom Dykstra e de Barry Dorrans (Twitter [@blowdart](https://twitter.com/blowdart)).</span><span class="sxs-lookup"><span data-stu-id="97611-314">This tutorial and the sample application was written by [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [@RickAndMSFT](https://twitter.com/RickAndMSFT)) with assistance from Tom Dykstra and Barry Dorrans (Twitter [@blowdart](https://twitter.com/blowdart)).</span></span> 

<span data-ttu-id="97611-315">Deixe comentários sobre o que você gostou ou do que você gostaria de ver melhorado, não apenas sobre o próprio tutorial, mas também sobre os produtos que ele demonstra.</span><span class="sxs-lookup"><span data-stu-id="97611-315">Please leave feedback on what you liked or what you would like to see improved, not only about the tutorial itself but also about the products that it demonstrates.</span></span> <span data-ttu-id="97611-316">Seus comentários nos ajudarão a priorizar melhorias.</span><span class="sxs-lookup"><span data-stu-id="97611-316">Your feedback will help us prioritize improvements.</span></span> <span data-ttu-id="97611-317">Estamos especialmente interessados em saber quanto há de interesse em mais automação para o processo de configuração e implantação de banco de dados de associação.</span><span class="sxs-lookup"><span data-stu-id="97611-317">We are especially interested in finding out how much interest there is in more automation for the process of configuring and deploying the membership database.</span></span> 

## <a name="whats-changed"></a><span data-ttu-id="97611-318">O que mudou</span><span class="sxs-lookup"><span data-stu-id="97611-318">What's changed</span></span>
* <span data-ttu-id="97611-319">Para obter um guia sobre a alteração de Sites para o Serviço de Aplicativo, consulte: [Serviço de Aplicativo do Azure e seu impacto sobre os serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="97611-319">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- bookmarks -->
[Add an OAuth Provider]: #addOauth
[Add Roles to the Membership Database]:#mbrDB
[Create a Data Deployment Script]:#ppd
[Update the Membership Database]:#ppd2
[setupdbenv]: #bkmk_setupdevenv
[setupwindowsazureenv]: #bkmk_setupwindowsazure
[createapplication]: #bkmk_createmvc4app
[deployapp1]: #bkmk_deploytowindowsazure1
[adddb]: #bkmk_addadatabase
[addcontroller]: #bkmk_addcontroller
[addwebapi]: #bkmk_addwebapi
[deploy2]: #bkmk_deploydatabaseupdate

<!-- links -->
[EFCodeFirstMVCTutorial]: http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
[dbcontext-link]: http://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx


<!-- images-->
[rxE]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxE.png
[rxP]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxP.png
[rx22]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/
[rxb2]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxb2.png
[rxz]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz.png
[rxzz]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxzz.png
[rxz2]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz2.png
[rxz3]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz3.png
[rxStyle]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxStyle.png
[rxz4]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz4.png
[rxz44]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz44.png
[rxNewCtx]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxNewCtx.png
[rxPrevDB]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxPrevDB.png
[rxOverwrite]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxOverwrite.png
[rxPWS]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxPWS.png
[rxNewCtx]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxNewCtx.png
[rxAddApiController]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxAddApiController.png
[rxFFchrome]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxFFchrome.png
[intro001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobil-intro-finished-web-app.png
[rxCreateWSwithDB]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxCreateWSwithDB.png
[setup007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-setup-azure-site-004.png
[setup009]: ../Media/dntutmobile-setup-azure-site-006.png
[newapp002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-createapp-002.png
[newapp004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-createapp-004.png
[firsdeploy007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-deploy1-publish-005.png
[firsdeploy009]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-deploy1-publish-007.png
[adddb001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-adddatabase-001.png
[adddb002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-adddatabase-002.png
[addcode001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-context-menu.png
[addcode002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-controller-dialog.png
[addcode004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-modify-index-context.png
[addcode005]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-contents-context-menu.png
[addcode007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-modify-bundleconfig-context.png
[addcode008]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-migrations-package-manager-menu.png
[addcode009]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-migrations-package-manager-console.png
[addwebapi004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-added-contact.png
[addwebapi006]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-save-returned-contacts.png
[addwebapi007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-contacts-in-notepad.png
[Add XSRF Protection]: #xsrf
[WebPIAzureSdk20NetVS12]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/WebPIAzureSdk20NetVS12.png
[Add XSRF Protection]: #xsrf
[ImportPublishSettings]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ImportPublishSettings.png
[ImportPublishProfile]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ImportPublishProfile.png
[PublishVSSolution]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/PublishVSSolution.png
[ValidateConnection]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ValidateConnection.png
[WebPIAzureSdk20NetVS12]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/WebPIAzureSdk20NetVS12.png
[prevent-csrf-attacks]: http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-(csrf)-attacks

