---
title: aaaCreate uma API REST no Azure com o ASP.NET e o banco de dados SQL | Microsoft Docs
description: "Um tutorial que ensina como toodeploy um aplicativo que usa Olá ASP.NET Web API tooan aplicativo web do Azure usando o Visual Studio."
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
ms.openlocfilehash: 1ef45dd1582bfda367e53c39f863164422ad678b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-rest-service-using-aspnet-web-api-and-sql-database-in-azure-app-service"></a><span data-ttu-id="1fc5c-103">Criar um serviço REST usando a API Web ASP.NET e o Banco de Dados SQL no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="1fc5c-103">Create a REST service using ASP.NET Web API and SQL Database in Azure App Service</span></span>
<span data-ttu-id="1fc5c-104">Este tutorial mostra como toodeploy uma ASP.NET web aplicativo tooan [do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) usando o Assistente de publicar Web Olá no Visual Studio 2013 ou o Visual Studio 2013 Community Edition.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-104">This tutorial shows how toodeploy an ASP.NET web app tooan [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by using hello Publish Web wizard in Visual Studio 2013 or Visual Studio 2013 Community Edition.</span></span> 

<span data-ttu-id="1fc5c-105">Você pode abrir uma conta do Azure gratuitamente e se você ainda não tiver o Visual Studio 2013, Olá SDK instalará automaticamente o Visual Studio 2013 para Web Express.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-105">You can open an Azure account for free, and if you don't already have Visual Studio 2013, hello SDK automatically installs Visual Studio 2013 for Web Express.</span></span> <span data-ttu-id="1fc5c-106">Portanto, você pode começar a desenvolver para o Azure de maneira totalmente gratuita.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-106">So you can start developing for Azure entirely for free.</span></span>

<span data-ttu-id="1fc5c-107">Este tutorial pressupõe que você não tem nenhuma experiência anterior com o Azure.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-107">This tutorial assumes that you have no prior experience using Azure.</span></span> <span data-ttu-id="1fc5c-108">Ao concluir este tutorial, você terá um aplicativo da web simples para cima e em execução na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-108">On completing this tutorial, you'll have a simple web app up and running in hello cloud.</span></span>

<span data-ttu-id="1fc5c-109">Você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="1fc5c-109">You'll learn:</span></span>

* <span data-ttu-id="1fc5c-110">Como tooenable sua máquina de desenvolvimento do Azure instalando Olá SDK do Azure.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-110">How tooenable your machine for Azure development by installing hello Azure SDK.</span></span>
* <span data-ttu-id="1fc5c-111">Como toocreate um Visual Studio ASP.NET MVC 5 do projeto e publicá-lo tooan aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-111">How toocreate a Visual Studio ASP.NET MVC 5 project and publish it tooan Azure app.</span></span>
* <span data-ttu-id="1fc5c-112">Como toouse Olá ASP.NET Web API tooenable chamadas de API Restful.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-112">How toouse hello ASP.NET Web API tooenable Restful API calls.</span></span>
* <span data-ttu-id="1fc5c-113">Como toouse um SQL banco de dados toostore dados no Azure.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-113">How toouse a SQL database toostore data in Azure.</span></span>
* <span data-ttu-id="1fc5c-114">Como o aplicativo toopublish atualiza tooAzure.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-114">How toopublish application updates tooAzure.</span></span>

<span data-ttu-id="1fc5c-115">Será possível compilar um aplicativo da web de lista de contatos simples que se baseia no ASP.NET MVC 5 e usa hello ADO.NET Entity Framework para acesso de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-115">You'll build a simple contact list web application that is built on ASP.NET MVC 5 and uses hello ADO.NET Entity Framework for database access.</span></span> <span data-ttu-id="1fc5c-116">Olá seguinte ilustração mostra Olá concluída aplicativo:</span><span class="sxs-lookup"><span data-stu-id="1fc5c-116">hello following illustration shows hello completed application:</span></span>

![captura de tela do site][intro001]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

### <a name="create-hello-project"></a><span data-ttu-id="1fc5c-118">Criar projeto Olá</span><span class="sxs-lookup"><span data-stu-id="1fc5c-118">Create hello project</span></span>
1. <span data-ttu-id="1fc5c-119">Inicie o Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-119">Start Visual Studio 2013.</span></span>
2. <span data-ttu-id="1fc5c-120">De saudação **arquivo** menu clique **novo projeto**.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-120">From hello **File** menu click **New Project**.</span></span>
3. <span data-ttu-id="1fc5c-121">Em Olá **novo projeto** caixa de diálogo caixa, expanda **Visual C#** e selecione **Web** e, em seguida, selecione **aplicativo Web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-121">In hello **New Project** dialog box, expand **Visual C#** and select **Web**  and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="1fc5c-122">Nome do aplicativo hello **ContactManager** e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-122">Name hello application **ContactManager** and click **OK**.</span></span>
   
    ![Caixa de diálogo Novo Projeto](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr4.png)
