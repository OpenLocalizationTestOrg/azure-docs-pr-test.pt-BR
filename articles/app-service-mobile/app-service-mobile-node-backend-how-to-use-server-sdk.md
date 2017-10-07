---
title: "toowork aaaHow com o servidor de back-end Olá Node. js SDK para aplicativos móveis | Microsoft Docs"
description: "Saiba como toowork com hello o servidor de back-end node. js SDK para aplicativos de celular do serviço de aplicativo do Azure."
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: e7d97d3b-356e-4fb3-ba88-38ecbda5ea50
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: node
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2b1ea5fda6f6ca422b92fe29ff8d16bf035018d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-mobile-apps-nodejs-sdk"></a><span data-ttu-id="89751-103">Como toouse Olá SDK de Node.js de aplicativos móveis do Azure</span><span class="sxs-lookup"><span data-stu-id="89751-103">How toouse hello Azure Mobile Apps Node.js SDK</span></span>
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

<span data-ttu-id="89751-104">Este artigo fornece informações detalhadas e exemplos que mostram como toowork com um back-end do Node. js em aplicativos de celular do serviço de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="89751-104">This article provides detailed information and examples showing how toowork with a Node.js backend in Azure App Service Mobile Apps.</span></span>

## <span data-ttu-id="89751-105"><a name="Introduction"></a>Introdução</span><span class="sxs-lookup"><span data-stu-id="89751-105"><a name="Introduction"></a>Introduction</span></span>
<span data-ttu-id="89751-106">Aplicativos móveis de serviço de aplicativo do Azure fornece acesso a dados Olá recurso tooadd mobile-otimizado aplicativo de web tooa API da Web.</span><span class="sxs-lookup"><span data-stu-id="89751-106">Azure App Service Mobile Apps provides hello capability tooadd a mobile-optimized data access Web API tooa web application.</span></span>  <span data-ttu-id="89751-107">Olá SDK de aplicativos móveis do serviço de aplicativo do Azure é fornecido para aplicativos web ASP.NET e Node. js.</span><span class="sxs-lookup"><span data-stu-id="89751-107">hello Azure App Service Mobile Apps SDK is provided for ASP.NET and Node.js web applications.</span></span>  <span data-ttu-id="89751-108">Olá SDK fornece Olá seguintes operações:</span><span class="sxs-lookup"><span data-stu-id="89751-108">hello SDK provides hello following operations:</span></span>

* <span data-ttu-id="89751-109">Operações de tabela (Ler, Inserir, Atualizar Excluir) para acesso a dados</span><span class="sxs-lookup"><span data-stu-id="89751-109">Table operations (Read, Insert, Update, Delete) for data access</span></span>
* <span data-ttu-id="89751-110">Operações de API personalizadas</span><span class="sxs-lookup"><span data-stu-id="89751-110">Custom API operations</span></span>

<span data-ttu-id="89751-111">Ambas as operações permitem a autenticação em todos os provedores de identidade permitidos pelo Serviço de Aplicativo do Azure, incluindo provedores de identidade social como Facebook, Twitter, Google e Microsoft, além do Active Directory do Azure para a identidade corporativa.</span><span class="sxs-lookup"><span data-stu-id="89751-111">Both operations provide for authentication across all identity providers allowed by Azure App Service, including social identity providers such as Facebook, Twitter, Google and Microsoft as well as Azure Active Directory for enterprise identity.</span></span>

<span data-ttu-id="89751-112">Você pode encontrar exemplos para cada caso de uso no hello [diretório de exemplos no GitHub].</span><span class="sxs-lookup"><span data-stu-id="89751-112">You can find samples for each use case in hello [samples directory on GitHub].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="89751-113">Plataformas com suporte</span><span class="sxs-lookup"><span data-stu-id="89751-113">Supported Platforms</span></span>
<span data-ttu-id="89751-114">Olá SDK de nó de aplicativos móveis do Azure oferece suporte a saudação que LTS atuais versão do nó e versões posteriores.</span><span class="sxs-lookup"><span data-stu-id="89751-114">hello Azure Mobile Apps Node SDK supports hello current LTS release of Node and later.</span></span>  <span data-ttu-id="89751-115">A partir de gravação, Olá LTS versão é v4.5.0 de nó.</span><span class="sxs-lookup"><span data-stu-id="89751-115">As of writing, hello latest LTS version is Node v4.5.0.</span></span>  <span data-ttu-id="89751-116">Outras versões do Node podem funcionar, mas não são têm suporte.</span><span class="sxs-lookup"><span data-stu-id="89751-116">Other versions of Node may work, but are not supported.</span></span>

<span data-ttu-id="89751-117">Olá SDK de nó de aplicativos móveis do Azure oferece suporte a dois drivers de banco de dados - Olá nó mssql driver dá suporte ao SQL Azure e as instâncias locais do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="89751-117">hello Azure Mobile Apps Node SDK supports two database drivers - hello node-mssql driver supports SQL Azure and local SQL Server instances.</span></span>  <span data-ttu-id="89751-118">driver de sqlite3 Olá dá suporte a bancos de dados SQLite em uma única instância.</span><span class="sxs-lookup"><span data-stu-id="89751-118">hello sqlite3 driver supports SQLite databases on a single instance only.</span></span>

### <span data-ttu-id="89751-119"><a name="howto-cmdline-basicapp"></a>Como: criar um back-end node. js básica usando Olá linha de comando</span><span class="sxs-lookup"><span data-stu-id="89751-119"><a name="howto-cmdline-basicapp"></a>How to: Create a Basic Node.js backend using hello Command Line</span></span>
<span data-ttu-id="89751-120">Cada back-end de Node.js do Aplicativo Móvel do Serviço de Aplicativo do Azure inicia como um aplicativo ExpressJS.</span><span class="sxs-lookup"><span data-stu-id="89751-120">Every Azure App Service Mobile App Node.js backend starts as an ExpressJS application.</span></span>  <span data-ttu-id="89751-121">ExpressJS é hello mais popular estrutura de serviço web disponível para Node. js.</span><span class="sxs-lookup"><span data-stu-id="89751-121">ExpressJS is hello most popular web service framework available for Node.js.</span></span>  <span data-ttu-id="89751-122">Você pode criar um aplicativo [Express] básico da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="89751-122">You can create a basic [Express] application as follows:</span></span>

1. <span data-ttu-id="89751-123">Em um comando ou a janela do PowerShell, crie um diretório para seu projeto.</span><span class="sxs-lookup"><span data-stu-id="89751-123">In a command or PowerShell window, create a directory for your project.</span></span>

        mkdir basicapp
2. <span data-ttu-id="89751-124">Execute a estrutura do pacote npm init tooinitialize hello.</span><span class="sxs-lookup"><span data-stu-id="89751-124">Run npm init tooinitialize hello package structure.</span></span>

        cd basicapp
        npm init

    <span data-ttu-id="89751-125">comando de inicialização de npm Olá solicita um conjunto de projeto de saudação tooinitialize perguntas.</span><span class="sxs-lookup"><span data-stu-id="89751-125">hello npm init command asks a set of questions tooinitialize hello project.</span></span>  <span data-ttu-id="89751-126">Consulte a saída de exemplo hello:</span><span class="sxs-lookup"><span data-stu-id="89751-126">See hello example output:</span></span>

    ![saída de init npm Hello][0]
3. <span data-ttu-id="89751-128">Instale bibliotecas de express e aplicativos do azure-mobile de saudação do repositório de npm hello.</span><span class="sxs-lookup"><span data-stu-id="89751-128">Install hello express and azure-mobile-apps libraries from hello npm repository.</span></span>

        npm install --save express azure-mobile-apps
4. <span data-ttu-id="89751-129">Crie um app.js tooimplement Olá básica móveis servidor de arquivos.</span><span class="sxs-lookup"><span data-stu-id="89751-129">Create an app.js file tooimplement hello basic mobile server.</span></span>

        var express = require('express'),
            azureMobileApps = require('azure-mobile-apps');

        var app = express(),
            mobile = azureMobileApps();

        // Define a TodoItem table
        mobile.tables.add('TodoItem');

        // Add hello mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);

<span data-ttu-id="89751-130">Esse aplicativo cria um WebAPI mobile otimizado com um ponto de extremidade (`/tables/TodoItem`) que fornece acesso não autenticado tooan subjacente usando um esquema dinâmico de armazenamento de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="89751-130">This application creates a mobile-optimized WebAPI with a single endpoint (`/tables/TodoItem`) that provides unauthenticated access tooan underlying SQL data store using a dynamic schema.</span></span>  <span data-ttu-id="89751-131">Ele é adequado para os seguintes inícios rápidos de biblioteca de cliente:</span><span class="sxs-lookup"><span data-stu-id="89751-131">It is suitable for following the client library quick starts:</span></span>

