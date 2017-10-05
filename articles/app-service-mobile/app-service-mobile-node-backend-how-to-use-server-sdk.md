---
title: "Como trabalhar com o SDK de servidor back-end do Node.js para Aplicativos Móveis | Microsoft Docs"
description: "Aprenda a trabalhar com o SDK do servidor back-end do Node.js para Aplicativos Móveis do Serviço de Aplicativo do Azure."
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
ms.openlocfilehash: 1d3aa7a0089279a8eafeb0ded951a5238e189eaa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-the-azure-mobile-apps-nodejs-sdk"></a><span data-ttu-id="031e1-103">Como usar o SDK do Node.js para Aplicativos Móveis do Azure</span><span class="sxs-lookup"><span data-stu-id="031e1-103">How to use the Azure Mobile Apps Node.js SDK</span></span>
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

<span data-ttu-id="031e1-104">Este artigo fornece informações detalhadas e exemplos de como trabalhar com um back-end de Node.js nos Aplicativos Móveis do Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="031e1-104">This article provides detailed information and examples showing how to work with a Node.js backend in Azure App Service Mobile Apps.</span></span>

## <span data-ttu-id="031e1-105"><a name="Introduction"></a>Introdução</span><span class="sxs-lookup"><span data-stu-id="031e1-105"><a name="Introduction"></a>Introduction</span></span>
<span data-ttu-id="031e1-106">Os Aplicativos Móveis do Serviço de Aplicativo do Azure fornece a capacidade de adicionar uma API Web de acesso a dados otimizada para mobilidade a um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="031e1-106">Azure App Service Mobile Apps provides the capability to add a mobile-optimized data access Web API to a web application.</span></span>  <span data-ttu-id="031e1-107">O SDK de Aplicativos Móveis do Serviço de Aplicativo do Azure é fornecido para aplicativos Web ASP.NET e Node.js.</span><span class="sxs-lookup"><span data-stu-id="031e1-107">The Azure App Service Mobile Apps SDK is provided for ASP.NET and Node.js web applications.</span></span>  <span data-ttu-id="031e1-108">O SDK oferece as seguintes operações:</span><span class="sxs-lookup"><span data-stu-id="031e1-108">The SDK provides the following operations:</span></span>

* <span data-ttu-id="031e1-109">Operações de tabela (Ler, Inserir, Atualizar Excluir) para acesso a dados</span><span class="sxs-lookup"><span data-stu-id="031e1-109">Table operations (Read, Insert, Update, Delete) for data access</span></span>
* <span data-ttu-id="031e1-110">Operações de API personalizadas</span><span class="sxs-lookup"><span data-stu-id="031e1-110">Custom API operations</span></span>

<span data-ttu-id="031e1-111">Ambas as operações permitem a autenticação em todos os provedores de identidade permitidos pelo Serviço de Aplicativo do Azure, incluindo provedores de identidade social como Facebook, Twitter, Google e Microsoft, além do Active Directory do Azure para a identidade corporativa.</span><span class="sxs-lookup"><span data-stu-id="031e1-111">Both operations provide for authentication across all identity providers allowed by Azure App Service, including social identity providers such as Facebook, Twitter, Google and Microsoft as well as Azure Active Directory for enterprise identity.</span></span>

<span data-ttu-id="031e1-112">Você pode encontrar exemplos para cada caso de uso no [diretório de exemplos no GitHub].</span><span class="sxs-lookup"><span data-stu-id="031e1-112">You can find samples for each use case in the [samples directory on GitHub].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="031e1-113">Plataformas com suporte</span><span class="sxs-lookup"><span data-stu-id="031e1-113">Supported Platforms</span></span>
<span data-ttu-id="031e1-114">O SDK de Node para Aplicativos Móveis do Azure dá suporte à versão atual de LTS do Node e posterior.</span><span class="sxs-lookup"><span data-stu-id="031e1-114">The Azure Mobile Apps Node SDK supports the current LTS release of Node and later.</span></span>  <span data-ttu-id="031e1-115">Até o momento, a versão mais recente do LTS é Node v4.5.0.</span><span class="sxs-lookup"><span data-stu-id="031e1-115">As of writing, the latest LTS version is Node v4.5.0.</span></span>  <span data-ttu-id="031e1-116">Outras versões do Node podem funcionar, mas não são têm suporte.</span><span class="sxs-lookup"><span data-stu-id="031e1-116">Other versions of Node may work, but are not supported.</span></span>

<span data-ttu-id="031e1-117">O SDK do Node para Aplicativos Móveis do Azure dá suporte a dois drivers de banco de dados: o driver de node-mssql dá suporte ao SQL Azure e às instâncias do SQL Server locais.</span><span class="sxs-lookup"><span data-stu-id="031e1-117">The Azure Mobile Apps Node SDK supports two database drivers - the node-mssql driver supports SQL Azure and local SQL Server instances.</span></span>  <span data-ttu-id="031e1-118">O driver sqlite3 dá suporte a bancos de dados SQLite somente em uma instância única.</span><span class="sxs-lookup"><span data-stu-id="031e1-118">The sqlite3 driver supports SQLite databases on a single instance only.</span></span>

### <span data-ttu-id="031e1-119"><a name="howto-cmdline-basicapp"></a>Como criar um back-end de Node.js básico usando a linha de comando</span><span class="sxs-lookup"><span data-stu-id="031e1-119"><a name="howto-cmdline-basicapp"></a>How to: Create a Basic Node.js backend using the Command Line</span></span>
<span data-ttu-id="031e1-120">Cada back-end de Node.js do Aplicativo Móvel do Serviço de Aplicativo do Azure inicia como um aplicativo ExpressJS.</span><span class="sxs-lookup"><span data-stu-id="031e1-120">Every Azure App Service Mobile App Node.js backend starts as an ExpressJS application.</span></span>  <span data-ttu-id="031e1-121">ExpressJS é a estrutura de serviços Web mais popular disponível para o Node.js.</span><span class="sxs-lookup"><span data-stu-id="031e1-121">ExpressJS is the most popular web service framework available for Node.js.</span></span>  <span data-ttu-id="031e1-122">Você pode criar um aplicativo [Express] básico da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="031e1-122">You can create a basic [Express] application as follows:</span></span>

1. <span data-ttu-id="031e1-123">Em um comando ou a janela do PowerShell, crie um diretório para seu projeto.</span><span class="sxs-lookup"><span data-stu-id="031e1-123">In a command or PowerShell window, create a directory for your project.</span></span>

        mkdir basicapp
2. <span data-ttu-id="031e1-124">Execute o npm init para inicializar a estrutura do pacote.</span><span class="sxs-lookup"><span data-stu-id="031e1-124">Run npm init to initialize the package structure.</span></span>

        cd basicapp
        npm init

    <span data-ttu-id="031e1-125">O comando init npm solicita um conjunto de perguntas para inicializar o projeto.</span><span class="sxs-lookup"><span data-stu-id="031e1-125">The npm init command asks a set of questions to initialize the project.</span></span>  <span data-ttu-id="031e1-126">Confira a saída de exemplo:</span><span class="sxs-lookup"><span data-stu-id="031e1-126">See the example output:</span></span>

    ![A saída de init npm][0]
3. <span data-ttu-id="031e1-128">Instale as bibliotecas express e azure-mobile-apps do repositório npm.</span><span class="sxs-lookup"><span data-stu-id="031e1-128">Install the express and azure-mobile-apps libraries from the npm repository.</span></span>

        npm install --save express azure-mobile-apps
4. <span data-ttu-id="031e1-129">Crie um arquivo app.js para implementar o servidor móvel básico.</span><span class="sxs-lookup"><span data-stu-id="031e1-129">Create an app.js file to implement the basic mobile server.</span></span>

        var express = require('express'),
            azureMobileApps = require('azure-mobile-apps');

        var app = express(),
            mobile = azureMobileApps();

        // Define a TodoItem table
        mobile.tables.add('TodoItem');

        // Add the mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);

<span data-ttu-id="031e1-130">Esse aplicativo cria uma API Web otimizada para celular com um único ponto de extremidade, (`/tables/TodoItem`) que fornece acesso não autenticado a um armazenamento de dados SQL subjacente usando um esquema dinâmico.</span><span class="sxs-lookup"><span data-stu-id="031e1-130">This application creates a mobile-optimized WebAPI with a single endpoint (`/tables/TodoItem`) that provides unauthenticated access to an underlying SQL data store using a dynamic schema.</span></span>  <span data-ttu-id="031e1-131">Ele é adequado para os seguintes inícios rápidos de biblioteca de cliente:</span><span class="sxs-lookup"><span data-stu-id="031e1-131">It is suitable for following the client library quick starts:</span></span>