4. <span data-ttu-id="1fc5c-124">Em Olá **novo projeto ASP.NET** caixa de diálogo, selecione Olá **MVC** modelo, verifique **API da Web** e, em seguida, clique em **alterar autenticação**.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-124">In hello **New ASP.NET Project** dialog box, select hello **MVC** template, check **Web API** and then click **Change Authentication**.</span></span>
5. <span data-ttu-id="1fc5c-125">Em Olá **alterar autenticação** caixa de diálogo, clique em **sem autenticação**e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-125">In hello **Change Authentication** dialog box, click **No Authentication**, and then click **OK**.</span></span>
   
    ![Sem Autenticação](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/GS13noauth.png)
   
    <span data-ttu-id="1fc5c-127">aplicativo de exemplo Hello que você está criando não tenha recursos que exigem toolog usuários em.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-127">hello sample application you're creating won't have features that require users toolog in.</span></span> <span data-ttu-id="1fc5c-128">Para obter informações sobre como tooimplement recursos de autenticação e autorização, consulte Olá [próximas etapas](#nextsteps) seção Olá final deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-128">For information about how tooimplement authentication and authorization features, see hello [Next Steps](#nextsteps) section at hello end of this tutorial.</span></span> 
6. <span data-ttu-id="1fc5c-129">Em Olá **novo projeto ASP.NET** caixa de diálogo, Olá se tornar **Host na nuvem de saudação** está marcada e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-129">In hello **New ASP.NET Project** dialog box, make sure hello **Host in hello Cloud** is checked and click **OK**.</span></span>

<span data-ttu-id="1fc5c-130">Se você não tiver entrado anteriormente no tooAzure, será solicitada toosign no.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-130">If you have not previously signed in tooAzure, you will be prompted toosign in.</span></span>

1. <span data-ttu-id="1fc5c-131">Assistente de configuração de saudação sugerirá um nome exclusivo baseado no *ContactManager* (consulte a imagem de saudação abaixo).</span><span class="sxs-lookup"><span data-stu-id="1fc5c-131">hello configuration wizard will suggest a unique name based on *ContactManager* (see hello image below).</span></span> <span data-ttu-id="1fc5c-132">Selecione uma região perto de você.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-132">Select a region near you.</span></span> <span data-ttu-id="1fc5c-133">Você pode usar [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") toofind Olá menor latência Datacenter.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-133">You can use [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") toofind hello lowest latency data center.</span></span> 
2. <span data-ttu-id="1fc5c-134">Se você não criou um servidor de banco de dados antes, selecione **Criar novo servidor**, digite um nome de usuário de banco de dados e uma senha.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-134">If you haven't created a database server before, select **Create new server**, enter a database user name and password.</span></span>
   
    ![Configurar o site do Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configAz.PNG)

<span data-ttu-id="1fc5c-136">Se você tiver um servidor de banco de dados, use esse toocreate um novo banco de dados.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-136">If you have a database server, use that toocreate a new database.</span></span> <span data-ttu-id="1fc5c-137">Servidores de banco de dados são um recurso precioso e geralmente você deseja toocreate vários bancos de dados Olá mesmo servidor de teste e desenvolvimento em vez de criar um servidor de banco de dados por banco de dados.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-137">Database servers are a precious resource, and you generally want toocreate multiple databases on hello same server for testing and development rather than creating a database server per database.</span></span> <span data-ttu-id="1fc5c-138">Verifique se o seu site da web e o banco de dados estão em hello mesma região.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-138">Make sure your web site and database are in hello same region.</span></span>

![Configurar o site do Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configWithDB.PNG)

### <a name="set-hello-page-header-and-footer"></a><span data-ttu-id="1fc5c-140">Definir Olá cabeçalho e rodapé</span><span class="sxs-lookup"><span data-stu-id="1fc5c-140">Set hello page header and footer</span></span>
1. <span data-ttu-id="1fc5c-141">Em **Solution Explorer**, expanda Olá *exibições \ compartilhadas* pasta e abra Olá *cshtml* arquivo.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-141">In **Solution Explorer**, expand hello *Views\Shared* folder and open hello *_Layout.cshtml* file.</span></span>
   
    ![_Layout.cshtml no Gerenciador de Soluções][newapp004]
2. <span data-ttu-id="1fc5c-143">Substitua o conteúdo de saudação do hello *Views\Shared_Layout.cshtml* arquivo com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="1fc5c-143">Replace hello contents of hello *Views\Shared_Layout.cshtml* file with hello following code:</span></span>

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

<span data-ttu-id="1fc5c-144">marcação de saudação acima do nome do aplicativo hello alterações de "My App ASP.NET" muito "gerente do contato" e remove links Olá muito**início**, **sobre** e **entre em contato com**.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-144">hello markup above changes hello app name from "My ASP.NET App" too"Contact Manager", and it removes hello links too**Home**, **About** and **Contact**.</span></span>

### <a name="run-hello-application-locally"></a><span data-ttu-id="1fc5c-145">Executar o aplicativo hello localmente</span><span class="sxs-lookup"><span data-stu-id="1fc5c-145">Run hello application locally</span></span>
1. <span data-ttu-id="1fc5c-146">Pressione CTRL + F5 aplicativo de hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-146">Press CTRL+F5 toorun hello application.</span></span>
   <span data-ttu-id="1fc5c-147">home page do aplicativo Hello aparece no navegador padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-147">hello application home page appears in hello default browser.</span></span>
    <span data-ttu-id="1fc5c-148">![página de início da lista de tooDo](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)</span><span class="sxs-lookup"><span data-stu-id="1fc5c-148">![tooDo List home page](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)</span></span>

<span data-ttu-id="1fc5c-149">Isso é tudo o que você precisa toodo para aplicativo de hello toocreate agora que você implantará tooAzure.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-149">This is all you need toodo for now toocreate hello application that you'll deploy tooAzure.</span></span> <span data-ttu-id="1fc5c-150">Posteriormente, você adicionará a funcionalidade do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-150">Later you'll add database functionality.</span></span>

## <a name="deploy-hello-application-tooazure"></a><span data-ttu-id="1fc5c-151">Implantar Olá aplicativo tooAzure</span><span class="sxs-lookup"><span data-stu-id="1fc5c-151">Deploy hello application tooAzure</span></span>
1. <span data-ttu-id="1fc5c-152">No Visual Studio, clique com botão direito Olá em **Solution Explorer** e selecione **publicar** Olá no menu de contexto.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-152">In Visual Studio, right-click hello project in **Solution Explorer** and select **Publish** from hello context menu.</span></span>
   
    ![Publicar no menu de contexto do projeto][PublishVSSolution]
   
    <span data-ttu-id="1fc5c-154">Olá **Publicar Web** assistente é aberto.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-154">hello **Publish Web** wizard opens.</span></span>
2. <span data-ttu-id="1fc5c-155">Clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-155">Click **Publish**.</span></span>

![Guia Configurações](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/pw.png)

<span data-ttu-id="1fc5c-157">O Visual Studio inicia o processo de saudação de copiar Olá arquivos toohello servidor do Azure.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-157">Visual Studio begins hello process of copying hello files toohello Azure server.</span></span> <span data-ttu-id="1fc5c-158">Olá **saída** janela mostra quais ações de implantação foram realizadas e relata a conclusão bem-sucedida da implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-158">hello **Output** window shows what deployment actions were taken and reports successful completion of hello deployment.</span></span>

