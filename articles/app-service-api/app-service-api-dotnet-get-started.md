---
title: "aaaGet iniciado com aplicativos de API e o ASP.NET no serviço de aplicativo | Microsoft Docs"
description: "Saiba como toocreate, implantar e consumir um aplicativo de API do ASP.NET no serviço de aplicativo do Azure, usando o Visual Studio 2015."
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
ms.openlocfilehash: d3e90f1585907d183b0435c6cafc5585bc1e29ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-api-apps-aspnet-and-swagger-in-azure-app-service"></a><span data-ttu-id="04dfc-103">Introdução aos aplicativos de API, ASP.NET e Swagger no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="04dfc-103">Get started with API Apps, ASP.NET, and Swagger in Azure App Service</span></span>
[!INCLUDE [selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="04dfc-104">Isso é hello primeiro em uma série de tutoriais que mostram como serviço toouse recursos do aplicativo do Azure que são úteis para desenvolver e hospedar APIs RESTful.</span><span class="sxs-lookup"><span data-stu-id="04dfc-104">This is hello first in a series of tutorials that show how toouse features of Azure App Service that are helpful for developing and hosting RESTful APIs.</span></span>  <span data-ttu-id="04dfc-105">Este tutorial aborda o suporte para metadados de API no formato Swagger.</span><span class="sxs-lookup"><span data-stu-id="04dfc-105">This tutorial covers support for API metadata in Swagger format.</span></span>

<span data-ttu-id="04dfc-106">Você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="04dfc-106">You'll learn:</span></span>

* <span data-ttu-id="04dfc-107">Como toocreate e implantar [aplicativos de API](app-service-api-apps-why-best-platform.md) no serviço de aplicativo do Azure usando ferramentas integradas ao Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="04dfc-107">How toocreate and deploy [API apps](app-service-api-apps-why-best-platform.md) in Azure App Service by using tools built into Visual Studio 2015.</span></span>
* <span data-ttu-id="04dfc-108">Como o pacote de Swashbuckle NuGet descoberta tooautomate API usando Olá toodynamically gerar metadados do Swagger API.</span><span class="sxs-lookup"><span data-stu-id="04dfc-108">How tooautomate API discovery by using hello Swashbuckle NuGet package toodynamically generate Swagger API metadata.</span></span>
* <span data-ttu-id="04dfc-109">Como tooautomatically de metadados do Swagger API toouse gerar o código do cliente para um aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="04dfc-109">How toouse Swagger API metadata tooautomatically generate client code for an API app.</span></span>

## <a name="sample-application-overview"></a><span data-ttu-id="04dfc-110">Visão geral do aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="04dfc-110">Sample application overview</span></span>
<span data-ttu-id="04dfc-111">Neste tutorial, você trabalha com um aplicativo de exemplo de lista de tarefas simples.</span><span class="sxs-lookup"><span data-stu-id="04dfc-111">In this tutorial, you work with a simple to-do list sample application.</span></span> <span data-ttu-id="04dfc-112">aplicativo Hello tem um front-end do aplicativo de página única (SPA), uma camada intermediária da API Web do ASP.NET e uma camada de dados de API da Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="04dfc-112">hello application has a single-page application (SPA) front end, an ASP.NET Web API middle tier, and an ASP.NET Web API data tier.</span></span>

![Diagrama do aplicativo de exemplo de Aplicativos de API](./media/app-service-api-dotnet-get-started/noauthdiagram.png)

<span data-ttu-id="04dfc-114">Aqui está uma captura de tela de saudação [AngularJS](https://angularjs.org/) front-end.</span><span class="sxs-lookup"><span data-stu-id="04dfc-114">Here's a screen shot of hello [AngularJS](https://angularjs.org/) front end.</span></span>

![Lista de toodo de aplicativo de exemplo de aplicativos de API](./media/app-service-api-dotnet-get-started/todospa.png)

<span data-ttu-id="04dfc-116">Olá solução do Visual Studio inclui três projetos:</span><span class="sxs-lookup"><span data-stu-id="04dfc-116">hello Visual Studio solution includes three projects:</span></span>

![](./media/app-service-api-dotnet-get-started/projectsinse.png)

* <span data-ttu-id="04dfc-117">**ToDoListAngular** -front-end Olá: um SPA AngularJS que chama a camada intermediária hello.</span><span class="sxs-lookup"><span data-stu-id="04dfc-117">**ToDoListAngular** - hello front end: an AngularJS SPA that calls hello middle tier.</span></span>
* <span data-ttu-id="04dfc-118">**ToDoListAPI** -camada intermediária Olá: um projeto de API da Web ASP.NET que chama a camada de dados Olá tooperform as operações CRUD em itens de tarefas pendentes.</span><span class="sxs-lookup"><span data-stu-id="04dfc-118">**ToDoListAPI** - hello middle tier: an ASP.NET Web API project that calls hello data tier tooperform CRUD operations on to-do items.</span></span>
* <span data-ttu-id="04dfc-119">**ToDoListDataAPI** -camada de dados Olá: um projeto de API da Web ASP.NET que executa operações CRUD de itens pendentes.</span><span class="sxs-lookup"><span data-stu-id="04dfc-119">**ToDoListDataAPI** - hello data tier:  an ASP.NET Web API project that performs CRUD operations on to-do items.</span></span>

<span data-ttu-id="04dfc-120">arquitetura de três camadas de saudação é uma das muitas arquiteturas que você pode implementar usando aplicativos de API e é usado aqui apenas para fins de demonstração.</span><span class="sxs-lookup"><span data-stu-id="04dfc-120">hello three-tier architecture is one of many architectures that you can implement by using API Apps and is used here only for demonstration purposes.</span></span> <span data-ttu-id="04dfc-121">código de saudação em cada camada é tão simple quanto possível toodemonstrate recursos de aplicativos de API; Por exemplo, a camada de dados Olá usa memória do servidor, em vez de um banco de dados como seu mecanismo de persistência.</span><span class="sxs-lookup"><span data-stu-id="04dfc-121">hello code in each tier is as simple as possible toodemonstrate API Apps features; for example, hello data tier uses server memory rather than a database as its persistence mechanism.</span></span>

<span data-ttu-id="04dfc-122">Ao concluir este tutorial, você terá dois projetos de API da Web Olá para cima e em execução na nuvem de saudação em aplicativos de API do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="04dfc-122">On completing this tutorial, you'll have hello two Web API projects up and running in hello cloud in App Service API apps.</span></span>

<span data-ttu-id="04dfc-123">tutorial Avançar Olá série de saudação implanta a nuvem de toohello Olá SPA front-end.</span><span class="sxs-lookup"><span data-stu-id="04dfc-123">hello next tutorial in hello series deploys hello SPA front end toohello cloud.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="04dfc-124">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="04dfc-124">Prerequisites</span></span>
* <span data-ttu-id="04dfc-125">ASP.NET Web API - Olá instruções de tutorial presumem que você tenha um conhecimento básico de como toowork com o ASP.NET [API Web 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="04dfc-125">ASP.NET Web API - hello tutorial instructions assume you have a basic knowledge of how toowork with ASP.NET [Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) in Visual Studio.</span></span>
* <span data-ttu-id="04dfc-126">Conta do Azure ‒ você pode [Abrir uma conta do Azure gratuitamente](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) ou [Ativar benefícios de assinante do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="04dfc-126">Azure account - You can [Open an Azure account for free](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) or [Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
  
    <span data-ttu-id="04dfc-127">Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de você se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/).</span><span class="sxs-lookup"><span data-stu-id="04dfc-127">If you want tooget started with Azure App Service before you sign up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/).</span></span> <span data-ttu-id="04dfc-128">Lá, você poderá criar imediatamente um aplicativo de curta duração inicial no Serviço de Aplicativo — **sem exigência de cartão de crédito**e sem compromisso.</span><span class="sxs-lookup"><span data-stu-id="04dfc-128">There, you can immediately create a short-lived starter app in App Service — **no credit card required**, and no commitments.</span></span>
* <span data-ttu-id="04dfc-129">Visual Studio 2015 com hello [SDK do Azure para .NET](https://azure.microsoft.com/downloads/archive-net-downloads/) -Olá SDK instala o Visual Studio 2015 automaticamente se você ainda não o fez.</span><span class="sxs-lookup"><span data-stu-id="04dfc-129">Visual Studio 2015 with hello [Azure SDK for .NET](https://azure.microsoft.com/downloads/archive-net-downloads/) - hello SDK installs Visual Studio 2015 automatically if you don't already have it.</span></span>
  
  * <span data-ttu-id="04dfc-130">No Visual Studio, clique em Ajuda -> Sobre o Microsoft Visual Studio e verifique se você tem "Ferramentas do Serviço de Aplicativo do Azure v2.9.1" ou superior instalado.</span><span class="sxs-lookup"><span data-stu-id="04dfc-130">In Visual Studio, click Help -> About Microsoft Visual Studio and ensure that you have "Azure App Service Tools v2.9.1" or higher installed.</span></span>
    
    ![Versão das Ferramentas de Aplicativo do Azure](./media/app-service-api-dotnet-get-started/apiversion.png)
    
    > [!NOTE]
    > <span data-ttu-id="04dfc-132">Dependendo de quantos das dependências do SDK Olá você já tiver em seu computador, Olá instalar SDK pode levar muito tempo, de alguns minutos tooa meia hora ou mais.</span><span class="sxs-lookup"><span data-stu-id="04dfc-132">Depending on how many of hello SDK dependencies you already have on your machine, installing hello SDK could take a long time, from several minutes tooa half hour or more.</span></span>
    > 
    > 

## <a name="download-hello-sample-application"></a><span data-ttu-id="04dfc-133">Baixe o aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="04dfc-133">Download hello sample application</span></span>
1. <span data-ttu-id="04dfc-134">Baixar Olá [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) repositório.</span><span class="sxs-lookup"><span data-stu-id="04dfc-134">Download hello [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) repository.</span></span>
   
    <span data-ttu-id="04dfc-135">Você pode clicar em Olá **baixar ZIP** botão ou clone do repositório de saudação em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="04dfc-135">You can click hello **Download ZIP** button or clone hello repository on your local machine.</span></span>
2. <span data-ttu-id="04dfc-136">Abra a solução de lista de tarefas pendentes de Olá no Visual Studio 2015 ou 2013.</span><span class="sxs-lookup"><span data-stu-id="04dfc-136">Open hello ToDoList solution in Visual Studio 2015 or 2013.</span></span>
   
   1. <span data-ttu-id="04dfc-137">Você precisará tootrust cada solução.</span><span class="sxs-lookup"><span data-stu-id="04dfc-137">You will need tootrust each solution.</span></span>
         <span data-ttu-id="04dfc-138">![Aviso de Segurança](./media/app-service-api-dotnet-get-started/securitywarning.png)</span><span class="sxs-lookup"><span data-stu-id="04dfc-138">![Security Warning](./media/app-service-api-dotnet-get-started/securitywarning.png)</span></span>
3. <span data-ttu-id="04dfc-139">Crie pacotes do NuGet Olá solução (CTRL + SHIFT + B) toorestore hello.</span><span class="sxs-lookup"><span data-stu-id="04dfc-139">Build hello solution (CTRL + SHIFT + B)  toorestore hello NuGet packages.</span></span>
   
    <span data-ttu-id="04dfc-140">Se você quiser toosee aplicativo hello operação antes de implantá-lo, você pode executá-lo localmente.</span><span class="sxs-lookup"><span data-stu-id="04dfc-140">If you want toosee hello application in operation before you deploy it, you can run it locally.</span></span> <span data-ttu-id="04dfc-141">Certifique-se de que ToDoListDataAPI é o projeto de inicialização e a solução de saudação de execução.</span><span class="sxs-lookup"><span data-stu-id="04dfc-141">Make sure that ToDoListDataAPI is your startup project and run hello solution.</span></span> <span data-ttu-id="04dfc-142">Você deve esperar o erro toosee um HTTP 403 em seu navegador.</span><span class="sxs-lookup"><span data-stu-id="04dfc-142">You should expect toosee a HTTP 403 error in your browser.</span></span>

## <a name="use-swagger-api-metadata-and-ui"></a><span data-ttu-id="04dfc-143">Usar a interface do usuário e metadados de API do Swagger</span><span class="sxs-lookup"><span data-stu-id="04dfc-143">Use Swagger API metadata and UI</span></span>
<span data-ttu-id="04dfc-144">O suporte a metadados da API 2.0 do [Swagger](http://swagger.io/) é integrado ao Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="04dfc-144">Support for [Swagger](http://swagger.io/) 2.0 API metadata is built into Azure App Service.</span></span> <span data-ttu-id="04dfc-145">Cada aplicativo de API pode especificar um ponto de extremidade de URL que retorna metadados para Olá API no formato JSON Swagger.</span><span class="sxs-lookup"><span data-stu-id="04dfc-145">Each API app can specify a URL endpoint that returns metadata for hello API in Swagger JSON format.</span></span> <span data-ttu-id="04dfc-146">Olá retornado do ponto de extremidade de metadados podem ser usado toogenerate o código do cliente.</span><span class="sxs-lookup"><span data-stu-id="04dfc-146">hello metadata returned from that endpoint can be used toogenerate client code.</span></span>

<span data-ttu-id="04dfc-147">Um projeto de API da Web ASP.NET pode gerar dinamicamente os metadados do Swagger usando Olá [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) pacote NuGet.</span><span class="sxs-lookup"><span data-stu-id="04dfc-147">An ASP.NET Web API project can dynamically generate Swagger metadata by using hello [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet package.</span></span> <span data-ttu-id="04dfc-148">Olá pacote Swashbuckle NuGet já está instalado em projetos Olá ToDoListDataAPI e ToDoListAPI que você baixou.</span><span class="sxs-lookup"><span data-stu-id="04dfc-148">hello Swashbuckle NuGet package is already installed in hello ToDoListDataAPI and ToDoListAPI projects that you downloaded.</span></span>

<span data-ttu-id="04dfc-149">Nesta seção do tutorial hello, examinar metadados do Swagger 2.0 Olá gerado e, em seguida, experimente um teste de interface do usuário com base nos metadados do Swagger hello.</span><span class="sxs-lookup"><span data-stu-id="04dfc-149">In this section of hello tutorial, you look at hello generated Swagger 2.0 metadata, and then you try out a test UI that is based on hello Swagger metadata.</span></span>

1. <span data-ttu-id="04dfc-150">Definir Olá ToDoListDataAPI projeto (**não** projeto de ToDoListAPI Olá) como o projeto de inicialização hello.</span><span class="sxs-lookup"><span data-stu-id="04dfc-150">Set hello ToDoListDataAPI project (**not** hello ToDoListAPI project) as hello startup project.</span></span>
   
    ![Definir ToDoDataAPI como Projeto de Inicialização](./media/app-service-api-dotnet-get-started/startupproject.png)
2. <span data-ttu-id="04dfc-152">Pressione F5 ou clique **Depurar > Iniciar depuração** projeto de saudação toorun no modo de depuração.</span><span class="sxs-lookup"><span data-stu-id="04dfc-152">Press F5 or click **Debug > Start Debugging** toorun hello project in debug mode.</span></span>
   
    <span data-ttu-id="04dfc-153">navegador de saudação é aberto e mostra a página de erro de HTTP 403 hello.</span><span class="sxs-lookup"><span data-stu-id="04dfc-153">hello browser opens and shows hello HTTP 403 error page.</span></span>
3. <span data-ttu-id="04dfc-154">Na barra de endereços do navegador, adicione `swagger/docs/v1` toohello final da linha de saudação e depois pressione Return.</span><span class="sxs-lookup"><span data-stu-id="04dfc-154">In your browser address bar, add `swagger/docs/v1` toohello end of hello line, and then press Return.</span></span> <span data-ttu-id="04dfc-155">(Olá URL é `http://localhost:45914/swagger/docs/v1`.)</span><span class="sxs-lookup"><span data-stu-id="04dfc-155">(hello URL is `http://localhost:45914/swagger/docs/v1`.)</span></span>
   
    <span data-ttu-id="04dfc-156">Este é o saudação padrão URL usado pelo Swashbuckle tooreturn Swagger 2.0 JSON metadados para Olá API.</span><span class="sxs-lookup"><span data-stu-id="04dfc-156">This is hello default URL used by Swashbuckle tooreturn Swagger 2.0 JSON metadata for hello API.</span></span>
   
    <span data-ttu-id="04dfc-157">Se você estiver usando o Internet Explorer, o navegador Olá solicita toodownload um *v1.json* arquivo.</span><span class="sxs-lookup"><span data-stu-id="04dfc-157">If you're using Internet Explorer, hello browser prompts you toodownload a *v1.json* file.</span></span>
   
    ![Baixar metadados JSON no IE](./media/app-service-api-dotnet-get-started/iev1json.png)
   
    <span data-ttu-id="04dfc-159">Se você estiver usando o Chrome, Firefox ou borda, o navegador de saudação exibe Olá JSON na janela do navegador hello.</span><span class="sxs-lookup"><span data-stu-id="04dfc-159">If you're using Chrome, Firefox, or Edge, hello browser displays hello JSON in hello browser window.</span></span> <span data-ttu-id="04dfc-160">Navegadores diferentes lidar com JSON diferente, e a janela do navegador pode não ser exatamente igual exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="04dfc-160">Different browsers handle JSON differently, and your browser window may not look exactly like hello example.</span></span>
   
    ![Metadados JSON no Chrome](./media/app-service-api-dotnet-get-started/chromev1json.png)
   
    <span data-ttu-id="04dfc-162">Olá, exemplo a seguir mostra a primeira seção Olá de metadados Swagger Olá Olá API, com definição Olá Olá método Get.</span><span class="sxs-lookup"><span data-stu-id="04dfc-162">hello following sample shows hello first section of hello Swagger metadata for hello API, with hello definition for hello Get method.</span></span> <span data-ttu-id="04dfc-163">Esses metadados são Olá quais unidades Swagger da interface do usuário que você usar Olá etapas a seguir e usá-lo em uma seção posterior tooautomatically tutorial Olá gerar código de cliente.</span><span class="sxs-lookup"><span data-stu-id="04dfc-163">This metadata is what drives hello Swagger UI that you use in hello following steps, and you use it in a later section of hello tutorial tooautomatically generate client code.</span></span>
   
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
4. <span data-ttu-id="04dfc-164">Feche o navegador hello e parar a depuração do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="04dfc-164">Close hello browser and stop Visual Studio debugging.</span></span>
5. <span data-ttu-id="04dfc-165">Em Olá ToDoListDataAPI project no **Solution Explorer**, abra Olá *App_Start\SwaggerConfig.cs* arquivo e, em seguida, role a tela para baixo tooline 174 e remova os comentários Olá código a seguir.</span><span class="sxs-lookup"><span data-stu-id="04dfc-165">In hello ToDoListDataAPI project in **Solution Explorer**, open hello *App_Start\SwaggerConfig.cs* file, then scroll down tooline 174 and uncomment hello following code.</span></span>
   
        /*
            })
        .EnableSwaggerUi(c =>
            {
        */
   
    <span data-ttu-id="04dfc-166">Olá *SwaggerConfig.cs* arquivo é criado quando você instala o pacote de Swashbuckle Olá em um projeto.</span><span class="sxs-lookup"><span data-stu-id="04dfc-166">hello *SwaggerConfig.cs* file is created when you install hello Swashbuckle package in a project.</span></span> <span data-ttu-id="04dfc-167">arquivo Hello fornece um número de maneiras tooconfigure Swashbuckle.</span><span class="sxs-lookup"><span data-stu-id="04dfc-167">hello file provides a number of ways tooconfigure Swashbuckle.</span></span>
   
    <span data-ttu-id="04dfc-168">código de saudação que tiver removidos Olá habilita Swagger interface do usuário que você usa em Olá seguindo as etapas.</span><span class="sxs-lookup"><span data-stu-id="04dfc-168">hello code you've uncommented enables hello Swagger UI that you use in hello following steps.</span></span> <span data-ttu-id="04dfc-169">Quando você cria um projeto de API da Web usando o modelo de projeto de aplicativo hello API, esse código é comentado por padrão como uma medida de segurança.</span><span class="sxs-lookup"><span data-stu-id="04dfc-169">When you create a Web API project by using hello API app project template, this code is commented out by default as a security measure.</span></span>
6. <span data-ttu-id="04dfc-170">Execute o projeto Olá novamente.</span><span class="sxs-lookup"><span data-stu-id="04dfc-170">Run hello project again.</span></span>
7. <span data-ttu-id="04dfc-171">Na barra de endereços do navegador, adicione `swagger` toohello final da linha de saudação e depois pressione Return.</span><span class="sxs-lookup"><span data-stu-id="04dfc-171">In your browser address bar, add `swagger` toohello end of hello line, and then press Return.</span></span> <span data-ttu-id="04dfc-172">(Olá URL é `http://localhost:45914/swagger`.)</span><span class="sxs-lookup"><span data-stu-id="04dfc-172">(hello URL is `http://localhost:45914/swagger`.)</span></span>
8. <span data-ttu-id="04dfc-173">Na página de interface do usuário Swagger hello, clique em **ToDoList** toosee métodos de saudação disponíveis.</span><span class="sxs-lookup"><span data-stu-id="04dfc-173">When hello Swagger UI page appears, click **ToDoList** toosee hello methods available.</span></span>
   
    ![Métodos disponíveis na interface do usuário do Swagger](./media/app-service-api-dotnet-get-started/methods.png)
9. <span data-ttu-id="04dfc-175">Clique em Olá primeiro **obter** botão na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="04dfc-175">Click hello first **Get** button in hello list.</span></span>
10. <span data-ttu-id="04dfc-176">Em Olá **parâmetros** seção, digite um asterisco como valor de saudação do hello `owner` parâmetro e clique **Experimente**.</span><span class="sxs-lookup"><span data-stu-id="04dfc-176">In hello **Parameters** section, enter an asterisk as hello value of hello `owner` parameter, and then click **Try it out**.</span></span>
    
    <span data-ttu-id="04dfc-177">Quando você adicionar autenticação em tutoriais subsequentes, camada intermediária Olá fornecerá a camada de dados toohello do ID de usuário real hello.</span><span class="sxs-lookup"><span data-stu-id="04dfc-177">When you add authentication in later tutorials, hello middle tier will provide hello actual user ID toohello data tier.</span></span> <span data-ttu-id="04dfc-178">Agora, todas as tarefas terá asterisco sua ID do proprietário enquanto executa o aplicativo hello sem autenticação habilitada.</span><span class="sxs-lookup"><span data-stu-id="04dfc-178">For now, all tasks will have asterisk as their owner ID while hello application runs without authentication enabled.</span></span>
    
    ![Teste da interface do usuário do Swagger](./media/app-service-api-dotnet-get-started/gettryitout1.png)
    
    <span data-ttu-id="04dfc-180">Olá Swagger da interface do usuário chama Olá método Get da lista de tarefas e exibe o código de resposta hello e resultados JSON.</span><span class="sxs-lookup"><span data-stu-id="04dfc-180">hello Swagger UI calls hello ToDoList Get method and displays hello response code and JSON results.</span></span>
    
    ![Resultados do teste da interface do usuário do Swagger](./media/app-service-api-dotnet-get-started/gettryitout.png)
11. <span data-ttu-id="04dfc-182">Clique em **Post**e, em seguida, clique em caixa Olá em **esquema de modelo**.</span><span class="sxs-lookup"><span data-stu-id="04dfc-182">Click **Post**, and then click hello box under **Model Schema**.</span></span>
    
    <span data-ttu-id="04dfc-183">Clicando em Olá modelo esquema prefills Olá caixa de entrada onde você pode especificar o valor do parâmetro hello para Olá método Post.</span><span class="sxs-lookup"><span data-stu-id="04dfc-183">Clicking hello model schema prefills hello input box where you can specify hello parameter value for hello Post method.</span></span> <span data-ttu-id="04dfc-184">(Se isso não funcionar no Internet Explorer, use um navegador diferente ou insira o valor do parâmetro hello manualmente na próxima etapa do hello.)</span><span class="sxs-lookup"><span data-stu-id="04dfc-184">(If this doesn't work in Internet Explorer, use a different browser or enter hello parameter value manually in hello next step.)</span></span>  
    
    ![Postagem do teste da interface do usuário do Swagger](./media/app-service-api-dotnet-get-started/post.png)
12. <span data-ttu-id="04dfc-186">Saudação de alteração JSON em Olá `todo` caixa para que ele se parece com hello exemplo a seguir, ou substituir seu próprio texto de descrição de entrada de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="04dfc-186">Change hello JSON in hello `todo` parameter input box so that it looks like hello following example, or substitute your own description text:</span></span>
    
        {
          "ID": 2,
          "Description": "buy hello dog a toy",
          "Owner": "*"
        }
13. <span data-ttu-id="04dfc-187">Clique em **Experimentar**.</span><span class="sxs-lookup"><span data-stu-id="04dfc-187">Click **Try it out**.</span></span>
    
    <span data-ttu-id="04dfc-188">Olá ToDoList API retorna um código de resposta HTTP 204 que indica êxito.</span><span class="sxs-lookup"><span data-stu-id="04dfc-188">hello ToDoList API returns an HTTP 204 response code that indicates success.</span></span>
14. <span data-ttu-id="04dfc-189">Clique Olá primeiro **obter** botão e clique em Olá nessa seção da página de saudação **Experimente** botão.</span><span class="sxs-lookup"><span data-stu-id="04dfc-189">Click hello first **Get** button, and then in that section of hello page click hello **Try it out** button.</span></span>
    
    <span data-ttu-id="04dfc-190">Olá resposta de obtenção de método agora inclui o novo item de toodo hello.</span><span class="sxs-lookup"><span data-stu-id="04dfc-190">hello Get method response now includes hello new toodo item.</span></span>
15. <span data-ttu-id="04dfc-191">Opcional: Tente também Olá Put, Delete e obter pelos métodos de ID.</span><span class="sxs-lookup"><span data-stu-id="04dfc-191">Optional: Try also hello Put, Delete, and Get by ID methods.</span></span>
16. <span data-ttu-id="04dfc-192">Feche o navegador hello e parar a depuração do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="04dfc-192">Close hello browser and stop Visual Studio debugging.</span></span>

<span data-ttu-id="04dfc-193">O Swashbuckle funciona com qualquer projeto de API Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="04dfc-193">Swashbuckle works with any ASP.NET Web API project.</span></span> <span data-ttu-id="04dfc-194">Se você desejar tooadd Swagger metadados geração tooan projeto existente, apenas instale o pacote de Swashbuckle de saudação.</span><span class="sxs-lookup"><span data-stu-id="04dfc-194">If you want tooadd Swagger metadata generation tooan existing project, just install hello Swashbuckle package.</span></span>

> [!NOTE]
> <span data-ttu-id="04dfc-195">Os metadados do Swagger incluem uma ID exclusiva para cada operação da API.</span><span class="sxs-lookup"><span data-stu-id="04dfc-195">Swagger metadata includes a unique ID for each API operation.</span></span> <span data-ttu-id="04dfc-196">Por padrão, o Swashbuckle pode gerar IDs de operação do Swagger duplicadas para os métodos do controlador da API Web.</span><span class="sxs-lookup"><span data-stu-id="04dfc-196">By default, Swashbuckle may generate duplicate Swagger operation IDs for your Web API controller methods.</span></span> <span data-ttu-id="04dfc-197">Isso acontecerá se o controlador tiver métodos HTTP sobrecarregados, como `Get()` e `Get(id)`.</span><span class="sxs-lookup"><span data-stu-id="04dfc-197">This happens if your controller has overloaded HTTP methods, such as `Get()` and `Get(id)`.</span></span> <span data-ttu-id="04dfc-198">Para obter informações sobre como toohandle sobrecargas, consulte [definições de API gerado personalizar Swashbuckle](app-service-api-dotnet-swashbuckle-customize.md).</span><span class="sxs-lookup"><span data-stu-id="04dfc-198">For information about how toohandle overloads, see [Customize Swashbuckle-generated API definitions](app-service-api-dotnet-swashbuckle-customize.md).</span></span> <span data-ttu-id="04dfc-199">Se você criar um projeto de API da Web no Visual Studio usando o modelo de aplicativo de API do Azure hello, o código que gera IDs exclusivo da operação será automaticamente adicionado toohello *SwaggerConfig.cs* arquivo.</span><span class="sxs-lookup"><span data-stu-id="04dfc-199">If you create a Web API project in Visual Studio by using hello Azure API App template, code that generates unique operation IDs is automatically added toohello *SwaggerConfig.cs* file.</span></span>  
> 
> 

## <span data-ttu-id="04dfc-200"><a id="createapiapp"></a>Criar um aplicativo de API no Azure e implantar código tooit</span><span class="sxs-lookup"><span data-stu-id="04dfc-200"><a id="createapiapp"></a> Create an API app in Azure and deploy code tooit</span></span>
<span data-ttu-id="04dfc-201">Nesta seção, você usar as ferramentas do Azure que são integradas a saudação Visual Studio **Publicar Web** Assistente toocreate uma nova API de aplicativo no Azure.</span><span class="sxs-lookup"><span data-stu-id="04dfc-201">In this section, you use Azure tools that are integrated into hello Visual Studio **Publish Web** wizard toocreate a new API app in Azure.</span></span> <span data-ttu-id="04dfc-202">Em seguida, implante Olá ToDoListDataAPI projeto toohello novo aplicativo de API e chamar a API de saudação executando Olá Swagger da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="04dfc-202">Then you deploy hello ToDoListDataAPI project toohello new API app and call hello API by running hello Swagger UI.</span></span>

1. <span data-ttu-id="04dfc-203">Em **Solution Explorer**, clique com botão direito Olá ToDoListDataAPI e, em seguida, clique em **publicar**.</span><span class="sxs-lookup"><span data-stu-id="04dfc-203">In **Solution Explorer**, right-click hello ToDoListDataAPI project, and then click **Publish**.</span></span>
   
    ![Clicar em Publicar no Visual Studio](./media/app-service-api-dotnet-get-started/pubinmenu.png)
2. <span data-ttu-id="04dfc-205">Em Olá **perfil** etapa Olá **Publicar Web** assistente, clique em **serviço de aplicativo do Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="04dfc-205">In hello **Profile** step of hello **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
   
   ![Clicar no Serviço de Aplicativo do Azure em Publicar Web](./media/app-service-api-dotnet-get-started/selectappservice.png)
3. <span data-ttu-id="04dfc-207">Entrar tooyour conta do Azure, se você ainda não tiver feito isso, ou atualizar suas credenciais se elas estiverem expirado.</span><span class="sxs-lookup"><span data-stu-id="04dfc-207">Sign in tooyour Azure account if you have not already done so, or refresh your credentials if they're expired.</span></span>
4. <span data-ttu-id="04dfc-208">Nas Olá a caixa de diálogo do serviço de aplicativo, escolha hello Azure **assinatura** você deseja toouse e, em seguida, clique em **novo**.</span><span class="sxs-lookup"><span data-stu-id="04dfc-208">In hello App Service dialog box, choose hello Azure **Subscription** you want toouse, and then click **New**.</span></span>
   
    ![Clicar em Novo no diálogo Serviço de Aplicativo](./media/app-service-api-dotnet-get-started/clicknew.png)
   
    <span data-ttu-id="04dfc-210">Olá **hospedagem** guia da saudação **criar serviço de aplicativo** caixa de diálogo é exibida.</span><span class="sxs-lookup"><span data-stu-id="04dfc-210">hello **Hosting** tab of hello **Create App Service** dialog box appears.</span></span>
   
    <span data-ttu-id="04dfc-211">Porque você estiver implantando um projeto de API da Web que tem Swashbuckle instalado, o Visual Studio pressupõe que você deseja toocreate App uma API.</span><span class="sxs-lookup"><span data-stu-id="04dfc-211">Because you're deploying a Web API project that has Swashbuckle installed, Visual Studio assumes that you want toocreate an API App.</span></span> <span data-ttu-id="04dfc-212">Isso é indicado por Olá **API App Name** title e por Olá fatos que Olá **alterar tipo** lista suspensa está definida muito**API App**.</span><span class="sxs-lookup"><span data-stu-id="04dfc-212">This is indicated by hello **API App Name** title and by hello fact that hello **Change Type** drop-down list is set too**API App**.</span></span>
   
    ![Tipo de aplicativo no diálogo Serviço de Aplicativos](./media/app-service-api-dotnet-get-started/apptype.png)
5. <span data-ttu-id="04dfc-214">Insira um **API App Name** que é exclusivo no hello *azurewebsites.net* domínio.</span><span class="sxs-lookup"><span data-stu-id="04dfc-214">Enter an **API App Name** that is unique in hello *azurewebsites.net* domain.</span></span> <span data-ttu-id="04dfc-215">Você pode aceitar o nome padrão de saudação que propõe do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="04dfc-215">You can accept hello default name that Visual Studio proposes.</span></span>
   
    <span data-ttu-id="04dfc-216">Se você inserir um nome que outra pessoa já usado, você verá um direito de toohello de ponto de exclamação vermelho.</span><span class="sxs-lookup"><span data-stu-id="04dfc-216">If you enter a name that someone else has already used, you see a red exclamation mark toohello right.</span></span>
   
    <span data-ttu-id="04dfc-217">Olá URL do aplicativo hello API será `{API app name}.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="04dfc-217">hello URL of hello API app will be `{API app name}.azurewebsites.net`.</span></span>
6. <span data-ttu-id="04dfc-218">Em Olá **grupo de recursos** lista suspensa, clique **novo**e, em seguida, digite "ToDoListGroup" ou outro nome se você preferir.</span><span class="sxs-lookup"><span data-stu-id="04dfc-218">In hello **Resource Group** drop-down, click **New**, and then enter "ToDoListGroup" or another name if you prefer.</span></span>
   
    <span data-ttu-id="04dfc-219">Um grupo de recursos é uma coleção de recursos do Azure, como aplicativos de API, bancos de dados, VMs e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="04dfc-219">A resource group is a collection of Azure resources such as API apps, databases, VMs, and so forth.</span></span>    <span data-ttu-id="04dfc-220">Para este tutorial, é melhor toocreate um novo grupo de recursos porque o que torna mais fácil toodelete em uma única etapa que todos Olá recursos do Azure que você cria para o tutorial hello.</span><span class="sxs-lookup"><span data-stu-id="04dfc-220">For this tutorial, it's best toocreate a new resource group because that makes it easy toodelete in one step all hello Azure resources that you create for hello tutorial.</span></span>
   
    <span data-ttu-id="04dfc-221">Essa caixa permite que você selecione um [grupo de recursos](../azure-resource-manager/resource-group-overview.md) existente ou crie um novo digitando um nome diferente de qualquer grupo de recursos existente na assinatura.</span><span class="sxs-lookup"><span data-stu-id="04dfc-221">This box lets you select an existing [resource group](../azure-resource-manager/resource-group-overview.md) or create a new one by typing in a name that is different from any existing resource group in your subscription.</span></span>
7. <span data-ttu-id="04dfc-222">Clique em Olá **novo** toohello próximo botão **plano do serviço de aplicativo** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="04dfc-222">Click hello **New** button next toohello **App Service Plan** drop-down.</span></span>
   
    <span data-ttu-id="04dfc-223">captura de tela Hello mostra valores de exemplo para **API App Name**, **assinatura**, e **grupo de recursos** – seus valores serão diferentes.</span><span class="sxs-lookup"><span data-stu-id="04dfc-223">hello screen shot shows sample values for **API App Name**, **Subscription**, and **Resource Group** -- your values will be different.</span></span>
   
    ![Criar caixa de diálogo do Serviço de Aplicativo](./media/app-service-api-dotnet-get-started/createas.png)
   
    <span data-ttu-id="04dfc-225">Olá etapas a seguir, você criará um plano de serviço de aplicativo hello novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="04dfc-225">In hello following steps you create an App Service plan for hello new resource group.</span></span> <span data-ttu-id="04dfc-226">Um plano de serviço de aplicativo especifica os recursos de computação Olá que executa o seu aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="04dfc-226">An App Service plan specifies hello compute resources that your API app runs on.</span></span> <span data-ttu-id="04dfc-227">Por exemplo, se você escolher a camada gratuita hello, seu aplicativo de API executa em máquinas virtuais compartilhados, enquanto para algumas camadas pagas, ele é executado em máquinas virtuais dedicadas.</span><span class="sxs-lookup"><span data-stu-id="04dfc-227">For example, if you choose hello free tier, your API app runs on shared VMs, while for some paid tiers it runs on dedicated VMs.</span></span> <span data-ttu-id="04dfc-228">Para saber mais sobre os planos do Serviço de Aplicativo, consulte a [Visão geral dos planos do Serviço de Aplicativo](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="04dfc-228">For information about App Service plans, see [App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
8. <span data-ttu-id="04dfc-229">Em Olá **configurar o plano de serviço de aplicativo** caixa de diálogo, digite "ToDoListPlan" ou outro nome, se você preferir.</span><span class="sxs-lookup"><span data-stu-id="04dfc-229">In hello **Configure App Service Plan** dialog, enter "ToDoListPlan" or another name if you prefer.</span></span>
9. <span data-ttu-id="04dfc-230">Em Olá **local** lista suspensa, escolha o local de saudação tooyou mais próximo.</span><span class="sxs-lookup"><span data-stu-id="04dfc-230">In hello **Location** drop-down list, choose hello location that is closest tooyou.</span></span>
   
    <span data-ttu-id="04dfc-231">Essa configuração especifica em qual datacenter do Azure o aplicativo será executado.</span><span class="sxs-lookup"><span data-stu-id="04dfc-231">This setting specifies which Azure datacenter your app will run in.</span></span> <span data-ttu-id="04dfc-232">Escolha um local fechar tooyou toominimize [latência](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090).</span><span class="sxs-lookup"><span data-stu-id="04dfc-232">Choose a location close tooyou toominimize [latency](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090).</span></span>
10. <span data-ttu-id="04dfc-233">Em Olá **tamanho** lista suspensa, clique **livre**.</span><span class="sxs-lookup"><span data-stu-id="04dfc-233">In hello **Size** drop-down, click **Free**.</span></span>
    
    <span data-ttu-id="04dfc-234">Para este tutorial, Olá livre preço fornecem desempenho suficiente.</span><span class="sxs-lookup"><span data-stu-id="04dfc-234">For this tutorial, hello free pricing tier will provide sufficient performance.</span></span>
11. <span data-ttu-id="04dfc-235">Em Olá **configurar o plano de serviço de aplicativo** caixa de diálogo, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="04dfc-235">In hello **Configure App Service Plan** dialog, click **OK**.</span></span>
    
    ![Clicar em OK em Configurar Plano do Serviço de Aplicativos](./media/app-service-api-dotnet-get-started/configasp.png)
12. <span data-ttu-id="04dfc-237">Em Olá **criar serviço de aplicativo** caixa de diálogo, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="04dfc-237">In hello **Create App Service** dialog box, click **Create**.</span></span>
    
    ![Clicar em Criar no diálogo Criar Serviço de Aplicativos](./media/app-service-api-dotnet-get-started/clickcreate.png)
    
    <span data-ttu-id="04dfc-239">Visual Studio cria o aplicativo de API hello e um perfil de publicação que tem todas as configurações de saudação necessária para o aplicativo hello API.</span><span class="sxs-lookup"><span data-stu-id="04dfc-239">Visual Studio creates hello API app and a publish profile that has all of hello required settings for hello API app.</span></span> <span data-ttu-id="04dfc-240">Em seguida, ele abre Olá **Publicar Web** assistente, que você usará toodeploy projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="04dfc-240">Then it opens hello **Publish Web** wizard, which you'll use toodeploy hello project.</span></span>
    
    <span data-ttu-id="04dfc-241">Olá **Publicar Web** assistente é aberto no hello **Conexão** guia (mostrado abaixo).</span><span class="sxs-lookup"><span data-stu-id="04dfc-241">hello **Publish Web** wizard opens on hello **Connection** tab (shown below).</span></span>
    
    <span data-ttu-id="04dfc-242">Em Olá **Conexão** guia hello **servidor** e **nome do Site** configurações do aplicativo de API tooyour ponto.</span><span class="sxs-lookup"><span data-stu-id="04dfc-242">On hello **Connection** tab, hello **Server** and **Site name** settings point tooyour API app.</span></span> <span data-ttu-id="04dfc-243">Olá **nome de usuário** e **senha** são credenciais de implantação que o Azure cria para você.</span><span class="sxs-lookup"><span data-stu-id="04dfc-243">hello **User name** and **Password** are deployment credentials that Azure creates for you.</span></span> <span data-ttu-id="04dfc-244">Após a implantação, o Visual Studio abrirá um navegador toohello **URL de destino** (que é a única finalidade Olá de **URL de destino**).</span><span class="sxs-lookup"><span data-stu-id="04dfc-244">After deployment, Visual Studio opens a browser toohello **Destination URL** (that's hello only purpose for **Destination URL**).</span></span>  
13. <span data-ttu-id="04dfc-245">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="04dfc-245">Click **Next**.</span></span>
    
    ![Clique em Avançar na guia Conexão de Publicar Web](./media/app-service-api-dotnet-get-started/connnext.png)
    
    <span data-ttu-id="04dfc-247">próxima guia do Hello é hello **configurações** guia (mostrado abaixo).</span><span class="sxs-lookup"><span data-stu-id="04dfc-247">hello next tab is hello **Settings** tab (shown below).</span></span> <span data-ttu-id="04dfc-248">Aqui você pode alterar toodeploy de guia de configuração de compilação Olá uma compilação de depuração para [depuração remota](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug).</span><span class="sxs-lookup"><span data-stu-id="04dfc-248">Here you can change hello build configuration tab toodeploy a debug build for [remote debugging](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug).</span></span> <span data-ttu-id="04dfc-249">Olá guia também oferece várias **opções de publicação do arquivo**:</span><span class="sxs-lookup"><span data-stu-id="04dfc-249">hello tab also offers several **File Publish Options**:</span></span>
    
    * <span data-ttu-id="04dfc-250">Remover os arquivos adicionais no destino</span><span class="sxs-lookup"><span data-stu-id="04dfc-250">Remove additional files at destination</span></span>
    * <span data-ttu-id="04dfc-251">Pré-compilar durante a publicação</span><span class="sxs-lookup"><span data-stu-id="04dfc-251">Precompile during publishing</span></span>
    * <span data-ttu-id="04dfc-252">Excluir arquivos da pasta App_Data de saudação</span><span class="sxs-lookup"><span data-stu-id="04dfc-252">Exclude files from hello App_Data folder</span></span>
    
    <span data-ttu-id="04dfc-253">Para este tutorial, você não precisará de qualquer uma delas.</span><span class="sxs-lookup"><span data-stu-id="04dfc-253">For this tutorial you don't need any of these.</span></span> <span data-ttu-id="04dfc-254">Para obter explicações detalhadas sobre o que fazem, confira [Como implantar um projeto Web usando a publicação de um clique no Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx).</span><span class="sxs-lookup"><span data-stu-id="04dfc-254">For detailed explanations of what they do, see [How to: Deploy a Web Project Using One-Click Publish in Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx).</span></span>
14. <span data-ttu-id="04dfc-255">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="04dfc-255">Click **Next**.</span></span>
    
    ![Clique em Avançar na guia Configurações de Publicar Web](./media/app-service-api-dotnet-get-started/settingsnext.png)
    
    <span data-ttu-id="04dfc-257">Next é Olá **visualização** guia (mostrado abaixo), que dá a você uma toosee oportunidade quais arquivos serão toobe copiado do seu aplicativo de API de toohello do projeto.</span><span class="sxs-lookup"><span data-stu-id="04dfc-257">Next is hello **Preview** tab (shown below), which gives you an opportunity toosee what files are going toobe copied from your project toohello API app.</span></span> <span data-ttu-id="04dfc-258">Quando você estiver implantando um aplicativo de tooan API do projeto que você já implantou tooearlier, somente os arquivos alterados são copiados.</span><span class="sxs-lookup"><span data-stu-id="04dfc-258">When you're deploying a project tooan API app that you already deployed tooearlier, only changed files are copied.</span></span> <span data-ttu-id="04dfc-259">Se você quiser toosee uma lista da qual serão copiados, você pode clicar em Olá **iniciar visualização** botão.</span><span class="sxs-lookup"><span data-stu-id="04dfc-259">If you want toosee a list of what will be copied, you can click hello **Start Preview** button.</span></span>
15. <span data-ttu-id="04dfc-260">Clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="04dfc-260">Click **Publish**.</span></span>
    
    ![Clicar em Publicar na guia Visualização de Publicar Web](./media/app-service-api-dotnet-get-started/clickpublish.png)
    
    <span data-ttu-id="04dfc-262">O Visual Studio implanta Olá ToDoListDataAPI projeto toohello novo aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="04dfc-262">Visual Studio deploys hello ToDoListDataAPI project toohello new API app.</span></span> <span data-ttu-id="04dfc-263">Olá **saída** janela registra o êxito da implantação e a página "criada com êxito" será exibida em uma URL do navegador janela aberta toohello do aplicativo hello API.</span><span class="sxs-lookup"><span data-stu-id="04dfc-263">hello **Output** window logs successful deployment, and a "successfully created" page appears in a browser window opened toohello URL of hello API app.</span></span>
    
    ![Implantação bem-sucedida da janela de saída](./media/app-service-api-dotnet-get-started/deploymentoutput.png)
    
    ![Página Novo aplicativo de API criado com êxito](./media/app-service-api-dotnet-get-started/appcreated.png)
16. <span data-ttu-id="04dfc-266">Adicionar URL de toohello "swagger" na barra de endereços do navegador hello e pressione Enter.</span><span class="sxs-lookup"><span data-stu-id="04dfc-266">Add "swagger" toohello URL in hello browser's address bar, and then press Enter.</span></span> <span data-ttu-id="04dfc-267">(Olá URL é `http://{apiappname}.azurewebsites.net/swagger`.)</span><span class="sxs-lookup"><span data-stu-id="04dfc-267">(hello URL is `http://{apiappname}.azurewebsites.net/swagger`.)</span></span>
    
    <span data-ttu-id="04dfc-268">navegador de saudação exibe Olá mesmo Swagger interface de usuário que você viu anteriormente, mas agora ele está em execução na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="04dfc-268">hello browser displays hello same Swagger UI that you saw earlier, but now it's running in hello cloud.</span></span> <span data-ttu-id="04dfc-269">Experimente Olá método Get, e você vê que você está itens de tarefas 2 toohello back padrão.</span><span class="sxs-lookup"><span data-stu-id="04dfc-269">Try out hello Get method, and you see that you're back toohello default 2 to-do items.</span></span> <span data-ttu-id="04dfc-270">Olá alterações feitas anteriormente salvas na memória no computador local hello.</span><span class="sxs-lookup"><span data-stu-id="04dfc-270">hello changes you made earlier were saved in memory in hello local machine.</span></span>
17. <span data-ttu-id="04dfc-271">Olá abrir [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="04dfc-271">Open hello [Azure portal](https://portal.azure.com/).</span></span>
    
    <span data-ttu-id="04dfc-272">Olá portal do Azure é uma interface da web para gerenciar os recursos do Azure, como aplicativos de API.</span><span class="sxs-lookup"><span data-stu-id="04dfc-272">hello Azure portal is a web interface for managing Azure resources such as API apps.</span></span>
18. <span data-ttu-id="04dfc-273">Clique em **Mais Serviços > Serviços de Aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="04dfc-273">Click **More Services > App Services**.</span></span>
    
    ![Procurar Serviços de Aplicativos](./media/app-service-api-dotnet-get-started/browseas.png)
19. <span data-ttu-id="04dfc-275">Em Olá **serviços de aplicativos** folha, localize e clique em seu novo aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="04dfc-275">In hello **App Services** blade, find and click your new API app.</span></span> <span data-ttu-id="04dfc-276">(No hello portal do Azure, são chamadas de janelas que são abertas direita toohello *folhas*.)</span><span class="sxs-lookup"><span data-stu-id="04dfc-276">(In hello Azure portal, windows that open toohello right are called *blades*.)</span></span>
    
    ![Folha Serviços de Aplicativos](./media/app-service-api-dotnet-get-started/choosenewapiappinportal.png)
    
    <span data-ttu-id="04dfc-278">Duas folhas são abertas.</span><span class="sxs-lookup"><span data-stu-id="04dfc-278">Two blades open.</span></span> <span data-ttu-id="04dfc-279">Um blade tem uma visão geral do aplicativo de API hello e um tem uma longa lista de configurações que você pode exibir e alterar.</span><span class="sxs-lookup"><span data-stu-id="04dfc-279">One blade has an overview of hello API app, and one has a long list of settings that you can view and change.</span></span>
20. <span data-ttu-id="04dfc-280">Em Olá **configurações** folha, localizar Olá **API** seção e clique em **de definição de API**.</span><span class="sxs-lookup"><span data-stu-id="04dfc-280">In hello **Settings** blade, find hello **API** section and click **API Definition**.</span></span>
    
    ![Definição de API na folha Configurações](./media/app-service-api-dotnet-get-started/apidefinsettings.png)
    
    <span data-ttu-id="04dfc-282">Olá **de definição de API** folha permite que você especifique o URL de saudação que retorna metadados do Swagger 2.0 no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="04dfc-282">hello **API Definition** blade lets you specify hello URL that returns Swagger 2.0 metadata in JSON format.</span></span> <span data-ttu-id="04dfc-283">Quando o Visual Studio cria um aplicativo hello API, ele define o valor de padrão do hello API definição URL toohello para Swashbuckle metadados gerados pelo que você viu anteriormente, que é o aplicativo hello API base URL mais `/swagger/docs/v1`.</span><span class="sxs-lookup"><span data-stu-id="04dfc-283">When Visual Studio creates hello API app, it sets hello API definition URL toohello default value for Swashbuckle-generated metadata that you saw earlier, which is hello API app's base URL plus `/swagger/docs/v1`.</span></span>
    
    ![URL de definição da API](./media/app-service-api-dotnet-get-started/apidefurl.png)
    
    <span data-ttu-id="04dfc-285">Quando você seleciona um código de cliente de toogenerate de aplicativo de API para ele, o Visual Studio recupera metadados de saudação dessa URL.</span><span class="sxs-lookup"><span data-stu-id="04dfc-285">When you select an API app toogenerate client code for it, Visual Studio retrieves hello metadata from this URL.</span></span>

## <span data-ttu-id="04dfc-286"><a id="codegen"></a>Gerar código de cliente para a camada de dados Olá</span><span class="sxs-lookup"><span data-stu-id="04dfc-286"><a id="codegen"></a> Generate client code for hello data tier</span></span>
<span data-ttu-id="04dfc-287">Uma das vantagens de saudação da integração do Swagger em aplicativos de API do Azure é a geração de código automática.</span><span class="sxs-lookup"><span data-stu-id="04dfc-287">One of hello advantages of integrating Swagger into Azure API apps is automatic code generation.</span></span> <span data-ttu-id="04dfc-288">Classes de cliente gerada tornam mais fácil toowrite o código que chama um aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="04dfc-288">Generated client classes make it easier toowrite code that calls an API app.</span></span>

<span data-ttu-id="04dfc-289">projeto de ToDoListAPI Olá já tiver um código de cliente de saudação gerado, mas no hello etapas você excluí-la e recriá-lo toosee como toodo Olá a geração de código.</span><span class="sxs-lookup"><span data-stu-id="04dfc-289">hello ToDoListAPI project already has hello generated client code, but in hello following steps you'll delete it and regenerate it toosee how toodo hello code generation.</span></span>

1. <span data-ttu-id="04dfc-290">No Visual Studio **Solution Explorer**, em Olá ToDoListAPI projeto, excluir Olá *ToDoListDataAPI* pasta.</span><span class="sxs-lookup"><span data-stu-id="04dfc-290">In Visual Studio **Solution Explorer**, in hello ToDoListAPI project, delete hello *ToDoListDataAPI* folder.</span></span> <span data-ttu-id="04dfc-291">**Cuidado: Exclua apenas o hello pasta, projeto de ToDoListDataAPI Olá não.**</span><span class="sxs-lookup"><span data-stu-id="04dfc-291">**Caution: Delete only hello folder, not hello ToDoListDataAPI project.**</span></span>
   
    ![Excluir código de cliente gerado](./media/app-service-api-dotnet-get-started/deletecodegen.png)
   
    <span data-ttu-id="04dfc-293">Esta pasta foi criada usando o processo de geração de código Olá que você está prestes a toogo por meio de.</span><span class="sxs-lookup"><span data-stu-id="04dfc-293">This folder was created by using hello code generation process that you're about toogo through.</span></span>
2. <span data-ttu-id="04dfc-294">Clique com botão direito Olá ToDoListAPI e, em seguida, clique em **Adicionar > REST API cliente**.</span><span class="sxs-lookup"><span data-stu-id="04dfc-294">Right-click hello ToDoListAPI project, and then click **Add > REST API Client**.</span></span>
   
    ![Adicionar o cliente da API REST ao Visual Studio](./media/app-service-api-dotnet-get-started/codegenmenu.png)
3. <span data-ttu-id="04dfc-296">Em Olá **Adicionar cliente de API REST** caixa de diálogo, clique em **URL Swagger**e, em seguida, clique em **selecione Azure ativo**.</span><span class="sxs-lookup"><span data-stu-id="04dfc-296">In hello **Add REST API Client** dialog box, click **Swagger URL**, and then click **Select Azure Asset**.</span></span>
   
    ![Selecionar Ativo do Azure](./media/app-service-api-dotnet-get-started/codegenbrowse.png)
4. <span data-ttu-id="04dfc-298">Em Olá **do serviço de aplicativo** caixa de diálogo, expanda o grupo de recursos de saudação você está usando para este tutorial e selecione seu aplicativo de API e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="04dfc-298">In hello **App Service** dialog box, expand hello resource group you're using for this tutorial and select your API app, and then click **OK**.</span></span>
   
    ![Selecionar aplicativo de API para geração de código](./media/app-service-api-dotnet-get-started/codegenselect.png)
   
    <span data-ttu-id="04dfc-300">Observe que, quando você retornar toohello **Adicionar cliente de API REST** caixa de diálogo, caixa de texto de saudação tenha sido preenchida com definição Olá API valor da URL que você viu anteriormente no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="04dfc-300">Notice that when you return toohello **Add REST API Client** dialog, hello text box has been filled in with hello API definition URL value that you saw earlier in hello portal.</span></span>
   
    ![URL de definição da API](./media/app-service-api-dotnet-get-started/codegenurlplugged.png)
   
   > [!TIP]
   > <span data-ttu-id="04dfc-302">Metadados de tooget uma maneira alternativa para geração de código são tooenter Olá URL diretamente em vez de passar pela caixa de diálogo de procura de saudação.</span><span class="sxs-lookup"><span data-stu-id="04dfc-302">An alternative way tooget metadata for code generation is tooenter hello URL directly instead of going through hello browse dialog.</span></span> <span data-ttu-id="04dfc-303">Se desejar que o código de cliente toogenerate antes de implantar tooAzure, é possível executar o projeto de API da Web hello localmente, vá toohello URL que fornece o arquivo de Swagger JSON hello, salve-Olá, e usar Olá **selecionar um arquivo de metadados do Swagger existente**opção.</span><span class="sxs-lookup"><span data-stu-id="04dfc-303">Or if you want toogenerate client code before deploying tooAzure, you could run hello Web API project locally, go toohello URL that provides hello Swagger JSON file, save hello file, and use hello **Select an existing Swagger metadata file** option.</span></span>
   > 
   > 
5. <span data-ttu-id="04dfc-304">Em Olá **Adicionar cliente de API REST** caixa de diálogo, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="04dfc-304">In hello **Add REST API Client** dialog box, click **OK**.</span></span>
   
    <span data-ttu-id="04dfc-305">Visual Studio cria uma pasta chamada após o aplicativo hello API e gera classes de cliente.</span><span class="sxs-lookup"><span data-stu-id="04dfc-305">Visual Studio creates a folder named after hello API app and generates client classes.</span></span>
   
    ![Arquivos de código para cliente gerado](./media/app-service-api-dotnet-get-started/codegenfiles.png)
6. <span data-ttu-id="04dfc-307">No projeto de ToDoListAPI hello, abra *Controllers\ToDoListController.cs* toosee código de saudação na linha 40 que chama a API hello usando gerada de saudação do cliente.</span><span class="sxs-lookup"><span data-stu-id="04dfc-307">In hello ToDoListAPI project, open *Controllers\ToDoListController.cs* toosee hello code at line 40  that calls hello API by using hello generated client.</span></span>
   
    <span data-ttu-id="04dfc-308">saudação de trecho de código a seguir mostra como o código Olá instancia o objeto de saudação do cliente e chama Olá método Get.</span><span class="sxs-lookup"><span data-stu-id="04dfc-308">hello following snippet shows how hello code instantiates hello client object and calls hello Get method.</span></span>
   
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
   
    <span data-ttu-id="04dfc-309">o parâmetro de construtor Olá obtém URL de ponto de extremidade de saudação do hello `toDoListDataAPIURL` configuração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="04dfc-309">hello constructor parameter gets hello endpoint URL from  hello `toDoListDataAPIURL` app setting.</span></span> <span data-ttu-id="04dfc-310">No arquivo Web. config de hello, esse valor é o conjunto toohello local IIS Express URL da API de saudação do projeto para que você possa executar o aplicativo hello localmente.</span><span class="sxs-lookup"><span data-stu-id="04dfc-310">In hello Web.config file, that value is set toohello local IIS Express URL of hello API project so that you can run hello application locally.</span></span> <span data-ttu-id="04dfc-311">Se você omitir o parâmetro de construtor Olá, o ponto de extremidade saudação padrão é a URL de Olá que gerou o código de saudação do.</span><span class="sxs-lookup"><span data-stu-id="04dfc-311">If you omit hello constructor parameter, hello default endpoint is hello URL that you generated hello code from.</span></span>
7. <span data-ttu-id="04dfc-312">A classe de cliente será gerado com um nome diferente com base no nome do aplicativo de API; alterar o código de saudação em *Controllers\ToDoListController.cs* para que hello tipo nome coincide com o que foi gerado em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="04dfc-312">Your client class will be generated with a different name based on your API app name; change hello code in *Controllers\ToDoListController.cs* so that hello type name matches what was generated in your project.</span></span> <span data-ttu-id="04dfc-313">Por exemplo, se chamar o aplicativo de API de ToDoListDataAPI071316, você alterará este código:</span><span class="sxs-lookup"><span data-stu-id="04dfc-313">For example, if you named your API App ToDoListDataAPI071316, you would change this code:</span></span>
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));

<span data-ttu-id="04dfc-314">toothis:</span><span class="sxs-lookup"><span data-stu-id="04dfc-314">toothis:</span></span>

        private static ToDoListDataAPI071316 NewDataAPIClient()
        {
            var client = new ToDoListDataAPI071316(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));


## <a name="create-an-api-app-toohost-hello-middle-tier"></a><span data-ttu-id="04dfc-315">Criar uma camada intermediária do API aplicativo toohost Olá</span><span class="sxs-lookup"><span data-stu-id="04dfc-315">Create an API app toohost hello middle tier</span></span>
<span data-ttu-id="04dfc-316">Anteriormente você [criado o aplicativo de API de camada de dados hello e implantado código tooit](#createapiapp).</span><span class="sxs-lookup"><span data-stu-id="04dfc-316">Earlier you [created hello data tier API app and deployed code tooit](#createapiapp).</span></span>  <span data-ttu-id="04dfc-317">Agora que você siga Olá mesmo procedimento para o aplicativo de camada intermediária API hello.</span><span class="sxs-lookup"><span data-stu-id="04dfc-317">Now you follow hello same procedure for hello middle tier API app.</span></span>

1. <span data-ttu-id="04dfc-318">Em **Solution Explorer**, com o botão direito Olá intermediária ToDoListAPI (não camada de dados de saudação ToDoListDataAPI) do projeto e, em seguida, clique em **publicar**.</span><span class="sxs-lookup"><span data-stu-id="04dfc-318">In **Solution Explorer**, right-click hello middle tier ToDoListAPI  project (not hello data tier ToDoListDataAPI), and then click **Publish**.</span></span>
   
    ![Clicar em Publicar no Visual Studio](./media/app-service-api-dotnet-get-started/pubinmenu2.png)
2. <span data-ttu-id="04dfc-320">Em Olá **perfil** guia da saudação **Publicar Web** assistente, clique em **serviço de aplicativo do Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="04dfc-320">In hello **Profile** tab of hello **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="04dfc-321">Em Olá **do serviço de aplicativo** caixa de diálogo, clique em **novo**.</span><span class="sxs-lookup"><span data-stu-id="04dfc-321">In hello **App Service** dialog box, click **New**.</span></span>
4. <span data-ttu-id="04dfc-322">Em Olá **hospedagem** guia da saudação **criar serviço de aplicativo** caixa de diálogo caixa, aceite o padrão de saudação **API App Name** ou digite um nome que seja exclusivo no hello  *azurewebsites.NET* domínio.</span><span class="sxs-lookup"><span data-stu-id="04dfc-322">In hello **Hosting** tab of hello **Create App Service** dialog box, accept hello default **API App Name** or enter a name that is unique in hello *azurewebsites.net* domain.</span></span>
5. <span data-ttu-id="04dfc-323">Escolha hello Azure **assinatura** que foi usado.</span><span class="sxs-lookup"><span data-stu-id="04dfc-323">Choose hello Azure **Subscription** you have been using.</span></span>
6. <span data-ttu-id="04dfc-324">Em Olá **grupo de recursos** lista suspensa, escolha Olá mesmo grupo de recursos que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="04dfc-324">In hello **Resource Group** drop-down, choose hello same resource group you created earlier.</span></span>
7. <span data-ttu-id="04dfc-325">Em Olá **plano do serviço de aplicativo** lista suspensa, escolha Olá mesmo plano que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="04dfc-325">In hello **App Service Plan** drop-down, choose hello same plan you created earlier.</span></span> <span data-ttu-id="04dfc-326">O padrão será o valor de toothat.</span><span class="sxs-lookup"><span data-stu-id="04dfc-326">It will default toothat value.</span></span>
8. <span data-ttu-id="04dfc-327">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="04dfc-327">Click **Create**.</span></span>
   
    <span data-ttu-id="04dfc-328">Visual Studio cria o aplicativo hello API, cria um perfil de publicação para ele e exibe o saudação **Conexão** etapa Olá **Publicar Web** assistente.</span><span class="sxs-lookup"><span data-stu-id="04dfc-328">Visual Studio creates hello API app, creates a publish profile for it, and displays hello **Connection** step of hello **Publish Web** wizard.</span></span>
9. <span data-ttu-id="04dfc-329">Em Olá **Conexão** etapa Olá **Publicar Web** assistente, clique em **publicar**.</span><span class="sxs-lookup"><span data-stu-id="04dfc-329">In hello **Connection** step of hello **Publish Web** wizard, click **Publish**.</span></span>
   
   <span data-ttu-id="04dfc-330">Visual Studio implanta Olá ToDoListAPI projeto toohello novo aplicativo de API e abre uma URL de toohello do navegador de saudação do aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="04dfc-330">Visual Studio deploys hello ToDoListAPI project toohello new API app and opens a browser toohello URL of hello API app.</span></span> <span data-ttu-id="04dfc-331">página Hello "criado com êxito" será exibida.</span><span class="sxs-lookup"><span data-stu-id="04dfc-331">hello "successfully created" page appears.</span></span>

## <a name="configure-hello-middle-tier-toocall-hello-data-tier"></a><span data-ttu-id="04dfc-332">Configurar a camada de dados Olá camada intermediária toocall Olá</span><span class="sxs-lookup"><span data-stu-id="04dfc-332">Configure hello middle tier toocall hello data tier</span></span>
<span data-ttu-id="04dfc-333">Se você chamou o aplicativo de API de camada intermediária Olá agora, ele seria tente toocall da camada de dados de saudação usando Olá localhost URL que ainda está no arquivo Web. config de saudação.</span><span class="sxs-lookup"><span data-stu-id="04dfc-333">If you called hello middle tier API app now, it would try toocall hello data tier using hello localhost URL that is still in hello Web.config file.</span></span> <span data-ttu-id="04dfc-334">Nesta seção você inserir a URL do aplicativo de API do hello dados da camada em uma configuração de ambiente no aplicativo de API de camada intermediária hello.</span><span class="sxs-lookup"><span data-stu-id="04dfc-334">In this section you enter hello data tier API app URL into an environment setting in hello middle tier API app.</span></span> <span data-ttu-id="04dfc-335">Quando hello código no aplicativo de API de camada intermediária Olá recupera configuração de URL de camada de dados hello, configuração do ambiente de saudação substituirá o que está no arquivo Web. config de saudação.</span><span class="sxs-lookup"><span data-stu-id="04dfc-335">When hello code in hello middle tier API app retrieves hello data tier URL setting, hello environment setting will override what's in hello Web.config file.</span></span>

1. <span data-ttu-id="04dfc-336">Vá toohello [portal do Azure](https://portal.azure.com/)e, em seguida, navegue toohello **API App** folha para o aplicativo hello API que você criou o projeto do toohost Olá TodoListAPI (camada intermediária).</span><span class="sxs-lookup"><span data-stu-id="04dfc-336">Go toohello [Azure portal](https://portal.azure.com/), and then navigate toohello **API App** blade for hello API app that you created toohost hello TodoListAPI (middle tier) project.</span></span>
2. <span data-ttu-id="04dfc-337">Em Olá da API App **configurações** folha, clique em **configurações de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="04dfc-337">In hello API App's **Settings** blade, click **Application settings**.</span></span>
3. <span data-ttu-id="04dfc-338">Em Olá da API App **configurações do aplicativo** folha, role para baixo toohello **configurações do aplicativo** seção e adicione o seguinte Olá chave e valor.</span><span class="sxs-lookup"><span data-stu-id="04dfc-338">In hello API App's **Application Settings** blade, scroll down toohello **App settings** section and add hello following key and value.</span></span> <span data-ttu-id="04dfc-339">valor de saudação será Olá URL da API de saudação primeiro aplicativo publicado neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="04dfc-339">hello value will be hello URL of hello first API App you published in this tutorial.</span></span>
   
   | <span data-ttu-id="04dfc-340">**Chave**</span><span class="sxs-lookup"><span data-stu-id="04dfc-340">**Key**</span></span> | <span data-ttu-id="04dfc-341">toDoListDataAPIURL</span><span class="sxs-lookup"><span data-stu-id="04dfc-341">toDoListDataAPIURL</span></span> |
   | --- | --- |
   | <span data-ttu-id="04dfc-342">**Valor**</span><span class="sxs-lookup"><span data-stu-id="04dfc-342">**Value**</span></span> |<span data-ttu-id="04dfc-343">https://{nome do aplicativo de API da sua camada de dados}.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="04dfc-343">https://{your data tier API app name}.azurewebsites.net</span></span> |
   | <span data-ttu-id="04dfc-344">**Exemplo**</span><span class="sxs-lookup"><span data-stu-id="04dfc-344">**Example**</span></span> |<span data-ttu-id="04dfc-345">https://todolistdataapi.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="04dfc-345">https://todolistdataapi.azurewebsites.net</span></span> |
4. <span data-ttu-id="04dfc-346">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="04dfc-346">Click **Save**.</span></span>
   
    ![Clicar em Salvar para Configurações de Aplicativo](./media/app-service-api-dotnet-get-started/asinportal.png)
   
    <span data-ttu-id="04dfc-348">Quando o código de saudação é executado no Azure, esse valor substituirá agora Olá localhost URL que está no arquivo Web. config de saudação.</span><span class="sxs-lookup"><span data-stu-id="04dfc-348">When hello code runs in Azure, this value will now override hello localhost URL that is in hello Web.config file.</span></span>

## <a name="test"></a><span data-ttu-id="04dfc-349">Teste</span><span class="sxs-lookup"><span data-stu-id="04dfc-349">Test</span></span>
1. <span data-ttu-id="04dfc-350">Em uma janela de navegador, procure toohello URL de camada intermediária novo aplicativo de API que você acabou de criar para ToDoListAPI hello.</span><span class="sxs-lookup"><span data-stu-id="04dfc-350">In a browser window, browse toohello URL of hello new middle tier API app that you just created for ToDoListAPI.</span></span> <span data-ttu-id="04dfc-351">Você pode chegar lá clicando em URL Olá na folha de principal do aplicativo hello API no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="04dfc-351">You can get there by clicking hello URL in hello API app's main blade in hello portal.</span></span>
2. <span data-ttu-id="04dfc-352">Adicionar URL de toohello "swagger" na barra de endereços do navegador hello e pressione Enter.</span><span class="sxs-lookup"><span data-stu-id="04dfc-352">Add "swagger" toohello URL in hello browser's address bar, and then press Enter.</span></span> <span data-ttu-id="04dfc-353">(Olá URL é `http://{apiappname}.azurewebsites.net/swagger`.)</span><span class="sxs-lookup"><span data-stu-id="04dfc-353">(hello URL is `http://{apiappname}.azurewebsites.net/swagger`.)</span></span>
   
    <span data-ttu-id="04dfc-354">navegador exibe Olá Olá mesmo Swagger da interface do usuário que você viu anteriormente para ToDoListDataAPI, mas agora `owner` não é um campo obrigatório para a operação de obtenção de hello, porque o aplicativo de camada intermediária API hello está enviando esse aplicativo de API do valor toohello dados da camada para você.</span><span class="sxs-lookup"><span data-stu-id="04dfc-354">hello browser displays hello same Swagger UI that you saw earlier for ToDoListDataAPI, but now `owner` is not a required field for hello Get operation, because hello middle tier API app is sending that value toohello data tier API app for you.</span></span> <span data-ttu-id="04dfc-355">(Hello tutoriais de autenticação, camada intermediária Olá enviará as IDs de usuário real para Olá `owner` parâmetro; para agora ela é codificar um asterisco.)</span><span class="sxs-lookup"><span data-stu-id="04dfc-355">(When you do hello authentication tutorials, hello middle tier will send actual user IDs for hello `owner` parameter; for now it is hard-coding an asterisk.)</span></span>
3. <span data-ttu-id="04dfc-356">Experimente Olá método Get e hello toovalidate outros métodos que Olá aplicativo de API de camada intermediária é com êxito chamando Olá da camada de dados do aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="04dfc-356">Try out hello Get method and hello other methods toovalidate that hello middle tier API app is successfully calling hello data tier API app.</span></span>
   
    ![Método Get da interface do usuário do Swagger](./media/app-service-api-dotnet-get-started/midtierget.png)

## <a name="troubleshooting"></a><span data-ttu-id="04dfc-358">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="04dfc-358">Troubleshooting</span></span>
<span data-ttu-id="04dfc-359">Caso você encontre um problema ao percorrer este tutorial, aqui estão algumas ideias para solução de problemas:</span><span class="sxs-lookup"><span data-stu-id="04dfc-359">In case you run into a problem as you go through this tutorial here are some troubleshooting ideas:</span></span>

* <span data-ttu-id="04dfc-360">Certifique-se de que você está usando a versão mais recente de saudação do hello [SDK do Azure para .NET](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="04dfc-360">Make sure that you're using hello latest version of hello [Azure SDK for .NET](http://go.microsoft.com/fwlink/?linkid=518003).</span></span>
* <span data-ttu-id="04dfc-361">Dois nomes de saudação do projeto são semelhante (ToDoListAPI, ToDoListDataAPI).</span><span class="sxs-lookup"><span data-stu-id="04dfc-361">Two of hello project names are similar (ToDoListAPI, ToDoListDataAPI).</span></span> <span data-ttu-id="04dfc-362">Se não estiver tudo conforme descrito nas instruções de hello quando você estiver trabalhando com um projeto, certifique-se de que abrir projeto correto hello.</span><span class="sxs-lookup"><span data-stu-id="04dfc-362">If things don't look as described in hello instructions when you are working with a project, make sure you have opened hello correct project.</span></span>
* <span data-ttu-id="04dfc-363">Se você estiver em uma rede corporativa e está tentando toodeploy tooAzure do serviço de aplicativo por meio de um firewall, certifique-se de que as portas 443 e 8172 estão abertas para implantação da Web.</span><span class="sxs-lookup"><span data-stu-id="04dfc-363">If you're on a corporate network and are trying toodeploy tooAzure App Service through a firewall, make sure that ports 443 and 8172 are open for Web Deploy.</span></span> <span data-ttu-id="04dfc-364">Se não puder abrir essas portas, você poderá usar outros métodos de implantação.</span><span class="sxs-lookup"><span data-stu-id="04dfc-364">If you can't open those ports, you can use other deployment methods.</span></span>  <span data-ttu-id="04dfc-365">Consulte [implantar tooAzure seu aplicativo do serviço de aplicativo](../app-service-web/web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="04dfc-365">See [Deploy your app tooAzure App Service](../app-service-web/web-sites-deploy.md).</span></span>
* <span data-ttu-id="04dfc-366">Erros de "nomes de rota devem ser exclusivos" – você pode obter essas se você acidentalmente implantar Olá projeto errado tooan API do aplicativo e, posteriormente, implante Olá tooit correta de um.</span><span class="sxs-lookup"><span data-stu-id="04dfc-366">"Route names must be unique" errors -- you could get these if you accidentally deploy hello wrong project tooan API app and then later deploy hello correct one tooit.</span></span> <span data-ttu-id="04dfc-367">toocorrect, reimplantação Olá projeto correto toohello API aplic e em Olá **configurações** guia da saudação **Publicar Web** assistente, selecione **remover arquivos adicionais no destino**.</span><span class="sxs-lookup"><span data-stu-id="04dfc-367">toocorrect this, redeploy hello correct project toohello API app, and on hello **Settings** tab of hello **Publish Web** wizard select **Remove additional files at destination**.</span></span>

<span data-ttu-id="04dfc-368">Depois de ter seu aplicativo de API do ASP.NET em execução no serviço de aplicativo do Azure, talvez você queira toolearn mais sobre os recursos do Visual Studio que simplificam a solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="04dfc-368">After you have your ASP.NET API app running in Azure App Service, you may want toolearn more about Visual Studio features that simplify troubleshooting.</span></span> <span data-ttu-id="04dfc-369">Para saber mais sobre o registro em log, a depuração remota e muito mais, confira [Solução de problemas dos aplicativos do Serviço de Aplicativo do Azure no Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="04dfc-369">For information about logging, remote debugging, and more, see  [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="04dfc-370">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="04dfc-370">Next steps</span></span>
<span data-ttu-id="04dfc-371">Você viu como toodeploy API da Web projetos tooAPI aplicativos existentes, gerar o código do cliente para aplicativos de API e consumir aplicativos de API de clientes .NET.</span><span class="sxs-lookup"><span data-stu-id="04dfc-371">You've seen how toodeploy existing Web API projects tooAPI apps, generate client code for API apps, and consume API apps from .NET clients.</span></span> <span data-ttu-id="04dfc-372">tutorial Avançar Olá nesta série mostra como muito[usar CORS tooconsume API aplicativos clientes do JavaScript](app-service-api-cors-consume-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="04dfc-372">hello next tutorial in this series shows how too[use CORS tooconsume API apps from JavaScript clients](app-service-api-cors-consume-javascript.md).</span></span>

<span data-ttu-id="04dfc-373">Para obter mais informações sobre geração de código de cliente, consulte Olá [Azure/AutoRest](https://github.com/azure/autorest) repositório em GitHub.com. Para obter ajuda com problemas para usar o cliente Olá gerado, abra um [problema no repositório de AutoRest Olá](https://github.com/azure/autorest/issues).</span><span class="sxs-lookup"><span data-stu-id="04dfc-373">For more information about client code generation, see hello [Azure/AutoRest](https://github.com/azure/autorest) repository on GitHub.com. For help with problems using hello generated client, open an [issue in hello AutoRest repository](https://github.com/azure/autorest/issues).</span></span>

<span data-ttu-id="04dfc-374">Se você quiser toocreate novos projetos de API aplicativo do zero, use Olá **aplicativo de API do Azure** modelo.</span><span class="sxs-lookup"><span data-stu-id="04dfc-374">If you want toocreate new API app projects from scratch, use hello **Azure API App** template.</span></span>

![Modelo de Aplicativo de API no Visual Studio](./media/app-service-api-dotnet-get-started/apiapptemplate.png)

<span data-ttu-id="04dfc-376">Olá **aplicativo de API do Azure** modelo de projeto é o equivalente toochoosing Olá **vazio** ASP.NET 4.5.2 modelo, clicando no suporte da API da Web tooadd Olá caixa de seleção e, em seguida, instalar Olá pacote Swashbuckle NuGet.</span><span class="sxs-lookup"><span data-stu-id="04dfc-376">hello **Azure API App** project template is equivalent toochoosing hello **Empty** ASP.NET 4.5.2 template, clicking hello check box tooadd Web API support, and installing hello Swashbuckle NuGet package.</span></span> <span data-ttu-id="04dfc-377">Além disso, o modelo de saudação adiciona alguns Swashbuckle configuração código desenvolvido tooprevent Olá criação da operação de Swagger duplicada IDs.</span><span class="sxs-lookup"><span data-stu-id="04dfc-377">In addition, hello template adds some Swashbuckle configuration code designed tooprevent hello creation of duplicate Swagger operation IDs.</span></span> <span data-ttu-id="04dfc-378">Depois de criar um projeto de API App, você pode implantá-lo tooan API Olá de aplicativo mesmo modo que você viu neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="04dfc-378">Once you've created an API App project, you can deploy it tooan API app hello same way you saw in this tutorial.</span></span>

