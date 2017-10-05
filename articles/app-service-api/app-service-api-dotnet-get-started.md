---
title: "Introdução aos aplicativos de API e ao ASP.NET no Serviço de Aplicativo | Microsoft Docs"
description: "Saiba como criar, implantar e consumir um aplicativo de API do ASP.NET no Serviço de Aplicativo do Azure usando o Visual Studio 2015."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: ddc028b2-cde0-4567-a6ee-32cb264a830a
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: hero-article
ms.date: 09/20/2016
ms.author: alkarche
ms.openlocfilehash: e8fbffde29efcdbb2f67362474061e9f6ee0d59d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-api-apps-aspnet-and-swagger-in-azure-app-service"></a><span data-ttu-id="43a37-103">Introdução aos aplicativos de API, ASP.NET e Swagger no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="43a37-103">Get started with API Apps, ASP.NET, and Swagger in Azure App Service</span></span>
[!INCLUDE [selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="43a37-104">Este é o primeiro de uma série de tutoriais que mostram como usar recursos do Serviço de Aplicativo do Azure que são úteis para desenvolver e hospedar APIs RESTful:</span><span class="sxs-lookup"><span data-stu-id="43a37-104">This is the first in a series of tutorials that show how to use features of Azure App Service that are helpful for developing and hosting RESTful APIs.</span></span>  <span data-ttu-id="43a37-105">Este tutorial aborda o suporte para metadados de API no formato Swagger.</span><span class="sxs-lookup"><span data-stu-id="43a37-105">This tutorial covers support for API metadata in Swagger format.</span></span>

<span data-ttu-id="43a37-106">O que você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="43a37-106">You'll learn:</span></span>

* <span data-ttu-id="43a37-107">Como criar e implantar [aplicativos de API](app-service-api-apps-why-best-platform.md) no Serviço de Aplicativo do Azure usando ferramentas internas do Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="43a37-107">How to create and deploy [API apps](app-service-api-apps-why-best-platform.md) in Azure App Service by using tools built into Visual Studio 2015.</span></span>
* <span data-ttu-id="43a37-108">Como automatizar a detecção de API usando o pacote NuGet do Swashbuckle para gerar dinamicamente os metadados de API do Swagger.</span><span class="sxs-lookup"><span data-stu-id="43a37-108">How to automate API discovery by using the Swashbuckle NuGet package to dynamically generate Swagger API metadata.</span></span>
* <span data-ttu-id="43a37-109">Como usar metadados de API do Swagger para gerar automaticamente o código do cliente para um aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="43a37-109">How to use Swagger API metadata to automatically generate client code for an API app.</span></span>

## <a name="sample-application-overview"></a><span data-ttu-id="43a37-110">Visão geral do aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="43a37-110">Sample application overview</span></span>
<span data-ttu-id="43a37-111">Neste tutorial, você trabalha com um aplicativo de exemplo de lista de tarefas simples.</span><span class="sxs-lookup"><span data-stu-id="43a37-111">In this tutorial, you work with a simple to-do list sample application.</span></span> <span data-ttu-id="43a37-112">O aplicativo tem um front-end SPA (aplicativo de página única), uma camada intermediária de API Web do ASP.NET e uma camada de dados de API Web do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="43a37-112">The application has a single-page application (SPA) front end, an ASP.NET Web API middle tier, and an ASP.NET Web API data tier.</span></span>

![Diagrama do aplicativo de exemplo de Aplicativos de API](./media/app-service-api-dotnet-get-started/noauthdiagram.png)

<span data-ttu-id="43a37-114">Aqui está uma captura de tela do front-end [AngularJS](https://angularjs.org/) .</span><span class="sxs-lookup"><span data-stu-id="43a37-114">Here's a screen shot of the [AngularJS](https://angularjs.org/) front end.</span></span>

![Lista de tarefas pendentes do aplicativo de exemplo de Aplicativos de API](./media/app-service-api-dotnet-get-started/todospa.png)

<span data-ttu-id="43a37-116">A solução do Visual Studio inclui três projetos:</span><span class="sxs-lookup"><span data-stu-id="43a37-116">The Visual Studio solution includes three projects:</span></span>

![](./media/app-service-api-dotnet-get-started/projectsinse.png)

* <span data-ttu-id="43a37-117">**ToDoListAngular** ‒ o front-end: um SPA do AngularJS que chama a camada intermediária.</span><span class="sxs-lookup"><span data-stu-id="43a37-117">**ToDoListAngular** - The front end: an AngularJS SPA that calls the middle tier.</span></span>
* <span data-ttu-id="43a37-118">**ToDoListAPI** ‒ a camada intermediária: um projeto de API Web ASP.NET que chama a camada de dados para executar operações CRUD em itens pendentes.</span><span class="sxs-lookup"><span data-stu-id="43a37-118">**ToDoListAPI** - The middle tier: an ASP.NET Web API project that calls the data tier to perform CRUD operations on to-do items.</span></span>
* <span data-ttu-id="43a37-119">**ToDoListDataAPI** ‒ a camada de dados: um projeto de API Web ASP.NET que executa operações CRUD nos itens pendentes.</span><span class="sxs-lookup"><span data-stu-id="43a37-119">**ToDoListDataAPI** - The data tier:  an ASP.NET Web API project that performs CRUD operations on to-do items.</span></span>

<span data-ttu-id="43a37-120">A arquitetura de três camadas é uma das várias arquiteturas que você pode implementar usando aplicativos de API e é usada aqui apenas para fins de demonstração.</span><span class="sxs-lookup"><span data-stu-id="43a37-120">The three-tier architecture is one of many architectures that you can implement by using API Apps and is used here only for demonstration purposes.</span></span> <span data-ttu-id="43a37-121">O código em cada camada é tão simples quanto possível para demonstrar os recursos de aplicativos de API. Por exemplo, a camada de dados usa memória de servidor em vez de um banco de dados como seu mecanismo de persistência.</span><span class="sxs-lookup"><span data-stu-id="43a37-121">The code in each tier is as simple as possible to demonstrate API Apps features; for example, the data tier uses server memory rather than a database as its persistence mechanism.</span></span>

<span data-ttu-id="43a37-122">Ao concluir este tutorial, você terá dois projetos de API Web em execução na nuvem em aplicativos de API do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="43a37-122">On completing this tutorial, you'll have the two Web API projects up and running in the cloud in App Service API apps.</span></span>

<span data-ttu-id="43a37-123">O próximo tutorial na série implanta o front-end do SPA na nuvem.</span><span class="sxs-lookup"><span data-stu-id="43a37-123">The next tutorial in the series deploys the SPA front end to the cloud.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="43a37-124">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="43a37-124">Prerequisites</span></span>
* <span data-ttu-id="43a37-125">API Web do ASP.NET ‒ as instruções do tutorial pressupõem que você tenha um conhecimento básico de como trabalhar com a [API Web 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) do ASP.NET no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="43a37-125">ASP.NET Web API - The tutorial instructions assume you have a basic knowledge of how to work with ASP.NET [Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) in Visual Studio.</span></span>
* <span data-ttu-id="43a37-126">Conta do Azure ‒ você pode [Abrir uma conta do Azure gratuitamente](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) ou [Ativar benefícios de assinante do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="43a37-126">Azure account - You can [Open an Azure account for free](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) or [Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
  
    <span data-ttu-id="43a37-127">Se você quiser ter uma introdução ao Serviço de Aplicativo do Azure antes de se inscrever em uma conta do Azure, vá para [Experimentar o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/).</span><span class="sxs-lookup"><span data-stu-id="43a37-127">If you want to get started with Azure App Service before you sign up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/).</span></span> <span data-ttu-id="43a37-128">Lá, você poderá criar imediatamente um aplicativo de curta duração inicial no Serviço de Aplicativo — **sem exigência de cartão de crédito**e sem compromisso.</span><span class="sxs-lookup"><span data-stu-id="43a37-128">There, you can immediately create a short-lived starter app in App Service — **no credit card required**, and no commitments.</span></span>
* <span data-ttu-id="43a37-129">Visual Studio 2015 com o [SDK do Azure para .NET](https://azure.microsoft.com/downloads/archive-net-downloads/) ‒ o SDK instalará automaticamente o Visual Studio 2015 se você ainda não o tiver.</span><span class="sxs-lookup"><span data-stu-id="43a37-129">Visual Studio 2015 with the [Azure SDK for .NET](https://azure.microsoft.com/downloads/archive-net-downloads/) - The SDK installs Visual Studio 2015 automatically if you don't already have it.</span></span>
  
  * <span data-ttu-id="43a37-130">No Visual Studio, clique em Ajuda -> Sobre o Microsoft Visual Studio e verifique se você tem "Ferramentas do Serviço de Aplicativo do Azure v2.9.1" ou superior instalado.</span><span class="sxs-lookup"><span data-stu-id="43a37-130">In Visual Studio, click Help -> About Microsoft Visual Studio and ensure that you have "Azure App Service Tools v2.9.1" or higher installed.</span></span>
    
    ![Versão das Ferramentas de Aplicativo do Azure](./media/app-service-api-dotnet-get-started/apiversion.png)
    
    > [!NOTE]
    > <span data-ttu-id="43a37-132">Dependendo de quantas dependências de SDK você já tiver no seu computador, a instalação do SDK pode demorar bastante, de vários minutos a meia hora ou mais.</span><span class="sxs-lookup"><span data-stu-id="43a37-132">Depending on how many of the SDK dependencies you already have on your machine, installing the SDK could take a long time, from several minutes to a half hour or more.</span></span>
    > 
    > 

## <a name="download-the-sample-application"></a><span data-ttu-id="43a37-133">Baixar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="43a37-133">Download the sample application</span></span>
1. <span data-ttu-id="43a37-134">Baixe o repositório [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) .</span><span class="sxs-lookup"><span data-stu-id="43a37-134">Download the [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) repository.</span></span>
   
    <span data-ttu-id="43a37-135">Você pode clicar no botão **Baixar ZIP** ou clonar o repositório no computador local.</span><span class="sxs-lookup"><span data-stu-id="43a37-135">You can click the **Download ZIP** button or clone the repository on your local machine.</span></span>
2. <span data-ttu-id="43a37-136">Abra a solução ToDoList no Visual Studio 2015 ou 2013.</span><span class="sxs-lookup"><span data-stu-id="43a37-136">Open the ToDoList solution in Visual Studio 2015 or 2013.</span></span>
   
   1. <span data-ttu-id="43a37-137">Você precisará confiar em cada solução.</span><span class="sxs-lookup"><span data-stu-id="43a37-137">You will need to trust each solution.</span></span>
         <span data-ttu-id="43a37-138">![Aviso de Segurança](./media/app-service-api-dotnet-get-started/securitywarning.png)</span><span class="sxs-lookup"><span data-stu-id="43a37-138">![Security Warning](./media/app-service-api-dotnet-get-started/securitywarning.png)</span></span>
3. <span data-ttu-id="43a37-139">Compile a solução (CTRL + SHIFT + B) para restaurar os pacotes NuGet.</span><span class="sxs-lookup"><span data-stu-id="43a37-139">Build the solution (CTRL + SHIFT + B)  to restore the NuGet packages.</span></span>
   
    <span data-ttu-id="43a37-140">Se quiser ver o aplicativo em operação antes de implantá-lo, você poderá executá-lo localmente.</span><span class="sxs-lookup"><span data-stu-id="43a37-140">If you want to see the application in operation before you deploy it, you can run it locally.</span></span> <span data-ttu-id="43a37-141">Verifique se ToDoListDataAPI é o projeto de inicialização e execute a solução.</span><span class="sxs-lookup"><span data-stu-id="43a37-141">Make sure that ToDoListDataAPI is your startup project and run the solution.</span></span> <span data-ttu-id="43a37-142">Você deve esperar ver um erro HTTP 403 em seu navegador.</span><span class="sxs-lookup"><span data-stu-id="43a37-142">You should expect to see a HTTP 403 error in your browser.</span></span>

## <a name="use-swagger-api-metadata-and-ui"></a><span data-ttu-id="43a37-143">Usar a interface do usuário e metadados de API do Swagger</span><span class="sxs-lookup"><span data-stu-id="43a37-143">Use Swagger API metadata and UI</span></span>
<span data-ttu-id="43a37-144">O suporte a metadados da API 2.0 do [Swagger](http://swagger.io/) é integrado ao Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="43a37-144">Support for [Swagger](http://swagger.io/) 2.0 API metadata is built into Azure App Service.</span></span> <span data-ttu-id="43a37-145">Cada aplicativo de API pode especificar um ponto de extremidade de URL que retorna metadados para a API no formato JSON Swagger.</span><span class="sxs-lookup"><span data-stu-id="43a37-145">Each API app can specify a URL endpoint that returns metadata for the API in Swagger JSON format.</span></span> <span data-ttu-id="43a37-146">Os metadados retornados do ponto de extremidade podem ser usados para gerar código de cliente.</span><span class="sxs-lookup"><span data-stu-id="43a37-146">The metadata returned from that endpoint can be used to generate client code.</span></span>

<span data-ttu-id="43a37-147">Um projeto de API Web ASP.NET pode gerar dinamicamente metadados do Swagger usando o pacote NuGet [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) .</span><span class="sxs-lookup"><span data-stu-id="43a37-147">An ASP.NET Web API project can dynamically generate Swagger metadata by using the [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet package.</span></span> <span data-ttu-id="43a37-148">O pacote NuGet Swashbuckle já está instalado nos projetos ToDoListDataAPI e ToDoListAPI que você baixou.</span><span class="sxs-lookup"><span data-stu-id="43a37-148">The Swashbuckle NuGet package is already installed in the ToDoListDataAPI and ToDoListAPI projects that you downloaded.</span></span>

<span data-ttu-id="43a37-149">Nesta seção do tutorial, você verá os metadados do Swagger 2.0 gerados e experimentará uma interface do usuário de teste baseada nos metadados do Swagger.</span><span class="sxs-lookup"><span data-stu-id="43a37-149">In this section of the tutorial, you look at the generated Swagger 2.0 metadata, and then you try out a test UI that is based on the Swagger metadata.</span></span>

1. <span data-ttu-id="43a37-150">Defina o projeto ToDoListDataAPI (**não** o projeto ToDoListAPI) como o projeto de inicialização.</span><span class="sxs-lookup"><span data-stu-id="43a37-150">Set the ToDoListDataAPI project (**not** the ToDoListAPI project) as the startup project.</span></span>
   
    ![Definir ToDoDataAPI como Projeto de Inicialização](./media/app-service-api-dotnet-get-started/startupproject.png)
2. <span data-ttu-id="43a37-152">Pressione F5 ou clique em **Depurar > Iniciar Depuração** para executar o projeto no modo de depuração.</span><span class="sxs-lookup"><span data-stu-id="43a37-152">Press F5 or click **Debug > Start Debugging** to run the project in debug mode.</span></span>
   
    <span data-ttu-id="43a37-153">O navegador é aberto e mostra a página de erro HTTP 403.</span><span class="sxs-lookup"><span data-stu-id="43a37-153">The browser opens and shows the HTTP 403 error page.</span></span>
3. <span data-ttu-id="43a37-154">Na barra de endereços do navegador, adicione `swagger/docs/v1` no fim da linha e pressione Return.</span><span class="sxs-lookup"><span data-stu-id="43a37-154">In your browser address bar, add `swagger/docs/v1` to the end of the line, and then press Return.</span></span> <span data-ttu-id="43a37-155">(A URL é `http://localhost:45914/swagger/docs/v1`.)</span><span class="sxs-lookup"><span data-stu-id="43a37-155">(The URL is `http://localhost:45914/swagger/docs/v1`.)</span></span>
   
    <span data-ttu-id="43a37-156">Essa é a URL padrão usada pelo Swashbuckle para retornar metadados JSON do Swagger 2.0 para a API.</span><span class="sxs-lookup"><span data-stu-id="43a37-156">This is the default URL used by Swashbuckle to return Swagger 2.0 JSON metadata for the API.</span></span>
   
    <span data-ttu-id="43a37-157">Se você estiver usando o Internet Explorer, o navegador solicitará que baixe um arquivo *v1.json* .</span><span class="sxs-lookup"><span data-stu-id="43a37-157">If you're using Internet Explorer, the browser prompts you to download a *v1.json* file.</span></span>
   
    ![Baixar metadados JSON no IE](./media/app-service-api-dotnet-get-started/iev1json.png)
   
    <span data-ttu-id="43a37-159">Se você estiver usando o Chrome, o Firefox ou o Edge, o navegador exibirá o JSON em sua janela.</span><span class="sxs-lookup"><span data-stu-id="43a37-159">If you're using Chrome, Firefox, or Edge, the browser displays the JSON in the browser window.</span></span> <span data-ttu-id="43a37-160">Navegadores diferentes lidam com o JSON de maneira diferente, e a janela do navegador pode não ser exatamente como o exemplo.</span><span class="sxs-lookup"><span data-stu-id="43a37-160">Different browsers handle JSON differently, and your browser window may not look exactly like the example.</span></span>
   
    ![Metadados JSON no Chrome](./media/app-service-api-dotnet-get-started/chromev1json.png)
   
    <span data-ttu-id="43a37-162">O exemplo a seguir mostra a primeira seção dos metadados do Swagger para a API, com a definição para o método Get.</span><span class="sxs-lookup"><span data-stu-id="43a37-162">The following sample shows the first section of the Swagger metadata for the API, with the definition for the Get method.</span></span> <span data-ttu-id="43a37-163">Esses metadados geram a interface do usuário do Swagger, que você usará nas etapas a seguir e em uma seção posterior do tutorial para gerar o código cliente automaticamente.</span><span class="sxs-lookup"><span data-stu-id="43a37-163">This metadata is what drives the Swagger UI that you use in the following steps, and you use it in a later section of the tutorial to automatically generate client code.</span></span>
   
        {
          "swagger": "2.0",
          "info": {
            "version": "v1",
            "title": "ToDoListDataAPI"
          },
          "host": "localhost:45914",
          "schemes": [ "http" ],
          "paths": {
            "/api/ToDoList": {
              "get": {
                "tags": [ "ToDoList" ],
                "operationId": "ToDoList_GetByOwner",
                "consumes": [ ],
                "produces": [ "application/json", "text/json", "application/xml", "text/xml" ],
                "parameters": [
                  {
                    "name": "owner",
                    "in": "query",
                    "required": true,
                    "type": "string"
                  }
                ],
                "responses": {
                  "200": {
                    "description": "OK",
                    "schema": {
                      "type": "array",
                      "items": { "$ref": "#/definitions/ToDoItem" }
                    }
                  }
                },
                "deprecated": false
              },
4. <span data-ttu-id="43a37-164">Feche o navegador e interrompa a depuração do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="43a37-164">Close the browser and stop Visual Studio debugging.</span></span>
5. <span data-ttu-id="43a37-165">No projeto ToDoListDataAPI no **Gerenciador de Soluções**, abra o arquivo *App_Start\SwaggerConfig.cs*, role para baixo até a linha 174 e remova o comentário do código a seguir.</span><span class="sxs-lookup"><span data-stu-id="43a37-165">In the ToDoListDataAPI project in **Solution Explorer**, open the *App_Start\SwaggerConfig.cs* file, then scroll down to line 174 and uncomment the following code.</span></span>
   
        /*
            })
        .EnableSwaggerUi(c =>
            {
        */
   
    <span data-ttu-id="43a37-166">O arquivo *SwaggerConfig.cs* é criado quando você instala o pacote do Swashbuckle em um projeto.</span><span class="sxs-lookup"><span data-stu-id="43a37-166">The *SwaggerConfig.cs* file is created when you install the Swashbuckle package in a project.</span></span> <span data-ttu-id="43a37-167">O arquivo fornece várias maneiras de se configurar o Swashbuckle.</span><span class="sxs-lookup"><span data-stu-id="43a37-167">The file provides a number of ways to configure Swashbuckle.</span></span>
   
    <span data-ttu-id="43a37-168">O código que você removeu habilita a interface do usuário do Swagger que será usada nas etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="43a37-168">The code you've uncommented enables the Swagger UI that you use in the following steps.</span></span> <span data-ttu-id="43a37-169">Quando você cria um projeto de API Web usando o modelo de projeto de aplicativo de API, o código é comentado por padrão como medida de segurança.</span><span class="sxs-lookup"><span data-stu-id="43a37-169">When you create a Web API project by using the API app project template, this code is commented out by default as a security measure.</span></span>
6. <span data-ttu-id="43a37-170">Execute o projeto novamente.</span><span class="sxs-lookup"><span data-stu-id="43a37-170">Run the project again.</span></span>
7. <span data-ttu-id="43a37-171">Na barra de endereços do navegador, adicione `swagger` no fim da linha e pressione Return.</span><span class="sxs-lookup"><span data-stu-id="43a37-171">In your browser address bar, add `swagger` to the end of the line, and then press Return.</span></span> <span data-ttu-id="43a37-172">(A URL é `http://localhost:45914/swagger`.)</span><span class="sxs-lookup"><span data-stu-id="43a37-172">(The URL is `http://localhost:45914/swagger`.)</span></span>
8. <span data-ttu-id="43a37-173">Quando for exibida a página de interface do usuário do Swagger, clique em **ToDoList** para ver os métodos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="43a37-173">When the Swagger UI page appears, click **ToDoList** to see the methods available.</span></span>
   
    ![Métodos disponíveis na interface do usuário do Swagger](./media/app-service-api-dotnet-get-started/methods.png)
9. <span data-ttu-id="43a37-175">Clique no primeiro botão **Obter** na lista.</span><span class="sxs-lookup"><span data-stu-id="43a37-175">Click the first **Get** button in the list.</span></span>
10. <span data-ttu-id="43a37-176">Na seção **Parâmetros**, digite um asterisco como o valor do parâmetro `owner` e clique em **Experimentar**.</span><span class="sxs-lookup"><span data-stu-id="43a37-176">In the **Parameters** section, enter an asterisk as the value of the `owner` parameter, and then click **Try it out**.</span></span>
    
    <span data-ttu-id="43a37-177">Quando você adicionar a autenticação nos tutoriais posteriores, a camada intermediária fornecerá a ID de usuário real para a camada de dados.</span><span class="sxs-lookup"><span data-stu-id="43a37-177">When you add authentication in later tutorials, the middle tier will provide the actual user ID to the data tier.</span></span> <span data-ttu-id="43a37-178">Por enquanto, todas as tarefas terão um asterisco como sua ID de proprietário, enquanto o aplicativo é executado sem autenticação habilitada.</span><span class="sxs-lookup"><span data-stu-id="43a37-178">For now, all tasks will have asterisk as their owner ID while the application runs without authentication enabled.</span></span>
    
    ![Teste da interface do usuário do Swagger](./media/app-service-api-dotnet-get-started/gettryitout1.png)
    
    <span data-ttu-id="43a37-180">A interface do usuário do Swagger chama o método Get ToDoList e exibe o código de resposta e os resultados JSON.</span><span class="sxs-lookup"><span data-stu-id="43a37-180">The Swagger UI calls the ToDoList Get method and displays the response code and JSON results.</span></span>
    
    ![Resultados do teste da interface do usuário do Swagger](./media/app-service-api-dotnet-get-started/gettryitout.png)
11. <span data-ttu-id="43a37-182">Clique em **Postar** e marque a caixa em **Esquema de Modelo**.</span><span class="sxs-lookup"><span data-stu-id="43a37-182">Click **Post**, and then click the box under **Model Schema**.</span></span>
    
    <span data-ttu-id="43a37-183">Clicar no esquema de modelo preencherá previamente a caixa de entrada onde é possível especificar o valor do parâmetro para o método Post.</span><span class="sxs-lookup"><span data-stu-id="43a37-183">Clicking the model schema prefills the input box where you can specify the parameter value for the Post method.</span></span> <span data-ttu-id="43a37-184">(Se isso não funcionar no Internet Explorer, use um navegador diferente ou insira o valor do parâmetro manualmente na próxima etapa).</span><span class="sxs-lookup"><span data-stu-id="43a37-184">(If this doesn't work in Internet Explorer, use a different browser or enter the parameter value manually in the next step.)</span></span>  
    
    ![Postagem do teste da interface do usuário do Swagger](./media/app-service-api-dotnet-get-started/post.png)
12. <span data-ttu-id="43a37-186">Altere o JSON na caixa de entrada do parâmetro `todo` para que ele seja semelhante ao seguinte exemplo ou substitua-o por seu próprio texto de descrição:</span><span class="sxs-lookup"><span data-stu-id="43a37-186">Change the JSON in the `todo` parameter input box so that it looks like the following example, or substitute your own description text:</span></span>
    
        {
          "ID": 2,
          "Description": "buy the dog a toy",
          "Owner": "*"
        }
13. <span data-ttu-id="43a37-187">Clique em **Experimentar**.</span><span class="sxs-lookup"><span data-stu-id="43a37-187">Click **Try it out**.</span></span>
    
    <span data-ttu-id="43a37-188">A API de ToDoList retorna um código de resposta HTTP 204 que indica êxito.</span><span class="sxs-lookup"><span data-stu-id="43a37-188">The ToDoList API returns an HTTP 204 response code that indicates success.</span></span>
14. <span data-ttu-id="43a37-189">Clique no primeiro botão **Obter** e, nessa seção da página, clique no botão **Experimentar**.</span><span class="sxs-lookup"><span data-stu-id="43a37-189">Click the first **Get** button, and then in that section of the page click the **Try it out** button.</span></span>
    
    <span data-ttu-id="43a37-190">A resposta do método Get agora inclui o novo item pendente.</span><span class="sxs-lookup"><span data-stu-id="43a37-190">The Get method response now includes the new to do item.</span></span>
15. <span data-ttu-id="43a37-191">Opcional: Também experimente os métodos Put, Delete e Get by ID.</span><span class="sxs-lookup"><span data-stu-id="43a37-191">Optional: Try also the Put, Delete, and Get by ID methods.</span></span>
16. <span data-ttu-id="43a37-192">Feche o navegador e interrompa a depuração do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="43a37-192">Close the browser and stop Visual Studio debugging.</span></span>

<span data-ttu-id="43a37-193">O Swashbuckle funciona com qualquer projeto de API Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="43a37-193">Swashbuckle works with any ASP.NET Web API project.</span></span> <span data-ttu-id="43a37-194">Se você deseja adicionar a geração de metadados de Swagger a um projeto existente, instale o pacote Swashbuckle.</span><span class="sxs-lookup"><span data-stu-id="43a37-194">If you want to add Swagger metadata generation to an existing project, just install the Swashbuckle package.</span></span>

> [!NOTE]
> <span data-ttu-id="43a37-195">Os metadados do Swagger incluem uma ID exclusiva para cada operação da API.</span><span class="sxs-lookup"><span data-stu-id="43a37-195">Swagger metadata includes a unique ID for each API operation.</span></span> <span data-ttu-id="43a37-196">Por padrão, o Swashbuckle pode gerar IDs de operação do Swagger duplicadas para os métodos do controlador da API Web.</span><span class="sxs-lookup"><span data-stu-id="43a37-196">By default, Swashbuckle may generate duplicate Swagger operation IDs for your Web API controller methods.</span></span> <span data-ttu-id="43a37-197">Isso acontecerá se o controlador tiver métodos HTTP sobrecarregados, como `Get()` e `Get(id)`.</span><span class="sxs-lookup"><span data-stu-id="43a37-197">This happens if your controller has overloaded HTTP methods, such as `Get()` and `Get(id)`.</span></span> <span data-ttu-id="43a37-198">Para obter informações sobre como lidar com sobrecargas, consulte [Personalizar definições de API geradas pelo Swashbuckle](app-service-api-dotnet-swashbuckle-customize.md).</span><span class="sxs-lookup"><span data-stu-id="43a37-198">For information about how to handle overloads, see [Customize Swashbuckle-generated API definitions](app-service-api-dotnet-swashbuckle-customize.md).</span></span> <span data-ttu-id="43a37-199">Se você criar um projeto de API Web no Visual Studio usando o modelo de Aplicativo de API do Azure, o código que gera IDs de operação exclusivas será adicionado automaticamente ao arquivo *SwaggerConfig.cs* .</span><span class="sxs-lookup"><span data-stu-id="43a37-199">If you create a Web API project in Visual Studio by using the Azure API App template, code that generates unique operation IDs is automatically added to the *SwaggerConfig.cs* file.</span></span>  
> 
> 

## <span data-ttu-id="43a37-200"><a id="createapiapp"></a> Criar um aplicativo de API no Azure e implantar código nele</span><span class="sxs-lookup"><span data-stu-id="43a37-200"><a id="createapiapp"></a> Create an API app in Azure and deploy code to it</span></span>
<span data-ttu-id="43a37-201">Nesta seção, você usará as ferramentas do Azure integradas no assistente **Publicar na Web** do Visual Studio para criar um novo aplicativo de API no Azure.</span><span class="sxs-lookup"><span data-stu-id="43a37-201">In this section, you use Azure tools that are integrated into the Visual Studio **Publish Web** wizard to create a new API app in Azure.</span></span> <span data-ttu-id="43a37-202">Em seguida, implante o projeto ToDoListDataAPI no novo aplicativo de API e chame a API executando a interface do usuário do Swagger.</span><span class="sxs-lookup"><span data-stu-id="43a37-202">Then you deploy the ToDoListDataAPI project to the new API app and call the API by running the Swagger UI.</span></span>

1. <span data-ttu-id="43a37-203">No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto ToDoListDataAPI e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="43a37-203">In **Solution Explorer**, right-click the ToDoListDataAPI project, and then click **Publish**.</span></span>
   
    ![Clicar em Publicar no Visual Studio](./media/app-service-api-dotnet-get-started/pubinmenu.png)
2. <span data-ttu-id="43a37-205">Na etapa **Perfil** do assistente **Publicar na Web**, clique em **Serviço de Aplicativo do Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="43a37-205">In the **Profile** step of the **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
   
   ![Clicar no Serviço de Aplicativo do Azure em Publicar Web](./media/app-service-api-dotnet-get-started/selectappservice.png)
3. <span data-ttu-id="43a37-207">Entre em sua conta do Azure, se ainda não tiver feito isso, ou atualize suas credenciais se elas tiverem expirado.</span><span class="sxs-lookup"><span data-stu-id="43a37-207">Sign in to your Azure account if you have not already done so, or refresh your credentials if they're expired.</span></span>
4. <span data-ttu-id="43a37-208">Na caixa de diálogo Serviço de Aplicativo, escolha a **Assinatura** do Azure que você deseja usar e clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="43a37-208">In the App Service dialog box, choose the Azure **Subscription** you want to use, and then click **New**.</span></span>
   
    ![Clicar em Novo no diálogo Serviço de Aplicativo](./media/app-service-api-dotnet-get-started/clicknew.png)
   
    <span data-ttu-id="43a37-210">A guia **Hospedagem** da caixa de diálogo **Criar Serviço de Aplicativo** será exibida.</span><span class="sxs-lookup"><span data-stu-id="43a37-210">The **Hosting** tab of the **Create App Service** dialog box appears.</span></span>
   
    <span data-ttu-id="43a37-211">Como você está implantando um projeto de API Web com o Swashbuckle instalado, o Visual Studio pressupõe que você queira criar Aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="43a37-211">Because you're deploying a Web API project that has Swashbuckle installed, Visual Studio assumes that you want to create an API App.</span></span> <span data-ttu-id="43a37-212">Isso é indicado pelo título **Nome do Aplicativo de API** e pelo fato de a lista suspensa **Alterar Tipo** estar definida para **Aplicativo de API**.</span><span class="sxs-lookup"><span data-stu-id="43a37-212">This is indicated by the **API App Name** title and by the fact that the **Change Type** drop-down list is set to **API App**.</span></span>
   
    ![Tipo de aplicativo no diálogo Serviço de Aplicativos](./media/app-service-api-dotnet-get-started/apptype.png)
5. <span data-ttu-id="43a37-214">Insira um **Nome de Aplicativo de API** que seja exclusivo no domínio *azurewebsites.net* .</span><span class="sxs-lookup"><span data-stu-id="43a37-214">Enter an **API App Name** that is unique in the *azurewebsites.net* domain.</span></span> <span data-ttu-id="43a37-215">Você pode aceitar o nome padrão que o Visual Studio propõe.</span><span class="sxs-lookup"><span data-stu-id="43a37-215">You can accept the default name that Visual Studio proposes.</span></span>
   
    <span data-ttu-id="43a37-216">Se inserir um nome que outra pessoa já tenha usado, você verá um ponto de exclamação vermelho à direita.</span><span class="sxs-lookup"><span data-stu-id="43a37-216">If you enter a name that someone else has already used, you see a red exclamation mark to the right.</span></span>
   
    <span data-ttu-id="43a37-217">A URL do aplicativo de API será `{API app name}.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="43a37-217">The URL of the API app will be `{API app name}.azurewebsites.net`.</span></span>
6. <span data-ttu-id="43a37-218">Na lista suspensa **Grupo de Recursos**, clique em **Novo** e insira "ToDoListGroup" ou outro nome, se preferir.</span><span class="sxs-lookup"><span data-stu-id="43a37-218">In the **Resource Group** drop-down, click **New**, and then enter "ToDoListGroup" or another name if you prefer.</span></span>
   
    <span data-ttu-id="43a37-219">Um grupo de recursos é uma coleção de recursos do Azure, como aplicativos de API, bancos de dados, VMs e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="43a37-219">A resource group is a collection of Azure resources such as API apps, databases, VMs, and so forth.</span></span>    <span data-ttu-id="43a37-220">Para este tutorial, é melhor criar um novo grupo de recursos porque isso facilitará a exclusão de todos os recursos do Azure criados para o tutorial em uma única etapa.</span><span class="sxs-lookup"><span data-stu-id="43a37-220">For this tutorial, it's best to create a new resource group because that makes it easy to delete in one step all the Azure resources that you create for the tutorial.</span></span>
   
    <span data-ttu-id="43a37-221">Essa caixa permite que você selecione um [grupo de recursos](../azure-resource-manager/resource-group-overview.md) existente ou crie um novo digitando um nome diferente de qualquer grupo de recursos existente na assinatura.</span><span class="sxs-lookup"><span data-stu-id="43a37-221">This box lets you select an existing [resource group](../azure-resource-manager/resource-group-overview.md) or create a new one by typing in a name that is different from any existing resource group in your subscription.</span></span>
7. <span data-ttu-id="43a37-222">Clique no botão **Novo** ao lado da lista suspensa **Plano do Serviço de Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="43a37-222">Click the **New** button next to the **App Service Plan** drop-down.</span></span>
   
    <span data-ttu-id="43a37-223">A captura de tela mostra valores de exemplo para o **Nome do Aplicativo de API**, **Assinatura** e **Grupo de Recursos**. Seus valores serão diferentes.</span><span class="sxs-lookup"><span data-stu-id="43a37-223">The screen shot shows sample values for **API App Name**, **Subscription**, and **Resource Group** -- your values will be different.</span></span>
   
    ![Criar caixa de diálogo do Serviço de Aplicativo](./media/app-service-api-dotnet-get-started/createas.png)
   
    <span data-ttu-id="43a37-225">Nas etapas a seguir, você criará um plano de Serviço de Aplicativo para o novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="43a37-225">In the following steps you create an App Service plan for the new resource group.</span></span> <span data-ttu-id="43a37-226">Um plano de Serviço de Aplicativo especifica os recursos de computação em que seu aplicativo de API é executado.</span><span class="sxs-lookup"><span data-stu-id="43a37-226">An App Service plan specifies the compute resources that your API app runs on.</span></span> <span data-ttu-id="43a37-227">Por exemplo, se você escolher a camada gratuita, seu aplicativo de API será executado em VMs compartilhadas, enquanto que para algumas camadas pagas, ele é executado em VMs dedicadas.</span><span class="sxs-lookup"><span data-stu-id="43a37-227">For example, if you choose the free tier, your API app runs on shared VMs, while for some paid tiers it runs on dedicated VMs.</span></span> <span data-ttu-id="43a37-228">Para saber mais sobre os planos do Serviço de Aplicativo, consulte a [Visão geral dos planos do Serviço de Aplicativo](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="43a37-228">For information about App Service plans, see [App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
8. <span data-ttu-id="43a37-229">Na caixa de diálogo **Configurar Plano do Serviço de Aplicativo** , insira "ToDoListPlan" ou outro nome, se preferir.</span><span class="sxs-lookup"><span data-stu-id="43a37-229">In the **Configure App Service Plan** dialog, enter "ToDoListPlan" or another name if you prefer.</span></span>
9. <span data-ttu-id="43a37-230">Na lista suspensa **Local** , escolha o local mais próximo de você.</span><span class="sxs-lookup"><span data-stu-id="43a37-230">In the **Location** drop-down list, choose the location that is closest to you.</span></span>
   
    <span data-ttu-id="43a37-231">Essa configuração especifica em qual datacenter do Azure o aplicativo será executado.</span><span class="sxs-lookup"><span data-stu-id="43a37-231">This setting specifies which Azure datacenter your app will run in.</span></span> <span data-ttu-id="43a37-232">Escolha um local perto de você para minimizar a [latência](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090).</span><span class="sxs-lookup"><span data-stu-id="43a37-232">Choose a location close to you to minimize [latency](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090).</span></span>
10. <span data-ttu-id="43a37-233">Na lista suspensa **Tamanho**, clique em **Gratuito**.</span><span class="sxs-lookup"><span data-stu-id="43a37-233">In the **Size** drop-down, click **Free**.</span></span>
    
    <span data-ttu-id="43a37-234">Neste tutorial, o tipo de preço gratuito permitirá um desempenho suficiente.</span><span class="sxs-lookup"><span data-stu-id="43a37-234">For this tutorial, the free pricing tier will provide sufficient performance.</span></span>
11. <span data-ttu-id="43a37-235">Na caixa de diálogo **Configurar o Plano do Serviço de Aplicativo**, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="43a37-235">In the **Configure App Service Plan** dialog, click **OK**.</span></span>
    
    ![Clicar em OK em Configurar Plano do Serviço de Aplicativos](./media/app-service-api-dotnet-get-started/configasp.png)
12. <span data-ttu-id="43a37-237">Na caixa de diálogo **Criar Serviço de Aplicativo**, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="43a37-237">In the **Create App Service** dialog box, click **Create**.</span></span>
    
    ![Clicar em Criar no diálogo Criar Serviço de Aplicativos](./media/app-service-api-dotnet-get-started/clickcreate.png)
    
    <span data-ttu-id="43a37-239">O Visual Studio cria o aplicativo de API e um perfil de publicação que tem todas as configurações necessárias para o aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="43a37-239">Visual Studio creates the API app and a publish profile that has all of the required settings for the API app.</span></span> <span data-ttu-id="43a37-240">Em seguida, ele abre o assistente **Publicar na Web** , que você usará para implantar o projeto.</span><span class="sxs-lookup"><span data-stu-id="43a37-240">Then it opens the **Publish Web** wizard, which you'll use to deploy the project.</span></span>
    
    <span data-ttu-id="43a37-241">O assistente **Publicar na Web** será aberto na guia **Conexão** (mostrada abaixo).</span><span class="sxs-lookup"><span data-stu-id="43a37-241">The **Publish Web** wizard opens on the **Connection** tab (shown below).</span></span>
    
    <span data-ttu-id="43a37-242">Na guia **Conexão**, as configurações **Servidor** e **Nome do site** apontam para seu aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="43a37-242">On the **Connection** tab, the **Server** and **Site name** settings point to your API app.</span></span> <span data-ttu-id="43a37-243">O **Nome de usuário** e a **Senha** são credenciais de implantação que o Azure cria para você.</span><span class="sxs-lookup"><span data-stu-id="43a37-243">The **User name** and **Password** are deployment credentials that Azure creates for you.</span></span> <span data-ttu-id="43a37-244">Após a implantação, o Visual Studio abre um navegador na **URL de Destino** (essa é a única finalidade da **URL de Destino**).</span><span class="sxs-lookup"><span data-stu-id="43a37-244">After deployment, Visual Studio opens a browser to the **Destination URL** (that's the only purpose for **Destination URL**).</span></span>  
13. <span data-ttu-id="43a37-245">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="43a37-245">Click **Next**.</span></span>
    
    ![Clique em Avançar na guia Conexão de Publicar Web](./media/app-service-api-dotnet-get-started/connnext.png)
    
    <span data-ttu-id="43a37-247">A próxima guia é **Configurações** (mostrada abaixo).</span><span class="sxs-lookup"><span data-stu-id="43a37-247">The next tab is the **Settings** tab (shown below).</span></span> <span data-ttu-id="43a37-248">Aqui, você pode alterar a guia de configuração da compilação para implantar uma compilação de depuração para a [depuração remota](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug).</span><span class="sxs-lookup"><span data-stu-id="43a37-248">Here you can change the build configuration tab to deploy a debug build for [remote debugging](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug).</span></span> <span data-ttu-id="43a37-249">A guia também oferece várias **Opções de Publicação do Arquivo**:</span><span class="sxs-lookup"><span data-stu-id="43a37-249">The tab also offers several **File Publish Options**:</span></span>
    
    * <span data-ttu-id="43a37-250">Remover os arquivos adicionais no destino</span><span class="sxs-lookup"><span data-stu-id="43a37-250">Remove additional files at destination</span></span>
    * <span data-ttu-id="43a37-251">Pré-compilar durante a publicação</span><span class="sxs-lookup"><span data-stu-id="43a37-251">Precompile during publishing</span></span>
    * <span data-ttu-id="43a37-252">Excluir arquivos da pasta App_Data</span><span class="sxs-lookup"><span data-stu-id="43a37-252">Exclude files from the App_Data folder</span></span>
    
    <span data-ttu-id="43a37-253">Para este tutorial, você não precisará de qualquer uma delas.</span><span class="sxs-lookup"><span data-stu-id="43a37-253">For this tutorial you don't need any of these.</span></span> <span data-ttu-id="43a37-254">Para obter explicações detalhadas sobre o que fazem, confira [Como implantar um projeto Web usando a publicação de um clique no Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx).</span><span class="sxs-lookup"><span data-stu-id="43a37-254">For detailed explanations of what they do, see [How to: Deploy a Web Project Using One-Click Publish in Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx).</span></span>
14. <span data-ttu-id="43a37-255">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="43a37-255">Click **Next**.</span></span>
    
    ![Clique em Avançar na guia Configurações de Publicar Web](./media/app-service-api-dotnet-get-started/settingsnext.png)
    
    <span data-ttu-id="43a37-257">A próxima guia é **Visualização** (mostrada abaixo), que oferece a oportunidade de ver quais arquivos serão copiados do projeto para o aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="43a37-257">Next is the **Preview** tab (shown below), which gives you an opportunity to see what files are going to be copied from your project to the API app.</span></span> <span data-ttu-id="43a37-258">Quando você estiver implantando um projeto para um aplicativo de API no qual já tenha implantado antes, somente os arquivos alterados serão copiados.</span><span class="sxs-lookup"><span data-stu-id="43a37-258">When you're deploying a project to an API app that you already deployed to earlier, only changed files are copied.</span></span> <span data-ttu-id="43a37-259">Se quiser ver uma lista do que será copiado, você poderá clicar no botão **Iniciar Visualização** .</span><span class="sxs-lookup"><span data-stu-id="43a37-259">If you want to see a list of what will be copied, you can click the **Start Preview** button.</span></span>
15. <span data-ttu-id="43a37-260">Clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="43a37-260">Click **Publish**.</span></span>
    
    ![Clicar em Publicar na guia Visualização de Publicar Web](./media/app-service-api-dotnet-get-started/clickpublish.png)
    
    <span data-ttu-id="43a37-262">O Visual Studio implanta o projeto ToDoListDataAPI para o novo aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="43a37-262">Visual Studio deploys the ToDoListDataAPI project to the new API app.</span></span> <span data-ttu-id="43a37-263">A janela **Saída** registrará uma implantação bem-sucedida, e uma página "criada com êxito" será exibida em uma janela do navegador aberta para a URL do aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="43a37-263">The **Output** window logs successful deployment, and a "successfully created" page appears in a browser window opened to the URL of the API app.</span></span>
    
    ![Implantação bem-sucedida da janela de saída](./media/app-service-api-dotnet-get-started/deploymentoutput.png)
    
    ![Página Novo aplicativo de API criado com êxito](./media/app-service-api-dotnet-get-started/appcreated.png)
16. <span data-ttu-id="43a37-266">Adicione "swagger" à URL na barra de endereço do navegador e pressione Enter.</span><span class="sxs-lookup"><span data-stu-id="43a37-266">Add "swagger" to the URL in the browser's address bar, and then press Enter.</span></span> <span data-ttu-id="43a37-267">(A URL é `http://{apiappname}.azurewebsites.net/swagger`.)</span><span class="sxs-lookup"><span data-stu-id="43a37-267">(The URL is `http://{apiappname}.azurewebsites.net/swagger`.)</span></span>
    
    <span data-ttu-id="43a37-268">O navegador exibe a mesma interface do usuário do Swagger que você viu anteriormente, mas agora ela está em execução na nuvem.</span><span class="sxs-lookup"><span data-stu-id="43a37-268">The browser displays the same Swagger UI that you saw earlier, but now it's running in the cloud.</span></span> <span data-ttu-id="43a37-269">Experimente o método Get e você verá que voltou aos itens de tarefas pendentes 2 padrão.</span><span class="sxs-lookup"><span data-stu-id="43a37-269">Try out the Get method, and you see that you're back to the default 2 to-do items.</span></span> <span data-ttu-id="43a37-270">As alterações feitas anteriormente foram salvas na memória do computador local.</span><span class="sxs-lookup"><span data-stu-id="43a37-270">The changes you made earlier were saved in memory in the local machine.</span></span>
17. <span data-ttu-id="43a37-271">Abra o [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="43a37-271">Open the [Azure portal](https://portal.azure.com/).</span></span>
    
    <span data-ttu-id="43a37-272">O portal do Azure é uma interface da Web para gerenciar recursos do Azure, como aplicativos de API.</span><span class="sxs-lookup"><span data-stu-id="43a37-272">The Azure portal is a web interface for managing Azure resources such as API apps.</span></span>
18. <span data-ttu-id="43a37-273">Clique em **Mais Serviços > Serviços de Aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="43a37-273">Click **More Services > App Services**.</span></span>
    
    ![Procurar Serviços de Aplicativos](./media/app-service-api-dotnet-get-started/browseas.png)
19. <span data-ttu-id="43a37-275">Na folha **Serviços de Aplicativos** , localize e clique no novo aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="43a37-275">In the **App Services** blade, find and click your new API app.</span></span> <span data-ttu-id="43a37-276">(No portal do Azure, as janelas abertas à direita são chamadas de *folhas*.)</span><span class="sxs-lookup"><span data-stu-id="43a37-276">(In the Azure portal, windows that open to the right are called *blades*.)</span></span>
    
    ![Folha Serviços de Aplicativos](./media/app-service-api-dotnet-get-started/choosenewapiappinportal.png)
    
    <span data-ttu-id="43a37-278">Duas folhas são abertas.</span><span class="sxs-lookup"><span data-stu-id="43a37-278">Two blades open.</span></span> <span data-ttu-id="43a37-279">Uma folha tem uma visão geral do aplicativo de API e outra tem uma longa lista de configurações que você pode exibir e alterar.</span><span class="sxs-lookup"><span data-stu-id="43a37-279">One blade has an overview of the API app, and one has a long list of settings that you can view and change.</span></span>
20. <span data-ttu-id="43a37-280">Na folha **Configurações**, localize a seção **API** e clique em **Definição da API**.</span><span class="sxs-lookup"><span data-stu-id="43a37-280">In the **Settings** blade, find the **API** section and click **API Definition**.</span></span>
    
    ![Definição de API na folha Configurações](./media/app-service-api-dotnet-get-started/apidefinsettings.png)
    
    <span data-ttu-id="43a37-282">A folha **Definição da API** permite que você especifique a URL para retornar os metadados do Swagger 2.0 no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="43a37-282">The **API Definition** blade lets you specify the URL that returns Swagger 2.0 metadata in JSON format.</span></span> <span data-ttu-id="43a37-283">Quando o Visual Studio cria o aplicativo de API, define a URL de definição da API com o valor padrão para os metadados gerados pelo Swashbuckle vistos anteriormente, que é a URL base do aplicativo de API mais `/swagger/docs/v1`.</span><span class="sxs-lookup"><span data-stu-id="43a37-283">When Visual Studio creates the API app, it sets the API definition URL to the default value for Swashbuckle-generated metadata that you saw earlier, which is the API app's base URL plus `/swagger/docs/v1`.</span></span>
    
    ![URL de definição da API](./media/app-service-api-dotnet-get-started/apidefurl.png)
    
    <span data-ttu-id="43a37-285">Quando você seleciona um aplicativo de API para gerar código para ele, o Visual Studio recupera os metadados dessa URL.</span><span class="sxs-lookup"><span data-stu-id="43a37-285">When you select an API app to generate client code for it, Visual Studio retrieves the metadata from this URL.</span></span>

## <span data-ttu-id="43a37-286"><a id="codegen"></a> Gerar o código de cliente para a camada de dados</span><span class="sxs-lookup"><span data-stu-id="43a37-286"><a id="codegen"></a> Generate client code for the data tier</span></span>
<span data-ttu-id="43a37-287">Uma das vantagens da integração do Swagger a aplicativos de API do Azure é a geração automática de código.</span><span class="sxs-lookup"><span data-stu-id="43a37-287">One of the advantages of integrating Swagger into Azure API apps is automatic code generation.</span></span> <span data-ttu-id="43a37-288">As classes de cliente geradas tornam mais fácil escrever código para chamar um aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="43a37-288">Generated client classes make it easier to write code that calls an API app.</span></span>

<span data-ttu-id="43a37-289">O projeto ToDoListAPI já tem o código de cliente gerado, mas, nas etapas a seguir, você o excluirá e recriará para ver como fazer a geração de código.</span><span class="sxs-lookup"><span data-stu-id="43a37-289">The ToDoListAPI project already has the generated client code, but in the following steps you'll delete it and regenerate it to see how to do the code generation.</span></span>

1. <span data-ttu-id="43a37-290">No **Gerenciador de Soluções**do Visual Studio, no projeto ToDoListAPI, exclua a pasta *ToDoListDataAPI* .</span><span class="sxs-lookup"><span data-stu-id="43a37-290">In Visual Studio **Solution Explorer**, in the ToDoListAPI project, delete the *ToDoListDataAPI* folder.</span></span> <span data-ttu-id="43a37-291">**Cuidado: exclua apenas a pasta, não o projeto ToDoListDataAPI.**</span><span class="sxs-lookup"><span data-stu-id="43a37-291">**Caution: Delete only the folder, not the ToDoListDataAPI project.**</span></span>
   
    ![Excluir código de cliente gerado](./media/app-service-api-dotnet-get-started/deletecodegen.png)
   
    <span data-ttu-id="43a37-293">Essa pasta foi criada usando o processo de geração de código que você está prestes a seguir.</span><span class="sxs-lookup"><span data-stu-id="43a37-293">This folder was created by using the code generation process that you're about to go through.</span></span>
2. <span data-ttu-id="43a37-294">Clique com o botão direito do mouse no projeto ToDoListAPI e clique em **Adicionar > Cliente da API REST**.</span><span class="sxs-lookup"><span data-stu-id="43a37-294">Right-click the ToDoListAPI project, and then click **Add > REST API Client**.</span></span>
   
    ![Adicionar o cliente da API REST ao Visual Studio](./media/app-service-api-dotnet-get-started/codegenmenu.png)
3. <span data-ttu-id="43a37-296">Na caixa de diálogo **Adicionar Cliente da API REST**, clique em **URL do Swagger** e **Selecionar Ativo do Azure**.</span><span class="sxs-lookup"><span data-stu-id="43a37-296">In the **Add REST API Client** dialog box, click **Swagger URL**, and then click **Select Azure Asset**.</span></span>
   
    ![Selecionar Ativo do Azure](./media/app-service-api-dotnet-get-started/codegenbrowse.png)
4. <span data-ttu-id="43a37-298">Na caixa de diálogo **Serviço de Aplicativo**, expanda o grupo de recursos que você está usando neste tutorial, selecione o aplicativo de API e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="43a37-298">In the **App Service** dialog box, expand the resource group you're using for this tutorial and select your API app, and then click **OK**.</span></span>
   
    ![Selecionar aplicativo de API para geração de código](./media/app-service-api-dotnet-get-started/codegenselect.png)
   
    <span data-ttu-id="43a37-300">Observe que, quando você retornar para o diálogo **Adicionar Cliente da API REST** , a caixa de texto terá sido preenchida com o valor de URL de definição de API vista anteriormente no portal.</span><span class="sxs-lookup"><span data-stu-id="43a37-300">Notice that when you return to the **Add REST API Client** dialog, the text box has been filled in with the API definition URL value that you saw earlier in the portal.</span></span>
   
    ![URL de definição da API](./media/app-service-api-dotnet-get-started/codegenurlplugged.png)
   
   > [!TIP]
   > <span data-ttu-id="43a37-302">Uma maneira alternativa de obter metadados para a geração de código é inserir a URL diretamente em vez de passar pelo diálogo Procurar.</span><span class="sxs-lookup"><span data-stu-id="43a37-302">An alternative way to get metadata for code generation is to enter the URL directly instead of going through the browse dialog.</span></span> <span data-ttu-id="43a37-303">Ou então, se quiser gerar o código de cliente antes de implantar o Azure, você poderá executar o projeto de API Web localmente, ir para a URL que fornece o arquivo JSON Swagger, salvar o arquivo e usar a opção **Selecionar um arquivo de metadados do Swagger** .</span><span class="sxs-lookup"><span data-stu-id="43a37-303">Or if you want to generate client code before deploying to Azure, you could run the Web API project locally, go to the URL that provides the Swagger JSON file, save the file, and use the **Select an existing Swagger metadata file** option.</span></span>
   > 
   > 
5. <span data-ttu-id="43a37-304">Na caixa de diálogo **Adicionar Cliente da API REST**, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="43a37-304">In the **Add REST API Client** dialog box, click **OK**.</span></span>
   
    <span data-ttu-id="43a37-305">O Visual Studio cria uma pasta com o nome do aplicativo de API e gera classes de cliente.</span><span class="sxs-lookup"><span data-stu-id="43a37-305">Visual Studio creates a folder named after the API app and generates client classes.</span></span>
   
    ![Arquivos de código para cliente gerado](./media/app-service-api-dotnet-get-started/codegenfiles.png)
6. <span data-ttu-id="43a37-307">No projeto ToDoListAPI, abra *Controllers\ToDoListController.cs* para ver o código na linha 40 que chama a API usando o cliente gerado.</span><span class="sxs-lookup"><span data-stu-id="43a37-307">In the ToDoListAPI project, open *Controllers\ToDoListController.cs* to see the code at line 40  that calls the API by using the generated client.</span></span>
   
    <span data-ttu-id="43a37-308">O trecho a seguir mostra como o código instancia o objeto de cliente e chama o método Get.</span><span class="sxs-lookup"><span data-stu-id="43a37-308">The following snippet shows how the code instantiates the client object and calls the Get method.</span></span>
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));
            return client;
        }
   
        public async Task<IEnumerable<ToDoItem>> Get()
        {
            using (var client = NewDataAPIClient())
            {
                var results = await client.ToDoList.GetByOwnerAsync(owner);
                return results.Select(m => new ToDoItem
                {
                    Description = m.Description,
                    ID = (int)m.ID,
                    Owner = m.Owner
                });
            }
        }
   
    <span data-ttu-id="43a37-309">O parâmetro do construtor obtém a URL do ponto de extremidade na configuração do aplicativo `toDoListDataAPIURL` .</span><span class="sxs-lookup"><span data-stu-id="43a37-309">The constructor parameter gets the endpoint URL from  the `toDoListDataAPIURL` app setting.</span></span> <span data-ttu-id="43a37-310">No arquivo Web.config, esse valor é definido como a URL do IIS Express local do projeto de API para que você possa executar o aplicativo localmente.</span><span class="sxs-lookup"><span data-stu-id="43a37-310">In the Web.config file, that value is set to the local IIS Express URL of the API project so that you can run the application locally.</span></span> <span data-ttu-id="43a37-311">Se você omitir o parâmetro do construtor, o ponto de extremidade padrão será a URL da qual você gerou o código.</span><span class="sxs-lookup"><span data-stu-id="43a37-311">If you omit the constructor parameter, the default endpoint is the URL that you generated the code from.</span></span>
7. <span data-ttu-id="43a37-312">A classe de cliente será gerada com um nome diferente baseado no nome do aplicativo de API. Altere o código em *Controllers\ToDoListController.cs* para que o nome do tipo corresponda ao que foi gerado em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="43a37-312">Your client class will be generated with a different name based on your API app name; change the code in *Controllers\ToDoListController.cs* so that the type name matches what was generated in your project.</span></span> <span data-ttu-id="43a37-313">Por exemplo, se chamar o aplicativo de API de ToDoListDataAPI071316, você alterará este código:</span><span class="sxs-lookup"><span data-stu-id="43a37-313">For example, if you named your API App ToDoListDataAPI071316, you would change this code:</span></span>
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));

<span data-ttu-id="43a37-314">para isto:</span><span class="sxs-lookup"><span data-stu-id="43a37-314">to this:</span></span>

        private static ToDoListDataAPI071316 NewDataAPIClient()
        {
            var client = new ToDoListDataAPI071316(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));


## <a name="create-an-api-app-to-host-the-middle-tier"></a><span data-ttu-id="43a37-315">Criar um aplicativo de API para hospedar a camada intermediária</span><span class="sxs-lookup"><span data-stu-id="43a37-315">Create an API app to host the middle tier</span></span>
<span data-ttu-id="43a37-316">Anteriormente, você [criou o aplicativo de API de camada de dados e implantou código nele](#createapiapp).</span><span class="sxs-lookup"><span data-stu-id="43a37-316">Earlier you [created the data tier API app and deployed code to it](#createapiapp).</span></span>  <span data-ttu-id="43a37-317">Agora, você segue o mesmo procedimento para o aplicativo de API de camada intermediária.</span><span class="sxs-lookup"><span data-stu-id="43a37-317">Now you follow the same procedure for the middle tier API app.</span></span>

1. <span data-ttu-id="43a37-318">No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto ToDoListAPI de camada intermediária (não no ToDoListDataAPI de camada de dados) e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="43a37-318">In **Solution Explorer**, right-click the middle tier ToDoListAPI  project (not the data tier ToDoListDataAPI), and then click **Publish**.</span></span>
   
    ![Clicar em Publicar no Visual Studio](./media/app-service-api-dotnet-get-started/pubinmenu2.png)
2. <span data-ttu-id="43a37-320">Na etapa **Perfil** do assistente **Publicar na Web**, clique em **Serviço de Aplicativo do Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="43a37-320">In the **Profile** tab of the **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="43a37-321">Na caixa de diálogo **Serviço de Aplicativo**, clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="43a37-321">In the **App Service** dialog box, click **New**.</span></span>
4. <span data-ttu-id="43a37-322">Na guia **Hospedagem** da caixa de diálogo **Criar Serviço de Aplicativo**, aceite o **Nome de Aplicativo de API** padrão ou digite um nome que seja exclusivo no domínio *azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="43a37-322">In the **Hosting** tab of the **Create App Service** dialog box, accept the default **API App Name** or enter a name that is unique in the *azurewebsites.net* domain.</span></span>
5. <span data-ttu-id="43a37-323">Escolha a **assinatura** do Azure que você usa.</span><span class="sxs-lookup"><span data-stu-id="43a37-323">Choose the Azure **Subscription** you have been using.</span></span>
6. <span data-ttu-id="43a37-324">Na lista suspensa **Grupo de Recursos** , escolha o mesmo grupo de recursos que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="43a37-324">In the **Resource Group** drop-down, choose the same resource group you created earlier.</span></span>
7. <span data-ttu-id="43a37-325">Na lista suspensa **Plano do Serviço de Aplicativo** , escolha o mesmo plano criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="43a37-325">In the **App Service Plan** drop-down, choose the same plan you created earlier.</span></span> <span data-ttu-id="43a37-326">O padrão será a esse valor.</span><span class="sxs-lookup"><span data-stu-id="43a37-326">It will default to that value.</span></span>
8. <span data-ttu-id="43a37-327">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="43a37-327">Click **Create**.</span></span>
   
    <span data-ttu-id="43a37-328">O Visual Studio cria o aplicativo de API, cria um perfil de publicação para ele e exibe a etapa **Conexão** do assistente **Publicar na Web**.</span><span class="sxs-lookup"><span data-stu-id="43a37-328">Visual Studio creates the API app, creates a publish profile for it, and displays the **Connection** step of the **Publish Web** wizard.</span></span>
9. <span data-ttu-id="43a37-329">Na etapa **Conexão** do assistente **Publicar na Web**, clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="43a37-329">In the **Connection** step of the **Publish Web** wizard, click **Publish**.</span></span>
   
   <span data-ttu-id="43a37-330">O Visual Studio implanta o projeto ToDoListAPI no novo aplicativo de API e abre um navegador para a URL do aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="43a37-330">Visual Studio deploys the ToDoListAPI project to the new API app and opens a browser to the URL of the API app.</span></span> <span data-ttu-id="43a37-331">A página "Criado com êxito" é exibida.</span><span class="sxs-lookup"><span data-stu-id="43a37-331">The "successfully created" page appears.</span></span>

## <a name="configure-the-middle-tier-to-call-the-data-tier"></a><span data-ttu-id="43a37-332">Configurar a camada intermediária para chamar a camada de dados</span><span class="sxs-lookup"><span data-stu-id="43a37-332">Configure the middle tier to call the data tier</span></span>
<span data-ttu-id="43a37-333">Se você chamasse o aplicativo de API da camada intermediária agora, ele tentaria chamar a camada de dados usando a URL do localhost que ainda está no arquivo Web.config.</span><span class="sxs-lookup"><span data-stu-id="43a37-333">If you called the middle tier API app now, it would try to call the data tier using the localhost URL that is still in the Web.config file.</span></span> <span data-ttu-id="43a37-334">Nesta seção, você insere a URL do aplicativo de API da camada de dados em uma configuração de ambiente no aplicativo de API da camada intermediária.</span><span class="sxs-lookup"><span data-stu-id="43a37-334">In this section you enter the data tier API app URL into an environment setting in the middle tier API app.</span></span> <span data-ttu-id="43a37-335">Quando o código no aplicativo de API da camada intermediária recupera a configuração da URL da camada de dados, a configuração do ambiente substitui o que está no arquivo Web.config.</span><span class="sxs-lookup"><span data-stu-id="43a37-335">When the code in the middle tier API app retrieves the data tier URL setting, the environment setting will override what's in the Web.config file.</span></span>

1. <span data-ttu-id="43a37-336">Vá para o [portal do Azure](https://portal.azure.com/)e navegue até a folha **Aplicativo de API** do aplicativo de API que você criou para hospedar o projeto TodoListAPI (camada intermediária).</span><span class="sxs-lookup"><span data-stu-id="43a37-336">Go to the [Azure portal](https://portal.azure.com/), and then navigate to the **API App** blade for the API app that you created to host the TodoListAPI (middle tier) project.</span></span>
2. <span data-ttu-id="43a37-337">Na folha **Configurações** do Aplicativo de API, clique em **Configurações do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="43a37-337">In the API App's **Settings** blade, click **Application settings**.</span></span>
3. <span data-ttu-id="43a37-338">Na folha **Configurações do Aplicativo** do Aplicativo de API, role para baixo até a seção **Configurações do aplicativo** e adicione a chave e o valor a seguir.</span><span class="sxs-lookup"><span data-stu-id="43a37-338">In the API App's **Application Settings** blade, scroll down to the **App settings** section and add the following key and value.</span></span> <span data-ttu-id="43a37-339">O valor será a URL do primeiro Aplicativo de API publicado neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="43a37-339">The value will be the URL of the first API App you published in this tutorial.</span></span>
   
   | <span data-ttu-id="43a37-340">**Chave**</span><span class="sxs-lookup"><span data-stu-id="43a37-340">**Key**</span></span> | <span data-ttu-id="43a37-341">toDoListDataAPIURL</span><span class="sxs-lookup"><span data-stu-id="43a37-341">toDoListDataAPIURL</span></span> |
   | --- | --- |
   | <span data-ttu-id="43a37-342">**Valor**</span><span class="sxs-lookup"><span data-stu-id="43a37-342">**Value**</span></span> |<span data-ttu-id="43a37-343">https://{nome do aplicativo de API da sua camada de dados}.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="43a37-343">https://{your data tier API app name}.azurewebsites.net</span></span> |
   | <span data-ttu-id="43a37-344">**Exemplo**</span><span class="sxs-lookup"><span data-stu-id="43a37-344">**Example**</span></span> |<span data-ttu-id="43a37-345">https://todolistdataapi.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="43a37-345">https://todolistdataapi.azurewebsites.net</span></span> |
4. <span data-ttu-id="43a37-346">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="43a37-346">Click **Save**.</span></span>
   
    ![Clicar em Salvar para Configurações de Aplicativo](./media/app-service-api-dotnet-get-started/asinportal.png)
   
    <span data-ttu-id="43a37-348">Quando o código for executado no Azure, esse valor substituirá a URL de localhost no arquivo Web.config.</span><span class="sxs-lookup"><span data-stu-id="43a37-348">When the code runs in Azure, this value will now override the localhost URL that is in the Web.config file.</span></span>

## <a name="test"></a><span data-ttu-id="43a37-349">Teste</span><span class="sxs-lookup"><span data-stu-id="43a37-349">Test</span></span>
1. <span data-ttu-id="43a37-350">Em uma janela de navegador, navegue até a URL do novo aplicativo de API da camada intermediária que você acabou de criar para ToDoListAPI.</span><span class="sxs-lookup"><span data-stu-id="43a37-350">In a browser window, browse to the URL of the new middle tier API app that you just created for ToDoListAPI.</span></span> <span data-ttu-id="43a37-351">Você pode acessá-lo clicando na URL na folha principal do aplicativo de API no portal.</span><span class="sxs-lookup"><span data-stu-id="43a37-351">You can get there by clicking the URL in the API app's main blade in the portal.</span></span>
2. <span data-ttu-id="43a37-352">Adicione "swagger" à URL na barra de endereço do navegador e pressione Enter.</span><span class="sxs-lookup"><span data-stu-id="43a37-352">Add "swagger" to the URL in the browser's address bar, and then press Enter.</span></span> <span data-ttu-id="43a37-353">(A URL é `http://{apiappname}.azurewebsites.net/swagger`.)</span><span class="sxs-lookup"><span data-stu-id="43a37-353">(The URL is `http://{apiappname}.azurewebsites.net/swagger`.)</span></span>
   
    <span data-ttu-id="43a37-354">O navegador exibe a mesma IU do Swagger vista anteriormente para ToDoListDataAPI, mas agora `owner` não é um campo obrigatório para a operação Get, pois o aplicativo de API da camada intermediária está enviando esse valor para o aplicativo de API da camada de dados.</span><span class="sxs-lookup"><span data-stu-id="43a37-354">The browser displays the same Swagger UI that you saw earlier for ToDoListDataAPI, but now `owner` is not a required field for the Get operation, because the middle tier API app is sending that value to the data tier API app for you.</span></span> <span data-ttu-id="43a37-355">(Quando você executar os tutoriais de autenticação, a camada intermediária enviará as IDs de usuário reais para o parâmetro `owner` ; no momento, ela está codificando um asterisco.)</span><span class="sxs-lookup"><span data-stu-id="43a37-355">(When you do the authentication tutorials, the middle tier will send actual user IDs for the `owner` parameter; for now it is hard-coding an asterisk.)</span></span>
3. <span data-ttu-id="43a37-356">Experimente o método Get e os outros métodos para validar se o aplicativo de API de camada intermediária está chamando o aplicativo de API de camada de dados com êxito.</span><span class="sxs-lookup"><span data-stu-id="43a37-356">Try out the Get method and the other methods to validate that the middle tier API app is successfully calling the data tier API app.</span></span>
   
    ![Método Get da interface do usuário do Swagger](./media/app-service-api-dotnet-get-started/midtierget.png)

## <a name="troubleshooting"></a><span data-ttu-id="43a37-358">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="43a37-358">Troubleshooting</span></span>
<span data-ttu-id="43a37-359">Caso você encontre um problema ao percorrer este tutorial, aqui estão algumas ideias para solução de problemas:</span><span class="sxs-lookup"><span data-stu-id="43a37-359">In case you run into a problem as you go through this tutorial here are some troubleshooting ideas:</span></span>

* <span data-ttu-id="43a37-360">Verifique se está usando a última versão do [SDK do Azure para .NET](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="43a37-360">Make sure that you're using the latest version of the [Azure SDK for .NET](http://go.microsoft.com/fwlink/?linkid=518003).</span></span>
* <span data-ttu-id="43a37-361">Dois nomes do projeto são semelhantes (ToDoListAPI, ToDoListDataAPI).</span><span class="sxs-lookup"><span data-stu-id="43a37-361">Two of the project names are similar (ToDoListAPI, ToDoListDataAPI).</span></span> <span data-ttu-id="43a37-362">Se as coisas não ficarem conforme descrito nas instruções quando você estiver trabalhando com um projeto, verifique se que você abriu o projeto correto.</span><span class="sxs-lookup"><span data-stu-id="43a37-362">If things don't look as described in the instructions when you are working with a project, make sure you have opened the correct project.</span></span>
* <span data-ttu-id="43a37-363">Se você estiver em uma rede corporativa e estiver tentando implantar no Serviço de Aplicativo do Azure por meio de um firewall, verifique se as portas 443 e 8172 estão abertas para implantação na Web.</span><span class="sxs-lookup"><span data-stu-id="43a37-363">If you're on a corporate network and are trying to deploy to Azure App Service through a firewall, make sure that ports 443 and 8172 are open for Web Deploy.</span></span> <span data-ttu-id="43a37-364">Se não puder abrir essas portas, você poderá usar outros métodos de implantação.</span><span class="sxs-lookup"><span data-stu-id="43a37-364">If you can't open those ports, you can use other deployment methods.</span></span>  <span data-ttu-id="43a37-365">Confira [Implantar seu aplicativo no Serviço de Aplicativo do Azure](../app-service-web/web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="43a37-365">See [Deploy your app to Azure App Service](../app-service-web/web-sites-deploy.md).</span></span>
* <span data-ttu-id="43a37-366">Erros do tipo "Nomes de rota devem ser exclusivos": você poderá recebê-los se implantar acidentalmente o projeto errado em um aplicativo de API e, mais tarde, implantar o projeto correto nele.</span><span class="sxs-lookup"><span data-stu-id="43a37-366">"Route names must be unique" errors -- you could get these if you accidentally deploy the wrong project to an API app and then later deploy the correct one to it.</span></span> <span data-ttu-id="43a37-367">Para corrigir isso, reimplante o projeto correto para o aplicativo de API e, na guia **Configurações** do assistente **Publicar na Web**, selecione **Remover arquivos adicionais no destino**.</span><span class="sxs-lookup"><span data-stu-id="43a37-367">To correct this, redeploy the correct project to the API app, and on the **Settings** tab of the **Publish Web** wizard select **Remove additional files at destination**.</span></span>

<span data-ttu-id="43a37-368">Quando seu aplicativo de API ASP.NET estiver em execução no Serviço de Aplicativo do Azure, procure saber mais sobre os recursos do Visual Studio que simplificam a solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="43a37-368">After you have your ASP.NET API app running in Azure App Service, you may want to learn more about Visual Studio features that simplify troubleshooting.</span></span> <span data-ttu-id="43a37-369">Para saber mais sobre o registro em log, a depuração remota e muito mais, confira [Solução de problemas dos aplicativos do Serviço de Aplicativo do Azure no Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="43a37-369">For information about logging, remote debugging, and more, see  [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="43a37-370">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="43a37-370">Next steps</span></span>
<span data-ttu-id="43a37-371">Neste tutorial, você viu como criar aplicativos de API, implantar código neles, gerar código cliente para eles e consumi-los usando clientes .NET.</span><span class="sxs-lookup"><span data-stu-id="43a37-371">You've seen how to deploy existing Web API projects to API apps, generate client code for API apps, and consume API apps from .NET clients.</span></span> <span data-ttu-id="43a37-372">O próximo tutorial desta série mostra como [usar CORS para consumir aplicativos de API de clientes JavaScript](app-service-api-cors-consume-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="43a37-372">The next tutorial in this series shows how to [use CORS to consume API apps from JavaScript clients](app-service-api-cors-consume-javascript.md).</span></span>

<span data-ttu-id="43a37-373">Para obter mais informações sobre geração de código de cliente, confira o repositório [Azure/AutoRest](https://github.com/azure/autorest) em GitHub.com.</span><span class="sxs-lookup"><span data-stu-id="43a37-373">For more information about client code generation, see the [Azure/AutoRest](https://github.com/azure/autorest) repository on GitHub.com.</span></span> <span data-ttu-id="43a37-374">Para obter ajuda com os problemas para usar o cliente gerado, abra um [problema no repositório AutoRest](https://github.com/azure/autorest/issues).</span><span class="sxs-lookup"><span data-stu-id="43a37-374">For help with problems using the generated client, open an [issue in the AutoRest repository](https://github.com/azure/autorest/issues).</span></span>

<span data-ttu-id="43a37-375">Se você quiser criar novos projetos de aplicativo de API do zero, use o modelo de **aplicativo de API do Azure** .</span><span class="sxs-lookup"><span data-stu-id="43a37-375">If you want to create new API app projects from scratch, use the **Azure API App** template.</span></span>

![Modelo de Aplicativo de API no Visual Studio](./media/app-service-api-dotnet-get-started/apiapptemplate.png)

<span data-ttu-id="43a37-377">O modelo de projeto **Aplicativo de API do Azure** é equivalente a escolher o modelo **Vazio** do ASP.NET 4.5.2, clicar na caixa de seleção para adicionar o suporte da API Web e instalar o pacote NuGet do Swashbuckle.</span><span class="sxs-lookup"><span data-stu-id="43a37-377">The **Azure API App** project template is equivalent to choosing the **Empty** ASP.NET 4.5.2 template, clicking the check box to add Web API support, and installing the Swashbuckle NuGet package.</span></span> <span data-ttu-id="43a37-378">Além disso, o modelo adiciona alguns códigos de configuração do Swashbuckle projetados para evitar a criação de IDs de operação do Swagger duplicadas.</span><span class="sxs-lookup"><span data-stu-id="43a37-378">In addition, the template adds some Swashbuckle configuration code designed to prevent the creation of duplicate Swagger operation IDs.</span></span> <span data-ttu-id="43a37-379">Depois de criar um projeto de aplicativo de API, você pode implantá-lo em um aplicativo de API da mesma maneira como viu neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="43a37-379">Once you've created an API App project, you can deploy it to an API app the same way you saw in this tutorial.</span></span>