1. <span data-ttu-id="1fc5c-159">navegador padrão de saudação é aberto automaticamente toohello URL do site Olá implantado.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-159">hello default browser automatically opens toohello URL of hello deployed site.</span></span>
   
   <span data-ttu-id="1fc5c-160">aplicativo Hello que você criou agora está em execução na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-160">hello application you created is now running in hello cloud.</span></span>
   
   ![página de início da lista de tooDo em execução no Azure][rxz2]

## <a name="add-a-database-toohello-application"></a><span data-ttu-id="1fc5c-162">Adicionar um aplicativo de toohello do banco de dados</span><span class="sxs-lookup"><span data-stu-id="1fc5c-162">Add a database toohello application</span></span>
<span data-ttu-id="1fc5c-163">Em seguida, você vai atualizar Olá MVC aplicativo tooadd Olá capacidade toodisplay e atualizar contatos e armazenar dados de saudação em um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-163">Next, you'll update hello MVC application tooadd hello ability toodisplay and update contacts and store hello data in a database.</span></span> <span data-ttu-id="1fc5c-164">aplicativo Hello usar tooread e o banco de dados do Entity Framework toocreate Olá Olá e atualizar dados no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-164">hello application will use hello Entity Framework toocreate hello database and tooread and update data in hello database.</span></span>

### <a name="add-data-model-classes-for-hello-contacts"></a><span data-ttu-id="1fc5c-165">Adicionar classes de modelo de dados para os contatos Olá</span><span class="sxs-lookup"><span data-stu-id="1fc5c-165">Add data model classes for hello contacts</span></span>
<span data-ttu-id="1fc5c-166">Você começa criando um modelo de dados simples no código.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-166">You begin by creating a simple data model in code.</span></span>

1. <span data-ttu-id="1fc5c-167">Em **Solution Explorer**, pasta de modelos de saudação, clique **adicionar**e, em seguida, **classe**.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-167">In **Solution Explorer**, right-click hello Models folder, click **Add**, and then **Class**.</span></span>
   
    ![Adicionar Classe no menu de contexto da pasta Modelos][adddb001]
2. <span data-ttu-id="1fc5c-169">Em Olá **Adicionar Novo Item** caixa de diálogo, o nome hello novo arquivo de classe *Contact.cs*e, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-169">In hello **Add New Item** dialog box, name hello new class file *Contact.cs*, and then click **Add**.</span></span>
   
    ![Caixa de diálogo Adicionar Novo Item][adddb002]
3. <span data-ttu-id="1fc5c-171">Substitua o conteúdo de saudação do arquivo de Contacts.cs de saudação com hello código a seguir.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-171">Replace hello contents of hello Contacts.cs file with hello following code.</span></span>
   
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