* <span data-ttu-id="89751-132">[Início rápido do cliente Android]</span><span class="sxs-lookup"><span data-stu-id="89751-132">[Android Client QuickStart]</span></span>
* <span data-ttu-id="89751-133">[Início rápido do cliente Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="89751-133">[Apache Cordova Client QuickStart]</span></span>
* <span data-ttu-id="89751-134">[Início rápido do cliente iOS]</span><span class="sxs-lookup"><span data-stu-id="89751-134">[iOS Client QuickStart]</span></span>
* <span data-ttu-id="89751-135">[Início rápido de cliente Windows Store]</span><span class="sxs-lookup"><span data-stu-id="89751-135">[Windows Store Client QuickStart]</span></span>
* <span data-ttu-id="89751-136">[Início rápido do cliente Xamarin.iOS]</span><span class="sxs-lookup"><span data-stu-id="89751-136">[Xamarin.iOS Client QuickStart]</span></span>
* <span data-ttu-id="89751-137">[Início rápido do cliente Xamarin.Android]</span><span class="sxs-lookup"><span data-stu-id="89751-137">[Xamarin.Android Client QuickStart]</span></span>
* <span data-ttu-id="89751-138">[Início rápido do cliente Xamarin.Forms]</span><span class="sxs-lookup"><span data-stu-id="89751-138">[Xamarin.Forms Client QuickStart]</span></span>

<span data-ttu-id="89751-139">Você pode encontrar o código de saudação para este aplicativo básico em Olá [basicapp exemplo no GitHub].</span><span class="sxs-lookup"><span data-stu-id="89751-139">You can find hello code for this basic application in hello [basicapp sample on GitHub].</span></span>

### <span data-ttu-id="89751-140"><a name="howto-vs2015-basicapp"></a>Como criar um back-end de nó com o Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="89751-140"><a name="howto-vs2015-basicapp"></a>How to: Create a Node backend with Visual Studio 2015</span></span>
<span data-ttu-id="89751-141">Visual Studio 2015 exige uma extensão de toodevelop de Node. js aplicativos dentro de saudação IDE.</span><span class="sxs-lookup"><span data-stu-id="89751-141">Visual Studio 2015 requires an extension toodevelop Node.js applications within hello IDE.</span></span>  <span data-ttu-id="89751-142">toostart, Olá install [Node. js Tools 1.1 para Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="89751-142">toostart, install hello [Node.js Tools 1.1 for Visual Studio].</span></span>  <span data-ttu-id="89751-143">Depois que Olá Node. js Tools para Visual Studio estiverem instalados, crie um aplicativo de 4. x Express:</span><span class="sxs-lookup"><span data-stu-id="89751-143">Once hello Node.js Tools for Visual Studio are installed, create an Express 4.x application:</span></span>

1. <span data-ttu-id="89751-144">Olá abrir **novo projeto** caixa de diálogo (de **arquivo** > **novo** > **projeto...** ).</span><span class="sxs-lookup"><span data-stu-id="89751-144">Open hello **New Project** dialog (from **File** > **New** > **Project...**).</span></span>
2. <span data-ttu-id="89751-145">Expanda **Modelos** > **JavaScript** > **Node. js**.</span><span class="sxs-lookup"><span data-stu-id="89751-145">Expand **Templates** > **JavaScript** > **Node.js**.</span></span>
3. <span data-ttu-id="89751-146">Selecione Olá **Basic do Azure Node. js Express 4 Application**.</span><span class="sxs-lookup"><span data-stu-id="89751-146">Select hello **Basic Azure Node.js Express 4 Application**.</span></span>
4. <span data-ttu-id="89751-147">Preencha o nome do projeto hello.</span><span class="sxs-lookup"><span data-stu-id="89751-147">Fill in hello project name.</span></span>  <span data-ttu-id="89751-148">Clique em *OK*.</span><span class="sxs-lookup"><span data-stu-id="89751-148">Click *OK*.</span></span>

    ![Novo projeto do Visual Studio 2015][1]
5. <span data-ttu-id="89751-150">Saudação de atalho **npm** nó e selecione **instalar novos pacotes de npm...** .</span><span class="sxs-lookup"><span data-stu-id="89751-150">Right-click hello **npm** node and select **Install New npm packages...**.</span></span>
6. <span data-ttu-id="89751-151">Talvez seja necessário toorefresh Olá npm catálogo criando seu primeiro aplicativo Node. js.</span><span class="sxs-lookup"><span data-stu-id="89751-151">You may need toorefresh hello npm catalog on creating your first Node.js application.</span></span>  <span data-ttu-id="89751-152">Clique em **Atualizar** , se necessário.</span><span class="sxs-lookup"><span data-stu-id="89751-152">Click **Refresh** if necessary.</span></span>
7. <span data-ttu-id="89751-153">Digite *aplicativos do azure-mobile* na caixa de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="89751-153">Enter *azure-mobile-apps* in hello search box.</span></span>  <span data-ttu-id="89751-154">Clique em Olá **aplicativos do azure-mobile-2.0.0** do pacote e, em seguida, clique em **instalar pacote**.</span><span class="sxs-lookup"><span data-stu-id="89751-154">Click hello **azure-mobile-apps 2.0.0** package, then click **Install Package**.</span></span>

    ![Instalar novos pacotes npm][2]
8. <span data-ttu-id="89751-156">Clique em **fechar**</span><span class="sxs-lookup"><span data-stu-id="89751-156">Click **Close**.</span></span>
9. <span data-ttu-id="89751-157">Olá abrir *app.js* arquivo tooadd suporte Olá SDK de aplicativos móveis do Azure.</span><span class="sxs-lookup"><span data-stu-id="89751-157">Open hello *app.js* file tooadd support for hello Azure Mobile Apps SDK.</span></span>  <span data-ttu-id="89751-158">Na parte inferior de saudação de 6 at linha da biblioteca de saudação requerem instruções, adicione Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="89751-158">At line 6 at hello bottom of hello library require statements, add hello following code:</span></span>

        var bodyParser = require('body-parser');
        var azureMobileApps = require('azure-mobile-apps');

    <span data-ttu-id="89751-159">Em aproximadamente linha 27 após Olá outras instruções app.use, adicione Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="89751-159">At approximately line 27 after hello other app.use statements, add hello following code:</span></span>

        app.use('/users', users);

        // Azure Mobile Apps Initialization
        var mobile = azureMobileApps();
        mobile.tables.add('TodoItem');
        app.use(mobile);

    <span data-ttu-id="89751-160">Salve o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="89751-160">Save hello file.</span></span>
10. <span data-ttu-id="89751-161">Execute o aplicativo hello localmente (Olá API é divulgada http://localhost:3000) ou publicar tooAzure.</span><span class="sxs-lookup"><span data-stu-id="89751-161">Either run hello application locally (hello API is served on http://localhost:3000) or publish tooAzure.</span></span>

### <span data-ttu-id="89751-162"><a name="create-node-backend-portal"></a>Como: criar um back-end node. js usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="89751-162"><a name="create-node-backend-portal"></a>How to: Create a Node.js backend using hello Azure portal</span></span>
<span data-ttu-id="89751-163">Você pode criar um direito de back-end do aplicativo móvel no hello [portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="89751-163">You can create a Mobile App backend right in hello [Azure portal].</span></span> <span data-ttu-id="89751-164">Você pode seguir Olá seguir as etapas ou cria um cliente e servidor juntos, Olá a seguir [criar um aplicativo móvel](app-service-mobile-ios-get-started.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="89751-164">You can either follow hello following steps or create a client and server together by following hello [Create a mobile app](app-service-mobile-ios-get-started.md) tutorial.</span></span> <span data-ttu-id="89751-165">tutorial de Olá contém uma versão simplificada dessas instruções e é melhor para a verificação de projetos de conceito.</span><span class="sxs-lookup"><span data-stu-id="89751-165">hello tutorial contains a simplified version of these instructions and is best for proof of concept projects.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

<span data-ttu-id="89751-166">Em Olá *começar* folha, em **criar uma tabela API**, escolha **Node. js** como seu **idioma de back-end**.</span><span class="sxs-lookup"><span data-stu-id="89751-166">Back in hello *Get started* blade, under **Create a table API**, choose **Node.js** as your **Backend language**.</span></span>
<span data-ttu-id="89751-167">Marque a caixa Olá para "**confirmo que isto substituirá todos os conteúdos do site.**", em seguida, clique em **tabela TodoItem criar**.</span><span class="sxs-lookup"><span data-stu-id="89751-167">Check hello box for "**I acknowledge that this will overwrite all site contents.**", then click **Create TodoItem table**.</span></span>

### <span data-ttu-id="89751-168"><a name="download-quickstart"></a>Como: Download Olá Node. js back-end quickstart projeto de código usando Git</span><span class="sxs-lookup"><span data-stu-id="89751-168"><a name="download-quickstart"></a>How to: Download hello Node.js backend quickstart code project using Git</span></span>
<span data-ttu-id="89751-169">Quando você cria um back-end do aplicativo móvel de Node. js usando o portal de saudação **início rápido** folha, um projeto de Node. js é criado para você e site tooyour implantado.</span><span class="sxs-lookup"><span data-stu-id="89751-169">When you create a Node.js Mobile App backend by using hello portal **Quick start** blade, a Node.js project is created for you and deployed tooyour site.</span></span> <span data-ttu-id="89751-170">Você pode adicionar tabelas e APIs e editar arquivos de código de back-end do hello Node. js no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="89751-170">You can add tables and APIs and edit code files for hello Node.js backend in hello portal.</span></span> <span data-ttu-id="89751-171">Você também pode usar várias ferramentas toodownload Olá back-end projeto de implantação de modo que você pode adicionar ou modificar tabelas e APIs e republicar o projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="89751-171">You can also use various deployment tools toodownload hello backend project so that you can add or modify tables and APIs, then republish hello project.</span></span> <span data-ttu-id="89751-172">Para saber mais, confira o [Guia de implantação do Serviço de Aplicativo do Azure].</span><span class="sxs-lookup"><span data-stu-id="89751-172">For more information, see the [Azure App Service Deployment Guide].</span></span> <span data-ttu-id="89751-173">Olá procedimento a seguir usa um código de projeto Git repositório toodownload Olá início rápido.</span><span class="sxs-lookup"><span data-stu-id="89751-173">hello following procedure uses a Git repository toodownload hello quickstart project code.</span></span>

1. <span data-ttu-id="89751-174">Instale o Git, caso ainda não tenha feito isso.</span><span class="sxs-lookup"><span data-stu-id="89751-174">Install Git, if you haven't already done so.</span></span> <span data-ttu-id="89751-175">Olá etapas necessárias tooinstall Git variar entre sistemas operacionais.</span><span class="sxs-lookup"><span data-stu-id="89751-175">hello steps required tooinstall Git vary between operating systems.</span></span> <span data-ttu-id="89751-176">Consulte [Instalando o Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) para distribuições específicas de sistemas operacionais e orientações de instalação.</span><span class="sxs-lookup"><span data-stu-id="89751-176">See [Installing Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) for operating system-specific distributions and installation guidance.</span></span>
2. <span data-ttu-id="89751-177">Siga as etapas de saudação em [habilitar Olá repositório de aplicativo de serviço de aplicativo](../app-service-web/app-service-deploy-local-git.md#Step3) repositório do Git tooenable Olá para seu site de back-end, fazendo uma anotação de saudação implantação username e password.</span><span class="sxs-lookup"><span data-stu-id="89751-177">Follow hello steps in [Enable hello App Service app repository](../app-service-web/app-service-deploy-local-git.md#Step3) tooenable hello Git repository for your backend site, making a note of hello deployment username and password.</span></span>
3. <span data-ttu-id="89751-178">Na folha de saudação para seu back-end do aplicativo móvel, anote Olá **URL de clone de Git** configuração.</span><span class="sxs-lookup"><span data-stu-id="89751-178">In hello blade for your Mobile App backend, make a note of hello **Git clone URL** setting.</span></span>
4. <span data-ttu-id="89751-179">Executar Olá `git clone` comando usando a URL de clone de Git hello, inserir sua senha, quando necessário, como no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="89751-179">Execute hello `git clone` command using hello Git clone URL, entering your password when required, as in the following example:</span></span>

        $ git clone https://username@todolist.scm.azurewebsites.net:443/todolist.git
5. <span data-ttu-id="89751-180">Procurar o diretório toolocal, que Olá anterior exemplo é /todolist e observe que os arquivos de projeto foram baixados.</span><span class="sxs-lookup"><span data-stu-id="89751-180">Browse toolocal directory, which in hello preceding example is /todolist, and notice that project files have been downloaded.</span></span> <span data-ttu-id="89751-181">Localizar Olá `todoitem.json` arquivo hello `/tables` directory.</span><span class="sxs-lookup"><span data-stu-id="89751-181">Locate hello `todoitem.json` file in hello `/tables` directory.</span></span>  <span data-ttu-id="89751-182">Esse arquivo define as permissões na tabela.</span><span class="sxs-lookup"><span data-stu-id="89751-182">This file defines permissions on the table.</span></span>  <span data-ttu-id="89751-183">Também encontrar hello `todoitem.js` arquivo hello mesmo diretório, que define que a operação CRUD scripts para a tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="89751-183">Also find hello `todoitem.js` file in hello same directory, which defines that CRUD operation scripts for hello table.</span></span>
6. <span data-ttu-id="89751-184">Depois que você fez alterações tooproject arquivos, execute Olá comandos tooadd, confirmar, em seguida, carregar o site de toohello alterações a seguir:</span><span class="sxs-lookup"><span data-stu-id="89751-184">After you have made changes tooproject files, execute hello following commands tooadd, commit, then upload the changes toohello site:</span></span>

        $ git commit -m "updated hello table script"
        $ git push origin master

    <span data-ttu-id="89751-185">Quando você adiciona um novo projeto de toohello de arquivos, é necessário primeiro Olá tooexecute `git add .` comando.</span><span class="sxs-lookup"><span data-stu-id="89751-185">When you add new files toohello project, you first need tooexecute hello `git add .` command.</span></span>

<span data-ttu-id="89751-186">site de saudação for publicada novamente sempre que um novo conjunto de confirmação é enviada por push toohello site.</span><span class="sxs-lookup"><span data-stu-id="89751-186">hello site is republished every time a new set of commits is pushed toohello site.</span></span>

### <span data-ttu-id="89751-187"><a name="howto-publish-to-azure"></a>Como: publicar sua tooAzure de back-end node. js</span><span class="sxs-lookup"><span data-stu-id="89751-187"><a name="howto-publish-to-azure"></a>How to: Publish your Node.js backend tooAzure</span></span>
<span data-ttu-id="89751-188">O Microsoft Azure fornece vários mecanismos para publicar seu back-end do Azure aplicativo serviços móveis aplicativos Node para Olá serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="89751-188">Microsoft Azure provides many mechanisms for publishing your Azure App Service Mobile Apps Node.js backend to hello Azure service.</span></span>  <span data-ttu-id="89751-189">Eles incluem a utilização das ferramentas de implantação integradas ao Visual Studio, das ferramentas de linha de comando e das opções de implantação contínua com base no controle de origem.</span><span class="sxs-lookup"><span data-stu-id="89751-189">These include utilizing deployment tools integrated into Visual Studio, command-line tools, and continuous deployment options based on source control.</span></span>  <span data-ttu-id="89751-190">Para saber mais sobre esse tópico, confira o [Guia de implantação do Serviço de Aplicativo do Azure].</span><span class="sxs-lookup"><span data-stu-id="89751-190">For more information on this topic, see the [Azure App Service Deployment Guide].</span></span>

<span data-ttu-id="89751-191">O Serviço de Aplicativo do Azure tem recomendações específicas para aplicativo Node.js que você deve examinar antes de implantar:</span><span class="sxs-lookup"><span data-stu-id="89751-191">Azure App Service has specific advice for Node.js application that you should review before deploying:</span></span>

* <span data-ttu-id="89751-192">Como muito[especificar Olá versão do nó]</span><span class="sxs-lookup"><span data-stu-id="89751-192">How too[specify hello Node Version]</span></span>
* <span data-ttu-id="89751-193">Como muito[usar módulos de nó]</span><span class="sxs-lookup"><span data-stu-id="89751-193">How too[use Node modules]</span></span>

### <span data-ttu-id="89751-194"><a name="howto-enable-homepage"></a>Como habilitar uma home page para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="89751-194"><a name="howto-enable-homepage"></a>How to: Enable a Home Page for your application</span></span>
<span data-ttu-id="89751-195">Muitos aplicativos são uma combinação de aplicativos web e móveis e Olá ExpressJS estrutura permite que você toocombine dois facetas.</span><span class="sxs-lookup"><span data-stu-id="89751-195">Many applications are a combination of web and mobile apps and hello ExpressJS framework allows you toocombine the two facets.</span></span>  <span data-ttu-id="89751-196">Às vezes, no entanto, talvez você queira tooonly implementar uma interface móvel.</span><span class="sxs-lookup"><span data-stu-id="89751-196">Sometimes, however, you may wish tooonly implement a mobile interface.</span></span>  <span data-ttu-id="89751-197">É útil tooprovide que um serviço de aplicativo da saudação inicial página tooensure está em execução.</span><span class="sxs-lookup"><span data-stu-id="89751-197">It is useful tooprovide a landing page tooensure hello app service is up and running.</span></span>  <span data-ttu-id="89751-198">Você pode fornecer sua própria home page ou habilitar uma home page temporária.</span><span class="sxs-lookup"><span data-stu-id="89751-198">You can either provide your own home page or enable a temporary home page.</span></span>  <span data-ttu-id="89751-199">tooenable uma home page temporária, use Olá tooinstantiate Azure Mobile aplicativos a seguir:</span><span class="sxs-lookup"><span data-stu-id="89751-199">tooenable a temporary home page, use hello following tooinstantiate Azure Mobile Apps:</span></span>

    var mobile = azureMobileApps({ homePage: true });

<span data-ttu-id="89751-200">Se você desejar somente essa opção disponível durante o desenvolvimento localmente, você pode adicionar essa configuração tooyour `azureMobile.js` arquivo.</span><span class="sxs-lookup"><span data-stu-id="89751-200">If you only want this option available when developing locally, you can add this setting tooyour `azureMobile.js` file.</span></span>

## <span data-ttu-id="89751-201"><a name="TableOperations"></a>Operações de tabela</span><span class="sxs-lookup"><span data-stu-id="89751-201"><a name="TableOperations"></a>Table operations</span></span>
<span data-ttu-id="89751-202">Olá aplicativos do azure-mobile Node. js servidor SDK fornece mecanismos tooexpose dados tabelas armazenadas no banco de dados SQL Azure como um WebAPI.</span><span class="sxs-lookup"><span data-stu-id="89751-202">hello azure-mobile-apps Node.js Server SDK provides mechanisms tooexpose data tables stored in Azure SQL Database as a WebAPI.</span></span>  <span data-ttu-id="89751-203">Cinco operações são fornecidas.</span><span class="sxs-lookup"><span data-stu-id="89751-203">Five operations are provided.</span></span>

| <span data-ttu-id="89751-204">Operação</span><span class="sxs-lookup"><span data-stu-id="89751-204">Operation</span></span> | <span data-ttu-id="89751-205">Descrição</span><span class="sxs-lookup"><span data-stu-id="89751-205">Description</span></span> |
| --- | --- |
| <span data-ttu-id="89751-206">GET /tables/*tablename*</span><span class="sxs-lookup"><span data-stu-id="89751-206">GET /tables/*tablename*</span></span> |<span data-ttu-id="89751-207">Obter todos os registros na tabela de saudação</span><span class="sxs-lookup"><span data-stu-id="89751-207">Get all records in hello table</span></span> |
| <span data-ttu-id="89751-208">GET /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="89751-208">GET /tables/*tablename*/:id</span></span> |<span data-ttu-id="89751-209">Obter um registro específico na tabela de saudação</span><span class="sxs-lookup"><span data-stu-id="89751-209">Get a specific record in hello table</span></span> |
| <span data-ttu-id="89751-210">POST /tables/*tablename*</span><span class="sxs-lookup"><span data-stu-id="89751-210">POST /tables/*tablename*</span></span> |<span data-ttu-id="89751-211">Criar um registro na tabela de saudação</span><span class="sxs-lookup"><span data-stu-id="89751-211">Create a record in hello table</span></span> |
| <span data-ttu-id="89751-212">PATCH /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="89751-212">PATCH /tables/*tablename*/:id</span></span> |<span data-ttu-id="89751-213">Atualizar um registro na tabela de saudação</span><span class="sxs-lookup"><span data-stu-id="89751-213">Update a record in hello table</span></span> |
| <span data-ttu-id="89751-214">DELETE /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="89751-214">DELETE /tables/*tablename*/:id</span></span> |<span data-ttu-id="89751-215">Excluir um registro na tabela de saudação</span><span class="sxs-lookup"><span data-stu-id="89751-215">Delete a record in hello table</span></span> |

<span data-ttu-id="89751-216">Oferece suporte a essa WebAPI [OData] e estende o toosupport de esquema de tabela Olá [a sincronização de dados offline].</span><span class="sxs-lookup"><span data-stu-id="89751-216">This WebAPI supports [OData] and extends hello table schema toosupport [offline data sync].</span></span>

### <span data-ttu-id="89751-217"><a name="howto-dynamicschema"></a>Como definir tabelas usando um esquema dinâmico</span><span class="sxs-lookup"><span data-stu-id="89751-217"><a name="howto-dynamicschema"></a>How to: Define tables using a dynamic schema</span></span>
<span data-ttu-id="89751-218">Antes de poder usar uma tabela, ela deve ser definida.</span><span class="sxs-lookup"><span data-stu-id="89751-218">Before a table can be used, it must be defined.</span></span>  <span data-ttu-id="89751-219">Tabelas podem ser definidas com um esquema estático (onde desenvolvedor Olá define colunas Olá no esquema de saudação) ou dinamicamente (onde Olá SDK controla o esquema de saudação com base nas solicitações de entrada).</span><span class="sxs-lookup"><span data-stu-id="89751-219">Tables can be defined with a static schema (where hello developer defines hello columns within hello schema) or dynamically (where hello SDK controls hello schema based on incoming requests).</span></span> <span data-ttu-id="89751-220">Além disso, o desenvolvedor de Olá pode controlar aspectos específicos de saudação WebAPI adicionando definição de toohello de código Javascript.</span><span class="sxs-lookup"><span data-stu-id="89751-220">In addition, hello developer can control specific aspects of hello WebAPI by adding Javascript code toohello definition.</span></span>

<span data-ttu-id="89751-221">Como uma prática recomendada, você deve definir cada tabela em um arquivo Javascript no diretório de tabelas de saudação e usar as tabelas de saudação tables.import() método tooimport.</span><span class="sxs-lookup"><span data-stu-id="89751-221">As a best practice, you should define each table in a Javascript file in hello tables directory, then use the tables.import() method tooimport hello tables.</span></span>  <span data-ttu-id="89751-222">Estender o aplicativo hello basic, arquivo de app.js Olá seria ajustado:</span><span class="sxs-lookup"><span data-stu-id="89751-222">Extending hello basic-app, hello app.js file would be adjusted:</span></span>

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Define hello database schema that is exposed
    mobile.tables.import('./tables');

    // Provide initialization of any tables that are statically defined
    mobile.tables.initialize().then(function () {
        // Add hello mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);
    });

<span data-ttu-id="89751-223">Definir tabela hello. / tables/TodoItem.js:</span><span class="sxs-lookup"><span data-stu-id="89751-223">Define hello table in ./tables/TodoItem.js:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Additional configuration for hello table goes here

    module.exports = table;

<span data-ttu-id="89751-224">As tabelas usam o esquema dinâmico por padrão.</span><span class="sxs-lookup"><span data-stu-id="89751-224">Tables use dynamic schema by default.</span></span>  <span data-ttu-id="89751-225">tooturn desativar dinâmicas de esquema definido globalmente, Olá configuração do aplicativo **MS_DynamicSchema** toofalse em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="89751-225">tooturn off dynamic schema globally, set hello App Setting **MS_DynamicSchema** toofalse within hello Azure portal.</span></span>

<span data-ttu-id="89751-226">Você pode encontrar um exemplo completo em Olá [exemplo todo no GitHub].</span><span class="sxs-lookup"><span data-stu-id="89751-226">You can find a complete example in hello [todo sample on GitHub].</span></span>

### <span data-ttu-id="89751-227"><a name="howto-staticschema"></a>Como definir tabelas usando um esquema estático</span><span class="sxs-lookup"><span data-stu-id="89751-227"><a name="howto-staticschema"></a>How to: Define tables using a static schema</span></span>
<span data-ttu-id="89751-228">Você pode definir explicitamente Olá colunas tooexpose via Olá WebAPI.</span><span class="sxs-lookup"><span data-stu-id="89751-228">You can explicitly define hello columns tooexpose via hello WebAPI.</span></span>  <span data-ttu-id="89751-229">Olá que aplicativos do azure-mobile Node. js SDK adiciona automaticamente a quaisquer colunas adicionais necessárias para a lista de toohello de sincronização de dados offline que você fornecer.</span><span class="sxs-lookup"><span data-stu-id="89751-229">hello azure-mobile-apps Node.js SDK automatically adds any additional columns required for offline data sync toohello list that you provide.</span></span>  <span data-ttu-id="89751-230">Por exemplo, os aplicativos de cliente QuickStart exigem uma tabela com duas colunas: texto (uma cadeia de caracteres) e completo (um valor booliano).</span><span class="sxs-lookup"><span data-stu-id="89751-230">For example, the QuickStart client applications require a table with two columns: text (a string) and complete (a boolean).</span></span>  
<span data-ttu-id="89751-231">tabela Olá pode ser definida no hello tabela JavaScript arquivo de definição (localizado no diretório de tabelas de saudação) da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="89751-231">hello table can be defined in hello table definition JavaScript file (located in hello tables directory) as follows:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    module.exports = table;

<span data-ttu-id="89751-232">Se você definir tabelas estaticamente, em seguida, você também deve chamar esquema de banco de dados de Olá Olá tables.initialize() método toocreate na inicialização.</span><span class="sxs-lookup"><span data-stu-id="89751-232">If you define tables statically, then you must also call hello tables.initialize() method toocreate hello database schema on startup.</span></span>  <span data-ttu-id="89751-233">Olá tables.initialize() método retorna um [promessa] para que o serviço web de saudação não atender a solicitações antes do banco de dados de hello está sendo inicializado.</span><span class="sxs-lookup"><span data-stu-id="89751-233">hello tables.initialize() method returns a [Promise] so that hello web service does not serve requests before hello database being initialized.</span></span>

### <span data-ttu-id="89751-234"><a name="howto-sqlexpress-setup"></a>Como usar o SQL Express como um armazenamento de dados de desenvolvimento em sua máquina local</span><span class="sxs-lookup"><span data-stu-id="89751-234"><a name="howto-sqlexpress-setup"></a>How to: Use SQL Express as a development data store on your local machine</span></span>
<span data-ttu-id="89751-235">os aplicativos móveis do Azure Olá AzureMobile aplicativos nó SDK Hello fornece três opções para dados do servidor sem necessidade de saudação: SDK fornece três opções para dados fora da caixa de saudação do servidor:</span><span class="sxs-lookup"><span data-stu-id="89751-235">hello Azure Mobile Apps hello AzureMobile Apps Node SDK provides three options for serving data out of hello box: SDK provides three options for serving data out of hello box:</span></span>

* <span data-ttu-id="89751-236">Saudação de uso **memória** repositório de exemplo do driver tooprovide um não persistente</span><span class="sxs-lookup"><span data-stu-id="89751-236">Use hello **memory** driver tooprovide a non-persistent example store</span></span>
* <span data-ttu-id="89751-237">Saudação de uso **mssql** tooprovide de driver para o desenvolvimento de um repositório de dados SQL Express</span><span class="sxs-lookup"><span data-stu-id="89751-237">Use hello **mssql** driver tooprovide a SQL Express data store for development</span></span>
* <span data-ttu-id="89751-238">Saudação de uso **mssql** driver tooprovide um repositório de dados do banco de dados SQL para produção</span><span class="sxs-lookup"><span data-stu-id="89751-238">Use hello **mssql** driver tooprovide an Azure SQL Database data store for production</span></span>

<span data-ttu-id="89751-239">Olá SDK de Node.js de aplicativos móveis do Azure usa Olá [mssql Node. js pacote] tooestablish e usar uma conexão tooboth SQL Express e o banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="89751-239">hello Azure Mobile Apps Node.js SDK uses hello [mssql Node.js package] tooestablish and use a connection tooboth SQL Express and SQL Database.</span></span>  <span data-ttu-id="89751-240">Este pacote requer que você habilite conexões TCP na instância do SQL Express.</span><span class="sxs-lookup"><span data-stu-id="89751-240">This package requires that you enable TCP connections on your SQL Express instance.</span></span>

> [!TIP]
> <span data-ttu-id="89751-241">driver de saudação de memória não fornece um conjunto completo de recursos para teste.</span><span class="sxs-lookup"><span data-stu-id="89751-241">hello memory driver does not provide a complete set of facilities for testing.</span></span>  <span data-ttu-id="89751-242">Se você desejar tootest localmente seu back-end, recomendamos usar saudação de um repositório de dados do SQL Express e Olá mssql driver.</span><span class="sxs-lookup"><span data-stu-id="89751-242">If you wish tootest your backend locally, we recommend hello use of a SQL Express data store and hello mssql driver.</span></span>
>
>

1. <span data-ttu-id="89751-243">Baixe e instale o [Microsoft SQL Server 2014 Express].</span><span class="sxs-lookup"><span data-stu-id="89751-243">Download and install [Microsoft SQL Server 2014 Express].</span></span>  <span data-ttu-id="89751-244">Certifique-se de que você instalar Olá SQL Server 2014 Express com ferramentas edition.</span><span class="sxs-lookup"><span data-stu-id="89751-244">Ensure you install hello SQL Server 2014 Express with Tools edition.</span></span>  <span data-ttu-id="89751-245">A menos que você explicitamente precisar do suporte de 64 bits, versão de 32 bits Olá consome menos memória durante a execução.</span><span class="sxs-lookup"><span data-stu-id="89751-245">Unless you explicitly require 64-bit support, hello 32-bit version consumes less memory when running.</span></span>
2. <span data-ttu-id="89751-246">Execute Olá Gerenciador de configuração do SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="89751-246">Run hello SQL Server 2014 Configuration Manager.</span></span>

   1. <span data-ttu-id="89751-247">Expanda Olá **configuração de rede do SQL Server** nó no menu de árvore à esquerda de saudação.</span><span class="sxs-lookup"><span data-stu-id="89751-247">Expand hello **SQL Server Network Configuration** node in hello left-hand tree menu.</span></span>
   2. <span data-ttu-id="89751-248">Clique em **Protocolos para SQLEXPRESS**.</span><span class="sxs-lookup"><span data-stu-id="89751-248">Click **Protocols for SQLEXPRESS**.</span></span>
   3. <span data-ttu-id="89751-249">Clique com o botão direito do mouse em **TCP/IP** e escolha **Habilitar**.</span><span class="sxs-lookup"><span data-stu-id="89751-249">Right-click **TCP/IP** and select **Enable**.</span></span>  <span data-ttu-id="89751-250">Clique em **Okey** na caixa de diálogo pop-up hello.</span><span class="sxs-lookup"><span data-stu-id="89751-250">Click **OK** in hello pop-up dialog.</span></span>
   4. <span data-ttu-id="89751-251">Clique com o botão direito do mouse em **TCP/IP** e escolha **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="89751-251">Right-click **TCP/IP** and select **Properties**.</span></span>
   5. <span data-ttu-id="89751-252">Clique em Olá **endereços IP** guia.</span><span class="sxs-lookup"><span data-stu-id="89751-252">Click hello **IP Addresses** tab.</span></span>
   6. <span data-ttu-id="89751-253">Localize Olá **IPAll** nó.</span><span class="sxs-lookup"><span data-stu-id="89751-253">Find hello **IPAll** node.</span></span>  <span data-ttu-id="89751-254">Em Olá **a porta TCP** , digite **1433**.</span><span class="sxs-lookup"><span data-stu-id="89751-254">In hello **TCP Port** field, enter **1433**.</span></span>

          ![Configure SQL Express for TCP/IP][3]
   7. <span data-ttu-id="89751-255">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="89751-255">Click **OK**.</span></span>  <span data-ttu-id="89751-256">Clique em **Okey** na caixa de diálogo pop-up hello.</span><span class="sxs-lookup"><span data-stu-id="89751-256">Click **OK** in hello pop-up dialog.</span></span>
   8. <span data-ttu-id="89751-257">Clique em **SQL Server Services** no menu de árvore à esquerda de saudação.</span><span class="sxs-lookup"><span data-stu-id="89751-257">Click **SQL Server Services** in hello left-hand tree menu.</span></span>
   9. <span data-ttu-id="89751-258">Clique com o botão direito do mouse em **SQL Server (SQLEXPRESS)** e escolha **Reiniciar**</span><span class="sxs-lookup"><span data-stu-id="89751-258">Right-click **SQL Server (SQLEXPRESS)** and select **Restart**</span></span>
   10. <span data-ttu-id="89751-259">Feche Olá Gerenciador de configuração do SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="89751-259">Close hello SQL Server 2014 Configuration Manager.</span></span>
3. <span data-ttu-id="89751-260">Executar Olá SQL Server 2014 Management Studio e conecte-se a instância do SQL Express local tooyour</span><span class="sxs-lookup"><span data-stu-id="89751-260">Run hello SQL Server 2014 Management Studio and connect tooyour local SQL Express instance</span></span>

   1. <span data-ttu-id="89751-261">Clique em sua instância de saudação Pesquisador de objetos e selecione **propriedades**</span><span class="sxs-lookup"><span data-stu-id="89751-261">Right-click your instance in hello Object Explorer and select **Properties**</span></span>
   2. <span data-ttu-id="89751-262">Selecione Olá **segurança** página.</span><span class="sxs-lookup"><span data-stu-id="89751-262">Select hello **Security** page.</span></span>
   3. <span data-ttu-id="89751-263">Certifique-se de saudação **modo de autenticação do Windows e SQL Server** está selecionada</span><span class="sxs-lookup"><span data-stu-id="89751-263">Ensure hello **SQL Server and Windows Authentication mode** is selected</span></span>
   4. <span data-ttu-id="89751-264">Clique em **OK**</span><span class="sxs-lookup"><span data-stu-id="89751-264">Click **OK**</span></span>

          ![Configure SQL Express Authentication][4]
   5. <span data-ttu-id="89751-265">Expanda **segurança** > **logons** em Olá Pesquisador de objetos</span><span class="sxs-lookup"><span data-stu-id="89751-265">Expand **Security** > **Logins** in hello Object Explorer</span></span>
   6. <span data-ttu-id="89751-266">Clique com o botão direito do mouse em **Logons** e escolha **Novo Logon...**</span><span class="sxs-lookup"><span data-stu-id="89751-266">Right-click **Logins** and select **New Login...**</span></span>
   7. <span data-ttu-id="89751-267">Insira um nome de logon.</span><span class="sxs-lookup"><span data-stu-id="89751-267">Enter a Login name.</span></span>  <span data-ttu-id="89751-268">Selecione **Autenticação do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="89751-268">Select **SQL Server authentication**.</span></span>  <span data-ttu-id="89751-269">Insira uma senha e digite Olá mesma senha em **Confirmar senha**.</span><span class="sxs-lookup"><span data-stu-id="89751-269">Enter a Password, then enter hello same password in **Confirm password**.</span></span>  <span data-ttu-id="89751-270">senha Olá deve atender aos requisitos de complexidade do Windows.</span><span class="sxs-lookup"><span data-stu-id="89751-270">hello password must meet Windows complexity requirements.</span></span>
   8. <span data-ttu-id="89751-271">Clique em **OK**</span><span class="sxs-lookup"><span data-stu-id="89751-271">Click **OK**</span></span>

          ![Add a new user tooSQL Express][5]
   9. <span data-ttu-id="89751-272">Clique com o botão direito do mouse em seu novo logon e escolha **Propriedades**</span><span class="sxs-lookup"><span data-stu-id="89751-272">Right-click your new login and select **Properties**</span></span>
   10. <span data-ttu-id="89751-273">Selecione Olá **funções de servidor** página</span><span class="sxs-lookup"><span data-stu-id="89751-273">Select hello **Server Roles** page</span></span>
   11. <span data-ttu-id="89751-274">Verificar Olá caixa próxima toohello **dbcreator** função de servidor</span><span class="sxs-lookup"><span data-stu-id="89751-274">Check hello box next toohello **dbcreator** server role</span></span>
   12. <span data-ttu-id="89751-275">Clique em **OK**</span><span class="sxs-lookup"><span data-stu-id="89751-275">Click **OK**</span></span>
   13. <span data-ttu-id="89751-276">Fechar Olá SQL Server 2015 Management Studio</span><span class="sxs-lookup"><span data-stu-id="89751-276">Close hello SQL Server 2015 Management Studio</span></span>

<span data-ttu-id="89751-277">Verifique se você Olá registro de nome de usuário e senha que você selecionou.</span><span class="sxs-lookup"><span data-stu-id="89751-277">Ensure you record hello username and password you selected.</span></span>  <span data-ttu-id="89751-278">Talvez seja necessário tooassign funções de servidor adicionais ou permissões, dependendo dos requisitos de banco de dados específico.</span><span class="sxs-lookup"><span data-stu-id="89751-278">You may need tooassign additional server roles or permissions depending on your specific database requirements.</span></span>

<span data-ttu-id="89751-279">Olá Node. js aplicativo lê Olá **SQLCONNSTR_MS_TableConnectionString** variável de ambiente para a cadeia de caracteres de conexão de saudação do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="89751-279">hello Node.js application reads hello **SQLCONNSTR_MS_TableConnectionString** environment variable for hello connection string for this database.</span></span>  <span data-ttu-id="89751-280">Você pode definir essa variável em seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="89751-280">You can set this variable within your environment.</span></span>  <span data-ttu-id="89751-281">Por exemplo, você pode usar PowerShell tooset essa variável de ambiente:</span><span class="sxs-lookup"><span data-stu-id="89751-281">For example, you can use PowerShell tooset this environment variable:</span></span>

    $env:SQLCONNSTR_MS_TableConnectionString = "Server=127.0.0.1; Database=mytestdatabase; User Id=azuremobile; Password=T3stPa55word;"

<span data-ttu-id="89751-282">Saudação de acesso de banco de dados por meio de uma conexão TCP/IP e fornecer um nome de usuário e senha para conexão hello.</span><span class="sxs-lookup"><span data-stu-id="89751-282">Access hello database through a TCP/IP connection and provide a username and password for hello connection.</span></span>

### <span data-ttu-id="89751-283"><a name="howto-config-localdev"></a>Como configurar seu projeto para desenvolvimento local</span><span class="sxs-lookup"><span data-stu-id="89751-283"><a name="howto-config-localdev"></a>How to: Configure your project for local development</span></span>
<span data-ttu-id="89751-284">Aplicativos móveis do Azure lê um arquivo JavaScript chamado *azureMobile.js* do sistema de arquivos local hello.</span><span class="sxs-lookup"><span data-stu-id="89751-284">Azure Mobile Apps reads a JavaScript file called *azureMobile.js* from hello local filesystem.</span></span>  <span data-ttu-id="89751-285">Não use Olá de tooconfigure este arquivo SDK de aplicativos móveis do Azure em produção - usar configurações de aplicativo em hello [portal do Azure] em vez disso.</span><span class="sxs-lookup"><span data-stu-id="89751-285">Do not use this file tooconfigure hello Azure Mobile Apps SDK in production - use App Settings within hello [Azure portal] instead.</span></span>  <span data-ttu-id="89751-286">Olá *azureMobile.js* arquivo deverá exportar um objeto de configuração.</span><span class="sxs-lookup"><span data-stu-id="89751-286">hello *azureMobile.js* file should export a configuration object.</span></span>  <span data-ttu-id="89751-287">configurações de Hello mais comuns são:</span><span class="sxs-lookup"><span data-stu-id="89751-287">hello most common settings are:</span></span>

* <span data-ttu-id="89751-288">Configurações do banco de dados</span><span class="sxs-lookup"><span data-stu-id="89751-288">Database Settings</span></span>
* <span data-ttu-id="89751-289">Configurações de registro em log de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="89751-289">Diagnostic Logging Settings</span></span>
* <span data-ttu-id="89751-290">Configurações de CORS alternativas</span><span class="sxs-lookup"><span data-stu-id="89751-290">Alternate CORS Settings</span></span>

<span data-ttu-id="89751-291">Um exemplo *azureMobile.js* arquivo implementando Olá anterior a maneira de configurações de banco de dados:</span><span class="sxs-lookup"><span data-stu-id="89751-291">An example *azureMobile.js* file implementing hello preceding database settings follows:</span></span>

    module.exports = {
        cors: {
            origins: [ 'localhost' ]
        },
        data: {
            provider: 'mssql',
            server: '127.0.0.1',
            database: 'mytestdatabase',
            user: 'azuremobile',
            password: 'T3stPa55word'
        },
        logging: {
            level: 'verbose'
        }
    };

<span data-ttu-id="89751-292">Recomendamos que você adicione *azureMobile.js* tooyour *. gitignore* arquivo (ou outro controle do código fonte Ignorar arquivo) tooprevent senhas sejam armazenadas na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="89751-292">We recommend that you add *azureMobile.js* tooyour *.gitignore* file (or other source code control ignore file) tooprevent passwords from being stored in hello cloud.</span></span>  <span data-ttu-id="89751-293">Sempre configurar configurações de produção em configurações do aplicativo em Olá [portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="89751-293">Always configure production settings in App Settings within hello [Azure portal].</span></span>

### <span data-ttu-id="89751-294"><a name="howto-appsettings"></a>Como definir configurações de aplicativo para seu aplicativo móvel</span><span class="sxs-lookup"><span data-stu-id="89751-294"><a name="howto-appsettings"></a>How: Configure App Settings for your Mobile App</span></span>
<span data-ttu-id="89751-295">A maioria das configurações no hello *azureMobile.js* arquivo tem uma configuração de aplicativo equivalente no hello [portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="89751-295">Most settings in hello *azureMobile.js* file have an equivalent App Setting in hello [Azure portal].</span></span>  <span data-ttu-id="89751-296">Use o aplicativo de saudação tooconfigure lista a seguir nas configurações do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="89751-296">Use hello following list tooconfigure your app in App Settings:</span></span>

| <span data-ttu-id="89751-297">Configurações de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="89751-297">App Setting</span></span> | <span data-ttu-id="89751-298">*azureMobile.js* </span><span class="sxs-lookup"><span data-stu-id="89751-298">*azureMobile.js* Setting</span></span> | <span data-ttu-id="89751-299">Descrição</span><span class="sxs-lookup"><span data-stu-id="89751-299">Description</span></span> | <span data-ttu-id="89751-300">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="89751-300">Valid Values</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="89751-301">**MS_MobileAppName**</span><span class="sxs-lookup"><span data-stu-id="89751-301">**MS_MobileAppName**</span></span> |<span data-ttu-id="89751-302">name</span><span class="sxs-lookup"><span data-stu-id="89751-302">name</span></span> |<span data-ttu-id="89751-303">nome de saudação do aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="89751-303">hello name of hello app</span></span> |<span data-ttu-id="89751-304">string</span><span class="sxs-lookup"><span data-stu-id="89751-304">string</span></span> |
| <span data-ttu-id="89751-305">**MS_MobileLoggingLevel**</span><span class="sxs-lookup"><span data-stu-id="89751-305">**MS_MobileLoggingLevel**</span></span> |<span data-ttu-id="89751-306">logging.level</span><span class="sxs-lookup"><span data-stu-id="89751-306">logging.level</span></span> |<span data-ttu-id="89751-307">Nível de log mínimo de toolog de mensagens</span><span class="sxs-lookup"><span data-stu-id="89751-307">Minimum log level of messages toolog</span></span> |<span data-ttu-id="89751-308">erro, aviso, informações, detalhado, depuração, simples</span><span class="sxs-lookup"><span data-stu-id="89751-308">error, warning, info, verbose, debug, silly</span></span> |
| <span data-ttu-id="89751-309">**MS_DebugMode**</span><span class="sxs-lookup"><span data-stu-id="89751-309">**MS_DebugMode**</span></span> |<span data-ttu-id="89751-310">depurar</span><span class="sxs-lookup"><span data-stu-id="89751-310">debug</span></span> |<span data-ttu-id="89751-311">Habilitar ou desabilitar o modo de depuração</span><span class="sxs-lookup"><span data-stu-id="89751-311">Enable or Disable debug mode</span></span> |<span data-ttu-id="89751-312">verdadeiro, falso</span><span class="sxs-lookup"><span data-stu-id="89751-312">true, false</span></span> |
| <span data-ttu-id="89751-313">**MS_TableSchema**</span><span class="sxs-lookup"><span data-stu-id="89751-313">**MS_TableSchema**</span></span> |<span data-ttu-id="89751-314">data.schema</span><span class="sxs-lookup"><span data-stu-id="89751-314">data.schema</span></span> |<span data-ttu-id="89751-315">Nome do esquema padrão para tabelas SQL</span><span class="sxs-lookup"><span data-stu-id="89751-315">Default schema name for SQL tables</span></span> |<span data-ttu-id="89751-316">cadeia de caracteres (padrão: dbo)</span><span class="sxs-lookup"><span data-stu-id="89751-316">string (default: dbo)</span></span> |
| <span data-ttu-id="89751-317">**MS_DynamicSchema**</span><span class="sxs-lookup"><span data-stu-id="89751-317">**MS_DynamicSchema**</span></span> |<span data-ttu-id="89751-318">data.dynamicSchema</span><span class="sxs-lookup"><span data-stu-id="89751-318">data.dynamicSchema</span></span> |<span data-ttu-id="89751-319">Habilitar ou desabilitar o modo de depuração</span><span class="sxs-lookup"><span data-stu-id="89751-319">Enable or Disable debug mode</span></span> |<span data-ttu-id="89751-320">verdadeiro, falso</span><span class="sxs-lookup"><span data-stu-id="89751-320">true, false</span></span> |
| <span data-ttu-id="89751-321">**MS_DisableVersionHeader**</span><span class="sxs-lookup"><span data-stu-id="89751-321">**MS_DisableVersionHeader**</span></span> |<span data-ttu-id="89751-322">versão (tooundefined conjunto)</span><span class="sxs-lookup"><span data-stu-id="89751-322">version (set tooundefined)</span></span> |<span data-ttu-id="89751-323">Desabilita o cabeçalho Olá X-ZUMO-Server-Version</span><span class="sxs-lookup"><span data-stu-id="89751-323">Disables hello X-ZUMO-Server-Version header</span></span> |<span data-ttu-id="89751-324">verdadeiro, falso</span><span class="sxs-lookup"><span data-stu-id="89751-324">true, false</span></span> |
| <span data-ttu-id="89751-325">**MS_SkipVersionCheck**</span><span class="sxs-lookup"><span data-stu-id="89751-325">**MS_SkipVersionCheck**</span></span> |<span data-ttu-id="89751-326">skipversioncheck</span><span class="sxs-lookup"><span data-stu-id="89751-326">skipversioncheck</span></span> |<span data-ttu-id="89751-327">Desabilita a verificação de versão de API do cliente Olá</span><span class="sxs-lookup"><span data-stu-id="89751-327">Disables hello client API version check</span></span> |<span data-ttu-id="89751-328">verdadeiro, falso</span><span class="sxs-lookup"><span data-stu-id="89751-328">true, false</span></span> |

<span data-ttu-id="89751-329">tooset uma configuração de aplicativo:</span><span class="sxs-lookup"><span data-stu-id="89751-329">tooset an App Setting:</span></span>

1. <span data-ttu-id="89751-330">Faça logon no toohello [portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="89751-330">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="89751-331">Selecione **todos os recursos** ou **serviços de aplicativos** , em seguida, clique em nome de saudação do seu aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="89751-331">Select **All resources** or **App Services** then click hello name of your Mobile App.</span></span>
3. <span data-ttu-id="89751-332">folha de configurações de saudação é aberto por padrão.</span><span class="sxs-lookup"><span data-stu-id="89751-332">hello Settings blade opens by default.</span></span> <span data-ttu-id="89751-333">Se ela não abrir, clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="89751-333">If it doesn't, click **Settings**.</span></span>
4. <span data-ttu-id="89751-334">Clique em **configurações de aplicativo** no menu geral hello.</span><span class="sxs-lookup"><span data-stu-id="89751-334">Click **Application settings** in hello GENERAL menu.</span></span>
5. <span data-ttu-id="89751-335">Role toohello seção configurações do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="89751-335">Scroll toohello App Settings section.</span></span>
6. <span data-ttu-id="89751-336">Se seu aplicativo definindo já existir, clique em valor Olá Olá aplicativo definindo tooedit Olá valor.</span><span class="sxs-lookup"><span data-stu-id="89751-336">If your app setting already exists, click hello value of hello app setting tooedit hello value.</span></span>
7. <span data-ttu-id="89751-337">Se sua configuração de aplicativo não existir, digite Olá configuração do aplicativo na caixa de chave de saudação e valor Olá na caixa de valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="89751-337">If your app setting does not exist, enter hello App Setting in hello Key box and hello value in hello Value box.</span></span>
8. <span data-ttu-id="89751-338">Quando você tiver concluído, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="89751-338">Once you are complete, click **Save**.</span></span>

<span data-ttu-id="89751-339">A alteração da maioria das Configurações do Aplicativo requer o reinício do serviço.</span><span class="sxs-lookup"><span data-stu-id="89751-339">Changing most app settings requires a service restart.</span></span>

### <span data-ttu-id="89751-340"><a name="howto-use-sqlazure"></a>Como usar o Banco de Dados SQL como o armazenamento de dados de produção</span><span class="sxs-lookup"><span data-stu-id="89751-340"><a name="howto-use-sqlazure"></a>How to: Use SQL Database as your production data store</span></span>
<!--- ALTERNATE INCLUDE - we can't use ../includes/app-service-mobile-dotnet-backend-create-new-service.md - slightly different semantics -->

<span data-ttu-id="89751-341">O uso do Banco de Dados SQL do Azure como armazenamento de dados é idêntico em todos os tipos de aplicativo do Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="89751-341">Using Azure SQL Database as a data store is identical across all Azure App Service application types.</span></span> <span data-ttu-id="89751-342">Se você não tiver feito isso ainda, siga essas etapas toocreate um back-end do aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="89751-342">If you have not done so already, follow these steps toocreate a Mobile App backend.</span></span>

1. <span data-ttu-id="89751-343">Faça logon no toohello [portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="89751-343">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="89751-344">Em hello superior esquerda da janela de saudação, clique em Olá **+ novo** botão > **Web + móvel** > **aplicativo móvel**, em seguida, forneça um nome para seu back-end do aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="89751-344">In hello top left of hello window, click hello **+NEW** button > **Web + Mobile** > **Mobile App**, then provide a name for your Mobile App backend.</span></span>
3. <span data-ttu-id="89751-345">Em Olá **grupo de recursos** , digite Olá mesmo nome do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="89751-345">In hello **Resource Group** box, enter hello same name as your app.</span></span>
4. <span data-ttu-id="89751-346">plano de serviço de aplicativo padrão de saudação é selecionado.</span><span class="sxs-lookup"><span data-stu-id="89751-346">hello Default App Service plan is selected.</span></span>  <span data-ttu-id="89751-347">Se você quiser toochange seu plano de serviço de aplicativo, você pode fazer isso clicando Olá plano do serviço de aplicativo > **+ criar novos**.</span><span class="sxs-lookup"><span data-stu-id="89751-347">If you wish toochange your App Service plan, you can do so by clicking hello App Service Plan > **+ Create New**.</span></span>  <span data-ttu-id="89751-348">Forneça um nome do novo plano do serviço de aplicativo hello e selecione um local apropriado.</span><span class="sxs-lookup"><span data-stu-id="89751-348">Provide a name of hello new App Service plan and select an appropriate location.</span></span>  <span data-ttu-id="89751-349">Clique em preço hello e selecione um preço apropriado para o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="89751-349">Click hello Pricing tier and select an appropriate pricing tier for hello service.</span></span> <span data-ttu-id="89751-350">Selecione **exibir todos os** tooview preços mais opções, como **livre** e **compartilhado**.</span><span class="sxs-lookup"><span data-stu-id="89751-350">Select **View all** tooview more pricing options, such as **Free** and **Shared**.</span></span>  <span data-ttu-id="89751-351">Depois que você selecionou o tipo de preço, clique em Olá **selecione** botão.</span><span class="sxs-lookup"><span data-stu-id="89751-351">Once you have selected the pricing tier, click hello **Select** button.</span></span>  <span data-ttu-id="89751-352">Em Olá **plano de serviço de aplicativo** folha, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="89751-352">Back in hello **App Service plan** blade, click **OK**.</span></span>
5. <span data-ttu-id="89751-353">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="89751-353">Click **Create**.</span></span> <span data-ttu-id="89751-354">O provisionamento de um back-end de aplicativo móvel pode levar alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="89751-354">Provisioning a Mobile App backend can take a couple of minutes.</span></span>  <span data-ttu-id="89751-355">Depois de back-end de aplicativo móvel Olá é configurado, o portal Olá abre Olá **configurações** folha de back-end de aplicativo móvel hello.</span><span class="sxs-lookup"><span data-stu-id="89751-355">Once hello Mobile App backend is provisioned, hello portal opens hello **Settings** blade for hello Mobile App backend.</span></span>

<span data-ttu-id="89751-356">Depois de back-end de aplicativo móvel Olá é criado, você pode escolher tooeither se conectar a um SQL database tooyour aplicativo móvel back-end existente ou criar um novo banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="89751-356">Once hello Mobile App backend is created, you can choose tooeither connect an existing SQL database tooyour Mobile App backend or create a new SQL database.</span></span>  <span data-ttu-id="89751-357">Nesta seção, criamos um banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="89751-357">In this section, we create a SQL database.</span></span>

> [!NOTE]
> <span data-ttu-id="89751-358">Se você já tiver um banco de dados em Olá mesmo local como back-end de aplicativo móvel hello, você pode optar por **usar um banco de dados** e, em seguida, selecione o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="89751-358">If you already have a database in hello same location as hello mobile app backend, you can instead choose **Use an existing database** and then select that database.</span></span> <span data-ttu-id="89751-359">uso de saudação do banco de dados em um local diferente não é recomendado devido a latências mais altas.</span><span class="sxs-lookup"><span data-stu-id="89751-359">hello use of a database in a different location is not recommended because of higher latencies.</span></span>
>
>

1. <span data-ttu-id="89751-360">No hello novo aplicativo móvel back-end, clique em **configurações** > **aplicativo móvel** > **dados** > **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="89751-360">In hello new Mobile App backend, click **Settings** > **Mobile App** > **Data** > **+Add**.</span></span>
2. <span data-ttu-id="89751-361">Em Olá **Adicionar conexão de dados** folha, clique em **banco de dados SQL - definir configurações obrigatórias** > **criar um novo banco de dados**.</span><span class="sxs-lookup"><span data-stu-id="89751-361">In hello **Add data connection** blade, click **SQL Database - Configure required settings** > **Create a new database**.</span></span>  <span data-ttu-id="89751-362">Insira o nome de saudação do novo banco de dados de saudação em Olá **nome** campo.</span><span class="sxs-lookup"><span data-stu-id="89751-362">Enter hello name of hello new database in hello **Name** field.</span></span>
3. <span data-ttu-id="89751-363">Clique em **Servidor**.</span><span class="sxs-lookup"><span data-stu-id="89751-363">Click **Server**.</span></span>  <span data-ttu-id="89751-364">Em Olá **novo servidor** folha, digite um nome de servidor exclusivo no hello **nome do servidor** campo e fornecer um adequado **logon de administrador do servidor** e **senha**.</span><span class="sxs-lookup"><span data-stu-id="89751-364">In hello **New server** blade, enter a unique server name in hello **Server name** field, and provide a suitable **Server admin login** and **Password**.</span></span>  <span data-ttu-id="89751-365">Certifique-se de **permitir servidor de tooaccess de serviços do azure** é verificada.</span><span class="sxs-lookup"><span data-stu-id="89751-365">Ensure **Allow azure services tooaccess server** is checked.</span></span>  <span data-ttu-id="89751-366">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="89751-366">Click **OK**.</span></span>

    ![Criar um Banco de Dados SQL do Azure][6]
4. <span data-ttu-id="89751-368">Em Olá **novo banco de dados** folha, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="89751-368">On hello **New database** blade, click **OK**.</span></span>
5. <span data-ttu-id="89751-369">Em Olá **Adicionar conexão de dados** folha, selecione **cadeia de caracteres de Conexão**, insira o logon de saudação e a senha que você forneceu ao criar o banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="89751-369">Back on hello **Add data connection** blade, select **Connection string**, enter hello login and password that you provided when creating hello database.</span></span>  <span data-ttu-id="89751-370">Se você usar um banco de dados existente, fornece credenciais de logon de saudação do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="89751-370">If you use an existing database, provide hello login credentials for that database.</span></span>  <span data-ttu-id="89751-371">Depois de inserir, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="89751-371">Once entered, click **OK**.</span></span>
6. <span data-ttu-id="89751-372">Em Olá **Adicionar conexão de dados** folha novamente, clique em **Okey** o banco de dados do toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="89751-372">Back on hello **Add data connection** blade again, click **OK** toocreate hello database.</span></span>

<!--- END OF ALTERNATE INCLUDE -->

<span data-ttu-id="89751-373">Criação de banco de dados de saudação pode levar alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="89751-373">Creation of hello database can take a few minutes.</span></span>  <span data-ttu-id="89751-374">Saudação de uso **notificações** progresso de saudação toomonitor área de implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="89751-374">Use hello **Notifications** area toomonitor hello progress of hello deployment.</span></span>  <span data-ttu-id="89751-375">Não andamento até que o banco de dados de saudação foi implantado com êxito.</span><span class="sxs-lookup"><span data-stu-id="89751-375">Do not progress until hello database has been deployed successfully.</span></span>  <span data-ttu-id="89751-376">Uma vez implantado com êxito, uma cadeia de caracteres de Conexão é criada para a instância de banco de dados SQL Olá em suas configurações do aplicativo de back-end móvel.</span><span class="sxs-lookup"><span data-stu-id="89751-376">Once successfully deployed, a Connection String is created for hello SQL Database instance in your Mobile backend App Settings.</span></span>  <span data-ttu-id="89751-377">Você pode ver essa configuração de aplicativo no hello **configurações** > **configurações do aplicativo** > **cadeias de caracteres de Conexão**.</span><span class="sxs-lookup"><span data-stu-id="89751-377">You can see this app setting in hello **Settings** > **Application settings** > **Connection strings**.</span></span>

### <span data-ttu-id="89751-378"><a name="howto-tables-auth"></a>Como: exigir autenticação para acesso tootables</span><span class="sxs-lookup"><span data-stu-id="89751-378"><a name="howto-tables-auth"></a>How to: Require authentication for access tootables</span></span>
<span data-ttu-id="89751-379">Se você quiser toouse autenticação do serviço de aplicativo com o ponto de extremidade do hello tabelas, você deve configurar autenticação do serviço de aplicativo no hello [portal do Azure] primeiro.</span><span class="sxs-lookup"><span data-stu-id="89751-379">If you wish toouse App Service Authentication with hello tables endpoint, you must configure App Service Authentication in hello [Azure portal] first.</span></span>  <span data-ttu-id="89751-380">Para obter mais detalhes sobre como configurar a autenticação em um serviço de aplicativo do Azure, examine Olá guia de configuração para o provedor de identidade Olá pretende toouse:</span><span class="sxs-lookup"><span data-stu-id="89751-380">For more details about configuring authentication in an Azure App Service, review hello Configuration Guide for hello identity provider you intend toouse:</span></span>

* <span data-ttu-id="89751-381">[Como tooconfigure autenticação do Active Directory do Azure]</span><span class="sxs-lookup"><span data-stu-id="89751-381">[How tooconfigure Azure Active Directory Authentication]</span></span>
* <span data-ttu-id="89751-382">[Como tooconfigure autenticação do Facebook]</span><span class="sxs-lookup"><span data-stu-id="89751-382">[How tooconfigure Facebook Authentication]</span></span>
* <span data-ttu-id="89751-383">[Como tooconfigure autenticação do Google]</span><span class="sxs-lookup"><span data-stu-id="89751-383">[How tooconfigure Google Authentication]</span></span>
* <span data-ttu-id="89751-384">[Como tooconfigure Microsoft Authentication]</span><span class="sxs-lookup"><span data-stu-id="89751-384">[How tooconfigure Microsoft Authentication]</span></span>
* <span data-ttu-id="89751-385">[Como tooconfigure autenticação do Twitter]</span><span class="sxs-lookup"><span data-stu-id="89751-385">[How tooconfigure Twitter Authentication]</span></span>

<span data-ttu-id="89751-386">Cada tabela tem uma propriedade de acesso que pode ser usado toocontrol acesso toohello tabela.</span><span class="sxs-lookup"><span data-stu-id="89751-386">Each table has an access property that can be used toocontrol access toohello table.</span></span>  <span data-ttu-id="89751-387">saudação de exemplo a seguir mostra uma tabela estaticamente definida com autenticação necessária.</span><span class="sxs-lookup"><span data-stu-id="89751-387">hello following sample shows a statically defined table with authentication required.</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="89751-388">propriedade de acesso Olá pode assumir um dos três valores</span><span class="sxs-lookup"><span data-stu-id="89751-388">hello access property can take one of three values</span></span>

* <span data-ttu-id="89751-389">*anônimo* indica que o aplicativo de cliente hello é permitido tooread dados sem autenticação</span><span class="sxs-lookup"><span data-stu-id="89751-389">*anonymous* indicates that hello client application is allowed tooread data without authentication</span></span>
* <span data-ttu-id="89751-390">*autenticado* indica que o aplicativo de cliente hello deve enviar um token de autenticação válido com a solicitação de saudação</span><span class="sxs-lookup"><span data-stu-id="89751-390">*authenticated* indicates that hello client application must send a valid authentication token with hello request</span></span>
* <span data-ttu-id="89751-391">*desabilitado* indica que essa tabela está desabilitada no momento</span><span class="sxs-lookup"><span data-stu-id="89751-391">*disabled* indicates that this table is currently disabled</span></span>

<span data-ttu-id="89751-392">Se a propriedade de acesso de saudação não estiver definida, o acesso não autenticado é permitido.</span><span class="sxs-lookup"><span data-stu-id="89751-392">If hello access property is undefined, unauthenticated access is allowed.</span></span>

### <span data-ttu-id="89751-393"><a name="howto-tables-getidentity"></a>Como usar declarações de autenticação com as tabelas</span><span class="sxs-lookup"><span data-stu-id="89751-393"><a name="howto-tables-getidentity"></a>How to: Use authentication claims with your tables</span></span>
<span data-ttu-id="89751-394">Você pode configurar várias declarações que são solicitadas durante a configuração da autenticação.</span><span class="sxs-lookup"><span data-stu-id="89751-394">You can set up various claims that are requested when authentication is set up.</span></span>  <span data-ttu-id="89751-395">Essas declarações normalmente não estão disponíveis por meio de saudação `context.user` objeto.</span><span class="sxs-lookup"><span data-stu-id="89751-395">These claims are not normally available through hello `context.user` object.</span></span>  <span data-ttu-id="89751-396">No entanto, eles podem ser recuperados usando Olá `context.user.getIdentity()` método.</span><span class="sxs-lookup"><span data-stu-id="89751-396">However, they can be retrieved using hello `context.user.getIdentity()` method.</span></span>  <span data-ttu-id="89751-397">Olá `getIdentity()` método retorna uma promessa resolvida tooan objeto.</span><span class="sxs-lookup"><span data-stu-id="89751-397">hello `getIdentity()` method returns a Promise that resolves tooan object.</span></span>  <span data-ttu-id="89751-398">objeto Olá é organizado pelo método de autenticação (facebook, google, twitter, conta da Microsoft ou aad).</span><span class="sxs-lookup"><span data-stu-id="89751-398">hello object is keyed by the authentication method (facebook, google, twitter, microsoftaccount, or aad).</span></span>

<span data-ttu-id="89751-399">Por exemplo, se você configurar a autenticação da Microsoft Account e declaração de endereços de email de saudação de solicitação, você pode adicionar o registro de toohello de endereço de email de saudação com hello controlador da tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="89751-399">For example, if you set up Microsoft Account authentication and request hello email addresses claim, you can add hello email address toohello record with hello following table controller:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    // Create a new table definition
    var table = azureMobileApps.table();

    table.columns = {
        "emailAddress": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;
    table.access = 'authenticated';

    /**
    * Limit hello context query toothose records with hello authenticated user email address
    * @param {Context} context hello operation context
    * @returns {Promise} context execution Promise
    */
    function queryContextForEmail(context) {
        return context.user.getIdentity().then((data) => {
            context.query.where({ emailAddress: data.microsoftaccount.claims.emailaddress });
            return context.execute();
        });
    }

    /**
    * Adds hello email address from hello claims toohello context item - used for
    * insert operations
    * @param {Context} context hello operation context
    * @returns {Promise} context execution Promise
    */
    function addEmailToContext(context) {
        return context.user.getIdentity().then((data) => {
            context.item.emailAddress = data.microsoftaccount.claims.emailaddress;
            return context.execute();
        });
    }

    // Configure specific code when hello client does a request
    // READ - only return records belonging toohello authenticated user
    table.read(queryContextForEmail);

    // CREATE - add or overwrite hello userId based on hello authenticated user
    table.insert(addEmailToContext);

    // UPDATE - only allow updating of record belong toohello authenticated user
    table.update(queryContextForEmail);

    // DELETE - only allow deletion of records belong toohello authenticated uer
    table.delete(queryContextForEmail);

    module.exports = table;

<span data-ttu-id="89751-400">toosee quais declarações estão disponíveis, use uma saudação de tooview do navegador da web `/.auth/me` ponto de extremidade do seu site.</span><span class="sxs-lookup"><span data-stu-id="89751-400">toosee what claims are available, use a web browser tooview hello `/.auth/me` endpoint of your site.</span></span>

### <span data-ttu-id="89751-401"><a name="howto-tables-disabled"></a>Como: operações de tabela desabilitar acesso toospecific</span><span class="sxs-lookup"><span data-stu-id="89751-401"><a name="howto-tables-disabled"></a>How to: Disable access toospecific table operations</span></span>
<span data-ttu-id="89751-402">Em adição tooappearing na tabela Olá, propriedade de acesso de saudação pode ser usado toocontrol as operações individuais.</span><span class="sxs-lookup"><span data-stu-id="89751-402">In addition tooappearing on hello table, hello access property can be used toocontrol individual operations.</span></span>  <span data-ttu-id="89751-403">Há quatro operações:</span><span class="sxs-lookup"><span data-stu-id="89751-403">There are four operations:</span></span>

* <span data-ttu-id="89751-404">*ler* é a operação obter RESTful Olá na tabela de saudação</span><span class="sxs-lookup"><span data-stu-id="89751-404">*read* is hello RESTful GET operation on hello table</span></span>
* <span data-ttu-id="89751-405">*Inserir* é Olá POST RESTful operação na tabela de saudação</span><span class="sxs-lookup"><span data-stu-id="89751-405">*insert* is hello RESTful POST operation on hello table</span></span>
* <span data-ttu-id="89751-406">*atualizar* é uma operação de PATCH RESTful Olá em tabela Olá</span><span class="sxs-lookup"><span data-stu-id="89751-406">*update* is hello RESTful PATCH operation on hello table</span></span>
* <span data-ttu-id="89751-407">*Excluir* é a operação Excluir RESTful Olá na tabela de saudação</span><span class="sxs-lookup"><span data-stu-id="89751-407">*delete* is hello RESTful DELETE operation on hello table</span></span>

<span data-ttu-id="89751-408">Por exemplo, você poderá tooprovide uma tabela não autenticada somente leitura:</span><span class="sxs-lookup"><span data-stu-id="89751-408">For example, you may wish tooprovide a read-only unauthenticated table:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Read-Only table - only allow READ operations
    table.read.access = 'anonymous';
    table.insert.access = 'disabled';
    table.update.access = 'disabled';
    table.delete.access = 'disabled';

    module.exports = table;

### <span data-ttu-id="89751-409"><a name="howto-tables-query"></a>Como: ajustar a consulta de saudação que é usada com operações de tabela</span><span class="sxs-lookup"><span data-stu-id="89751-409"><a name="howto-tables-query"></a>How to: Adjust hello query that is used with table operations</span></span>
<span data-ttu-id="89751-410">Um requisito comum para operações de tabela é tooprovide uma exibição restrita do dados saudação.</span><span class="sxs-lookup"><span data-stu-id="89751-410">A common requirement for table operations is tooprovide a restricted view of hello data.</span></span>  <span data-ttu-id="89751-411">Por exemplo, você pode fornecer uma tabela que é marcada com hello autenticado a ID de usuário, de modo que você pode apenas ler ou atualizar seus próprios registros.</span><span class="sxs-lookup"><span data-stu-id="89751-411">For example, you may provide a table that is tagged with hello authenticated user ID such that you can only read or update your own records.</span></span>  <span data-ttu-id="89751-412">Olá definição da tabela a seguir fornece essa funcionalidade:</span><span class="sxs-lookup"><span data-stu-id="89751-412">hello following table definition provides this functionality:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define a static schema for hello table
    table.columns = {
        "userId": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;

    // Require authentication for this table
    table.access = 'authenticated';

    // Ensure that only records for hello authenticated user are retrieved
    table.read(function (context) {
        context.query.where({ userId: context.user.id });
        return context.execute();
    });

    // When adding records, add or overwrite hello userId with hello authenticated user
    table.insert(function (context) {
        context.item.userId = context.user.id;
        return context.execute();
    });

    module.exports = table;

<span data-ttu-id="89751-413">As operações que normalmente executam uma consulta têm uma propriedade de consulta que você pode ajustar com um cláusula where.</span><span class="sxs-lookup"><span data-stu-id="89751-413">Operations that normally execute a query have a query property that you can adjust with a where clause.</span></span> <span data-ttu-id="89751-414">Olá consulta propriedade é um [QueryJS] objeto tooconvert usado um toosomething de consulta OData que Olá dados back-end pode processar.</span><span class="sxs-lookup"><span data-stu-id="89751-414">hello query property is a [QueryJS] object that is used tooconvert an OData query toosomething that hello data backend can process.</span></span>  <span data-ttu-id="89751-415">Para casos de igualdade simples (como Olá precedentes), um mapa pode ser usado.</span><span class="sxs-lookup"><span data-stu-id="89751-415">For simple equality cases (like hello preceding one), a map can be used.</span></span> <span data-ttu-id="89751-416">Você também pode adicionar cláusulas SQL específicas:</span><span class="sxs-lookup"><span data-stu-id="89751-416">You can also add specific SQL clauses:</span></span>

    context.query.where('myfield eq ?', 'value');

### <span data-ttu-id="89751-417"><a name="howto-tables-softdelete"></a>Como configurar a exclusão reversível em uma tabela</span><span class="sxs-lookup"><span data-stu-id="89751-417"><a name="howto-tables-softdelete"></a>How to: Configure soft delete on a table</span></span>
<span data-ttu-id="89751-418">A Exclusão Reversível não exclui registros.</span><span class="sxs-lookup"><span data-stu-id="89751-418">Soft Delete does not actually delete records.</span></span>  <span data-ttu-id="89751-419">Em vez disso, ele marca como excluídos no banco de dados de saudação definindo Olá excluído tootrue de coluna.</span><span class="sxs-lookup"><span data-stu-id="89751-419">Instead it marks them as deleted within hello database by setting hello deleted column tootrue.</span></span>  <span data-ttu-id="89751-420">Olá SDK de aplicativos móveis do Azure remove automaticamente registros excluídos por software de resultados, a menos que Olá SDK de cliente móveis usa IncludeDeleted().</span><span class="sxs-lookup"><span data-stu-id="89751-420">hello Azure Mobile Apps SDK automatically removes soft-deleted records from results unless hello Mobile Client SDK uses IncludeDeleted().</span></span>  <span data-ttu-id="89751-421">tooconfigure excluir uma tabela para o software, definir Olá `softDelete` propriedade no arquivo de definição de tabela hello:</span><span class="sxs-lookup"><span data-stu-id="89751-421">tooconfigure a table for soft delete, set hello `softDelete` property in hello table definition file:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Turn on Soft Delete
    table.softDelete = true;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="89751-422">Você deve estabelecer um mecanismo para limpar registros, seja usando aplicativo cliente, trabalho Web, Azure Function ou API personalizada.</span><span class="sxs-lookup"><span data-stu-id="89751-422">You should establish a mechanism for purging records - either from a client application, via a WebJob, Azure Function or through a custom API.</span></span>

### <span data-ttu-id="89751-423"><a name="howto-tables-seeding"></a>Como propagar seu banco de dados com dados</span><span class="sxs-lookup"><span data-stu-id="89751-423"><a name="howto-tables-seeding"></a>How to: Seed your database with data</span></span>
<span data-ttu-id="89751-424">Ao criar um novo aplicativo, talvez você queira tooseed uma tabela com dados.</span><span class="sxs-lookup"><span data-stu-id="89751-424">When creating a new application, you may wish tooseed a table with data.</span></span>  <span data-ttu-id="89751-425">Isso pode ser feito no arquivo de JavaScript de definição de tabela de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="89751-425">This can be done within hello table definition JavaScript file as follows:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };
    table.seed = [
        { text: 'Example 1', complete: false },
        { text: 'Example 2', complete: true }
    ];

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="89751-426">A propagação de dados é feita apenas quando Olá tabela é criada por Olá SDK de aplicativos móveis do Azure.</span><span class="sxs-lookup"><span data-stu-id="89751-426">Seeding of data is only done when hello table is created by hello Azure Mobile Apps SDK.</span></span>  <span data-ttu-id="89751-427">Se a tabela de saudação já existir no banco de dados Olá, nenhum dado é injetado em tabela hello.</span><span class="sxs-lookup"><span data-stu-id="89751-427">If hello table already exists within hello database, no data is injected into hello table.</span></span>  <span data-ttu-id="89751-428">Se o esquema dinâmico está ativada, o esquema é inferido do hello propagado dados.</span><span class="sxs-lookup"><span data-stu-id="89751-428">If dynamic schema is turned on, then the schema is inferred from hello seeded data.</span></span>

<span data-ttu-id="89751-429">É recomendável que você chamar explicitamente Olá `tables.initialize()` tabela de saudação do método toocreate quando Olá execução é iniciada.</span><span class="sxs-lookup"><span data-stu-id="89751-429">We recommend that you explicitly call hello `tables.initialize()` method toocreate hello table when hello service starts running.</span></span>

### <span data-ttu-id="89751-430"><a name="Swagger"></a>Como habilitar o suporte para o Swagger</span><span class="sxs-lookup"><span data-stu-id="89751-430"><a name="Swagger"></a>How to: Enable Swagger support</span></span>
<span data-ttu-id="89751-431">Os Aplicativos Móveis do Serviço de Aplicativo do Azure vêm com suporte interno para o [Swagger] .</span><span class="sxs-lookup"><span data-stu-id="89751-431">Azure App Service Mobile Apps comes with built-in [Swagger] support.</span></span>  <span data-ttu-id="89751-432">tooenable Swagger suporte, primeiro instale Olá swagger-interface do usuário como uma dependência:</span><span class="sxs-lookup"><span data-stu-id="89751-432">tooenable Swagger support, first install hello swagger-ui as a dependency:</span></span>

    npm install --save swagger-ui

<span data-ttu-id="89751-433">Uma vez instalado, você pode habilitar o suporte de Swagger no construtor de aplicativos do Azure Mobile hello:</span><span class="sxs-lookup"><span data-stu-id="89751-433">Once installed, you can enable Swagger support in hello Azure Mobile Apps constructor:</span></span>

    var mobile = azureMobileApps({ swagger: true });

<span data-ttu-id="89751-434">Você provavelmente só deseja tooenable Swagger suporte nas edições de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="89751-434">You probably only want tooenable Swagger support in development editions.</span></span>  <span data-ttu-id="89751-435">Faça isso utilizando a configuração do aplicativo `NODE_ENV` :</span><span class="sxs-lookup"><span data-stu-id="89751-435">You can do this by utilizing the `NODE_ENV` app setting:</span></span>

    var mobile = azureMobileApps({ swagger: process.env.NODE_ENV !== 'production' });

<span data-ttu-id="89751-436">Olá ponto de extremidade de swagger está localizado em http://*yoursite*.azurewebsites.net/swagger.</span><span class="sxs-lookup"><span data-stu-id="89751-436">hello swagger endpoint is located at http://*yoursite*.azurewebsites.net/swagger.</span></span>  <span data-ttu-id="89751-437">Você pode acessar Olá Swagger da interface do usuário por meio de saudação `/swagger/ui` ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="89751-437">You can access hello Swagger UI via hello `/swagger/ui` endpoint.</span></span>  <span data-ttu-id="89751-438">Se você escolher autenticação toorequire em todo o seu aplicativo, Swagger produz um erro.</span><span class="sxs-lookup"><span data-stu-id="89751-438">if you choose toorequire authentication across your entire application, Swagger produces an error.</span></span>  <span data-ttu-id="89751-439">Para obter melhores resultados, escolha solicitações tooallow não autenticado no hello autenticação do serviço de aplicativo do Azure / configurações de autorização, em seguida, controlar autenticação usando Olá `table.access` propriedade.</span><span class="sxs-lookup"><span data-stu-id="89751-439">For best results, choose tooallow unauthenticated requests through in hello Azure App Service Authentication / Authorization settings, then control authentication using hello `table.access` property.</span></span>

<span data-ttu-id="89751-440">Você também pode adicionar Olá Swagger opção tooyour `azureMobile.js` arquivo se desejar Swagger suporte somente ao desenvolver localmente.</span><span class="sxs-lookup"><span data-stu-id="89751-440">You can also add hello Swagger option tooyour `azureMobile.js` file if you only want Swagger support when developing locally.</span></span>

## <a name="a-namepushpush-notifications"></a><span data-ttu-id="89751-441"><a name="push">Notificações por Push</span><span class="sxs-lookup"><span data-stu-id="89751-441"><a name="push">Push notifications</span></span>
<span data-ttu-id="89751-442">Aplicativos móveis integra tooenable de Hubs de notificação do Azure você toosend direcionado toomillions de notificações por push de dispositivos em todas as plataformas principais.</span><span class="sxs-lookup"><span data-stu-id="89751-442">Mobile Apps integrates with Azure Notification Hubs tooenable you toosend targeted push notifications toomillions of devices across all major platforms.</span></span> <span data-ttu-id="89751-443">Usando Hubs de notificação, você pode enviar por push tooiOS notificações, dispositivos Android e Windows.</span><span class="sxs-lookup"><span data-stu-id="89751-443">By using Notification Hubs, you can send push notifications tooiOS, Android and Windows devices.</span></span> <span data-ttu-id="89751-444">toolearn mais sobre tudo o que você podem fazer com os Hubs de notificação, consulte [visão geral de Hubs de notificação](../notification-hubs/notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="89751-444">toolearn more about all that you can do with Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span></span>

### <span data-ttu-id="89751-445"></a><a name="send-push"></a>Como enviar notificações por push</span><span class="sxs-lookup"><span data-stu-id="89751-445"></a><a name="send-push"></a>How to: Send push notifications</span></span>
<span data-ttu-id="89751-446">saudação de código a seguir mostra como toouse Olá push objeto toosend uma difusão por push a dispositivos de iOS tooregistered notificação:</span><span class="sxs-lookup"><span data-stu-id="89751-446">hello following code shows how toouse hello push object toosend a broadcast push notification tooregistered iOS devices:</span></span>

    // Create an APNS payload.
    var payload = '{"aps": {"alert": "This is an APNS payload."}}';

    // Only do hello push if configured
    if (context.push) {
        // Send a push notification using APNS.
        context.push.apns.send(null, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }

<span data-ttu-id="89751-447">Ao criar um registro de envio por push do modelo de cliente Olá, em vez disso, você pode enviar uma toodevices de mensagem de envio por push do modelo em todas as plataformas com suporte.</span><span class="sxs-lookup"><span data-stu-id="89751-447">By creating a template push registration from hello client, you can instead send a template push message toodevices on all supported platforms.</span></span> <span data-ttu-id="89751-448">Olá mostrado no código a seguir como toosend uma notificação de modelo:</span><span class="sxs-lookup"><span data-stu-id="89751-448">hello following code shows how toosend a template notification:</span></span>

    // Define hello template payload.
    var payload = '{"messageParam": "This is a template payload."}';

    // Only do hello push if configured
    if (context.push) {
        // Send a template notification.
        context.push.send(null, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }


### <span data-ttu-id="89751-449"><a name="push-user"></a>Como: enviar por push notificações tooan autenticado usando marcas de usuário</span><span class="sxs-lookup"><span data-stu-id="89751-449"><a name="push-user"></a>How to: Send push notifications tooan authenticated user using tags</span></span>
<span data-ttu-id="89751-450">Quando um usuário autenticado se registra para notificações de push, uma marca de identificação do usuário é adicionada automaticamente toohello registro.</span><span class="sxs-lookup"><span data-stu-id="89751-450">When an authenticated user registers for push notifications, a user ID tag is automatically added toohello registration.</span></span> <span data-ttu-id="89751-451">Usando essa marca, você pode enviar por push dispositivos de tooall notificações registrados por um usuário específico.</span><span class="sxs-lookup"><span data-stu-id="89751-451">By using this tag, you can send push notifications tooall devices registered by a specific user.</span></span> <span data-ttu-id="89751-452">Olá código a seguir obtém Olá SID do usuário que fez a solicitação de saudação e envia um registro de dispositivo tooevery de notificação do modelo por push para o usuário:</span><span class="sxs-lookup"><span data-stu-id="89751-452">hello following code gets hello SID of user making hello request and sends a template push notification tooevery device registration for that user:</span></span>

    // Only do hello push if configured
    if (context.push) {
        // Send a notification toohello current user.
        context.push.send(context.user.id, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }

<span data-ttu-id="89751-453">Ao se registrar para notificações por push de um cliente autenticado, verifique se a autenticação foi concluída antes de tentar o registro.</span><span class="sxs-lookup"><span data-stu-id="89751-453">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span></span>

## <span data-ttu-id="89751-454"><a name="CustomAPI"></a> APIs personalizadas</span><span class="sxs-lookup"><span data-stu-id="89751-454"><a name="CustomAPI"></a> Custom APIs</span></span>
### <span data-ttu-id="89751-455"><a name="howto-customapi-basic"></a>Como definir uma API personalizada</span><span class="sxs-lookup"><span data-stu-id="89751-455"><a name="howto-customapi-basic"></a>How to: Define a custom API</span></span>
<span data-ttu-id="89751-456">Além disso toohello de acesso a dados API pelo ponto de extremidade de /tables hello, aplicativos móveis do Azure pode fornecer a cobertura de API personalizada.</span><span class="sxs-lookup"><span data-stu-id="89751-456">In addition toohello data access API via hello /tables endpoint, Azure Mobile Apps can provide custom API coverage.</span></span>  <span data-ttu-id="89751-457">APIs personalizadas são definidas em um definições de tabela de toohello de maneira semelhante e pode acessar todos os Olá mesmo recursos, incluindo autenticação.</span><span class="sxs-lookup"><span data-stu-id="89751-457">Custom APIs are defined in a similar way toohello table definitions and can access all hello same facilities, including authentication.</span></span>

<span data-ttu-id="89751-458">Se você quiser toouse autenticação do serviço de aplicativo com uma API personalizada, você deve configurar autenticação do serviço de aplicativo no hello [portal do Azure] primeiro.</span><span class="sxs-lookup"><span data-stu-id="89751-458">If you wish toouse App Service Authentication with a Custom API, you must configure App Service Authentication in hello [Azure portal] first.</span></span>  <span data-ttu-id="89751-459">Para obter mais detalhes sobre como configurar a autenticação em um serviço de aplicativo do Azure, examine Olá guia de configuração para o provedor de identidade Olá pretende toouse:</span><span class="sxs-lookup"><span data-stu-id="89751-459">For more details about configuring authentication in an Azure App Service, review hello Configuration Guide for hello identity provider you intend toouse:</span></span>

* <span data-ttu-id="89751-460">[Como tooconfigure autenticação do Active Directory do Azure]</span><span class="sxs-lookup"><span data-stu-id="89751-460">[How tooconfigure Azure Active Directory Authentication]</span></span>
* <span data-ttu-id="89751-461">[Como tooconfigure autenticação do Facebook]</span><span class="sxs-lookup"><span data-stu-id="89751-461">[How tooconfigure Facebook Authentication]</span></span>
* <span data-ttu-id="89751-462">[Como tooconfigure autenticação do Google]</span><span class="sxs-lookup"><span data-stu-id="89751-462">[How tooconfigure Google Authentication]</span></span>
* <span data-ttu-id="89751-463">[Como tooconfigure Microsoft Authentication]</span><span class="sxs-lookup"><span data-stu-id="89751-463">[How tooconfigure Microsoft Authentication]</span></span>
* <span data-ttu-id="89751-464">[Como tooconfigure autenticação do Twitter]</span><span class="sxs-lookup"><span data-stu-id="89751-464">[How tooconfigure Twitter Authentication]</span></span>

<span data-ttu-id="89751-465">APIs personalizadas são definidas em grande parte Olá mesma maneira que Olá API de tabelas.</span><span class="sxs-lookup"><span data-stu-id="89751-465">Custom APIs are defined in much hello same way as hello Tables API.</span></span>

1. <span data-ttu-id="89751-466">Crie um diretório **api**</span><span class="sxs-lookup"><span data-stu-id="89751-466">Create an **api** directory</span></span>
2. <span data-ttu-id="89751-467">Criar um arquivo de JavaScript da definição de API no hello **api** directory.</span><span class="sxs-lookup"><span data-stu-id="89751-467">Create an API definition JavaScript file in hello **api** directory.</span></span>
3. <span data-ttu-id="89751-468">Use Olá importação método tooimport Olá **api** directory.</span><span class="sxs-lookup"><span data-stu-id="89751-468">Use hello import method tooimport hello **api** directory.</span></span>

<span data-ttu-id="89751-469">Aqui está a definição de api de protótipo Olá com base em amostra de aplicativo basic Olá que usamos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="89751-469">Here is hello prototype api definition based on hello basic-app sample we used earlier.</span></span>

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Import hello Custom API
    mobile.api.import('./api');

    // Add hello mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

<span data-ttu-id="89751-470">Vejamos um exemplo de API que retorna a data de servidor de saudação usando Olá *Date.now()* método.</span><span class="sxs-lookup"><span data-stu-id="89751-470">Let's take an example API that returns hello server date using hello *Date.now()* method.</span></span>  <span data-ttu-id="89751-471">Aqui está o arquivo de api/date.js hello:</span><span class="sxs-lookup"><span data-stu-id="89751-471">Here is hello api/date.js file:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };

    module.exports = api;

<span data-ttu-id="89751-472">Cada parâmetro é uma saudação RESTful verbos padrão - GET, POST, PATCH ou DELETE.</span><span class="sxs-lookup"><span data-stu-id="89751-472">Each parameter is one of hello standard RESTful verbs - GET, POST, PATCH, or DELETE.</span></span>  <span data-ttu-id="89751-473">método Hello é um padrão [ExpressJS Middleware] função que envia saída de hello necessário.</span><span class="sxs-lookup"><span data-stu-id="89751-473">hello method is a standard [ExpressJS Middleware] function that sends hello required output.</span></span>

### <span data-ttu-id="89751-474"><a name="howto-customapi-auth"></a>Como: exigir autenticação de API personalizada do acesso tooa</span><span class="sxs-lookup"><span data-stu-id="89751-474"><a name="howto-customapi-auth"></a>How to: Require authentication for access tooa custom API</span></span>
<span data-ttu-id="89751-475">SDK de aplicativos móveis do Azure implementa a autenticação em Olá mesma forma para o ponto de extremidade do hello tabelas e APIs personalizadas.</span><span class="sxs-lookup"><span data-stu-id="89751-475">Azure Mobile Apps SDK implements authentication in hello same way for both hello tables endpoint and custom APIs.</span></span>  <span data-ttu-id="89751-476">Para adicionar autenticação toohello API desenvolvido na seção anterior hello, adicione um **acesso** propriedade:</span><span class="sxs-lookup"><span data-stu-id="89751-476">To add authentication toohello API developed in hello previous section, add an **access** property:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };
    // All methods must be authenticated.
    api.access = 'authenticated';

    module.exports = api;

<span data-ttu-id="89751-477">Você também pode especificar a autenticação em operações específicas:</span><span class="sxs-lookup"><span data-stu-id="89751-477">You can also specify authentication on specific operations:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        }
    };
    // hello GET methods must be authenticated.
    api.get.access = 'authenticated';

    module.exports = api;

<span data-ttu-id="89751-478">Olá mesmo token que é usado para o ponto de extremidade do hello tabelas deve ser usado para APIs personalizadas que requer autenticação.</span><span class="sxs-lookup"><span data-stu-id="89751-478">hello same token that is used for hello tables endpoint must be used for custom APIs requiring authentication.</span></span>

### <span data-ttu-id="89751-479"><a name="howto-customapi-auth"></a>Como manipular transferências de arquivos grandes</span><span class="sxs-lookup"><span data-stu-id="89751-479"><a name="howto-customapi-auth"></a>How to: Handle large file uploads</span></span>
<span data-ttu-id="89751-480">SDK de aplicativos móveis do Azure usa Olá [corpo analisador middleware](https://github.com/expressjs/body-parser) tooaccept e decodificar o conteúdo do corpo no seu envio.</span><span class="sxs-lookup"><span data-stu-id="89751-480">Azure Mobile Apps SDK uses hello [body-parser middleware](https://github.com/expressjs/body-parser) tooaccept and decode body content in your submission.</span></span>  <span data-ttu-id="89751-481">Você pode pré-configurar carregamentos de arquivo maior do analisador de corpo tooaccept:</span><span class="sxs-lookup"><span data-stu-id="89751-481">You can pre-configure body-parser tooaccept larger file uploads:</span></span>

    var express = require('express'),
        bodyParser = require('body-parser'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Set up large body content handling
    app.use(bodyParser.json({ limit: '50mb' }));
    app.use(bodyParser.urlencoded({ limit: '50mb', extended: true }));

    // Import hello Custom API
    mobile.api.import('./api');

    // Add hello mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

<span data-ttu-id="89751-482">arquivo Hello é codificada antes da transmissão de base 64.</span><span class="sxs-lookup"><span data-stu-id="89751-482">hello file is base-64 encoded before transmission.</span></span>  <span data-ttu-id="89751-483">Isso aumenta o tamanho de saudação do carregamento real hello (e hello, portanto, você deve considerar de tamanho).</span><span class="sxs-lookup"><span data-stu-id="89751-483">This increases hello size of hello actual upload (and hence hello size you must account for).</span></span>

### <span data-ttu-id="89751-484"><a name="howto-customapi-sql"></a>Como executar instruções SQL personalizadas</span><span class="sxs-lookup"><span data-stu-id="89751-484"><a name="howto-customapi-sql"></a>How to: Execute custom SQL statements</span></span>
<span data-ttu-id="89751-485">Olá SDK de aplicativos móveis do Azure permite acesso toohello contexto inteiro por meio do objeto de solicitação hello, permitindo que você tooexecute parametrizadas provedor de dados definidas SQL instruções toohello facilmente:</span><span class="sxs-lookup"><span data-stu-id="89751-485">hello Azure Mobile Apps SDK allows access toohello entire Context through hello request object, allowing you tooexecute parameterized SQL statements toohello defined data provider easily:</span></span>

    var api = {
        get: function (request, response, next) {
            // Check for parameters - if not there, pass on tooa later API call
            if (typeof request.params.completed === 'undefined')
                return next();

            // Define hello query - anything that can be handled by hello mssql
            // driver is allowed.
            var query = {
                sql: 'UPDATE TodoItem SET complete=@completed',
                parameters: [{
                    completed: request.params.completed
                }]
            };

            // Execute hello query.  hello context for Azure Mobile Apps is available through
            // request.azureMobile - hello data object contains hello configured data provider.
            request.azureMobile.data.execute(query)
            .then(function (results) {
                response.json(results);
            });
        }
    };

    api.get.access = 'authenticated';
    module.exports = api;

## <span data-ttu-id="89751-486"><a name="Debugging"></a>Depuração, Tabelas Fáceis e APIs Fáceis</span><span class="sxs-lookup"><span data-stu-id="89751-486"><a name="Debugging"></a>Debugging, Easy Tables, and Easy APIs</span></span>
### <span data-ttu-id="89751-487"><a name="howto-diagnostic-logs"></a>Como depurar, diagnosticar e solucionar problemas dos Aplicativos Móveis do Azure</span><span class="sxs-lookup"><span data-stu-id="89751-487"><a name="howto-diagnostic-logs"></a>How to: Debug, diagnose, and troubleshoot Azure Mobile apps</span></span>
<span data-ttu-id="89751-488">saudação do serviço de aplicativo do Azure fornece vários depuração e solução de problemas técnicas para aplicativos Node. js.</span><span class="sxs-lookup"><span data-stu-id="89751-488">hello Azure App Service provides several debugging and troubleshooting techniques for Node.js applications.</span></span>
<span data-ttu-id="89751-489">Consulte toohello artigos tooget iniciado no seu back-end node. js móvel de solução de problemas a seguir:</span><span class="sxs-lookup"><span data-stu-id="89751-489">Refer toohello following articles tooget started in troubleshooting your Node.js Mobile backend:</span></span>

* <span data-ttu-id="89751-490">[Monitorando um Serviço de Aplicativo do Azure]</span><span class="sxs-lookup"><span data-stu-id="89751-490">[Monitoring an Azure App Service]</span></span>
* <span data-ttu-id="89751-491">[Habilitar o registro em log de diagnósticos no Serviço de Aplicativo do Azure]</span><span class="sxs-lookup"><span data-stu-id="89751-491">[Enable Diagnostic Logging in Azure App Service]</span></span>
* <span data-ttu-id="89751-492">[Solucionar problemas de um Serviço de Aplicativo do Azure no Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="89751-492">[Troubleshoot an Azure App Service in Visual Studio]</span></span>

<span data-ttu-id="89751-493">Aplicativos Node.js têm acesso tooa ampla variedade de ferramentas de log de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="89751-493">Node.js applications have access tooa wide range of diagnostic log tools.</span></span>  <span data-ttu-id="89751-494">Internamente, Olá usa o SDK do Azure Mobile aplicativos Node.js [Winston] para log de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="89751-494">Internally, hello Azure Mobile Apps Node.js SDK uses [Winston] for diagnostic logging.</span></span>  <span data-ttu-id="89751-495">Registro em log é habilitado automaticamente, habilitando o modo de depuração ou por configuração Olá **MS_DebugMode** tootrue de configuração do aplicativo no hello [portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="89751-495">Logging is automatically enabled by enabling debug mode or by setting hello **MS_DebugMode** app setting tootrue in hello [Azure portal].</span></span> <span data-ttu-id="89751-496">Os logs gerados aparecem no hello Logs de diagnóstico em Olá [portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="89751-496">Generated logs appear in hello Diagnostic Logs on hello [Azure portal].</span></span>

### <span data-ttu-id="89751-497"><a name="in-portal-editing"></a><a name="work-easy-tables"></a>Como: trabalhar com tabelas fácil Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="89751-497"><a name="in-portal-editing"></a><a name="work-easy-tables"></a>How to: Work with Easy Tables in hello Azure portal</span></span>
<span data-ttu-id="89751-498">Tabelas fácil no portal de saudação lhe permitem criar e trabalhar com o direito de tabelas no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="89751-498">Easy Tables in hello portal let you create and work with tables right in hello portal.</span></span> <span data-ttu-id="89751-499">Você ainda pode editar operações de tabela usando Olá Editor de aplicativo de serviço.</span><span class="sxs-lookup"><span data-stu-id="89751-499">You can even edit table operations using hello App Service Editor.</span></span>

<span data-ttu-id="89751-500">Quando você clica em **Tabelas fáceis** em suas configurações de site de back-end, você pode adicionar, modificar ou excluir uma tabela.</span><span class="sxs-lookup"><span data-stu-id="89751-500">When you click **Easy tables** in your backend site settings, you can add, modify, or delete a table.</span></span> <span data-ttu-id="89751-501">Você também pode ver os dados na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="89751-501">You can also see data in hello table.</span></span>

![Trabalhar com Tabelas fáceis](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-tables.png)

<span data-ttu-id="89751-503">Olá a comandos a seguir estão disponíveis na barra de comandos Olá para uma tabela:</span><span class="sxs-lookup"><span data-stu-id="89751-503">hello following commands are available on hello command bar for a table:</span></span>

* <span data-ttu-id="89751-504">**Alterar permissões** - modificar Olá permissão de leitura, inserção, atualização e excluir operações na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="89751-504">**Change permissions** - modify hello permission for read, insert, update and delete operations on hello table.</span></span>
  <span data-ttu-id="89751-505">As opções são tooallow o acesso anônimo, autenticação toorequire ou toodisable todos os acessos toohello operação.</span><span class="sxs-lookup"><span data-stu-id="89751-505">Options are tooallow anonymous access, toorequire authentication, or toodisable all access toohello operation.</span></span>
* <span data-ttu-id="89751-506">**Editar script** -arquivo de script hello para tabela Olá é aberto no hello Editor de aplicativo de serviço.</span><span class="sxs-lookup"><span data-stu-id="89751-506">**Edit script** - hello script file for hello table is opened in hello App Service Editor.</span></span>
* <span data-ttu-id="89751-507">**Gerenciar o esquema** - adicionar ou excluir colunas ou alterar o índice da tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="89751-507">**Manage schema** - add or delete columns or change hello table index.</span></span>
* <span data-ttu-id="89751-508">**Limpar tabela** -trunca a uma tabela existente ser excluir todas as linhas de dados, mas deixar o esquema de saudação inalterado.</span><span class="sxs-lookup"><span data-stu-id="89751-508">**Clear table** - truncates an existing table be deleting all data rows but leaving hello schema unchanged.</span></span>
* <span data-ttu-id="89751-509">**Excluir linhas** : exclua linhas individuais de dados.</span><span class="sxs-lookup"><span data-stu-id="89751-509">**Delete rows** - delete individual rows of data.</span></span>
* <span data-ttu-id="89751-510">**Exibir logs de streaming** -conecta você toohello serviço de log para o site de streaming.</span><span class="sxs-lookup"><span data-stu-id="89751-510">**View streaming logs** - connects you toohello streaming log service for your site.</span></span>

### <span data-ttu-id="89751-511"><a name="work-easy-apis"></a>Como: trabalhar com APIs fácil Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="89751-511"><a name="work-easy-apis"></a>How to: Work with Easy APIs in hello Azure portal</span></span>
<span data-ttu-id="89751-512">APIs de fácil no portal de saudação permitem que você criar e trabalhar com o direito APIs personalizado no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="89751-512">Easy APIs in hello portal let you create and work with custom APIs right in hello portal.</span></span> <span data-ttu-id="89751-513">Você pode editar scripts de API usando Olá Editor de aplicativo de serviço.</span><span class="sxs-lookup"><span data-stu-id="89751-513">You can edit API scripts using hello App Service Editor.</span></span>

<span data-ttu-id="89751-514">Quando você clica em **APIs fáceis** em suas configurações de site de back-end, você pode adicionar, modificar ou excluir um ponto de extremidade de API.</span><span class="sxs-lookup"><span data-stu-id="89751-514">When you click **Easy APIs** in your backend site settings, you can add, modify, or delete a custom API endpoint.</span></span>

![Trabalhar com APIs fáceis](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-apis.png)

<span data-ttu-id="89751-516">No portal de hello, alterar permissões de acesso de saudação para uma determinada ação HTTP, editar o arquivo de script hello API no Editor de serviço de aplicativo ou exibir logs de streaming hello.</span><span class="sxs-lookup"><span data-stu-id="89751-516">In hello portal, you can change hello access permissions for a given HTTP action, edit hello API script file in the App Service Editor, or view hello streaming logs.</span></span>

### <span data-ttu-id="89751-517"><a name="online-editor"></a>Como: editar o código no hello Editor de aplicativo de serviço</span><span class="sxs-lookup"><span data-stu-id="89751-517"><a name="online-editor"></a>How to: Edit code in hello App Service Editor</span></span>
<span data-ttu-id="89751-518">Olá portal do Azure permite que você edite seus arquivos de script de back-end node. js em Olá Editor de aplicativo de serviço sem a necessidade de baixar o computador local do hello projeto tooyour.</span><span class="sxs-lookup"><span data-stu-id="89751-518">hello Azure portal lets you edit your Node.js backend script files in hello App Service Editor without having to download hello project tooyour local computer.</span></span> <span data-ttu-id="89751-519">arquivos de script tooedit no editor online hello:</span><span class="sxs-lookup"><span data-stu-id="89751-519">tooedit script files in hello online editor:</span></span>

1. <span data-ttu-id="89751-520">Na folha do back-end de Aplicativo Móvel, clique em **Todas as configurações** > em **Tabelas fáceis** ou **APIs fáceis**, clique em uma tabela ou API e clique em **Editar script**.</span><span class="sxs-lookup"><span data-stu-id="89751-520">In your Mobile App backend blade, click **All settings** > either **Easy tables** or **Easy APIs**, click a table or API, then click **Edit script**.</span></span> <span data-ttu-id="89751-521">arquivo de script Hello é aberto em Olá Editor de aplicativo de serviço.</span><span class="sxs-lookup"><span data-stu-id="89751-521">hello script file is opened in hello App Service Editor.</span></span>

    ![Editor de Serviço de Aplicativo](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-visual-studio-editor.png)
2. <span data-ttu-id="89751-523">Verifique o arquivo de código toohello alterações no editor online hello.</span><span class="sxs-lookup"><span data-stu-id="89751-523">Make your changes toohello code file in hello online editor.</span></span> <span data-ttu-id="89751-524">As alterações são salvas automaticamente enquanto você digita.</span><span class="sxs-lookup"><span data-stu-id="89751-524">Changes are saved automatically as you type.</span></span>

<!-- Images -->
[0]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/npm-init.png
[1]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-new-project.png
[2]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-install-npm.png
[3]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-config.png
[4]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-authconfig.png
[5]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-newuser-1.png
[6]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/dotnet-backend-create-db.png

<!-- URLs -->
[Início rápido do cliente Android]: app-service-mobile-android-get-started.md
[Início rápido do cliente Apache Cordova]: app-service-mobile-cordova-get-started.md
[Início rápido do cliente iOS]: app-service-mobile-ios-get-started.md
[Início rápido do cliente Xamarin.iOS]: app-service-mobile-xamarin-ios-get-started.md
[Início rápido do cliente Xamarin.Android]: app-service-mobile-xamarin-android-get-started.md
[Início rápido do cliente Xamarin.Forms]: app-service-mobile-xamarin-forms-get-started.md
[Início rápido de cliente Windows Store]: app-service-mobile-windows-store-dotnet-get-started.md
[HTML/Javascript Client QuickStart]: app-service-html-get-started.md
[a sincronização de dados offline]: app-service-mobile-offline-data-sync.md
[Como tooconfigure autenticação do Active Directory do Azure]: app-service-mobile-how-to-configure-active-directory-authentication.md
[Como tooconfigure autenticação do Facebook]: app-service-mobile-how-to-configure-facebook-authentication.md
[Como tooconfigure autenticação do Google]: app-service-mobile-how-to-configure-google-authentication.md
[Como tooconfigure Microsoft Authentication]: app-service-mobile-how-to-configure-microsoft-authentication.md
[Como tooconfigure autenticação do Twitter]: app-service-mobile-how-to-configure-twitter-authentication.md
[Guia de implantação do Serviço de Aplicativo do Azure]: ../app-service-web/web-sites-deploy.md
[Monitorando um Serviço de Aplicativo do Azure]: ../app-service-web/web-sites-monitor.md
[Habilitar o registro em log de diagnósticos no Serviço de Aplicativo do Azure]: ../app-service-web/web-sites-enable-diagnostic-log.md
[Solucionar problemas de um Serviço de Aplicativo do Azure no Visual Studio]: ../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md
[especificar Olá versão do nó]: ../nodejs-specify-node-version-azure-apps.md
[usar módulos de nó]: ../nodejs-use-node-modules-azure-apps.md
[Create a new Azure App Service]: ../app-service-web/
[azure-mobile-apps]: https://www.npmjs.com/package/azure-mobile-apps
[Express]: http://expressjs.com/
[Swagger]: http://swagger.io/

[portal do Azure]: https://portal.azure.com/
[OData]: http://www.odata.org
[promessa]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[basicapp exemplo no GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app
[exemplo todo no GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo
[diretório de exemplos no GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
[QueryJS]: https://github.com/Azure/queryjs
[Node. js Tools 1.1 para Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1
[mssql Node. js pacote]: https://www.npmjs.com/package/mssql
[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx
[ExpressJS Middleware]: http://expressjs.com/guide/using-middleware.html
[Winston]: https://github.com/winstonjs/winston