* <span data-ttu-id="031e1-132">[Início rápido do cliente Android]</span><span class="sxs-lookup"><span data-stu-id="031e1-132">[Android Client QuickStart]</span></span>
* <span data-ttu-id="031e1-133">[Início rápido do cliente Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="031e1-133">[Apache Cordova Client QuickStart]</span></span>
* <span data-ttu-id="031e1-134">[Início rápido do cliente iOS]</span><span class="sxs-lookup"><span data-stu-id="031e1-134">[iOS Client QuickStart]</span></span>
* <span data-ttu-id="031e1-135">[Início rápido de cliente Windows Store]</span><span class="sxs-lookup"><span data-stu-id="031e1-135">[Windows Store Client QuickStart]</span></span>
* <span data-ttu-id="031e1-136">[Início rápido do cliente Xamarin.iOS]</span><span class="sxs-lookup"><span data-stu-id="031e1-136">[Xamarin.iOS Client QuickStart]</span></span>
* <span data-ttu-id="031e1-137">[Início rápido do cliente Xamarin.Android]</span><span class="sxs-lookup"><span data-stu-id="031e1-137">[Xamarin.Android Client QuickStart]</span></span>
* <span data-ttu-id="031e1-138">[Início rápido do cliente Xamarin.Forms]</span><span class="sxs-lookup"><span data-stu-id="031e1-138">[Xamarin.Forms Client QuickStart]</span></span>

<span data-ttu-id="031e1-139">Você pode encontrar o código para esse aplicativo básico no [exemplo de aplicativo básico no GitHub].</span><span class="sxs-lookup"><span data-stu-id="031e1-139">You can find the code for this basic application in the [basicapp sample on GitHub].</span></span>

### <span data-ttu-id="031e1-140"><a name="howto-vs2015-basicapp"></a>Como criar um back-end de nó com o Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="031e1-140"><a name="howto-vs2015-basicapp"></a>How to: Create a Node backend with Visual Studio 2015</span></span>
<span data-ttu-id="031e1-141">O Visual Studio 2015 exige uma extensão para desenvolver aplicativos Node.js no IDE.</span><span class="sxs-lookup"><span data-stu-id="031e1-141">Visual Studio 2015 requires an extension to develop Node.js applications within the IDE.</span></span>  <span data-ttu-id="031e1-142">Para começar, instale as [Ferramentas do Node.js 1.1 para Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="031e1-142">To start, install the [Node.js Tools 1.1 for Visual Studio].</span></span>  <span data-ttu-id="031e1-143">Depois que as ferramentas do Node.js para o Visual Studio estiverem instaladas, crie um aplicativo Express 4.x:</span><span class="sxs-lookup"><span data-stu-id="031e1-143">Once the Node.js Tools for Visual Studio are installed, create an Express 4.x application:</span></span>

1. <span data-ttu-id="031e1-144">Abra a caixa de diálogo **Novo Projeto** (de **Arquivo** > **Novo** > **Projeto...**).</span><span class="sxs-lookup"><span data-stu-id="031e1-144">Open the **New Project** dialog (from **File** > **New** > **Project...**).</span></span>
2. <span data-ttu-id="031e1-145">Expanda **Modelos** > **JavaScript** > **Node. js**.</span><span class="sxs-lookup"><span data-stu-id="031e1-145">Expand **Templates** > **JavaScript** > **Node.js**.</span></span>
3. <span data-ttu-id="031e1-146">Selecione o **Aplicativo básico do Azure Node.js Express 4**.</span><span class="sxs-lookup"><span data-stu-id="031e1-146">Select the **Basic Azure Node.js Express 4 Application**.</span></span>
4. <span data-ttu-id="031e1-147">Preencha o nome do projeto.</span><span class="sxs-lookup"><span data-stu-id="031e1-147">Fill in the project name.</span></span>  <span data-ttu-id="031e1-148">Clique em *OK*.</span><span class="sxs-lookup"><span data-stu-id="031e1-148">Click *OK*.</span></span>

    ![Novo projeto do Visual Studio 2015][1]
5. <span data-ttu-id="031e1-150">Clique com o botão direito do mouse no nó **npm** e selecione **Instalar Novos pacotes de npm...**.</span><span class="sxs-lookup"><span data-stu-id="031e1-150">Right-click the **npm** node and select **Install New npm packages...**.</span></span>
6. <span data-ttu-id="031e1-151">Talvez você precise atualizar o catálogo npm quando criar seu primeiro aplicativo do Node.js.</span><span class="sxs-lookup"><span data-stu-id="031e1-151">You may need to refresh the npm catalog on creating your first Node.js application.</span></span>  <span data-ttu-id="031e1-152">Clique em **Atualizar** , se necessário.</span><span class="sxs-lookup"><span data-stu-id="031e1-152">Click **Refresh** if necessary.</span></span>
7. <span data-ttu-id="031e1-153">Digite *azure-mobile-apps* na caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="031e1-153">Enter *azure-mobile-apps* in the search box.</span></span>  <span data-ttu-id="031e1-154">Clique no pacote **azure-mobile-apps 2.0.0** e clique em **Instalar Pacote**.</span><span class="sxs-lookup"><span data-stu-id="031e1-154">Click the **azure-mobile-apps 2.0.0** package, then click **Install Package**.</span></span>

    ![Instalar novos pacotes npm][2]
8. <span data-ttu-id="031e1-156">Clique em **fechar**</span><span class="sxs-lookup"><span data-stu-id="031e1-156">Click **Close**.</span></span>
9. <span data-ttu-id="031e1-157">Abra o arquivo *app.js* para adicionar suporte ao SDK de Aplicativos Móveis do Azure.</span><span class="sxs-lookup"><span data-stu-id="031e1-157">Open the *app.js* file to add support for the Azure Mobile Apps SDK.</span></span>  <span data-ttu-id="031e1-158">Na linha 6, na parte inferior das exigências de declarações da biblioteca, adicione o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="031e1-158">At line 6 at the bottom of the library require statements, add the following code:</span></span>

        var bodyParser = require('body-parser');
        var azureMobileApps = require('azure-mobile-apps');

    <span data-ttu-id="031e1-159">Aproximadamente na linha 27, após outras instruções app.use, adicione o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="031e1-159">At approximately line 27 after the other app.use statements, add the following code:</span></span>

        app.use('/users', users);

        // Azure Mobile Apps Initialization
        var mobile = azureMobileApps();
        mobile.tables.add('TodoItem');
        app.use(mobile);

    <span data-ttu-id="031e1-160">Salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="031e1-160">Save the file.</span></span>
10. <span data-ttu-id="031e1-161">Execute o aplicativo localmente (a API é fornecida em http://localhost:3000) ou publique no Azure.</span><span class="sxs-lookup"><span data-stu-id="031e1-161">Either run the application locally (the API is served on http://localhost:3000) or publish to Azure.</span></span>

### <span data-ttu-id="031e1-162"><a name="create-node-backend-portal"></a>Como criar um back-end do Node.js usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="031e1-162"><a name="create-node-backend-portal"></a>How to: Create a Node.js backend using the Azure portal</span></span>
<span data-ttu-id="031e1-163">Você pode criar um back-end de aplicativo móvel diretamente no [portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="031e1-163">You can create a Mobile App backend right in the [Azure portal].</span></span> <span data-ttu-id="031e1-164">Você pode seguir as etapas a seguir ou criar um cliente e um servidor juntos acompanhando o tutorial [Criar um aplicativo móvel](app-service-mobile-ios-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="031e1-164">You can either follow the following steps or create a client and server together by following the [Create a mobile app](app-service-mobile-ios-get-started.md) tutorial.</span></span> <span data-ttu-id="031e1-165">O tutorial contém uma versão simplificada dessas instruções e funciona melhor para projetos de prova de conceito.</span><span class="sxs-lookup"><span data-stu-id="031e1-165">The tutorial contains a simplified version of these instructions and is best for proof of concept projects.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

<span data-ttu-id="031e1-166">De volta à folha *Introdução*, em **Criar uma API de tabela**, escolha **Node.js** como a **Linguagem de back-end**.</span><span class="sxs-lookup"><span data-stu-id="031e1-166">Back in the *Get started* blade, under **Create a table API**, choose **Node.js** as your **Backend language**.</span></span>
<span data-ttu-id="031e1-167">Marque a caixa que diz "**Estou ciente de que isso substituirá todo o conteúdo do site.**" e clique em **Criar tabela TodoItem**.</span><span class="sxs-lookup"><span data-stu-id="031e1-167">Check the box for "**I acknowledge that this will overwrite all site contents.**", then click **Create TodoItem table**.</span></span>

### <span data-ttu-id="031e1-168"><a name="download-quickstart"></a>Como baixar o projeto de código de início rápido do back-end de Node.js usando Git</span><span class="sxs-lookup"><span data-stu-id="031e1-168"><a name="download-quickstart"></a>How to: Download the Node.js backend quickstart code project using Git</span></span>
<span data-ttu-id="031e1-169">Quando você cria um back-end de Aplicativo Móvel do Node.js usando a folha **Início Rápido** no portal, um projeto do Node.js é criado e implantado em seu site.</span><span class="sxs-lookup"><span data-stu-id="031e1-169">When you create a Node.js Mobile App backend by using the portal **Quick start** blade, a Node.js project is created for you and deployed to your site.</span></span> <span data-ttu-id="031e1-170">Você pode adicionar tabelas e APIs e editar arquivos de código para o back-end de Node.js no portal.</span><span class="sxs-lookup"><span data-stu-id="031e1-170">You can add tables and APIs and edit code files for the Node.js backend in the portal.</span></span> <span data-ttu-id="031e1-171">Você também pode usar várias ferramentas de implantação a fim de baixar o projeto de back-end e adicionar ou modificar tabelas e APIs, e publicar novamente o projeto.</span><span class="sxs-lookup"><span data-stu-id="031e1-171">You can also use various deployment tools to download the backend project so that you can add or modify tables and APIs, then republish the project.</span></span> <span data-ttu-id="031e1-172">Para saber mais, confira o [Guia de implantação do Serviço de Aplicativo do Azure].</span><span class="sxs-lookup"><span data-stu-id="031e1-172">For more information, see the [Azure App Service Deployment Guide].</span></span> <span data-ttu-id="031e1-173">o procedimento a seguir usa um repositório Git para baixar o código de projeto de início rápido.</span><span class="sxs-lookup"><span data-stu-id="031e1-173">the following procedure uses a Git repository to download the quickstart project code.</span></span>

1. <span data-ttu-id="031e1-174">Instale o Git, caso ainda não tenha feito isso.</span><span class="sxs-lookup"><span data-stu-id="031e1-174">Install Git, if you haven't already done so.</span></span> <span data-ttu-id="031e1-175">As etapas necessárias para instalar o Git variam de acordo com o sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="031e1-175">The steps required to install Git vary between operating systems.</span></span> <span data-ttu-id="031e1-176">Consulte [Instalando o Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) para distribuições específicas de sistemas operacionais e orientações de instalação.</span><span class="sxs-lookup"><span data-stu-id="031e1-176">See [Installing Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) for operating system-specific distributions and installation guidance.</span></span>
2. <span data-ttu-id="031e1-177">Siga as etapas em [Habilitar o repositório de aplicativos do Serviço de Aplicativo](../app-service-web/app-service-deploy-local-git.md#Step3) para habilitar o repositório Git para seu site de back-end, anotando o nome de usuário e a senha de implantação.</span><span class="sxs-lookup"><span data-stu-id="031e1-177">Follow the steps in [Enable the App Service app repository](../app-service-web/app-service-deploy-local-git.md#Step3) to enable the Git repository for your backend site, making a note of the deployment username and password.</span></span>
3. <span data-ttu-id="031e1-178">Na folha de seu back-end do Aplicativo Móvel, anote a configuração de **URL de clone de Git** .</span><span class="sxs-lookup"><span data-stu-id="031e1-178">In the blade for your Mobile App backend, make a note of the **Git clone URL** setting.</span></span>
4. <span data-ttu-id="031e1-179">Execute o comando `git clone` usando a URL de clone de Git, digitando a senha quando for necessário, como no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="031e1-179">Execute the `git clone` command using the Git clone URL, entering your password when required, as in the following example:</span></span>

        $ git clone https://username@todolist.scm.azurewebsites.net:443/todolist.git
5. <span data-ttu-id="031e1-180">Navegue até o diretório local, que no exemplo anterior é /todolist, e veja se os arquivos do projeto foram baixados.</span><span class="sxs-lookup"><span data-stu-id="031e1-180">Browse to local directory, which in the preceding example is /todolist, and notice that project files have been downloaded.</span></span> <span data-ttu-id="031e1-181">Localize o arquivo `todoitem.json` no diretório `/tables`.</span><span class="sxs-lookup"><span data-stu-id="031e1-181">Locate the `todoitem.json` file in the `/tables` directory.</span></span>  <span data-ttu-id="031e1-182">Esse arquivo define as permissões na tabela.</span><span class="sxs-lookup"><span data-stu-id="031e1-182">This file defines permissions on the table.</span></span>  <span data-ttu-id="031e1-183">Encontre também o arquivo `todoitem.js` no mesmo diretório, que define os scripts de operação CRUD para a tabela.</span><span class="sxs-lookup"><span data-stu-id="031e1-183">Also find the `todoitem.js` file in the same directory, which defines that CRUD operation scripts for the table.</span></span>
6. <span data-ttu-id="031e1-184">Depois de fazer as alterações nos arquivos do projeto, execute os seguintes comandos para adicionar, confirmar e carregar as alterações no site:</span><span class="sxs-lookup"><span data-stu-id="031e1-184">After you have made changes to project files, execute the following commands to add, commit, then upload the changes to the site:</span></span>

        $ git commit -m "updated the table script"
        $ git push origin master

    <span data-ttu-id="031e1-185">Ao adicionar novos arquivos ao projeto, primeiro você precisa executar o comando `git add .`.</span><span class="sxs-lookup"><span data-stu-id="031e1-185">When you add new files to the project, you first need to execute the `git add .` command.</span></span>

<span data-ttu-id="031e1-186">O site é publicado novamente sempre que um novo conjunto de confirmações é enviado ao site.</span><span class="sxs-lookup"><span data-stu-id="031e1-186">The site is republished every time a new set of commits is pushed to the site.</span></span>

### <span data-ttu-id="031e1-187"><a name="howto-publish-to-azure"></a>Como publicar seu back-end de Node.js no Azure</span><span class="sxs-lookup"><span data-stu-id="031e1-187"><a name="howto-publish-to-azure"></a>How to: Publish your Node.js backend to Azure</span></span>
<span data-ttu-id="031e1-188">O Microsoft Azure fornece vários mecanismos de publicação de back-end de Node.js dos Aplicativos Móveis do Serviço de Aplicativo do Azure no serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="031e1-188">Microsoft Azure provides many mechanisms for publishing your Azure App Service Mobile Apps Node.js backend to the Azure service.</span></span>  <span data-ttu-id="031e1-189">Eles incluem a utilização das ferramentas de implantação integradas ao Visual Studio, das ferramentas de linha de comando e das opções de implantação contínua com base no controle de origem.</span><span class="sxs-lookup"><span data-stu-id="031e1-189">These include utilizing deployment tools integrated into Visual Studio, command-line tools, and continuous deployment options based on source control.</span></span>  <span data-ttu-id="031e1-190">Para saber mais sobre esse tópico, confira o [Guia de implantação do Serviço de Aplicativo do Azure].</span><span class="sxs-lookup"><span data-stu-id="031e1-190">For more information on this topic, see the [Azure App Service Deployment Guide].</span></span>

<span data-ttu-id="031e1-191">O Serviço de Aplicativo do Azure tem recomendações específicas para aplicativo Node.js que você deve examinar antes de implantar:</span><span class="sxs-lookup"><span data-stu-id="031e1-191">Azure App Service has specific advice for Node.js application that you should review before deploying:</span></span>

* <span data-ttu-id="031e1-192">Como [especificar a versão do Node]</span><span class="sxs-lookup"><span data-stu-id="031e1-192">How to [specify the Node Version]</span></span>
* <span data-ttu-id="031e1-193">Como [usar módulos do Node]</span><span class="sxs-lookup"><span data-stu-id="031e1-193">How to [use Node modules]</span></span>

### <span data-ttu-id="031e1-194"><a name="howto-enable-homepage"></a>Como habilitar uma home page para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="031e1-194"><a name="howto-enable-homepage"></a>How to: Enable a Home Page for your application</span></span>
<span data-ttu-id="031e1-195">Muitos aplicativos são uma combinação de aplicativos Web e móveis, e a estrutura do ExpressJS permite a combinação das duas facetas.</span><span class="sxs-lookup"><span data-stu-id="031e1-195">Many applications are a combination of web and mobile apps and the ExpressJS framework allows you to combine the two facets.</span></span>  <span data-ttu-id="031e1-196">Às vezes, no entanto, talvez você queira implementar apenas uma interface móvel.</span><span class="sxs-lookup"><span data-stu-id="031e1-196">Sometimes, however, you may wish to only implement a mobile interface.</span></span>  <span data-ttu-id="031e1-197">É útil fornecer uma página de aterrissagem para garantir que o serviço de aplicativo esteja em execução.</span><span class="sxs-lookup"><span data-stu-id="031e1-197">It is useful to provide a landing page to ensure the app service is up and running.</span></span>  <span data-ttu-id="031e1-198">Você pode fornecer sua própria home page ou habilitar uma home page temporária.</span><span class="sxs-lookup"><span data-stu-id="031e1-198">You can either provide your own home page or enable a temporary home page.</span></span>  <span data-ttu-id="031e1-199">Para habilitar uma home page temporária, use o seguinte para criar instância dos Aplicativos Móveis do Azure:</span><span class="sxs-lookup"><span data-stu-id="031e1-199">To enable a temporary home page, use the following to instantiate Azure Mobile Apps:</span></span>

    var mobile = azureMobileApps({ homePage: true });

<span data-ttu-id="031e1-200">Se quiser que essa opção fique disponível apenas durante o desenvolvimento local, você pode adicionar essa configuração ao seu arquivo `azureMobile.js` .</span><span class="sxs-lookup"><span data-stu-id="031e1-200">If you only want this option available when developing locally, you can add this setting to your `azureMobile.js` file.</span></span>

## <span data-ttu-id="031e1-201"><a name="TableOperations"></a>Operações de tabela</span><span class="sxs-lookup"><span data-stu-id="031e1-201"><a name="TableOperations"></a>Table operations</span></span>
<span data-ttu-id="031e1-202">O SDK do servidor de Node.js do azure-mobile-apps fornece mecanismos para expor tabelas de dados armazenadas no Banco de Dados SQL do Azure como uma API Web.</span><span class="sxs-lookup"><span data-stu-id="031e1-202">The azure-mobile-apps Node.js Server SDK provides mechanisms to expose data tables stored in Azure SQL Database as a WebAPI.</span></span>  <span data-ttu-id="031e1-203">Cinco operações são fornecidas.</span><span class="sxs-lookup"><span data-stu-id="031e1-203">Five operations are provided.</span></span>

| <span data-ttu-id="031e1-204">Operação</span><span class="sxs-lookup"><span data-stu-id="031e1-204">Operation</span></span> | <span data-ttu-id="031e1-205">Descrição</span><span class="sxs-lookup"><span data-stu-id="031e1-205">Description</span></span> |
| --- | --- |
| <span data-ttu-id="031e1-206">GET /tables/*tablename*</span><span class="sxs-lookup"><span data-stu-id="031e1-206">GET /tables/*tablename*</span></span> |<span data-ttu-id="031e1-207">Obter todos os registros na tabela</span><span class="sxs-lookup"><span data-stu-id="031e1-207">Get all records in the table</span></span> |
| <span data-ttu-id="031e1-208">GET /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="031e1-208">GET /tables/*tablename*/:id</span></span> |<span data-ttu-id="031e1-209">Obter um registro específico na tabela</span><span class="sxs-lookup"><span data-stu-id="031e1-209">Get a specific record in the table</span></span> |
| <span data-ttu-id="031e1-210">POST /tables/*tablename*</span><span class="sxs-lookup"><span data-stu-id="031e1-210">POST /tables/*tablename*</span></span> |<span data-ttu-id="031e1-211">Criar um registro na tabela</span><span class="sxs-lookup"><span data-stu-id="031e1-211">Create a record in the table</span></span> |
| <span data-ttu-id="031e1-212">PATCH /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="031e1-212">PATCH /tables/*tablename*/:id</span></span> |<span data-ttu-id="031e1-213">Atualizar um registro na tabela</span><span class="sxs-lookup"><span data-stu-id="031e1-213">Update a record in the table</span></span> |
| <span data-ttu-id="031e1-214">DELETE /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="031e1-214">DELETE /tables/*tablename*/:id</span></span> |<span data-ttu-id="031e1-215">Excluir um registro na tabela</span><span class="sxs-lookup"><span data-stu-id="031e1-215">Delete a record in the table</span></span> |

<span data-ttu-id="031e1-216">Essa WebAPI dá suporte a [OData] e estende o esquema da tabela para dar suporte à [sincronização de dados offline].</span><span class="sxs-lookup"><span data-stu-id="031e1-216">This WebAPI supports [OData] and extends the table schema to support [offline data sync].</span></span>

### <span data-ttu-id="031e1-217"><a name="howto-dynamicschema"></a>Como definir tabelas usando um esquema dinâmico</span><span class="sxs-lookup"><span data-stu-id="031e1-217"><a name="howto-dynamicschema"></a>How to: Define tables using a dynamic schema</span></span>
<span data-ttu-id="031e1-218">Antes de poder usar uma tabela, ela deve ser definida.</span><span class="sxs-lookup"><span data-stu-id="031e1-218">Before a table can be used, it must be defined.</span></span>  <span data-ttu-id="031e1-219">As tabelas podem ser definidas com um esquema estático (quando o desenvolvedor define as colunas no esquema) ou dinamicamente (quando o SDK controla o esquema com base em solicitações de entrada).</span><span class="sxs-lookup"><span data-stu-id="031e1-219">Tables can be defined with a static schema (where the developer defines the columns within the schema) or dynamically (where the SDK controls the schema based on incoming requests).</span></span> <span data-ttu-id="031e1-220">Além disso, o desenvolvedor pode controlar aspectos específicos da API Web adicionando código Javascript à definição.</span><span class="sxs-lookup"><span data-stu-id="031e1-220">In addition, the developer can control specific aspects of the WebAPI by adding Javascript code to the definition.</span></span>

<span data-ttu-id="031e1-221">Como uma prática recomendada, você deve definir cada tabela em um arquivo Javascript no diretório de tabelas e usar o método tables.import() para importar as tabelas.</span><span class="sxs-lookup"><span data-stu-id="031e1-221">As a best practice, you should define each table in a Javascript file in the tables directory, then use the tables.import() method to import the tables.</span></span>  <span data-ttu-id="031e1-222">Estendendo o basic-app, o arquivo app.js seria ajustado:</span><span class="sxs-lookup"><span data-stu-id="031e1-222">Extending the basic-app, the app.js file would be adjusted:</span></span>

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Define the database schema that is exposed
    mobile.tables.import('./tables');

    // Provide initialization of any tables that are statically defined
    mobile.tables.initialize().then(function () {
        // Add the mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);
    });

<span data-ttu-id="031e1-223">Definir a tabela em. /tables/TodoItem.js:</span><span class="sxs-lookup"><span data-stu-id="031e1-223">Define the table in ./tables/TodoItem.js:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Additional configuration for the table goes here

    module.exports = table;

<span data-ttu-id="031e1-224">As tabelas usam o esquema dinâmico por padrão.</span><span class="sxs-lookup"><span data-stu-id="031e1-224">Tables use dynamic schema by default.</span></span>  <span data-ttu-id="031e1-225">Para desabilitar o esquema dinâmico globalmente, defina a Configuração do Aplicativo **MS_DynamicSchema** como falso no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="031e1-225">To turn off dynamic schema globally, set the App Setting **MS_DynamicSchema** to false within the Azure portal.</span></span>

<span data-ttu-id="031e1-226">Você pode encontrar um exemplo completo no [exemplo de tarefas pendentes no GitHub].</span><span class="sxs-lookup"><span data-stu-id="031e1-226">You can find a complete example in the [todo sample on GitHub].</span></span>

### <span data-ttu-id="031e1-227"><a name="howto-staticschema"></a>Como definir tabelas usando um esquema estático</span><span class="sxs-lookup"><span data-stu-id="031e1-227"><a name="howto-staticschema"></a>How to: Define tables using a static schema</span></span>
<span data-ttu-id="031e1-228">Você pode definir explicitamente as colunas que serão expostas usando a API Web.</span><span class="sxs-lookup"><span data-stu-id="031e1-228">You can explicitly define the columns to expose via the WebAPI.</span></span>  <span data-ttu-id="031e1-229">O SDK do NOde.js do azure-mobile-apps adiciona automaticamente as colunas adicionais necessárias à sincronização de dados offline para a lista fornecida por você.</span><span class="sxs-lookup"><span data-stu-id="031e1-229">The azure-mobile-apps Node.js SDK automatically adds any additional columns required for offline data sync to the list that you provide.</span></span>  <span data-ttu-id="031e1-230">Por exemplo, os aplicativos de cliente QuickStart exigem uma tabela com duas colunas: texto (uma cadeia de caracteres) e completo (um valor booliano).</span><span class="sxs-lookup"><span data-stu-id="031e1-230">For example, the QuickStart client applications require a table with two columns: text (a string) and complete (a boolean).</span></span>  
<span data-ttu-id="031e1-231">Essa tabela pode ser definida no arquivo JavaScript de definição de tabela (localizado no diretório de tabelas) da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="031e1-231">The table can be defined in the table definition JavaScript file (located in the tables directory) as follows:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define the columns within the table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    module.exports = table;

<span data-ttu-id="031e1-232">Se você definir as tabelas estaticamente, também deverá chamar o método tables.initialize() para criar o esquema de banco de dados na inicialização.</span><span class="sxs-lookup"><span data-stu-id="031e1-232">If you define tables statically, then you must also call the tables.initialize() method to create the database schema on startup.</span></span>  <span data-ttu-id="031e1-233">O método tables.initialize() retorna uma [Promessa] , para que o serviço Web não atenda a solicitações antes do banco de dados ser inicializado.</span><span class="sxs-lookup"><span data-stu-id="031e1-233">The tables.initialize() method returns a [Promise] so that the web service does not serve requests before the database being initialized.</span></span>

### <span data-ttu-id="031e1-234"><a name="howto-sqlexpress-setup"></a>Como usar o SQL Express como um armazenamento de dados de desenvolvimento em sua máquina local</span><span class="sxs-lookup"><span data-stu-id="031e1-234"><a name="howto-sqlexpress-setup"></a>How to: Use SQL Express as a development data store on your local machine</span></span>
<span data-ttu-id="031e1-235">O SDK do Node dos Aplicativos Móveis do Azure fornece três opções para fornecer dados prontos para uso:</span><span class="sxs-lookup"><span data-stu-id="031e1-235">The Azure Mobile Apps The AzureMobile Apps Node SDK provides three options for serving data out of the box: SDK provides three options for serving data out of the box:</span></span>

* <span data-ttu-id="031e1-236">Usar o driver de **memória** para fornecer um repositório de exemplo não persistente</span><span class="sxs-lookup"><span data-stu-id="031e1-236">Use the **memory** driver to provide a non-persistent example store</span></span>
* <span data-ttu-id="031e1-237">Usar o driver de **mssql** para fornecer um repositório de dados do SQL Express para desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="031e1-237">Use the **mssql** driver to provide a SQL Express data store for development</span></span>
* <span data-ttu-id="031e1-238">Use o driver de **mssql** para fornecer um repositório de dados do Banco de Dados SQL do Azure para produção</span><span class="sxs-lookup"><span data-stu-id="031e1-238">Use the **mssql** driver to provide an Azure SQL Database data store for production</span></span>

<span data-ttu-id="031e1-239">O SDK do Node.js dos Aplicativos Móveis do Azure usa o [pacote de Node.js mssql] para estabelecer e usar uma conexão com o SQL Express e com o Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="031e1-239">The Azure Mobile Apps Node.js SDK uses the [mssql Node.js package] to establish and use a connection to both SQL Express and SQL Database.</span></span>  <span data-ttu-id="031e1-240">Este pacote requer que você habilite conexões TCP na instância do SQL Express.</span><span class="sxs-lookup"><span data-stu-id="031e1-240">This package requires that you enable TCP connections on your SQL Express instance.</span></span>

> [!TIP]
> <span data-ttu-id="031e1-241">O driver de memória não fornece um conjunto completo de recursos para teste.</span><span class="sxs-lookup"><span data-stu-id="031e1-241">The memory driver does not provide a complete set of facilities for testing.</span></span>  <span data-ttu-id="031e1-242">Se você quiser testar localmente seu back-end, recomendamos o uso de um repositório de dados SQL Express e o driver do mssql.</span><span class="sxs-lookup"><span data-stu-id="031e1-242">If you wish to test your backend locally, we recommend the use of a SQL Express data store and the mssql driver.</span></span>
>
>

1. <span data-ttu-id="031e1-243">Baixe e instale o [Microsoft SQL Server 2014 Express].</span><span class="sxs-lookup"><span data-stu-id="031e1-243">Download and install [Microsoft SQL Server 2014 Express].</span></span>  <span data-ttu-id="031e1-244">Instale o SQL Server 2014 Express com a edição Ferramentas.</span><span class="sxs-lookup"><span data-stu-id="031e1-244">Ensure you install the SQL Server 2014 Express with Tools edition.</span></span>  <span data-ttu-id="031e1-245">A menos que você precise explicitamente do suporte de 64 bits, a versão de 32 bits consome menos memória durante a execução.</span><span class="sxs-lookup"><span data-stu-id="031e1-245">Unless you explicitly require 64-bit support, the 32-bit version consumes less memory when running.</span></span>
2. <span data-ttu-id="031e1-246">Execute o Gerenciador de Configurações do SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="031e1-246">Run the SQL Server 2014 Configuration Manager.</span></span>

   1. <span data-ttu-id="031e1-247">Expanda o nó **Configuração da Rede do SQL Server** no menu de árvore à esquerda.</span><span class="sxs-lookup"><span data-stu-id="031e1-247">Expand the **SQL Server Network Configuration** node in the left-hand tree menu.</span></span>
   2. <span data-ttu-id="031e1-248">Clique em **Protocolos para SQLEXPRESS**.</span><span class="sxs-lookup"><span data-stu-id="031e1-248">Click **Protocols for SQLEXPRESS**.</span></span>
   3. <span data-ttu-id="031e1-249">Clique com o botão direito do mouse em **TCP/IP** e escolha **Habilitar**.</span><span class="sxs-lookup"><span data-stu-id="031e1-249">Right-click **TCP/IP** and select **Enable**.</span></span>  <span data-ttu-id="031e1-250">Clique em **OK** no diálogo pop-up.</span><span class="sxs-lookup"><span data-stu-id="031e1-250">Click **OK** in the pop-up dialog.</span></span>
   4. <span data-ttu-id="031e1-251">Clique com o botão direito do mouse em **TCP/IP** e escolha **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="031e1-251">Right-click **TCP/IP** and select **Properties**.</span></span>
   5. <span data-ttu-id="031e1-252">Clique na guia **Endereços IP** .</span><span class="sxs-lookup"><span data-stu-id="031e1-252">Click the **IP Addresses** tab.</span></span>
   6. <span data-ttu-id="031e1-253">Encontre o nó **IPAll** .</span><span class="sxs-lookup"><span data-stu-id="031e1-253">Find the **IPAll** node.</span></span>  <span data-ttu-id="031e1-254">No campo **Porta TCP**, insira **1433**.</span><span class="sxs-lookup"><span data-stu-id="031e1-254">In the **TCP Port** field, enter **1433**.</span></span>

          ![Configure SQL Express for TCP/IP][3]
   7. <span data-ttu-id="031e1-255">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="031e1-255">Click **OK**.</span></span>  <span data-ttu-id="031e1-256">Clique em **OK** no diálogo pop-up.</span><span class="sxs-lookup"><span data-stu-id="031e1-256">Click **OK** in the pop-up dialog.</span></span>
   8. <span data-ttu-id="031e1-257">Clique em **Serviços do SQL Server** no menu de árvore no lado esquerdo.</span><span class="sxs-lookup"><span data-stu-id="031e1-257">Click **SQL Server Services** in the left-hand tree menu.</span></span>
   9. <span data-ttu-id="031e1-258">Clique com o botão direito do mouse em **SQL Server (SQLEXPRESS)** e escolha **Reiniciar**</span><span class="sxs-lookup"><span data-stu-id="031e1-258">Right-click **SQL Server (SQLEXPRESS)** and select **Restart**</span></span>
   10. <span data-ttu-id="031e1-259">Feche o Gerenciador de Configurações do SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="031e1-259">Close the SQL Server 2014 Configuration Manager.</span></span>
3. <span data-ttu-id="031e1-260">Executar o SQL Server 2014 Management Studio e conectar-se à instância do SQL Express local</span><span class="sxs-lookup"><span data-stu-id="031e1-260">Run the SQL Server 2014 Management Studio and connect to your local SQL Express instance</span></span>

   1. <span data-ttu-id="031e1-261">Clique com o botão direito do mouse em sua instância no Explorador de Objetos e escolha **Propriedades**</span><span class="sxs-lookup"><span data-stu-id="031e1-261">Right-click your instance in the Object Explorer and select **Properties**</span></span>
   2. <span data-ttu-id="031e1-262">Escolha a página **Segurança** .</span><span class="sxs-lookup"><span data-stu-id="031e1-262">Select the **Security** page.</span></span>
   3. <span data-ttu-id="031e1-263">Verifique se a opção **Modo de Autenticação do SQL Server e do Windows** está selecionada</span><span class="sxs-lookup"><span data-stu-id="031e1-263">Ensure the **SQL Server and Windows Authentication mode** is selected</span></span>
   4. <span data-ttu-id="031e1-264">Clique em **OK**</span><span class="sxs-lookup"><span data-stu-id="031e1-264">Click **OK**</span></span>

          ![Configure SQL Express Authentication][4]
   5. <span data-ttu-id="031e1-265">Expandaa **Segurança** > **Logons** no Explorador de Objetos</span><span class="sxs-lookup"><span data-stu-id="031e1-265">Expand **Security** > **Logins** in the Object Explorer</span></span>
   6. <span data-ttu-id="031e1-266">Clique com o botão direito do mouse em **Logons** e escolha **Novo Logon...**</span><span class="sxs-lookup"><span data-stu-id="031e1-266">Right-click **Logins** and select **New Login...**</span></span>
   7. <span data-ttu-id="031e1-267">Insira um nome de logon.</span><span class="sxs-lookup"><span data-stu-id="031e1-267">Enter a Login name.</span></span>  <span data-ttu-id="031e1-268">Selecione **Autenticação do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="031e1-268">Select **SQL Server authentication**.</span></span>  <span data-ttu-id="031e1-269">Digite uma Senha e, depois, digite a mesma senha em **Confirmar senha**.</span><span class="sxs-lookup"><span data-stu-id="031e1-269">Enter a Password, then enter the same password in **Confirm password**.</span></span>  <span data-ttu-id="031e1-270">A senha deve atender aos requisitos de complexidade do Windows.</span><span class="sxs-lookup"><span data-stu-id="031e1-270">The password must meet Windows complexity requirements.</span></span>
   8. <span data-ttu-id="031e1-271">Clique em **OK**</span><span class="sxs-lookup"><span data-stu-id="031e1-271">Click **OK**</span></span>

          ![Add a new user to SQL Express][5]
   9. <span data-ttu-id="031e1-272">Clique com o botão direito do mouse em seu novo logon e escolha **Propriedades**</span><span class="sxs-lookup"><span data-stu-id="031e1-272">Right-click your new login and select **Properties**</span></span>
   10. <span data-ttu-id="031e1-273">Escolha a página **Funções de Servidor**</span><span class="sxs-lookup"><span data-stu-id="031e1-273">Select the **Server Roles** page</span></span>
   11. <span data-ttu-id="031e1-274">Marque a caixa ao lado da função de servidor **dbcreator**</span><span class="sxs-lookup"><span data-stu-id="031e1-274">Check the box next to the **dbcreator** server role</span></span>
   12. <span data-ttu-id="031e1-275">Clique em **OK**</span><span class="sxs-lookup"><span data-stu-id="031e1-275">Click **OK**</span></span>
   13. <span data-ttu-id="031e1-276">Feche o SQL Server 2015 Management Studio.</span><span class="sxs-lookup"><span data-stu-id="031e1-276">Close the SQL Server 2015 Management Studio</span></span>

<span data-ttu-id="031e1-277">Não deixe de registrar o nome de usuário e senha que você selecionou.</span><span class="sxs-lookup"><span data-stu-id="031e1-277">Ensure you record the username and password you selected.</span></span>  <span data-ttu-id="031e1-278">Talvez seja necessário atribuir funções de servidor ou permissões adicionais dependendo dos requisitos do banco de dados específico.</span><span class="sxs-lookup"><span data-stu-id="031e1-278">You may need to assign additional server roles or permissions depending on your specific database requirements.</span></span>

<span data-ttu-id="031e1-279">O aplicativo Node.js lê a variável de ambiente **SQLCONNSTR_MS_TableConnectionString** para a cadeia de conexão desse banco de dados.</span><span class="sxs-lookup"><span data-stu-id="031e1-279">The Node.js application reads the **SQLCONNSTR_MS_TableConnectionString** environment variable for the connection string for this database.</span></span>  <span data-ttu-id="031e1-280">Você pode definir essa variável em seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="031e1-280">You can set this variable within your environment.</span></span>  <span data-ttu-id="031e1-281">Por exemplo, você pode usar o PowerShell para definir essa variável de ambiente:</span><span class="sxs-lookup"><span data-stu-id="031e1-281">For example, you can use PowerShell to set this environment variable:</span></span>

    $env:SQLCONNSTR_MS_TableConnectionString = "Server=127.0.0.1; Database=mytestdatabase; User Id=azuremobile; Password=T3stPa55word;"

<span data-ttu-id="031e1-282">Acesse o banco de dados usando conexão TCP/IP e fornecer um nome de usuário e uma senha para a conexão.</span><span class="sxs-lookup"><span data-stu-id="031e1-282">Access the database through a TCP/IP connection and provide a username and password for the connection.</span></span>

### <span data-ttu-id="031e1-283"><a name="howto-config-localdev"></a>Como configurar seu projeto para desenvolvimento local</span><span class="sxs-lookup"><span data-stu-id="031e1-283"><a name="howto-config-localdev"></a>How to: Configure your project for local development</span></span>
<span data-ttu-id="031e1-284">Os Aplicativos Móveis do Azure leem um arquivo JavaScript chamado *azureMobile.js* no sistema de arquivos local.</span><span class="sxs-lookup"><span data-stu-id="031e1-284">Azure Mobile Apps reads a JavaScript file called *azureMobile.js* from the local filesystem.</span></span>  <span data-ttu-id="031e1-285">Não use esse arquivo para configurar o SDK dos Aplicativos Móveis do Azure em produção; em vez disso, use as Configurações de Aplicativo no [portal do Azure] .</span><span class="sxs-lookup"><span data-stu-id="031e1-285">Do not use this file to configure the Azure Mobile Apps SDK in production - use App Settings within the [Azure portal] instead.</span></span>  <span data-ttu-id="031e1-286">O arquivo *azureMobile.js* deve exportar um objeto de configuração.</span><span class="sxs-lookup"><span data-stu-id="031e1-286">The *azureMobile.js* file should export a configuration object.</span></span>  <span data-ttu-id="031e1-287">As configurações mais comuns são:</span><span class="sxs-lookup"><span data-stu-id="031e1-287">The most common settings are:</span></span>

* <span data-ttu-id="031e1-288">Configurações do banco de dados</span><span class="sxs-lookup"><span data-stu-id="031e1-288">Database Settings</span></span>
* <span data-ttu-id="031e1-289">Configurações de registro em log de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="031e1-289">Diagnostic Logging Settings</span></span>
* <span data-ttu-id="031e1-290">Configurações de CORS alternativas</span><span class="sxs-lookup"><span data-stu-id="031e1-290">Alternate CORS Settings</span></span>

<span data-ttu-id="031e1-291">Um exemplo de arquivo *azureMobile.js* implementando as configurações de banco de dados fornecidas anteriormente é dado abaixo:</span><span class="sxs-lookup"><span data-stu-id="031e1-291">An example *azureMobile.js* file implementing the preceding database settings follows:</span></span>

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

<span data-ttu-id="031e1-292">Recomendamos que você adicione *azureMobile.js* ao arquivo *.gitignore* (ou outro arquivo de controle do código-fonte a ser ignorado) para impedir que as senhas sejam armazenadas na nuvem.</span><span class="sxs-lookup"><span data-stu-id="031e1-292">We recommend that you add *azureMobile.js* to your *.gitignore* file (or other source code control ignore file) to prevent passwords from being stored in the cloud.</span></span>  <span data-ttu-id="031e1-293">Sempre defina as configurações de produção nas Configurações do Aplicativo no [portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="031e1-293">Always configure production settings in App Settings within the [Azure portal].</span></span>

### <span data-ttu-id="031e1-294"><a name="howto-appsettings"></a>Como definir configurações de aplicativo para seu aplicativo móvel</span><span class="sxs-lookup"><span data-stu-id="031e1-294"><a name="howto-appsettings"></a>How: Configure App Settings for your Mobile App</span></span>
<span data-ttu-id="031e1-295">A maioria das configurações no arquivo *azureMobile.js* tem uma Configuração do Aplicativo equivalente no [portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="031e1-295">Most settings in the *azureMobile.js* file have an equivalent App Setting in the [Azure portal].</span></span>  <span data-ttu-id="031e1-296">Use a lista a seguir para configurar seu aplicativo nas Configurações de Aplicativo:</span><span class="sxs-lookup"><span data-stu-id="031e1-296">Use the following list to configure your app in App Settings:</span></span>

| <span data-ttu-id="031e1-297">Configurações de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="031e1-297">App Setting</span></span> | <span data-ttu-id="031e1-298">*azureMobile.js* </span><span class="sxs-lookup"><span data-stu-id="031e1-298">*azureMobile.js* Setting</span></span> | <span data-ttu-id="031e1-299">Descrição</span><span class="sxs-lookup"><span data-stu-id="031e1-299">Description</span></span> | <span data-ttu-id="031e1-300">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="031e1-300">Valid Values</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="031e1-301">**MS_MobileAppName**</span><span class="sxs-lookup"><span data-stu-id="031e1-301">**MS_MobileAppName**</span></span> |<span data-ttu-id="031e1-302">name</span><span class="sxs-lookup"><span data-stu-id="031e1-302">name</span></span> |<span data-ttu-id="031e1-303">O nome do aplicativo</span><span class="sxs-lookup"><span data-stu-id="031e1-303">The name of the app</span></span> |<span data-ttu-id="031e1-304">string</span><span class="sxs-lookup"><span data-stu-id="031e1-304">string</span></span> |
| <span data-ttu-id="031e1-305">**MS_MobileLoggingLevel**</span><span class="sxs-lookup"><span data-stu-id="031e1-305">**MS_MobileLoggingLevel**</span></span> |<span data-ttu-id="031e1-306">logging.level</span><span class="sxs-lookup"><span data-stu-id="031e1-306">logging.level</span></span> |<span data-ttu-id="031e1-307">Nível de log mínimo das mensagens a serem registradas</span><span class="sxs-lookup"><span data-stu-id="031e1-307">Minimum log level of messages to log</span></span> |<span data-ttu-id="031e1-308">erro, aviso, informações, detalhado, depuração, simples</span><span class="sxs-lookup"><span data-stu-id="031e1-308">error, warning, info, verbose, debug, silly</span></span> |
| <span data-ttu-id="031e1-309">**MS_DebugMode**</span><span class="sxs-lookup"><span data-stu-id="031e1-309">**MS_DebugMode**</span></span> |<span data-ttu-id="031e1-310">depurar</span><span class="sxs-lookup"><span data-stu-id="031e1-310">debug</span></span> |<span data-ttu-id="031e1-311">Habilitar ou desabilitar o modo de depuração</span><span class="sxs-lookup"><span data-stu-id="031e1-311">Enable or Disable debug mode</span></span> |<span data-ttu-id="031e1-312">verdadeiro, falso</span><span class="sxs-lookup"><span data-stu-id="031e1-312">true, false</span></span> |
| <span data-ttu-id="031e1-313">**MS_TableSchema**</span><span class="sxs-lookup"><span data-stu-id="031e1-313">**MS_TableSchema**</span></span> |<span data-ttu-id="031e1-314">data.schema</span><span class="sxs-lookup"><span data-stu-id="031e1-314">data.schema</span></span> |<span data-ttu-id="031e1-315">Nome do esquema padrão para tabelas SQL</span><span class="sxs-lookup"><span data-stu-id="031e1-315">Default schema name for SQL tables</span></span> |<span data-ttu-id="031e1-316">cadeia de caracteres (padrão: dbo)</span><span class="sxs-lookup"><span data-stu-id="031e1-316">string (default: dbo)</span></span> |
| <span data-ttu-id="031e1-317">**MS_DynamicSchema**</span><span class="sxs-lookup"><span data-stu-id="031e1-317">**MS_DynamicSchema**</span></span> |<span data-ttu-id="031e1-318">data.dynamicSchema</span><span class="sxs-lookup"><span data-stu-id="031e1-318">data.dynamicSchema</span></span> |<span data-ttu-id="031e1-319">Habilitar ou desabilitar o modo de depuração</span><span class="sxs-lookup"><span data-stu-id="031e1-319">Enable or Disable debug mode</span></span> |<span data-ttu-id="031e1-320">verdadeiro, falso</span><span class="sxs-lookup"><span data-stu-id="031e1-320">true, false</span></span> |
| <span data-ttu-id="031e1-321">**MS_DisableVersionHeader**</span><span class="sxs-lookup"><span data-stu-id="031e1-321">**MS_DisableVersionHeader**</span></span> |<span data-ttu-id="031e1-322">versão (definido como indefinido)</span><span class="sxs-lookup"><span data-stu-id="031e1-322">version (set to undefined)</span></span> |<span data-ttu-id="031e1-323">Desabilita o cabeçalho X-ZUMO-Server-Version</span><span class="sxs-lookup"><span data-stu-id="031e1-323">Disables the X-ZUMO-Server-Version header</span></span> |<span data-ttu-id="031e1-324">verdadeiro, falso</span><span class="sxs-lookup"><span data-stu-id="031e1-324">true, false</span></span> |
| <span data-ttu-id="031e1-325">**MS_SkipVersionCheck**</span><span class="sxs-lookup"><span data-stu-id="031e1-325">**MS_SkipVersionCheck**</span></span> |<span data-ttu-id="031e1-326">skipversioncheck</span><span class="sxs-lookup"><span data-stu-id="031e1-326">skipversioncheck</span></span> |<span data-ttu-id="031e1-327">Desabilita a verificação de versão de API do cliente</span><span class="sxs-lookup"><span data-stu-id="031e1-327">Disables the client API version check</span></span> |<span data-ttu-id="031e1-328">verdadeiro, falso</span><span class="sxs-lookup"><span data-stu-id="031e1-328">true, false</span></span> |

<span data-ttu-id="031e1-329">Para definir uma Configuração do Aplicativo:</span><span class="sxs-lookup"><span data-stu-id="031e1-329">To set an App Setting:</span></span>

1. <span data-ttu-id="031e1-330">Faça logon no [portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="031e1-330">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="031e1-331">Selecione **Todos os recursos** ou **Serviços de Aplicativos** e clique no nome do Aplicativo Móvel.</span><span class="sxs-lookup"><span data-stu-id="031e1-331">Select **All resources** or **App Services** then click the name of your Mobile App.</span></span>
3. <span data-ttu-id="031e1-332">A folha Configurações abre por padrão.</span><span class="sxs-lookup"><span data-stu-id="031e1-332">The Settings blade opens by default.</span></span> <span data-ttu-id="031e1-333">Se ela não abrir, clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="031e1-333">If it doesn't, click **Settings**.</span></span>
4. <span data-ttu-id="031e1-334">Clique em **Configurações do aplicativo** no menu GERAL.</span><span class="sxs-lookup"><span data-stu-id="031e1-334">Click **Application settings** in the GENERAL menu.</span></span>
5. <span data-ttu-id="031e1-335">Role até a seção Configurações de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="031e1-335">Scroll to the App Settings section.</span></span>
6. <span data-ttu-id="031e1-336">Se a configuração do aplicativo já existir, clique no valor da configuração do aplicativo para editá-lo.</span><span class="sxs-lookup"><span data-stu-id="031e1-336">If your app setting already exists, click the value of the app setting to edit the value.</span></span>
7. <span data-ttu-id="031e1-337">Se a configuração do aplicativo não existir, insira a Configuração do Aplicativo na caixa Chave e o valor na caixa Valor.</span><span class="sxs-lookup"><span data-stu-id="031e1-337">If your app setting does not exist, enter the App Setting in the Key box and the value in the Value box.</span></span>
8. <span data-ttu-id="031e1-338">Quando você tiver concluído, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="031e1-338">Once you are complete, click **Save**.</span></span>

<span data-ttu-id="031e1-339">A alteração da maioria das Configurações do Aplicativo requer o reinício do serviço.</span><span class="sxs-lookup"><span data-stu-id="031e1-339">Changing most app settings requires a service restart.</span></span>

### <span data-ttu-id="031e1-340"><a name="howto-use-sqlazure"></a>Como usar o Banco de Dados SQL como o armazenamento de dados de produção</span><span class="sxs-lookup"><span data-stu-id="031e1-340"><a name="howto-use-sqlazure"></a>How to: Use SQL Database as your production data store</span></span>
<!--- ALTERNATE INCLUDE - we can't use ../includes/app-service-mobile-dotnet-backend-create-new-service.md - slightly different semantics -->

<span data-ttu-id="031e1-341">O uso do Banco de Dados SQL do Azure como armazenamento de dados é idêntico em todos os tipos de aplicativo do Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="031e1-341">Using Azure SQL Database as a data store is identical across all Azure App Service application types.</span></span> <span data-ttu-id="031e1-342">Se você não tiver feito isso, siga estas etapas para criar um back-end do Aplicativo Móvel.</span><span class="sxs-lookup"><span data-stu-id="031e1-342">If you have not done so already, follow these steps to create a Mobile App backend.</span></span>

1. <span data-ttu-id="031e1-343">Faça logon no [portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="031e1-343">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="031e1-344">Na parte superior esquerda da janela, clique no **+ novo** botão > **Web + móvel** > **aplicativo móvel**, em seguida, forneça um nome para seu back-end do aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="031e1-344">In the top left of the window, click the **+NEW** button > **Web + Mobile** > **Mobile App**, then provide a name for your Mobile App backend.</span></span>
3. <span data-ttu-id="031e1-345">Na caixa **Grupo de Recursos** , digite o mesmo nome do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="031e1-345">In the **Resource Group** box, enter the same name as your app.</span></span>
4. <span data-ttu-id="031e1-346">O Plano do Serviço de Aplicativo Padrão é selecionado.</span><span class="sxs-lookup"><span data-stu-id="031e1-346">The Default App Service plan is selected.</span></span>  <span data-ttu-id="031e1-347">Se você deseja alterar o Plano do Serviço de Aplicativo, é possível fazer isso clicando em Plano do Serviço de Aplicativo > **+ Criar Novo**.</span><span class="sxs-lookup"><span data-stu-id="031e1-347">If you wish to change your App Service plan, you can do so by clicking the App Service Plan > **+ Create New**.</span></span>  <span data-ttu-id="031e1-348">Forneça um nome ao novo Plano de Serviço de Aplicativo e selecione um local apropriado.</span><span class="sxs-lookup"><span data-stu-id="031e1-348">Provide a name of the new App Service plan and select an appropriate location.</span></span>  <span data-ttu-id="031e1-349">Clique em Camada de Preços e selecione uma camada de preços apropriada para o serviço.</span><span class="sxs-lookup"><span data-stu-id="031e1-349">Click the Pricing tier and select an appropriate pricing tier for the service.</span></span> <span data-ttu-id="031e1-350">Selecione **Exibir tudo** para exibir mais opções de preço, como **Gratuito** e **Compartilhado**.</span><span class="sxs-lookup"><span data-stu-id="031e1-350">Select **View all** to view more pricing options, such as **Free** and **Shared**.</span></span>  <span data-ttu-id="031e1-351">Depois de selecionar a camada de preços, clique no botão **Selecionar** .</span><span class="sxs-lookup"><span data-stu-id="031e1-351">Once you have selected the pricing tier, click the **Select** button.</span></span>  <span data-ttu-id="031e1-352">De volta à folha **Plano do Serviço de Aplicativo**, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="031e1-352">Back in the **App Service plan** blade, click **OK**.</span></span>
5. <span data-ttu-id="031e1-353">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="031e1-353">Click **Create**.</span></span> <span data-ttu-id="031e1-354">O provisionamento de um back-end de aplicativo móvel pode levar alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="031e1-354">Provisioning a Mobile App backend can take a couple of minutes.</span></span>  <span data-ttu-id="031e1-355">Depois que o back-end do Aplicativo Móvel for provisionado, o portal abre a folha **Configurações** do back-end do Aplicativo Móvel.</span><span class="sxs-lookup"><span data-stu-id="031e1-355">Once the Mobile App backend is provisioned, the portal opens the **Settings** blade for the Mobile App backend.</span></span>

<span data-ttu-id="031e1-356">Depois que o back-end do Aplicativo Móvel for criado, você poderá conectar um banco de dados existente do SQL ao back-end do Aplicativo Móvel ou criar um novo Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="031e1-356">Once the Mobile App backend is created, you can choose to either connect an existing SQL database to your Mobile App backend or create a new SQL database.</span></span>  <span data-ttu-id="031e1-357">Nesta seção, criamos um banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="031e1-357">In this section, we create a SQL database.</span></span>

> [!NOTE]
> <span data-ttu-id="031e1-358">Se já houver um banco de dados no mesmo local do back-end do aplicativo móvel, você poderá escolher **Usar um banco de dados existente** e selecionar esse banco de dados.</span><span class="sxs-lookup"><span data-stu-id="031e1-358">If you already have a database in the same location as the mobile app backend, you can instead choose **Use an existing database** and then select that database.</span></span> <span data-ttu-id="031e1-359">O uso de um banco de dados em um local diferente não é recomendado devido a latências maiores.</span><span class="sxs-lookup"><span data-stu-id="031e1-359">The use of a database in a different location is not recommended because of higher latencies.</span></span>
>
>

1. <span data-ttu-id="031e1-360">No novo back-end do Aplicativo Móvel, clique em **Configurações** > **Aplicativo Móvel** > **Dados** > **+Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="031e1-360">In the new Mobile App backend, click **Settings** > **Mobile App** > **Data** > **+Add**.</span></span>
2. <span data-ttu-id="031e1-361">Na folha **Adicionar conexão de dados**, clique em **Banco de Dados SQL - Definir configurações necessárias** > **Criar um novo banco de dados**.</span><span class="sxs-lookup"><span data-stu-id="031e1-361">In the **Add data connection** blade, click **SQL Database - Configure required settings** > **Create a new database**.</span></span>  <span data-ttu-id="031e1-362">Insira o nome do novo banco de dados no campo **Nome** .</span><span class="sxs-lookup"><span data-stu-id="031e1-362">Enter the name of the new database in the **Name** field.</span></span>
3. <span data-ttu-id="031e1-363">Clique em **Servidor**.</span><span class="sxs-lookup"><span data-stu-id="031e1-363">Click **Server**.</span></span>  <span data-ttu-id="031e1-364">Na folha **Novo servidor**, insira um nome de servidor exclusivo no campo **Nome do servidor** e forneça um **Logon de administração de servidor** e **Senha** adequados.</span><span class="sxs-lookup"><span data-stu-id="031e1-364">In the **New server** blade, enter a unique server name in the **Server name** field, and provide a suitable **Server admin login** and **Password**.</span></span>  <span data-ttu-id="031e1-365">Verifique se **Permitir que os serviços do Azure acessem o servidor** está marcado.</span><span class="sxs-lookup"><span data-stu-id="031e1-365">Ensure **Allow azure services to access server** is checked.</span></span>  <span data-ttu-id="031e1-366">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="031e1-366">Click **OK**.</span></span>

    ![Criar um Banco de Dados SQL do Azure][6]
4. <span data-ttu-id="031e1-368">Na folha **Novo banco de dados**, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="031e1-368">On the **New database** blade, click **OK**.</span></span>
5. <span data-ttu-id="031e1-369">De volta à folha **Adicionar conexão de dados**, selecione **Cadeia de conexão**, insira o logon e a senha que você forneceu ao criar o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="031e1-369">Back on the **Add data connection** blade, select **Connection string**, enter the login and password that you provided when creating the database.</span></span>  <span data-ttu-id="031e1-370">Se você usar um banco de dados existente, forneça as credenciais de logon desse banco de dados.</span><span class="sxs-lookup"><span data-stu-id="031e1-370">If you use an existing database, provide the login credentials for that database.</span></span>  <span data-ttu-id="031e1-371">Depois de inserir, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="031e1-371">Once entered, click **OK**.</span></span>
6. <span data-ttu-id="031e1-372">De volta à folha **Adicionar conexão de dados**, clique em **OK** para criar o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="031e1-372">Back on the **Add data connection** blade again, click **OK** to create the database.</span></span>

<!--- END OF ALTERNATE INCLUDE -->

<span data-ttu-id="031e1-373">A criação do banco de dados pode levar alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="031e1-373">Creation of the database can take a few minutes.</span></span>  <span data-ttu-id="031e1-374">Use a área **Notificações** para monitorar o progresso da implantação.</span><span class="sxs-lookup"><span data-stu-id="031e1-374">Use the **Notifications** area to monitor the progress of the deployment.</span></span>  <span data-ttu-id="031e1-375">Não siga adiante enquanto o banco de dados não tiver sido implantado com êxito.</span><span class="sxs-lookup"><span data-stu-id="031e1-375">Do not progress until the database has been deployed successfully.</span></span>  <span data-ttu-id="031e1-376">Uma vez implantado com êxito, uma Cadeia de conexão é criada para a instância do Banco de Dados SQL em suas configurações do aplicativo back-end móvel.</span><span class="sxs-lookup"><span data-stu-id="031e1-376">Once successfully deployed, a Connection String is created for the SQL Database instance in your Mobile backend App Settings.</span></span>  <span data-ttu-id="031e1-377">Você pode ver essa configuração do aplicativo em **Configurações** > **Configurações do aplicativo** > **Cadeias de conexão**.</span><span class="sxs-lookup"><span data-stu-id="031e1-377">You can see this app setting in the **Settings** > **Application settings** > **Connection strings**.</span></span>

### <span data-ttu-id="031e1-378"><a name="howto-tables-auth"></a>Como exigir autenticação para acesso às tabelas</span><span class="sxs-lookup"><span data-stu-id="031e1-378"><a name="howto-tables-auth"></a>How to: Require authentication for access to tables</span></span>
<span data-ttu-id="031e1-379">Se você deseja usar a Autenticação do Serviço de Aplicativo com o ponto de extremidade das tabelas, precisa configurar a Autenticação do Serviço de Aplicativo no [portal do Azure] primeiro.</span><span class="sxs-lookup"><span data-stu-id="031e1-379">If you wish to use App Service Authentication with the tables endpoint, you must configure App Service Authentication in the [Azure portal] first.</span></span>  <span data-ttu-id="031e1-380">Para obter mais detalhes sobre como configurar a autenticação em um Serviço de Aplicativo do Azure, examine o Guia de Configuração para o provedor de identidade que você pretende usar:</span><span class="sxs-lookup"><span data-stu-id="031e1-380">For more details about configuring authentication in an Azure App Service, review the Configuration Guide for the identity provider you intend to use:</span></span>

* <span data-ttu-id="031e1-381">[Como configurar a autenticação do Active Directory do Azure]</span><span class="sxs-lookup"><span data-stu-id="031e1-381">[How to configure Azure Active Directory Authentication]</span></span>
* <span data-ttu-id="031e1-382">[Como configurar a autenticação do Facebook]</span><span class="sxs-lookup"><span data-stu-id="031e1-382">[How to configure Facebook Authentication]</span></span>
* <span data-ttu-id="031e1-383">[Como configurar a autenticação do Google]</span><span class="sxs-lookup"><span data-stu-id="031e1-383">[How to configure Google Authentication]</span></span>
* <span data-ttu-id="031e1-384">[Como configurar a autenticação da Microsoft]</span><span class="sxs-lookup"><span data-stu-id="031e1-384">[How to configure Microsoft Authentication]</span></span>
* <span data-ttu-id="031e1-385">[Como configurar a autenticação do Twitter]</span><span class="sxs-lookup"><span data-stu-id="031e1-385">[How to configure Twitter Authentication]</span></span>

<span data-ttu-id="031e1-386">Cada tabela tem uma propriedade de acesso que pode ser usada para controlar o acesso à tabela.</span><span class="sxs-lookup"><span data-stu-id="031e1-386">Each table has an access property that can be used to control access to the table.</span></span>  <span data-ttu-id="031e1-387">O exemplo a seguir mostra uma tabela estaticamente definida com autenticação necessária.</span><span class="sxs-lookup"><span data-stu-id="031e1-387">The following sample shows a statically defined table with authentication required.</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define the columns within the table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication to access the table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="031e1-388">A propriedade de acesso pode assumir um dentre três valores</span><span class="sxs-lookup"><span data-stu-id="031e1-388">The access property can take one of three values</span></span>

* <span data-ttu-id="031e1-389">*anonymous* indica que o aplicativo cliente tem permissão para ler os dados sem autenticação</span><span class="sxs-lookup"><span data-stu-id="031e1-389">*anonymous* indicates that the client application is allowed to read data without authentication</span></span>
* <span data-ttu-id="031e1-390">*authenticated* indica que o aplicativo cliente deve enviar um token de autenticação válido com a solicitação</span><span class="sxs-lookup"><span data-stu-id="031e1-390">*authenticated* indicates that the client application must send a valid authentication token with the request</span></span>
* <span data-ttu-id="031e1-391">*desabilitado* indica que essa tabela está desabilitada no momento</span><span class="sxs-lookup"><span data-stu-id="031e1-391">*disabled* indicates that this table is currently disabled</span></span>

<span data-ttu-id="031e1-392">Se a propriedade de acesso estiver indefinida, o acesso não autenticado será permitido.</span><span class="sxs-lookup"><span data-stu-id="031e1-392">If the access property is undefined, unauthenticated access is allowed.</span></span>

### <span data-ttu-id="031e1-393"><a name="howto-tables-getidentity"></a>Como usar declarações de autenticação com as tabelas</span><span class="sxs-lookup"><span data-stu-id="031e1-393"><a name="howto-tables-getidentity"></a>How to: Use authentication claims with your tables</span></span>
<span data-ttu-id="031e1-394">Você pode configurar várias declarações que são solicitadas durante a configuração da autenticação.</span><span class="sxs-lookup"><span data-stu-id="031e1-394">You can set up various claims that are requested when authentication is set up.</span></span>  <span data-ttu-id="031e1-395">Normalmente, essas declarações não estão disponíveis por meio do objeto `context.user` .</span><span class="sxs-lookup"><span data-stu-id="031e1-395">These claims are not normally available through the `context.user` object.</span></span>  <span data-ttu-id="031e1-396">No entanto, elas podem ser recuperadas usando o método `context.user.getIdentity()` .</span><span class="sxs-lookup"><span data-stu-id="031e1-396">However, they can be retrieved using the `context.user.getIdentity()` method.</span></span>  <span data-ttu-id="031e1-397">O método `getIdentity()` retorna uma Promessa que resolve um objeto.</span><span class="sxs-lookup"><span data-stu-id="031e1-397">The `getIdentity()` method returns a Promise that resolves to an object.</span></span>  <span data-ttu-id="031e1-398">O objeto é inserido pelo método de autenticação (facebook, google, twitter, microsoftaccount ou aad).</span><span class="sxs-lookup"><span data-stu-id="031e1-398">The object is keyed by the authentication method (facebook, google, twitter, microsoftaccount, or aad).</span></span>

<span data-ttu-id="031e1-399">Por exemplo, se você configurar a autenticação da Conta da Microsoft e solicitar a declaração dos endereços de email, é possível adicionar o endereço de email ao registro com o seguinte controlador de tabela:</span><span class="sxs-lookup"><span data-stu-id="031e1-399">For example, if you set up Microsoft Account authentication and request the email addresses claim, you can add the email address to the record with the following table controller:</span></span>

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
    * Limit the context query to those records with the authenticated user email address
    * @param {Context} context the operation context
    * @returns {Promise} context execution Promise
    */
    function queryContextForEmail(context) {
        return context.user.getIdentity().then((data) => {
            context.query.where({ emailAddress: data.microsoftaccount.claims.emailaddress });
            return context.execute();
        });
    }

    /**
    * Adds the email address from the claims to the context item - used for
    * insert operations
    * @param {Context} context the operation context
    * @returns {Promise} context execution Promise
    */
    function addEmailToContext(context) {
        return context.user.getIdentity().then((data) => {
            context.item.emailAddress = data.microsoftaccount.claims.emailaddress;
            return context.execute();
        });
    }

    // Configure specific code when the client does a request
    // READ - only return records belonging to the authenticated user
    table.read(queryContextForEmail);

    // CREATE - add or overwrite the userId based on the authenticated user
    table.insert(addEmailToContext);

    // UPDATE - only allow updating of record belong to the authenticated user
    table.update(queryContextForEmail);

    // DELETE - only allow deletion of records belong to the authenticated uer
    table.delete(queryContextForEmail);

    module.exports = table;

<span data-ttu-id="031e1-400">Para ver quais declarações estão disponíveis, use um navegador da Web para exibir o ponto de extremidade do `/.auth/me` de seu site.</span><span class="sxs-lookup"><span data-stu-id="031e1-400">To see what claims are available, use a web browser to view the `/.auth/me` endpoint of your site.</span></span>

### <span data-ttu-id="031e1-401"><a name="howto-tables-disabled"></a>Como desabilitar o acesso a operações de tabela específicas</span><span class="sxs-lookup"><span data-stu-id="031e1-401"><a name="howto-tables-disabled"></a>How to: Disable access to specific table operations</span></span>
<span data-ttu-id="031e1-402">Além de aparecer na tabela, a propriedade de acesso pode ser usada para controlar operações individuais.</span><span class="sxs-lookup"><span data-stu-id="031e1-402">In addition to appearing on the table, the access property can be used to control individual operations.</span></span>  <span data-ttu-id="031e1-403">Há quatro operações:</span><span class="sxs-lookup"><span data-stu-id="031e1-403">There are four operations:</span></span>

* <span data-ttu-id="031e1-404">*read* é a operação RESTful GET na tabela</span><span class="sxs-lookup"><span data-stu-id="031e1-404">*read* is the RESTful GET operation on the table</span></span>
* <span data-ttu-id="031e1-405">*insert* é a operação RESTful POST na tabela</span><span class="sxs-lookup"><span data-stu-id="031e1-405">*insert* is the RESTful POST operation on the table</span></span>
* <span data-ttu-id="031e1-406">*update* é a operação RESTful PATCH na tabela</span><span class="sxs-lookup"><span data-stu-id="031e1-406">*update* is the RESTful PATCH operation on the table</span></span>
* <span data-ttu-id="031e1-407">*delete* é a operação RESTful DELETE na tabela</span><span class="sxs-lookup"><span data-stu-id="031e1-407">*delete* is the RESTful DELETE operation on the table</span></span>

<span data-ttu-id="031e1-408">Por exemplo, você pode querer fornecer uma tabela não autenticada somente leitura:</span><span class="sxs-lookup"><span data-stu-id="031e1-408">For example, you may wish to provide a read-only unauthenticated table:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Read-Only table - only allow READ operations
    table.read.access = 'anonymous';
    table.insert.access = 'disabled';
    table.update.access = 'disabled';
    table.delete.access = 'disabled';

    module.exports = table;

### <span data-ttu-id="031e1-409"><a name="howto-tables-query"></a>Como ajustar a consulta usada em operações de tabela</span><span class="sxs-lookup"><span data-stu-id="031e1-409"><a name="howto-tables-query"></a>How to: Adjust the query that is used with table operations</span></span>
<span data-ttu-id="031e1-410">Um requisito comum para operações de tabela é fornecer uma exibição restrita dos dados.</span><span class="sxs-lookup"><span data-stu-id="031e1-410">A common requirement for table operations is to provide a restricted view of the data.</span></span>  <span data-ttu-id="031e1-411">Por exemplo, você pode fornecer uma tabela que é marcada com a ID de usuário autenticado, de modo que só possa ler ou atualizar seus próprios registros.</span><span class="sxs-lookup"><span data-stu-id="031e1-411">For example, you may provide a table that is tagged with the authenticated user ID such that you can only read or update your own records.</span></span>  <span data-ttu-id="031e1-412">A definição da tabela abaixo fornece essa funcionalidade:</span><span class="sxs-lookup"><span data-stu-id="031e1-412">The following table definition provides this functionality:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define a static schema for the table
    table.columns = {
        "userId": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;

    // Require authentication for this table
    table.access = 'authenticated';

    // Ensure that only records for the authenticated user are retrieved
    table.read(function (context) {
        context.query.where({ userId: context.user.id });
        return context.execute();
    });

    // When adding records, add or overwrite the userId with the authenticated user
    table.insert(function (context) {
        context.item.userId = context.user.id;
        return context.execute();
    });

    module.exports = table;

<span data-ttu-id="031e1-413">As operações que normalmente executam uma consulta têm uma propriedade de consulta que você pode ajustar com um cláusula where.</span><span class="sxs-lookup"><span data-stu-id="031e1-413">Operations that normally execute a query have a query property that you can adjust with a where clause.</span></span> <span data-ttu-id="031e1-414">A propriedade de consulta é um objeto [QueryJS] usado para converter uma consulta OData em algo que pode ser processado pelo back-end de dados.</span><span class="sxs-lookup"><span data-stu-id="031e1-414">The query property is a [QueryJS] object that is used to convert an OData query to something that the data backend can process.</span></span>  <span data-ttu-id="031e1-415">Para casos de igualdade simples (como o mostrado anteriormente), um mapa pode ser usado.</span><span class="sxs-lookup"><span data-stu-id="031e1-415">For simple equality cases (like the preceding one), a map can be used.</span></span> <span data-ttu-id="031e1-416">Você também pode adicionar cláusulas SQL específicas:</span><span class="sxs-lookup"><span data-stu-id="031e1-416">You can also add specific SQL clauses:</span></span>

    context.query.where('myfield eq ?', 'value');

### <span data-ttu-id="031e1-417"><a name="howto-tables-softdelete"></a>Como configurar a exclusão reversível em uma tabela</span><span class="sxs-lookup"><span data-stu-id="031e1-417"><a name="howto-tables-softdelete"></a>How to: Configure soft delete on a table</span></span>
<span data-ttu-id="031e1-418">A Exclusão Reversível não exclui registros.</span><span class="sxs-lookup"><span data-stu-id="031e1-418">Soft Delete does not actually delete records.</span></span>  <span data-ttu-id="031e1-419">Em vez disso, ela os marca como excluídos no banco de dados definindo a coluna excluída como true.</span><span class="sxs-lookup"><span data-stu-id="031e1-419">Instead it marks them as deleted within the database by setting the deleted column to true.</span></span>  <span data-ttu-id="031e1-420">O SDK de Aplicativos Móveis do Azure remove automaticamente registros com exclusão reversível dos resultados, a menos que o SDK de cliente móvel use IncludeDeleted().</span><span class="sxs-lookup"><span data-stu-id="031e1-420">The Azure Mobile Apps SDK automatically removes soft-deleted records from results unless the Mobile Client SDK uses IncludeDeleted().</span></span>  <span data-ttu-id="031e1-421">Para configurar uma tabela para exclusão reversível, defina a propriedade `softDelete` no arquivo de definição de tabela:</span><span class="sxs-lookup"><span data-stu-id="031e1-421">To configure a table for soft delete, set the `softDelete` property in the table definition file:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define the columns within the table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Turn on Soft Delete
    table.softDelete = true;

    // Require authentication to access the table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="031e1-422">Você deve estabelecer um mecanismo para limpar registros, seja usando aplicativo cliente, trabalho Web, Azure Function ou API personalizada.</span><span class="sxs-lookup"><span data-stu-id="031e1-422">You should establish a mechanism for purging records - either from a client application, via a WebJob, Azure Function or through a custom API.</span></span>

### <span data-ttu-id="031e1-423"><a name="howto-tables-seeding"></a>Como propagar seu banco de dados com dados</span><span class="sxs-lookup"><span data-stu-id="031e1-423"><a name="howto-tables-seeding"></a>How to: Seed your database with data</span></span>
<span data-ttu-id="031e1-424">Ao criar um novo aplicativo, você pode querer propagar uma tabela com dados.</span><span class="sxs-lookup"><span data-stu-id="031e1-424">When creating a new application, you may wish to seed a table with data.</span></span>  <span data-ttu-id="031e1-425">Isso pode ser feito no arquivo JavaScript de definição de tabela da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="031e1-425">This can be done within the table definition JavaScript file as follows:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define the columns within the table
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

    // Require authentication to access the table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="031e1-426">A propagação de dados é feita somente quando a tabela é criada pelo SDK de Aplicativos Móveis do Azure.</span><span class="sxs-lookup"><span data-stu-id="031e1-426">Seeding of data is only done when the table is created by the Azure Mobile Apps SDK.</span></span>  <span data-ttu-id="031e1-427">Se a tabela já existir no banco de dados, nenhum dado será injetado nela.</span><span class="sxs-lookup"><span data-stu-id="031e1-427">If the table already exists within the database, no data is injected into the table.</span></span>  <span data-ttu-id="031e1-428">Se o esquema dinâmico estiver habilitado, o esquema será inferido dos dados propagados.</span><span class="sxs-lookup"><span data-stu-id="031e1-428">If dynamic schema is turned on, then the schema is inferred from the seeded data.</span></span>

<span data-ttu-id="031e1-429">Recomendamos que você chame explicitamente o método `tables.initialize()` para criar a tabela quando o serviço começar a ser executado.</span><span class="sxs-lookup"><span data-stu-id="031e1-429">We recommend that you explicitly call the `tables.initialize()` method to create the table when the service starts running.</span></span>

### <span data-ttu-id="031e1-430"><a name="Swagger"></a>Como habilitar o suporte para o Swagger</span><span class="sxs-lookup"><span data-stu-id="031e1-430"><a name="Swagger"></a>How to: Enable Swagger support</span></span>
<span data-ttu-id="031e1-431">Os Aplicativos Móveis do Serviço de Aplicativo do Azure vêm com suporte interno para o [Swagger] .</span><span class="sxs-lookup"><span data-stu-id="031e1-431">Azure App Service Mobile Apps comes with built-in [Swagger] support.</span></span>  <span data-ttu-id="031e1-432">Para habilitar o suporte do Swagger, primeiro instale a swagger-ui como uma dependência:</span><span class="sxs-lookup"><span data-stu-id="031e1-432">To enable Swagger support, first install the swagger-ui as a dependency:</span></span>

    npm install --save swagger-ui

<span data-ttu-id="031e1-433">Uma vez instalada, você poderá habilitar o suporte do Swagger no construtor dos Aplicativos Móveis do Azure:</span><span class="sxs-lookup"><span data-stu-id="031e1-433">Once installed, you can enable Swagger support in the Azure Mobile Apps constructor:</span></span>

    var mobile = azureMobileApps({ swagger: true });

<span data-ttu-id="031e1-434">Provavelmente você quer apenas habilitar o suporte do Swagger em edições de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="031e1-434">You probably only want to enable Swagger support in development editions.</span></span>  <span data-ttu-id="031e1-435">Faça isso utilizando a configuração do aplicativo `NODE_ENV` :</span><span class="sxs-lookup"><span data-stu-id="031e1-435">You can do this by utilizing the `NODE_ENV` app setting:</span></span>

    var mobile = azureMobileApps({ swagger: process.env.NODE_ENV !== 'production' });

<span data-ttu-id="031e1-436">O ponto de extremidade do swagger está localizado em http://*seusite*.azurewebsites.net/swagger.</span><span class="sxs-lookup"><span data-stu-id="031e1-436">The swagger endpoint is located at http://*yoursite*.azurewebsites.net/swagger.</span></span>  <span data-ttu-id="031e1-437">Você pode acessar a interface do usuário do Swagger pelo ponto de extremidade `/swagger/ui` .</span><span class="sxs-lookup"><span data-stu-id="031e1-437">You can access the Swagger UI via the `/swagger/ui` endpoint.</span></span>  <span data-ttu-id="031e1-438">Se decidir exigir autenticação em todo o aplicativo, o Swagger apresentará um erro.</span><span class="sxs-lookup"><span data-stu-id="031e1-438">if you choose to require authentication across your entire application, Swagger produces an error.</span></span>  <span data-ttu-id="031e1-439">Para obter melhores resultados, opte por permitir solicitações não autenticadas nas configurações de Autenticação/Autorização do Serviço de Aplicativo do Azure e controle a autenticação usando a propriedade `table.access` .</span><span class="sxs-lookup"><span data-stu-id="031e1-439">For best results, choose to allow unauthenticated requests through in the Azure App Service Authentication / Authorization settings, then control authentication using the `table.access` property.</span></span>

<span data-ttu-id="031e1-440">Também será possível adicionar a opção do Swagger ao arquivo `azureMobile.js` se quiser o suporte do Swagger apenas durante o desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="031e1-440">You can also add the Swagger option to your `azureMobile.js` file if you only want Swagger support when developing locally.</span></span>

## <a name="a-namepushpush-notifications"></a><span data-ttu-id="031e1-441"><a name="push">Notificações por Push</span><span class="sxs-lookup"><span data-stu-id="031e1-441"><a name="push">Push notifications</span></span>
<span data-ttu-id="031e1-442">Os Aplicativos Móveis integram-se aos Hubs de Notificação do Azure para que você possa enviar notificações por push direcionadas para milhões de dispositivos em todas as plataformas principais.</span><span class="sxs-lookup"><span data-stu-id="031e1-442">Mobile Apps integrates with Azure Notification Hubs to enable you to send targeted push notifications to millions of devices across all major platforms.</span></span> <span data-ttu-id="031e1-443">Usando os Hubs de Notificação, você pode enviar notificações por push para iOS, Android e dispositivos com Windows.</span><span class="sxs-lookup"><span data-stu-id="031e1-443">By using Notification Hubs, you can send push notifications to iOS, Android and Windows devices.</span></span> <span data-ttu-id="031e1-444">Para saber mais sobre tudo o que você pode fazer com os Hubs de Notificação, confira [Visão geral dos Hubs de Notificação](../notification-hubs/notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="031e1-444">To learn more about all that you can do with Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span></span>

### <span data-ttu-id="031e1-445"></a><a name="send-push"></a>Como enviar notificações por push</span><span class="sxs-lookup"><span data-stu-id="031e1-445"></a><a name="send-push"></a>How to: Send push notifications</span></span>
<span data-ttu-id="031e1-446">O código abaixo mostra como usar o objeto de push para enviar uma notificação por push para dispositivos iOS registrados:</span><span class="sxs-lookup"><span data-stu-id="031e1-446">The following code shows how to use the push object to send a broadcast push notification to registered iOS devices:</span></span>

    // Create an APNS payload.
    var payload = '{"aps": {"alert": "This is an APNS payload."}}';

    // Only do the push if configured
    if (context.push) {
        // Send a push notification using APNS.
        context.push.apns.send(null, payload, function (error) {
            if (error) {
                // Do something or log the error.
            }
        });
    }

<span data-ttu-id="031e1-447">Ao criar um registro de envio por push modelo do cliente, você poderá enviar uma mensagem de envio de modelo para dispositivos em todas as plataformas com suporte.</span><span class="sxs-lookup"><span data-stu-id="031e1-447">By creating a template push registration from the client, you can instead send a template push message to devices on all supported platforms.</span></span> <span data-ttu-id="031e1-448">O código abaixo mostra como enviar uma notificação de modelo:</span><span class="sxs-lookup"><span data-stu-id="031e1-448">The following code shows how to send a template notification:</span></span>

    // Define the template payload.
    var payload = '{"messageParam": "This is a template payload."}';

    // Only do the push if configured
    if (context.push) {
        // Send a template notification.
        context.push.send(null, payload, function (error) {
            if (error) {
                // Do something or log the error.
            }
        });
    }


### <span data-ttu-id="031e1-449"><a name="push-user"></a>Como enviar notificações por push para um usuário autenticado usando marcações</span><span class="sxs-lookup"><span data-stu-id="031e1-449"><a name="push-user"></a>How to: Send push notifications to an authenticated user using tags</span></span>
<span data-ttu-id="031e1-450">Quando um usuário autenticado se registra para notificações por push, uma marca de ID de usuário é adicionada automaticamente ao registro.</span><span class="sxs-lookup"><span data-stu-id="031e1-450">When an authenticated user registers for push notifications, a user ID tag is automatically added to the registration.</span></span> <span data-ttu-id="031e1-451">Usando essa marca, você pode enviar notificações por push para todos os dispositivos registrados por um usuário específico.</span><span class="sxs-lookup"><span data-stu-id="031e1-451">By using this tag, you can send push notifications to all devices registered by a specific user.</span></span> <span data-ttu-id="031e1-452">O código abaixo obtém a SID do usuário que fez a solicitação e envia um modelo de notificação por push para cada registro de dispositivo do usuário:</span><span class="sxs-lookup"><span data-stu-id="031e1-452">The following code gets the SID of user making the request and sends a template push notification to every device registration for that user:</span></span>

    // Only do the push if configured
    if (context.push) {
        // Send a notification to the current user.
        context.push.send(context.user.id, payload, function (error) {
            if (error) {
                // Do something or log the error.
            }
        });
    }

<span data-ttu-id="031e1-453">Ao se registrar para notificações por push de um cliente autenticado, verifique se a autenticação foi concluída antes de tentar o registro.</span><span class="sxs-lookup"><span data-stu-id="031e1-453">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span></span>

## <span data-ttu-id="031e1-454"><a name="CustomAPI"></a> APIs personalizadas</span><span class="sxs-lookup"><span data-stu-id="031e1-454"><a name="CustomAPI"></a> Custom APIs</span></span>
### <span data-ttu-id="031e1-455"><a name="howto-customapi-basic"></a>Como definir uma API personalizada</span><span class="sxs-lookup"><span data-stu-id="031e1-455"><a name="howto-customapi-basic"></a>How to: Define a custom API</span></span>
<span data-ttu-id="031e1-456">Além da API de acesso a dados por meio do ponto de extremidade/tabelas, os Aplicativos Móveis do Azure podem fornecer cobertura de API personalizada.</span><span class="sxs-lookup"><span data-stu-id="031e1-456">In addition to the data access API via the /tables endpoint, Azure Mobile Apps can provide custom API coverage.</span></span>  <span data-ttu-id="031e1-457">As APIs personalizadas são definidas de forma semelhante às definições de tabela e pode acessar todos os mesmos recursos, incluindo autenticação.</span><span class="sxs-lookup"><span data-stu-id="031e1-457">Custom APIs are defined in a similar way to the table definitions and can access all the same facilities, including authentication.</span></span>

<span data-ttu-id="031e1-458">Se você deseja usar a Autenticação do Serviço de Aplicativo com uma API Personalizada, precisa configurar a Autenticação do Serviço de Aplicativo no [portal do Azure] primeiro.</span><span class="sxs-lookup"><span data-stu-id="031e1-458">If you wish to use App Service Authentication with a Custom API, you must configure App Service Authentication in the [Azure portal] first.</span></span>  <span data-ttu-id="031e1-459">Para obter mais detalhes sobre como configurar a autenticação em um Serviço de Aplicativo do Azure, examine o Guia de Configuração para o provedor de identidade que você pretende usar:</span><span class="sxs-lookup"><span data-stu-id="031e1-459">For more details about configuring authentication in an Azure App Service, review the Configuration Guide for the identity provider you intend to use:</span></span>

* <span data-ttu-id="031e1-460">[Como configurar a autenticação do Active Directory do Azure]</span><span class="sxs-lookup"><span data-stu-id="031e1-460">[How to configure Azure Active Directory Authentication]</span></span>
* <span data-ttu-id="031e1-461">[Como configurar a autenticação do Facebook]</span><span class="sxs-lookup"><span data-stu-id="031e1-461">[How to configure Facebook Authentication]</span></span>
* <span data-ttu-id="031e1-462">[Como configurar a autenticação do Google]</span><span class="sxs-lookup"><span data-stu-id="031e1-462">[How to configure Google Authentication]</span></span>
* <span data-ttu-id="031e1-463">[Como configurar a autenticação da Microsoft]</span><span class="sxs-lookup"><span data-stu-id="031e1-463">[How to configure Microsoft Authentication]</span></span>
* <span data-ttu-id="031e1-464">[Como configurar a autenticação do Twitter]</span><span class="sxs-lookup"><span data-stu-id="031e1-464">[How to configure Twitter Authentication]</span></span>

<span data-ttu-id="031e1-465">As APIs personalizadas são definidas da mesma forma que a API de tabelas.</span><span class="sxs-lookup"><span data-stu-id="031e1-465">Custom APIs are defined in much the same way as the Tables API.</span></span>

1. <span data-ttu-id="031e1-466">Crie um diretório **api**</span><span class="sxs-lookup"><span data-stu-id="031e1-466">Create an **api** directory</span></span>
2. <span data-ttu-id="031e1-467">Crie um arquivo JavaScript de definição de API no diretório **api** .</span><span class="sxs-lookup"><span data-stu-id="031e1-467">Create an API definition JavaScript file in the **api** directory.</span></span>
3. <span data-ttu-id="031e1-468">Use o método import para importar o diretório **api** .</span><span class="sxs-lookup"><span data-stu-id="031e1-468">Use the import method to import the **api** directory.</span></span>

<span data-ttu-id="031e1-469">Aqui está a definição de api do protótipo com base na amostra de aplicativo básico que usamos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="031e1-469">Here is the prototype api definition based on the basic-app sample we used earlier.</span></span>

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Import the Custom API
    mobile.api.import('./api');

    // Add the mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

<span data-ttu-id="031e1-470">Vamos pegar uma API de exemplo que retorna a data do servidor usando o método *Date.now()* .</span><span class="sxs-lookup"><span data-stu-id="031e1-470">Let's take an example API that returns the server date using the *Date.now()* method.</span></span>  <span data-ttu-id="031e1-471">Eis o arquivo api/date.js:</span><span class="sxs-lookup"><span data-stu-id="031e1-471">Here is the api/date.js file:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };

    module.exports = api;

<span data-ttu-id="031e1-472">Cada parâmetro é um dos verbos padrão RESTful – GET, POST, PATCH ou DELETE.</span><span class="sxs-lookup"><span data-stu-id="031e1-472">Each parameter is one of the standard RESTful verbs - GET, POST, PATCH, or DELETE.</span></span>  <span data-ttu-id="031e1-473">O método é uma função padrão [ExpressJS Middleware] que envia a saída necessária.</span><span class="sxs-lookup"><span data-stu-id="031e1-473">The method is a standard [ExpressJS Middleware] function that sends the required output.</span></span>

### <span data-ttu-id="031e1-474"><a name="howto-customapi-auth"></a>Como solicitar autenticação para acesso a uma API personalizada</span><span class="sxs-lookup"><span data-stu-id="031e1-474"><a name="howto-customapi-auth"></a>How to: Require authentication for access to a custom API</span></span>
<span data-ttu-id="031e1-475">O SDK de aplicativos móveis do Azure implementa a autenticação da mesma forma para o ponto de extremidade de tabelas e para APIs personalizadas.</span><span class="sxs-lookup"><span data-stu-id="031e1-475">Azure Mobile Apps SDK implements authentication in the same way for both the tables endpoint and custom APIs.</span></span>  <span data-ttu-id="031e1-476">Para adicionar autenticação à API desenvolvida na seção anterior, adicione uma propriedade **access** :</span><span class="sxs-lookup"><span data-stu-id="031e1-476">To add authentication to the API developed in the previous section, add an **access** property:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };
    // All methods must be authenticated.
    api.access = 'authenticated';

    module.exports = api;

<span data-ttu-id="031e1-477">Você também pode especificar a autenticação em operações específicas:</span><span class="sxs-lookup"><span data-stu-id="031e1-477">You can also specify authentication on specific operations:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        }
    };
    // The GET methods must be authenticated.
    api.get.access = 'authenticated';

    module.exports = api;

<span data-ttu-id="031e1-478">O mesmo token que é usado para o ponto de extremidade de tabelas deve ser usado para APIs personalizadas que requerem autenticação.</span><span class="sxs-lookup"><span data-stu-id="031e1-478">The same token that is used for the tables endpoint must be used for custom APIs requiring authentication.</span></span>

### <span data-ttu-id="031e1-479"><a name="howto-customapi-auth"></a>Como manipular transferências de arquivos grandes</span><span class="sxs-lookup"><span data-stu-id="031e1-479"><a name="howto-customapi-auth"></a>How to: Handle large file uploads</span></span>
<span data-ttu-id="031e1-480">O SDK dos Aplicativos Móveis do Azure usa o [middleware de analisador de corpo](https://github.com/expressjs/body-parser) para aceitar e decodificar o conteúdo do corpo em seu envio.</span><span class="sxs-lookup"><span data-stu-id="031e1-480">Azure Mobile Apps SDK uses the [body-parser middleware](https://github.com/expressjs/body-parser) to accept and decode body content in your submission.</span></span>  <span data-ttu-id="031e1-481">Você pode pré-configurar o analisador de corpo para aceitar carregamentos de arquivos maiores:</span><span class="sxs-lookup"><span data-stu-id="031e1-481">You can pre-configure body-parser to accept larger file uploads:</span></span>

    var express = require('express'),
        bodyParser = require('body-parser'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Set up large body content handling
    app.use(bodyParser.json({ limit: '50mb' }));
    app.use(bodyParser.urlencoded({ limit: '50mb', extended: true }));

    // Import the Custom API
    mobile.api.import('./api');

    // Add the mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

<span data-ttu-id="031e1-482">O arquivo é codificado em base 64 antes da transmissão.</span><span class="sxs-lookup"><span data-stu-id="031e1-482">The file is base-64 encoded before transmission.</span></span>  <span data-ttu-id="031e1-483">Isso aumenta o tamanho do carregamento real (e, portanto, o tamanho que você deve considerar).</span><span class="sxs-lookup"><span data-stu-id="031e1-483">This increases the size of the actual upload (and hence the size you must account for).</span></span>

### <span data-ttu-id="031e1-484"><a name="howto-customapi-sql"></a>Como executar instruções SQL personalizadas</span><span class="sxs-lookup"><span data-stu-id="031e1-484"><a name="howto-customapi-sql"></a>How to: Execute custom SQL statements</span></span>
<span data-ttu-id="031e1-485">O SDK de Aplicativos Móveis do Azure permite o acesso a todo o Contexto por meio do objeto da solicitação, permitindo que você execute facilmente instruções SQL com parâmetros para o provedor de dados definido:</span><span class="sxs-lookup"><span data-stu-id="031e1-485">The Azure Mobile Apps SDK allows access to the entire Context through the request object, allowing you to execute parameterized SQL statements to the defined data provider easily:</span></span>

    var api = {
        get: function (request, response, next) {
            // Check for parameters - if not there, pass on to a later API call
            if (typeof request.params.completed === 'undefined')
                return next();

            // Define the query - anything that can be handled by the mssql
            // driver is allowed.
            var query = {
                sql: 'UPDATE TodoItem SET complete=@completed',
                parameters: [{
                    completed: request.params.completed
                }]
            };

            // Execute the query.  The context for Azure Mobile Apps is available through
            // request.azureMobile - the data object contains the configured data provider.
            request.azureMobile.data.execute(query)
            .then(function (results) {
                response.json(results);
            });
        }
    };

    api.get.access = 'authenticated';
    module.exports = api;

## <span data-ttu-id="031e1-486"><a name="Debugging"></a>Depuração, Tabelas Fáceis e APIs Fáceis</span><span class="sxs-lookup"><span data-stu-id="031e1-486"><a name="Debugging"></a>Debugging, Easy Tables, and Easy APIs</span></span>
### <span data-ttu-id="031e1-487"><a name="howto-diagnostic-logs"></a>Como depurar, diagnosticar e solucionar problemas dos Aplicativos Móveis do Azure</span><span class="sxs-lookup"><span data-stu-id="031e1-487"><a name="howto-diagnostic-logs"></a>How to: Debug, diagnose, and troubleshoot Azure Mobile apps</span></span>
<span data-ttu-id="031e1-488">O Serviço de Aplicativo do Azure fornece várias técnicas de depuração e de solução de problemas para aplicativos Node.js.</span><span class="sxs-lookup"><span data-stu-id="031e1-488">The Azure App Service provides several debugging and troubleshooting techniques for Node.js applications.</span></span>
<span data-ttu-id="031e1-489">Consulte os artigos a seguir para iniciar a solução de problemas do back-end do Mobile Node.js:</span><span class="sxs-lookup"><span data-stu-id="031e1-489">Refer to the following articles to get started in troubleshooting your Node.js Mobile backend:</span></span>

* <span data-ttu-id="031e1-490">[Monitorando um Serviço de Aplicativo do Azure]</span><span class="sxs-lookup"><span data-stu-id="031e1-490">[Monitoring an Azure App Service]</span></span>
* <span data-ttu-id="031e1-491">[Habilitar o registro em log de diagnósticos no Serviço de Aplicativo do Azure]</span><span class="sxs-lookup"><span data-stu-id="031e1-491">[Enable Diagnostic Logging in Azure App Service]</span></span>
* <span data-ttu-id="031e1-492">[Solucionar problemas de um Serviço de Aplicativo do Azure no Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="031e1-492">[Troubleshoot an Azure App Service in Visual Studio]</span></span>

<span data-ttu-id="031e1-493">Os aplicativos Node.js têm acesso a uma ampla gama de ferramentas de log de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="031e1-493">Node.js applications have access to a wide range of diagnostic log tools.</span></span>  <span data-ttu-id="031e1-494">Internamente, o SDK do Node.js dos Aplicativos Móveis do Azure usa o [Winston] para o registro em log de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="031e1-494">Internally, the Azure Mobile Apps Node.js SDK uses [Winston] for diagnostic logging.</span></span>  <span data-ttu-id="031e1-495">O registro em log é ativado automaticamente habilitando o modo de depuração ou definindo a configuração de aplicativo **MS_DebugMode** como true no [portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="031e1-495">Logging is automatically enabled by enabling debug mode or by setting the **MS_DebugMode** app setting to true in the [Azure portal].</span></span> <span data-ttu-id="031e1-496">Logs gerados aparecem nos Logs de Diagnóstico no [portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="031e1-496">Generated logs appear in the Diagnostic Logs on the [Azure portal].</span></span>

### <span data-ttu-id="031e1-497"><a name="in-portal-editing"></a><a name="work-easy-tables"></a>Como trabalhar com Tabelas Fáceis no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="031e1-497"><a name="in-portal-editing"></a><a name="work-easy-tables"></a>How to: Work with Easy Tables in the Azure portal</span></span>
<span data-ttu-id="031e1-498">Tabelas fáceis no portal do permitem que você crie e trabalhe com as tabelas certas no portal.</span><span class="sxs-lookup"><span data-stu-id="031e1-498">Easy Tables in the portal let you create and work with tables right in the portal.</span></span> <span data-ttu-id="031e1-499">Você ainda pode editar operações de tabela usando Editor de Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="031e1-499">You can even edit table operations using the App Service Editor.</span></span>

<span data-ttu-id="031e1-500">Quando você clica em **Tabelas fáceis** em suas configurações de site de back-end, você pode adicionar, modificar ou excluir uma tabela.</span><span class="sxs-lookup"><span data-stu-id="031e1-500">When you click **Easy tables** in your backend site settings, you can add, modify, or delete a table.</span></span> <span data-ttu-id="031e1-501">Você também pode ver dados na tabela.</span><span class="sxs-lookup"><span data-stu-id="031e1-501">You can also see data in the table.</span></span>

![Trabalhar com Tabelas fáceis](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-tables.png)

<span data-ttu-id="031e1-503">Os comandos a seguir estão disponíveis na barra de comandos de uma tabela:</span><span class="sxs-lookup"><span data-stu-id="031e1-503">The following commands are available on the command bar for a table:</span></span>

* <span data-ttu-id="031e1-504">**Alterar permissões** : modifique a permissão para operações de leitura, inserção, atualização e exclusão na tabela.</span><span class="sxs-lookup"><span data-stu-id="031e1-504">**Change permissions** - modify the permission for read, insert, update and delete operations on the table.</span></span>
  <span data-ttu-id="031e1-505">As opções são permitir acesso anônimo, exigir autenticação ou desabilitar todo o acesso à operação.</span><span class="sxs-lookup"><span data-stu-id="031e1-505">Options are to allow anonymous access, to require authentication, or to disable all access to the operation.</span></span>
* <span data-ttu-id="031e1-506">**Editar script** : o arquivo de script da tabela é aberto no Editor de Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="031e1-506">**Edit script** - the script file for the table is opened in the App Service Editor.</span></span>
* <span data-ttu-id="031e1-507">**Gerenciar esquema** : adicione ou exclua colunas, ou altere o índice da tabela.</span><span class="sxs-lookup"><span data-stu-id="031e1-507">**Manage schema** - add or delete columns or change the table index.</span></span>
* <span data-ttu-id="031e1-508">**Limpar tabela** : trunca uma tabela existente excluindo todas as linhas de dados, mas deixando o esquema inalterado.</span><span class="sxs-lookup"><span data-stu-id="031e1-508">**Clear table** - truncates an existing table be deleting all data rows but leaving the schema unchanged.</span></span>
* <span data-ttu-id="031e1-509">**Excluir linhas** : exclua linhas individuais de dados.</span><span class="sxs-lookup"><span data-stu-id="031e1-509">**Delete rows** - delete individual rows of data.</span></span>
* <span data-ttu-id="031e1-510">**Exibir logs de streaming** : conecta você ao serviço de log de streaming de seu site.</span><span class="sxs-lookup"><span data-stu-id="031e1-510">**View streaming logs** - connects you to the streaming log service for your site.</span></span>

### <span data-ttu-id="031e1-511"><a name="work-easy-apis"></a>Como trabalhar com APIs fáceis no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="031e1-511"><a name="work-easy-apis"></a>How to: Work with Easy APIs in the Azure portal</span></span>
<span data-ttu-id="031e1-512">APIs fáceis de usar permitem que você crie e trabalhe com APIs personalizadas diretamente no Portal.</span><span class="sxs-lookup"><span data-stu-id="031e1-512">Easy APIs in the portal let you create and work with custom APIs right in the portal.</span></span> <span data-ttu-id="031e1-513">Você pode editar scripts de API usando o Editor de Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="031e1-513">You can edit API scripts using the App Service Editor.</span></span>

<span data-ttu-id="031e1-514">Quando você clica em **APIs fáceis** em suas configurações de site de back-end, você pode adicionar, modificar ou excluir um ponto de extremidade de API.</span><span class="sxs-lookup"><span data-stu-id="031e1-514">When you click **Easy APIs** in your backend site settings, you can add, modify, or delete a custom API endpoint.</span></span>

![Trabalhar com APIs fáceis](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-apis.png)

<span data-ttu-id="031e1-516">No Portal, você pode alterar as permissões de acesso de uma determinada ação HTTP, editar o arquivo de script da API no Editor de Serviço de Aplicativo ou exibir os logs de streaming.</span><span class="sxs-lookup"><span data-stu-id="031e1-516">In the portal, you can change the access permissions for a given HTTP action, edit the API script file in the App Service Editor, or view the streaming logs.</span></span>

### <span data-ttu-id="031e1-517"><a name="online-editor"></a>Como editar o código no Editor de Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="031e1-517"><a name="online-editor"></a>How to: Edit code in the App Service Editor</span></span>
<span data-ttu-id="031e1-518">O Portal do Azure permite a edição dos arquivos de script de back-end do Node.js no Editor de Serviço de Aplicativo sem a necessidade de baixar o projeto no computador local.</span><span class="sxs-lookup"><span data-stu-id="031e1-518">The Azure portal lets you edit your Node.js backend script files in the App Service Editor without having to download the project to your local computer.</span></span> <span data-ttu-id="031e1-519">Para editar arquivos de script no editor online:</span><span class="sxs-lookup"><span data-stu-id="031e1-519">To edit script files in the online editor:</span></span>

1. <span data-ttu-id="031e1-520">Na folha do back-end de Aplicativo Móvel, clique em **Todas as configurações** > em **Tabelas fáceis** ou **APIs fáceis**, clique em uma tabela ou API e clique em **Editar script**.</span><span class="sxs-lookup"><span data-stu-id="031e1-520">In your Mobile App backend blade, click **All settings** > either **Easy tables** or **Easy APIs**, click a table or API, then click **Edit script**.</span></span> <span data-ttu-id="031e1-521">O arquivo de é aberto no Editor de Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="031e1-521">The script file is opened in the App Service Editor.</span></span>

    ![Editor de Serviço de Aplicativo](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-visual-studio-editor.png)
2. <span data-ttu-id="031e1-523">Faça as alterações no arquivo de código no editor online.</span><span class="sxs-lookup"><span data-stu-id="031e1-523">Make your changes to the code file in the online editor.</span></span> <span data-ttu-id="031e1-524">As alterações são salvas automaticamente enquanto você digita.</span><span class="sxs-lookup"><span data-stu-id="031e1-524">Changes are saved automatically as you type.</span></span>

<!-- Images -->
[0]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/npm-init.png
[1]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-new-project.png
[2]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-install-npm.png
[3]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-config.png
[4]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-authconfig.png
[5]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-newuser-1.png
[6]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/dotnet-backend-create-db.png

<!-- URLs -->
<span data-ttu-id="031e1-525">[Início rápido do cliente Android]: app-service-mobile-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="031e1-525">[Android Client QuickStart]: app-service-mobile-android-get-started.md</span></span>
<span data-ttu-id="031e1-526">[Início rápido do cliente Apache Cordova]: app-service-mobile-cordova-get-started.md</span><span class="sxs-lookup"><span data-stu-id="031e1-526">[Apache Cordova Client QuickStart]: app-service-mobile-cordova-get-started.md</span></span>
<span data-ttu-id="031e1-527">[Início rápido do cliente iOS]: app-service-mobile-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="031e1-527">[iOS Client QuickStart]: app-service-mobile-ios-get-started.md</span></span>
<span data-ttu-id="031e1-528">[Início rápido do cliente Xamarin.iOS]: app-service-mobile-xamarin-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="031e1-528">[Xamarin.iOS Client QuickStart]: app-service-mobile-xamarin-ios-get-started.md</span></span>
<span data-ttu-id="031e1-529">[Início rápido do cliente Xamarin.Android]: app-service-mobile-xamarin-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="031e1-529">[Xamarin.Android Client QuickStart]: app-service-mobile-xamarin-android-get-started.md</span></span>
<span data-ttu-id="031e1-530">[Início rápido do cliente Xamarin.Forms]: app-service-mobile-xamarin-forms-get-started.md</span><span class="sxs-lookup"><span data-stu-id="031e1-530">[Xamarin.Forms Client QuickStart]: app-service-mobile-xamarin-forms-get-started.md</span></span>
<span data-ttu-id="031e1-531">[Início rápido de cliente Windows Store]: app-service-mobile-windows-store-dotnet-get-started.md</span><span class="sxs-lookup"><span data-stu-id="031e1-531">[Windows Store Client QuickStart]: app-service-mobile-windows-store-dotnet-get-started.md</span></span>
[HTML/Javascript Client QuickStart]: app-service-html-get-started.md
<span data-ttu-id="031e1-532">[sincronização de dados offline]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="031e1-532">[offline data sync]: app-service-mobile-offline-data-sync.md</span></span>
<span data-ttu-id="031e1-533">[Como configurar a autenticação do Active Directory do Azure]: app-service-mobile-how-to-configure-active-directory-authentication.md</span><span class="sxs-lookup"><span data-stu-id="031e1-533">[How to configure Azure Active Directory Authentication]: app-service-mobile-how-to-configure-active-directory-authentication.md</span></span>
<span data-ttu-id="031e1-534">[Como configurar a autenticação do Facebook]: app-service-mobile-how-to-configure-facebook-authentication.md</span><span class="sxs-lookup"><span data-stu-id="031e1-534">[How to configure Facebook Authentication]: app-service-mobile-how-to-configure-facebook-authentication.md</span></span>
<span data-ttu-id="031e1-535">[Como configurar a autenticação do Google]: app-service-mobile-how-to-configure-google-authentication.md</span><span class="sxs-lookup"><span data-stu-id="031e1-535">[How to configure Google Authentication]: app-service-mobile-how-to-configure-google-authentication.md</span></span>
<span data-ttu-id="031e1-536">[Como configurar a autenticação da Microsoft]: app-service-mobile-how-to-configure-microsoft-authentication.md</span><span class="sxs-lookup"><span data-stu-id="031e1-536">[How to configure Microsoft Authentication]: app-service-mobile-how-to-configure-microsoft-authentication.md</span></span>
<span data-ttu-id="031e1-537">[Como configurar a autenticação do Twitter]: app-service-mobile-how-to-configure-twitter-authentication.md</span><span class="sxs-lookup"><span data-stu-id="031e1-537">[How to configure Twitter Authentication]: app-service-mobile-how-to-configure-twitter-authentication.md</span></span>
<span data-ttu-id="031e1-538">[Guia de implantação do Serviço de Aplicativo do Azure]: ../app-service-web/web-sites-deploy.md</span><span class="sxs-lookup"><span data-stu-id="031e1-538">[Azure App Service Deployment Guide]: ../app-service-web/web-sites-deploy.md</span></span>
<span data-ttu-id="031e1-539">[Monitorando um Serviço de Aplicativo do Azure]: ../app-service-web/web-sites-monitor.md</span><span class="sxs-lookup"><span data-stu-id="031e1-539">[Monitoring an Azure App Service]: ../app-service-web/web-sites-monitor.md</span></span>
<span data-ttu-id="031e1-540">[Habilitar o registro em log de diagnósticos no Serviço de Aplicativo do Azure]: ../app-service-web/web-sites-enable-diagnostic-log.md</span><span class="sxs-lookup"><span data-stu-id="031e1-540">[Enable Diagnostic Logging in Azure App Service]: ../app-service-web/web-sites-enable-diagnostic-log.md</span></span>
<span data-ttu-id="031e1-541">[Solucionar problemas de um Serviço de Aplicativo do Azure no Visual Studio]: ../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md</span><span class="sxs-lookup"><span data-stu-id="031e1-541">[Troubleshoot an Azure App Service in Visual Studio]: ../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md</span></span>
<span data-ttu-id="031e1-542">[especificar a versão do Node]: ../nodejs-specify-node-version-azure-apps.md</span><span class="sxs-lookup"><span data-stu-id="031e1-542">[specify the Node Version]: ../nodejs-specify-node-version-azure-apps.md</span></span>
<span data-ttu-id="031e1-543">[usar módulos do Node]: ../nodejs-use-node-modules-azure-apps.md</span><span class="sxs-lookup"><span data-stu-id="031e1-543">[use Node modules]: ../nodejs-use-node-modules-azure-apps.md</span></span>
[Create a new Azure App Service]: ../app-service-web/
[azure-mobile-apps]: https://www.npmjs.com/package/azure-mobile-apps
<span data-ttu-id="031e1-544">[Express]: http://expressjs.com/</span><span class="sxs-lookup"><span data-stu-id="031e1-544">[Express]: http://expressjs.com/</span></span>
<span data-ttu-id="031e1-545">[Swagger]: http://swagger.io/</span><span class="sxs-lookup"><span data-stu-id="031e1-545">[Swagger]: http://swagger.io/</span></span>

<span data-ttu-id="031e1-546">[portal do Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="031e1-546">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="031e1-547">[OData]: http://www.odata.org</span><span class="sxs-lookup"><span data-stu-id="031e1-547">[OData]: http://www.odata.org</span></span>
<span data-ttu-id="031e1-548">[Promessa]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise</span><span class="sxs-lookup"><span data-stu-id="031e1-548">[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise</span></span>
<span data-ttu-id="031e1-549">[exemplo de aplicativo básico no GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app</span><span class="sxs-lookup"><span data-stu-id="031e1-549">[basicapp sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app</span></span>
<span data-ttu-id="031e1-550">[exemplo de tarefas pendentes no GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo</span><span class="sxs-lookup"><span data-stu-id="031e1-550">[todo sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo</span></span>
<span data-ttu-id="031e1-551">[diretório de exemplos no GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples</span><span class="sxs-lookup"><span data-stu-id="031e1-551">[samples directory on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples</span></span>
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
<span data-ttu-id="031e1-552">[QueryJS]: https://github.com/Azure/queryjs</span><span class="sxs-lookup"><span data-stu-id="031e1-552">[QueryJS]: https://github.com/Azure/queryjs</span></span>
<span data-ttu-id="031e1-553">[Ferramentas do Node.js 1.1 para Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1</span><span class="sxs-lookup"><span data-stu-id="031e1-553">[Node.js Tools 1.1 for Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1</span></span>
<span data-ttu-id="031e1-554">[pacote de Node.js mssql]: https://www.npmjs.com/package/mssql</span><span class="sxs-lookup"><span data-stu-id="031e1-554">[mssql Node.js package]: https://www.npmjs.com/package/mssql</span></span>
<span data-ttu-id="031e1-555">[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx</span><span class="sxs-lookup"><span data-stu-id="031e1-555">[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx</span></span>
<span data-ttu-id="031e1-556">[ExpressJS Middleware]: http://expressjs.com/guide/using-middleware.html</span><span class="sxs-lookup"><span data-stu-id="031e1-556">[ExpressJS Middleware]: http://expressjs.com/guide/using-middleware.html</span></span>
<span data-ttu-id="031e1-557">[Winston]: https://github.com/winstonjs/winston</span><span class="sxs-lookup"><span data-stu-id="031e1-557">[Winston]: https://github.com/winstonjs/winston</span></span>