<span data-ttu-id="1fc5c-172">Olá **entre em contato com** classe define dados hello serão armazenados para cada contato, além de uma chave primária, a ID de contato, que é necessária para o banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-172">hello **Contact** class defines hello data that you will store for each contact, plus a primary key, ContactID, that is needed by hello database.</span></span> <span data-ttu-id="1fc5c-173">Você pode obter mais informações sobre modelos de dados em Olá [próximas etapas](#nextsteps) seção Olá final deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-173">You can get more information about data models in hello [Next Steps](#nextsteps) section at hello end of this tutorial.</span></span>

### <a name="create-web-pages-that-enable-app-users-toowork-with-hello-contacts"></a><span data-ttu-id="1fc5c-174">Criar páginas da web que permitem toowork de usuários do aplicativo com contatos Olá</span><span class="sxs-lookup"><span data-stu-id="1fc5c-174">Create web pages that enable app users toowork with hello contacts</span></span>
<span data-ttu-id="1fc5c-175">Olá recurso do ASP.NET MVC Olá scaffolding pode gerar automaticamente código que executa a criar, ler, atualizar e excluir ações (CRUD).</span><span class="sxs-lookup"><span data-stu-id="1fc5c-175">hello ASP.NET MVC hello scaffolding feature can automatically generate code that performs create, read, update, and delete (CRUD) actions.</span></span>

## <a name="add-a-controller-and-a-view-for-hello-data"></a><span data-ttu-id="1fc5c-176">Adicionar um controlador e uma exibição para dados de saudação</span><span class="sxs-lookup"><span data-stu-id="1fc5c-176">Add a Controller and a view for hello data</span></span>
1. <span data-ttu-id="1fc5c-177">Em **Solution Explorer**, expanda a pasta de controladores de saudação.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-177">In **Solution Explorer**, expand hello Controllers folder.</span></span>
2. <span data-ttu-id="1fc5c-178">Criar projeto Olá **(Ctrl + Shift + B)**.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-178">Build hello project **(Ctrl+Shift+B)**.</span></span> <span data-ttu-id="1fc5c-179">(Você deve criar o projeto de saudação antes de usar o mecanismo de scaffolding.)</span><span class="sxs-lookup"><span data-stu-id="1fc5c-179">(You must build hello project before using scaffolding mechanism.)</span></span> 
3. <span data-ttu-id="1fc5c-180">Pasta de controladores de saudação de mouse e clique em **adicionar**e, em seguida, clique em **controlador**.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-180">Right-click hello Controllers folder and click **Add**, and then click **Controller**.</span></span>
   
    ![Adicionar Controlador no menu de contexto da pasta Controladores][addcode001]
4. <span data-ttu-id="1fc5c-182">Em Olá **adicionar Scaffold** caixa de diálogo, selecione **controlador MVC com modos de exibição usando o Entity Framework** e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-182">In hello **Add Scaffold** dialog box, select **MVC Controller with views, using Entity Framework** and click **Add**.</span></span>
   
   ![Adicionar controlador](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rrAC.png)
5. <span data-ttu-id="1fc5c-184">Defina o nome do controlador Olá muito**HomeController**.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-184">Set hello controller name too**HomeController**.</span></span> <span data-ttu-id="1fc5c-185">Selecione **Contato** como a classe de modelo.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-185">Select **Contact** as your model class.</span></span> <span data-ttu-id="1fc5c-186">Clique em Olá **novo contexto de dados** botão e aceite o padrão de hello "ContactManager.Models.ContactManagerContext" hello **novo tipo de contexto de dados**.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-186">Click hello **New data context** button and accept hello default "ContactManager.Models.ContactManagerContext" for hello **New data context type**.</span></span> <span data-ttu-id="1fc5c-187">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-187">Click **Add**.</span></span>

    <span data-ttu-id="1fc5c-188">Uma caixa de diálogo solicitará que você: "um arquivo com nome hello HomeController já existente.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-188">A dialog box will prompt you: "A file with hello name HomeController already exits.</span></span> <span data-ttu-id="1fc5c-189">Você deseja tooreplace-lo? ".</span><span class="sxs-lookup"><span data-stu-id="1fc5c-189">Do you want tooreplace it?".</span></span> <span data-ttu-id="1fc5c-190">Clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-190">Click **Yes**.</span></span> <span data-ttu-id="1fc5c-191">Nós são substituindo Olá início controlador que foi criado com o novo projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-191">We are overwriting hello Home Controller that was created with hello new project.</span></span> <span data-ttu-id="1fc5c-192">Usaremos Olá novo início controlador para nossa lista de contatos.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-192">We will use hello new Home Controller for our contact list.</span></span>

    <span data-ttu-id="1fc5c-193">O Visual Studio cria métodos do controlador e modos de exibição para as operações de banco de dados CRUD para objetos **Contact** .</span><span class="sxs-lookup"><span data-stu-id="1fc5c-193">Visual Studio creates controller methods and views for CRUD database operations for **Contact** objects.</span></span>

## <a name="enable-migrations-create-hello-database-add-sample-data-and-a-data-initializer"></a><span data-ttu-id="1fc5c-194">Permitir as migrações, criar hello banco de dados, adicionar dados de exemplo e um inicializador de dados</span><span class="sxs-lookup"><span data-stu-id="1fc5c-194">Enable Migrations, create hello database, add sample data and a data initializer</span></span>
<span data-ttu-id="1fc5c-195">Olá próxima tarefa é Olá tooenable [migrações do Code First](http://curah.microsoft.com/55220) recurso no banco de dados do pedido toocreate Olá baseada no modelo de dados de saudação criado por você.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-195">hello next task is tooenable hello [Code First Migrations](http://curah.microsoft.com/55220) feature in order toocreate hello database based on hello data model you created.</span></span>

1. <span data-ttu-id="1fc5c-196">Em Olá **ferramentas** menu, selecione **Gerenciador de biblioteca de pacote** e **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-196">In hello **Tools** menu, select **Library Package Manager** and then **Package Manager Console**.</span></span>
   
    ![Console do Gerenciador de Pacotes no menu Ferramentas][addcode008]
2. <span data-ttu-id="1fc5c-198">Em Olá **Package Manager Console** janela, digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="1fc5c-198">In hello **Package Manager Console** window, enter hello following command:</span></span>
   
        enable-migrations 
   
    <span data-ttu-id="1fc5c-199">Olá **enable-migrations** comando cria um *migrações* pasta e o coloca na pasta um *Configuration.cs* arquivo que você pode editar tooconfigure migrações.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-199">hello **enable-migrations** command creates a *Migrations* folder and it puts in that folder a *Configuration.cs* file that you can edit tooconfigure Migrations.</span></span> 
3. <span data-ttu-id="1fc5c-200">Em Olá **Package Manager Console** janela, digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="1fc5c-200">In hello **Package Manager Console** window, enter hello following command:</span></span>
   
        add-migration Initial
   
    <span data-ttu-id="1fc5c-201">Olá **inicial de migração adicionar** comando gera uma classe denominada  **&lt;date_stamp&gt;inicial** que cria o banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-201">hello **add-migration Initial** command generates a class named **&lt;date_stamp&gt;Initial** that creates hello database.</span></span> <span data-ttu-id="1fc5c-202">Olá primeiro parâmetro ( *inicial* ) é arbitrário e usada toocreate Olá nome do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-202">hello first parameter ( *Initial* ) is arbitrary and used toocreate hello name of hello file.</span></span> <span data-ttu-id="1fc5c-203">Você pode ver os novos arquivos de classe Olá no **Gerenciador de soluções**.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-203">You can see hello new class files in **Solution Explorer**.</span></span>
   
    <span data-ttu-id="1fc5c-204">Em Olá **inicial** classe hello **backup** método cria a tabela de contatos hello e hello **para baixo** descarta método (usado quando você deseja que o estado anterior do tooreturn toohello).</span><span class="sxs-lookup"><span data-stu-id="1fc5c-204">In hello **Initial** class, hello **Up** method creates hello Contacts table, and hello **Down** method (used when you want tooreturn toohello previous state) drops it.</span></span>
4. <span data-ttu-id="1fc5c-205">Olá abrir *Migrations\Configuration.cs* arquivo.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-205">Open hello *Migrations\Configuration.cs* file.</span></span> 
5. <span data-ttu-id="1fc5c-206">Adicione Olá namespaces a seguir.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-206">Add hello following namespaces.</span></span> 
   
         using ContactManager.Models;
6. <span data-ttu-id="1fc5c-207">Substituir saudação *semente* método com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="1fc5c-207">Replace hello *Seed* method with hello following code:</span></span>
   
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
   
    <span data-ttu-id="1fc5c-208">Esse código acima será inicializar banco de dados de saudação com informações de contato de saudação.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-208">This code above will initialize hello database with hello contact information.</span></span> <span data-ttu-id="1fc5c-209">Para obter mais informações sobre a propagação do banco de dados hello, consulte [bancos de dados de depuração Entity Framework (EF)](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).</span><span class="sxs-lookup"><span data-stu-id="1fc5c-209">For more information on seeding hello database, see [Debugging Entity Framework (EF) DBs](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).</span></span>
7. <span data-ttu-id="1fc5c-210">Em Olá **Package Manager Console** digite Olá comando:</span><span class="sxs-lookup"><span data-stu-id="1fc5c-210">In hello **Package Manager Console** enter hello command:</span></span>
   
        update-database
   
    ![Comandos do Console do Gerenciador de Pacotes][addcode009]
   
    <span data-ttu-id="1fc5c-212">Olá **Atualizar banco de dados** executa Olá primeiro migração que cria o banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-212">hello **update-database** runs hello first migration which creates hello database.</span></span> <span data-ttu-id="1fc5c-213">Por padrão, o banco de dados de saudação é criado como um banco de dados do SQL Server Express LocalDB.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-213">By default, hello database is created as a SQL Server Express LocalDB database.</span></span>
8. <span data-ttu-id="1fc5c-214">Pressione CTRL + F5 aplicativo de hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-214">Press CTRL+F5 toorun hello application.</span></span> 

<span data-ttu-id="1fc5c-215">aplicativo Hello mostra dados de propagação de saudação e fornece edição, detalhes e links de exclusão.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-215">hello application shows hello seed data and provides edit, details and delete links.</span></span>

![Exibição do MVC de dados][rxz3]

## <a name="edit-hello-view"></a><span data-ttu-id="1fc5c-217">Editar saudação exibição</span><span class="sxs-lookup"><span data-stu-id="1fc5c-217">Edit hello View</span></span>
1. <span data-ttu-id="1fc5c-218">Olá abrir *Views\Home\Index.cshtml* arquivo.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-218">Open hello *Views\Home\Index.cshtml* file.</span></span> <span data-ttu-id="1fc5c-219">Na próxima etapa de hello, substituiremos marcação Olá gerado pelo código que usa [jQuery](http://jquery.com/) e [Knockout. js](http://knockoutjs.com/).</span><span class="sxs-lookup"><span data-stu-id="1fc5c-219">In hello next step, we will replace hello generated markup with code that uses [jQuery](http://jquery.com/) and [Knockout.js](http://knockoutjs.com/).</span></span> <span data-ttu-id="1fc5c-220">Esse novo código recupera a lista de contatos de saudação do usando a API da web e JSON e, em seguida, associa Olá entre em contato com dados toohello da interface do usuário usando Knockout. js.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-220">This new code retrieves hello list of contacts from using web API and JSON and then binds hello contact data toohello UI using knockout.js.</span></span> <span data-ttu-id="1fc5c-221">Para obter mais informações, consulte Olá [próximas etapas](#nextsteps) seção Olá final deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-221">For more information, see hello [Next Steps](#nextsteps) section at hello end of this tutorial.</span></span> 
2. <span data-ttu-id="1fc5c-222">Substitua o conteúdo de saudação do arquivo hello com hello código a seguir.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-222">Replace hello contents of hello file with hello following code.</span></span>
   
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
3. <span data-ttu-id="1fc5c-223">Pasta de conteúdo de saudação de mouse e clique em **adicionar**e, em seguida, clique em **Novo Item...** .</span><span class="sxs-lookup"><span data-stu-id="1fc5c-223">Right-click hello Content folder and click **Add**, and then click **New Item...**.</span></span>
   
    ![Adicionar folha de estilos no menu de contexto da pasta Content][addcode005]
4. <span data-ttu-id="1fc5c-225">Em Olá **Adicionar Novo Item** caixa de diálogo, digite **estilo** Olá caixa de pesquisa à direita superior e, em seguida, selecione **folha de estilo**.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-225">In hello **Add New Item** dialog box, enter **Style** in hello upper right search box and then select **Style Sheet**.</span></span>
    <span data-ttu-id="1fc5c-226">![Caixa de diálogo Adicionar Novo Item][rxStyle]</span><span class="sxs-lookup"><span data-stu-id="1fc5c-226">![Add New Item dialog box][rxStyle]</span></span>
5. <span data-ttu-id="1fc5c-227">Arquivo de saudação do nome *Contacts.css* e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-227">Name hello file *Contacts.css* and click **Add**.</span></span> <span data-ttu-id="1fc5c-228">Substitua o conteúdo de saudação do arquivo hello com hello código a seguir.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-228">Replace hello contents of hello file with hello following code.</span></span>
   
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
   
    <span data-ttu-id="1fc5c-229">Usaremos esta folha de estilos para layout hello, cores e estilos usados no aplicativo de contato do Gerenciador de saudação.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-229">We will use this style sheet for hello layout, colors and styles used in hello contact manager app.</span></span>
6. <span data-ttu-id="1fc5c-230">Olá abrir *App_Start\BundleConfig.cs* arquivo.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-230">Open hello *App_Start\BundleConfig.cs* file.</span></span>
7. <span data-ttu-id="1fc5c-231">Adicionar Olá Olá de tooregister de código a seguir [Knockout](http://knockoutjs.com/index.html "KO") plug-in.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-231">Add hello following code tooregister hello [Knockout](http://knockoutjs.com/index.html "KO") plugin.</span></span>
   
        bundles.Add(new ScriptBundle("~/bundles/knockout").Include(
                    "~/Scripts/knockout-{version}.js"));
    <span data-ttu-id="1fc5c-232">Este exemplo usando knockout toosimplify dinâmico código JavaScript que trata os modelos de tela hello.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-232">This sample using knockout toosimplify dynamic JavaScript code that handles hello screen templates.</span></span>
8. <span data-ttu-id="1fc5c-233">Modificar Olá Olá de tooregister de entrada de conteúdo/css *contacts.css* folha de estilos.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-233">Modify hello contents/css entry tooregister hello *contacts.css* style sheet.</span></span> <span data-ttu-id="1fc5c-234">Alterar Olá seguinte linha:</span><span class="sxs-lookup"><span data-stu-id="1fc5c-234">Change hello following line:</span></span>
   
                 bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/site.css"));
   <span data-ttu-id="1fc5c-235">Para:</span><span class="sxs-lookup"><span data-stu-id="1fc5c-235">To:</span></span>
   
        bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/contacts.css",
                   "~/Content/site.css"));
9. <span data-ttu-id="1fc5c-236">Olá Package Manager Console, a execução Olá comando tooinstall Knockout a seguir.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-236">In hello Package Manager Console, run hello following command tooinstall Knockout.</span></span>
   
        Install-Package knockoutjs

## <a name="add-a-controller-for-hello-web-api-restful-interface"></a><span data-ttu-id="1fc5c-237">Adicionar um controlador de interface da Web API Restful Olá</span><span class="sxs-lookup"><span data-stu-id="1fc5c-237">Add a controller for hello Web API Restful interface</span></span>
1. <span data-ttu-id="1fc5c-238">No **Gerenciador de Soluções**, clique com o botão direito do mouse em Controllers, clique em **Adicionar** e, em seguida, em **Controlador...**</span><span class="sxs-lookup"><span data-stu-id="1fc5c-238">In **Solution Explorer**, right-click Controllers and click **Add** and then **Controller....**</span></span> 
2. <span data-ttu-id="1fc5c-239">Em Olá **adicionar Scaffold** caixa de diálogo, digite **Web 2 controlador API com ações, usando o Entity Framework** e, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-239">In hello **Add Scaffold** dialog box, enter **Web API 2 Controller with actions, using Entity Framework** and then click **Add**.</span></span>
   
    ![Adicionar a API do controlador](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt1.png)
3. <span data-ttu-id="1fc5c-241">Em Olá **Adicionar controlador** caixa de diálogo, digite "ContactsController" como o nome do controlador.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-241">In hello **Add Controller** dialog box, enter "ContactsController" as your controller name.</span></span> <span data-ttu-id="1fc5c-242">Selecione "Contato (ContactManager.Models)" para Olá **classe modelo**.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-242">Select "Contact (ContactManager.Models)" for hello **Model class**.</span></span>  <span data-ttu-id="1fc5c-243">Manter o valor padrão Olá Olá **classe de contexto de dados**.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-243">Keep hello default value for hello **Data context class**.</span></span> 
4. <span data-ttu-id="1fc5c-244">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-244">Click **Add**.</span></span>

### <a name="run-hello-application-locally"></a><span data-ttu-id="1fc5c-245">Executar o aplicativo hello localmente</span><span class="sxs-lookup"><span data-stu-id="1fc5c-245">Run hello application locally</span></span>
1. <span data-ttu-id="1fc5c-246">Pressione CTRL + F5 aplicativo de hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-246">Press CTRL+F5 toorun hello application.</span></span>
   
    ![Página de índice][intro001]
2. <span data-ttu-id="1fc5c-248">Digite um contato e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-248">Enter a contact and click **Add**.</span></span> <span data-ttu-id="1fc5c-249">aplicativo Hello retorna home page do toohello e exibe o contato Olá inserido.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-249">hello app returns toohello home page and displays hello contact you entered.</span></span>
   
    ![Página de índice com itens da lista de tarefas pendentes][addwebapi004]
3. <span data-ttu-id="1fc5c-251">No navegador de hello, acrescente **/api/contatos** toohello URL.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-251">In hello browser, append **/api/contacts** toohello URL.</span></span>
   
    <span data-ttu-id="1fc5c-252">URL de saudação resultante será parecida com a api/http://localhost:1234/contatos.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-252">hello resulting URL will resemble http://localhost:1234/api/contacts.</span></span> <span data-ttu-id="1fc5c-253">Olá web RESTful API que você adicionou retorna contatos Olá armazenado.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-253">hello RESTful web API you added returns hello stored contacts.</span></span> <span data-ttu-id="1fc5c-254">Firefox e no Chrome, exibirá dados de saudação em formato XML.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-254">Firefox and Chrome will display hello data in XML format.</span></span>
   
    ![Página de índice com itens da lista de tarefas pendentes][rxFFchrome]

    <span data-ttu-id="1fc5c-256">IE será solicitará que você tooopen ou salvar contatos hello.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-256">IE will prompt you tooopen or save hello contacts.</span></span>

    ![Caixa de diálogo Salvar API Web][addwebapi006]


    <span data-ttu-id="1fc5c-258">Você pode abrir hello retornada contatos no bloco de notas ou em um navegador.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-258">You can open hello returned contacts in notepad or a browser.</span></span>

    <span data-ttu-id="1fc5c-259">Essa saída pode ser consumida por outro aplicativo, como um aplicativo ou uma página da web móvel.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-259">This output can be consumed by another application such as mobile web page or application.</span></span>

    ![Caixa de diálogo Salvar API Web][addwebapi007]

    <span data-ttu-id="1fc5c-261">**Aviso de segurança**: neste ponto, seu aplicativo é inseguro e vulnerável tooCSRF ataque.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-261">**Security Warning**: At this point, your application is insecure and vulnerable tooCSRF attack.</span></span> <span data-ttu-id="1fc5c-262">Posteriormente no tutorial Olá removeremos essa vulnerabilidade.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-262">Later in hello tutorial we will remove this vulnerability.</span></span> <span data-ttu-id="1fc5c-263">Para obter mais informações, confira [Evitando ataques de solicitação intersite forjada (CSRF)][prevent-csrf-attacks].</span><span class="sxs-lookup"><span data-stu-id="1fc5c-263">For more information see [Preventing Cross-Site Request Forgery (CSRF) Attacks][prevent-csrf-attacks].</span></span>
## <a name="add-xsrf-protection"></a><span data-ttu-id="1fc5c-264">Adicionar proteção XSRF</span><span class="sxs-lookup"><span data-stu-id="1fc5c-264">Add XSRF Protection</span></span>
<span data-ttu-id="1fc5c-265">Falsificação de solicitação entre sites (também conhecido como XSRF ou CSRF) é um ataque contra aplicativos web hospedados no qual um site mal-intencionado pode influenciar a interação de saudação entre um navegador de cliente e um site confiada pelo navegador.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-265">Cross-site request forgery (also known as XSRF or CSRF) is an attack against web-hosted applications whereby a malicious website can influence hello interaction between a client browser and a website trusted by that browser.</span></span> <span data-ttu-id="1fc5c-266">Esses ataques são possibilitados como navegadores da web enviará os tokens de autenticação automaticamente com o site de tooa cada solicitação.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-266">These attacks are made possible because web browsers will send authentication tokens automatically with every request tooa website.</span></span> <span data-ttu-id="1fc5c-267">exemplo canônico Hello é um cookie de autenticação, como ASP. Tíquete de autenticação de formulários do NET.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-267">hello canonical example is an authentication cookie, such as ASP.NET's Forms Authentication ticket.</span></span> <span data-ttu-id="1fc5c-268">No entanto, os sites que usam qualquer mecanismo de autenticação persistente (como a autenticação do Windows, Basic e assim por diante) podem ser alvos desses ataques.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-268">However, websites which use any persistent authentication mechanism (such as Windows Authentication, Basic, and so forth) can be targeted by these attacks.</span></span>

<span data-ttu-id="1fc5c-269">Um ataque XSRF é diferente de um ataque de phishing.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-269">An XSRF attack is distinct from a phishing attack.</span></span> <span data-ttu-id="1fc5c-270">Ataques de phishing requerem interação da vítima hello.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-270">Phishing attacks require interaction from hello victim.</span></span> <span data-ttu-id="1fc5c-271">Em um ataque de phishing, um site mal-intencionado imitar o site de destino hello e vítima Olá enganar fornecendo invasor de toohello informações confidenciais.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-271">In a phishing attack, a malicious website will mimic hello target website, and hello victim is fooled into providing sensitive information toohello attacker.</span></span> <span data-ttu-id="1fc5c-272">Em um ataque de XSRF, geralmente há nenhuma interação necessárias da vítima hello.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-272">In an XSRF attack, there is often no interaction necessary from hello victim.</span></span> <span data-ttu-id="1fc5c-273">Em vez disso, invasor Olá depende navegador Olá enviar automaticamente todos os site de destino de toohello cookies relevantes.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-273">Rather, hello attacker is relying on hello browser automatically sending all relevant cookies toohello destination website.</span></span>

<span data-ttu-id="1fc5c-274">Para obter mais informações, consulte Olá [Abrir projeto de segurança do aplicativo Web](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).</span><span class="sxs-lookup"><span data-stu-id="1fc5c-274">For more information, see hello [Open Web Application Security Project](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).</span></span>

1. <span data-ttu-id="1fc5c-275">No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto **ContactManager**, clique em **Adicionar** e em **Classe**.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-275">In **Solution Explorer**, right **ContactManager** project and click **Add** and then click **Class**.</span></span>
2. <span data-ttu-id="1fc5c-276">Arquivo de saudação do nome *ValidateHttpAntiForgeryTokenAttribute.cs* e adicione Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="1fc5c-276">Name hello file *ValidateHttpAntiForgeryTokenAttribute.cs* and add hello following code:</span></span>
   
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
3. <span data-ttu-id="1fc5c-277">Adicione o seguinte Olá *usando* toohello de instrução de contratos de controlador para que você tenha acesso toohello **[ValidateHttpAntiForgeryToken]** atributo.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-277">Add hello following *using* statement toohello contracts controller so you have access toohello **[ValidateHttpAntiForgeryToken]** attribute.</span></span>
   
        using ContactManager.Filters;
4. <span data-ttu-id="1fc5c-278">Adicionar Olá **[ValidateHttpAntiForgeryToken]** toohello métodos de postagem de saudação do atributo **ContactsController** tooprotect-lo contra ameaças XSRF.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-278">Add hello **[ValidateHttpAntiForgeryToken]** attribute toohello Post methods of hello **ContactsController** tooprotect it from XSRF threats.</span></span> <span data-ttu-id="1fc5c-279">Você irá adicionar toohello "PutContact", "PostContact" e **DeleteContact** métodos de ação.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-279">You will add it toohello "PutContact",  "PostContact" and **DeleteContact** action methods.</span></span>
   
        [ValidateHttpAntiForgeryToken]
            public IHttpActionResult PutContact(int id, Contact contact)
            {
5. <span data-ttu-id="1fc5c-280">Saudação de atualização *Scripts* seção Olá *Views\Home\Index.cshtml* tokens de XSRF tooinclude código tooget saudação do arquivo.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-280">Update hello *Scripts* section of hello *Views\Home\Index.cshtml* file tooinclude code tooget hello XSRF tokens.</span></span>
   
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

## <a name="publish-hello-application-update-tooazure-and-sql-database"></a><span data-ttu-id="1fc5c-281">Publicar Olá tooAzure de atualização de aplicativo e banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="1fc5c-281">Publish hello application update tooAzure and SQL Database</span></span>
<span data-ttu-id="1fc5c-282">aplicativo de hello toopublish, você repetir procedimento Olá que você seguiu anteriormente.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-282">toopublish hello application, you repeat hello procedure you followed earlier.</span></span>

1. <span data-ttu-id="1fc5c-283">Em **Solution Explorer**, projeto Olá clique com botão direito e selecione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-283">In **Solution Explorer**, right click hello project and select **Publish**.</span></span>
   
    ![Publicar][rxP]
2. <span data-ttu-id="1fc5c-285">Clique em Olá **configurações** guia.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-285">Click hello **Settings** tab.</span></span>
3. <span data-ttu-id="1fc5c-286">Em **ContactsManagerContext(ContactsManagerContext)**, clique em Olá **v** ícone toochange *cadeia de caracteres de conexão remota* toohello cadeia de caracteres de conexão para contato Olá banco de dados.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-286">Under **ContactsManagerContext(ContactsManagerContext)**, click hello **v** icon toochange *Remote connection string* toohello connection string for hello contact database.</span></span> <span data-ttu-id="1fc5c-287">Clique em **ContactDB**.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-287">Click **ContactDB**.</span></span>
   
    ![Configurações](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt5.png)
4. <span data-ttu-id="1fc5c-289">Marque a caixa Olá para **executar migrações do Code First (executado na inicialização do aplicativo)**.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-289">Check hello box for **Execute Code First Migrations (runs on application start)**.</span></span>
5. <span data-ttu-id="1fc5c-290">Clique em **Avançar** e, em seguida, em **Visualizar**.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-290">Click **Next** and then click **Preview**.</span></span> <span data-ttu-id="1fc5c-291">O Visual Studio exibe uma lista de arquivos de saudação que serão adicionados ou atualizados.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-291">Visual Studio displays a list of hello files that will be added or updated.</span></span>
6. <span data-ttu-id="1fc5c-292">Clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-292">Click **Publish**.</span></span>
   <span data-ttu-id="1fc5c-293">Após a conclusão da implantação hello, o navegador de saudação abre toohello home page do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-293">After hello deployment completes, hello browser opens toohello home page of hello application.</span></span>
   
    ![Página de índice sem contatos][intro001]
   
    <span data-ttu-id="1fc5c-295">Olá Visual Studio publicar cadeia de caracteres de conexão do processo configurado automaticamente Olá no hello implantado *Web. config* banco de dados do arquivo toopoint toohello SQL.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-295">hello Visual Studio publish process automatically configured hello connection string in hello deployed *Web.config* file toopoint toohello SQL database.</span></span> <span data-ttu-id="1fc5c-296">Ele também configurado migrações do Code First tooautomatically Olá Atualizar banco de dados toohello versão mais recente primeiro aplicativo de saudação tempo hello acessa o banco de dados de saudação após a implantação.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-296">It also configured Code First Migrations tooautomatically upgrade hello database toohello latest version hello first time hello application accesses hello database after deployment.</span></span>
   
    <span data-ttu-id="1fc5c-297">Como resultado, essa configuração Code First criou Olá banco de dados, executando código Olá em Olá **inicial** classe que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-297">As a result of this configuration, Code First created hello database by running hello code in hello **Initial** class that you created earlier.</span></span> <span data-ttu-id="1fc5c-298">Que este Olá primeiro tempo Olá aplicativo tentado tooaccess Olá banco de dados após a implantação.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-298">It did this hello first time hello application tried tooaccess hello database after deployment.</span></span>
7. <span data-ttu-id="1fc5c-299">Insira um contato como você fez quando você executou Olá aplicativo localmente, tooverify implantação de banco de dados foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-299">Enter a contact as you did when you ran hello app locally, tooverify that database deployment succeeded.</span></span>

<span data-ttu-id="1fc5c-300">Quando você vir esse item Olá que inserir é salva e aparece na página de contato do Gerenciador de saudação, você saberá que foram armazenado no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-300">When you see that hello item you enter is saved and appears on hello contact manager page, you know that it has been stored in hello database.</span></span>

![Página de índice com contatos][addwebapi004]

<span data-ttu-id="1fc5c-302">aplicativo Hello está em execução na nuvem hello, usando o banco de dados SQL toostore seus dados.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-302">hello application is now running in hello cloud, using SQL Database toostore its data.</span></span> <span data-ttu-id="1fc5c-303">Depois de concluir o teste o aplicativo hello no Azure, exclua-o.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-303">After you finish testing hello application in Azure, delete it.</span></span> <span data-ttu-id="1fc5c-304">aplicativo Hello é público e não tem acesso de toolimit um mecanismo.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-304">hello application is public and doesn't have a mechanism toolimit access.</span></span>

> [!NOTE]
> <span data-ttu-id="1fc5c-305">Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-305">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="1fc5c-306">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-306">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="1fc5c-307">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1fc5c-307">Next Steps</span></span>
<span data-ttu-id="1fc5c-308">Outra maneira como toostore os dados em um aplicativo do Azure serão toouse armazenamento do Azure, que fornecem armazenamento de dados não relacionais no formato de saudação de blobs e tabelas.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-308">Another way toostore data in an Azure application is toouse Azure storage, which provide non-relational data storage in hello form of blobs and tables.</span></span> <span data-ttu-id="1fc5c-309">Olá links a seguir fornece mais informações sobre a API da Web, o ASP.NET MVC e o Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-309">hello following links provide more information on Web API, ASP.NET MVC and Window Azure.</span></span>

* <span data-ttu-id="1fc5c-310">[Introdução ao Entity Framework usando MVC][EFCodeFirstMVCTutorial]</span><span class="sxs-lookup"><span data-stu-id="1fc5c-310">[Getting Started with Entity Framework using MVC][EFCodeFirstMVCTutorial]</span></span>
* [<span data-ttu-id="1fc5c-311">Introdução tooASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="1fc5c-311">Intro tooASP.NET MVC 5</span></span>](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [<span data-ttu-id="1fc5c-312">Sua primeira API Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1fc5c-312">Your First ASP.NET Web API</span></span>](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)
* [<span data-ttu-id="1fc5c-313">Depurando WAWS</span><span class="sxs-lookup"><span data-stu-id="1fc5c-313">Debugging WAWS</span></span>](web-sites-dotnet-troubleshoot-visual-studio.md)

<span data-ttu-id="1fc5c-314">Este aplicativo de exemplo do tutorial e hello foi escrito por [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [ @RickAndMSFT ](https://twitter.com/RickAndMSFT)) com a Ajuda de Tom Dykstra e Barry Dorrans (Twitter [ @blowdart ](https://twitter.com/blowdart)).</span><span class="sxs-lookup"><span data-stu-id="1fc5c-314">This tutorial and hello sample application was written by [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [@RickAndMSFT](https://twitter.com/RickAndMSFT)) with assistance from Tom Dykstra and Barry Dorrans (Twitter [@blowdart](https://twitter.com/blowdart)).</span></span> 

<span data-ttu-id="1fc5c-315">Deixe comentários sobre o que você gostou ou o que você gostaria que toosee aprimorado, não apenas sobre tutorial Olá em si, mas também sobre produtos Olá demonstra.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-315">Please leave feedback on what you liked or what you would like toosee improved, not only about hello tutorial itself but also about hello products that it demonstrates.</span></span> <span data-ttu-id="1fc5c-316">Seus comentários nos ajudarão a priorizar melhorias.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-316">Your feedback will help us prioritize improvements.</span></span> <span data-ttu-id="1fc5c-317">Estamos especialmente interessados em saber quantos interesse lá está em mais automação para o processo de saudação de configuração e implantação de banco de dados de associação de saudação.</span><span class="sxs-lookup"><span data-stu-id="1fc5c-317">We are especially interested in finding out how much interest there is in more automation for hello process of configuring and deploying hello membership database.</span></span> 

## <a name="whats-changed"></a><span data-ttu-id="1fc5c-318">O que mudou</span><span class="sxs-lookup"><span data-stu-id="1fc5c-318">What's changed</span></span>
* <span data-ttu-id="1fc5c-319">Para um guia toohello alteração de sites tooApp serviço consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="1fc5c-319">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- bookmarks -->
[Add an OAuth Provider]: #addOauth
[Add Roles toohello Membership Database]:#mbrDB
[Create a Data Deployment Script]:#ppd
[Update hello Membership Database]:#ppd2
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

