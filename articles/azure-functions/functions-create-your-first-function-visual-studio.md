---
title: "aaaCreate sua primeira função no Azure usando o Visual Studio | Microsoft Docs"
description: "Criar e publicar um tooAzure de função HTTP disparado simple usando ferramentas de funções do Azure para Visual Studio."
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
editor: 
tags: 
keywords: "azure functions, funções, processamento de eventos, computação, arquitetura sem servidor"
ms.assetid: 82db1177-2295-4e39-bd42-763f6082e796
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 07/05/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 851e5b98dcc2da00334620896a0ea31f566589f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-using-visual-studio"></a><span data-ttu-id="bfc38-104">Criar sua primeira função usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bfc38-104">Create your first function using Visual Studio</span></span>

<span data-ttu-id="bfc38-105">As funções do Azure permite que você execute seu código em um ambiente sem servidor sem ter que toofirst criar uma VM ou publicar um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="bfc38-105">Azure Functions lets you execute your code in a serverless environment without having toofirst create a VM or publish a web application.</span></span>

<span data-ttu-id="bfc38-106">Neste tópico, você aprenderá como toouse Olá 2017 do Visual Studio tools para toocreate de funções do Azure e testar uma função de "hello world" localmente.</span><span class="sxs-lookup"><span data-stu-id="bfc38-106">In this topic, you learn how toouse hello Visual Studio 2017 tools for Azure Functions toocreate and test a "hello world" function locally.</span></span> <span data-ttu-id="bfc38-107">Em seguida, você publicará Olá tooAzure de código de função.</span><span class="sxs-lookup"><span data-stu-id="bfc38-107">You will then publish hello function code tooAzure.</span></span> <span data-ttu-id="bfc38-108">Essas ferramentas estão disponíveis como parte da carga de trabalho de desenvolvimento do Azure de saudação no Visual Studio 2017 versão 15,3 ou uma versão posterior.</span><span class="sxs-lookup"><span data-stu-id="bfc38-108">These tools are available as part of hello Azure development workload in Visual Studio 2017 version 15.3, or a later version.</span></span>

![Código do Azure Functions em um projeto do Visual Studio](./media/functions-create-your-first-function-visual-studio/functions-vstools-intro.png)

## <a name="prerequisites"></a><span data-ttu-id="bfc38-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bfc38-110">Prerequisites</span></span>

<span data-ttu-id="bfc38-111">toocomplete este tutorial, instalar:</span><span class="sxs-lookup"><span data-stu-id="bfc38-111">toocomplete this tutorial, install:</span></span>

* <span data-ttu-id="bfc38-112">[Visual Studio 2017 versão 15,3](https://www.visualstudio.com/vs/preview/), incluindo Olá **desenvolvimento do Azure** carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="bfc38-112">[Visual Studio 2017 version 15.3](https://www.visualstudio.com/vs/preview/), including hello **Azure development** workload.</span></span>

    ![Instalar o Visual Studio de 2017 com carga de trabalho de desenvolvimento do Azure Olá](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)
    
    >[!NOTE]  
    <span data-ttu-id="bfc38-114">Depois de instalar ou atualizar tooVisual 2017 Studio versão 15,3, talvez seja necessário também ferramentas de saudação 2017 do Visual Studio atualização toomanually para funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="bfc38-114">After you install or upgrade tooVisual Studio 2017 version 15.3, you might also need toomanually update hello Visual Studio 2017 tools for Azure Functions.</span></span> <span data-ttu-id="bfc38-115">Você pode atualizar as ferramentas de saudação da saudação **ferramentas** menu em **extensões e atualizações...**   >  **Atualizações** > **Visual Studio Marketplace** > **Web e funções do Azure trabalhos ferramentas**  >  **Atualização**.</span><span class="sxs-lookup"><span data-stu-id="bfc38-115">You can update hello tools from hello **Tools** menu under **Extensions and Updates...** > **Updates** > **Visual Studio Marketplace** > **Azure Functions and Web Jobs Tools** > **Update**.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] 

## <a name="create-an-azure-functions-project-in-visual-studio"></a><span data-ttu-id="bfc38-116">Criar um projeto do Azure Functions no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bfc38-116">Create an Azure Functions project in Visual Studio</span></span>

[!INCLUDE [Create a project using hello Azure Functions template](../../includes/functions-vstools-create.md)]

<span data-ttu-id="bfc38-117">Agora que você criou o projeto hello, você pode criar sua primeira função.</span><span class="sxs-lookup"><span data-stu-id="bfc38-117">Now that you have created hello project, you can create your first function.</span></span>

## <a name="create-hello-function"></a><span data-ttu-id="bfc38-118">Criar função hello</span><span class="sxs-lookup"><span data-stu-id="bfc38-118">Create hello function</span></span>

1. <span data-ttu-id="bfc38-119">No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó do projeto e selecione **Adicionar** > **Novo Item**.</span><span class="sxs-lookup"><span data-stu-id="bfc38-119">In **Solution Explorer**, right-click on your project node and select **Add** > **New Item**.</span></span> <span data-ttu-id="bfc38-120">Selecione **Azure Function** e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="bfc38-120">Select **Azure Function** and click **Add**.</span></span>

2. <span data-ttu-id="bfc38-121">Selecione **HttpTrigger**, digite um **Nome da Função**, selecione **Anônimo** para **Direitos de Acesso**e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="bfc38-121">Select **HttpTrigger**, type a **Function Name**, select **Anonymous** for **Access Rights**, and click **Create**.</span></span> <span data-ttu-id="bfc38-122">função Hello criada é acessada por uma solicitação HTTP de qualquer cliente.</span><span class="sxs-lookup"><span data-stu-id="bfc38-122">hello function created is accessed by an HTTP request from any client.</span></span> 

    ![Criar uma nova função do Azure](./media/functions-create-your-first-function-visual-studio/functions-vstools-add-new-function-2.png)

    <span data-ttu-id="bfc38-124">Um arquivo de código é adicionado tooyour projeto que contém uma classe que implementa o código de função.</span><span class="sxs-lookup"><span data-stu-id="bfc38-124">A code file is added tooyour project that contains a class that implements your function code.</span></span> <span data-ttu-id="bfc38-125">Esse código é baseado em um modelo, que recebe um valor de nome e ecoa esse valor novamente.</span><span class="sxs-lookup"><span data-stu-id="bfc38-125">This code is based on a template, which receives a name value and echos it back.</span></span> <span data-ttu-id="bfc38-126">Olá **FunctionName** atributo define o nome de saudação da sua função.</span><span class="sxs-lookup"><span data-stu-id="bfc38-126">hello **FunctionName** attribute sets hello name of your function.</span></span> <span data-ttu-id="bfc38-127">Olá **HttpTrigger** atributo indica a mensagem de saudação que dispara a função hello.</span><span class="sxs-lookup"><span data-stu-id="bfc38-127">hello **HttpTrigger** attribute indicates hello message that triggers hello function.</span></span> 

    ![Arquivo do código de função](./media/functions-create-your-first-function-visual-studio/functions-code-page.png)

<span data-ttu-id="bfc38-129">Agora que você criou uma função disparada por HTTP, poderá testá-la em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="bfc38-129">Now that you have created an HTTP-triggered function, you can test it on your local computer.</span></span>

## <a name="test-hello-function-locally"></a><span data-ttu-id="bfc38-130">Testar função do hello localmente</span><span class="sxs-lookup"><span data-stu-id="bfc38-130">Test hello function locally</span></span>

<span data-ttu-id="bfc38-131">As Ferramentas Principais do Azure Functions permitem executar o projeto do Azure Functions no seu computador de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="bfc38-131">Azure Functions Core Tools lets you run Azure Functions project on your local development computer.</span></span> <span data-ttu-id="bfc38-132">Você é solicitado tooinstall essas ferramentas Olá a primeira vez que iniciar uma função do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bfc38-132">You are prompted tooinstall these tools hello first time you start a function from Visual Studio.</span></span>  

1. <span data-ttu-id="bfc38-133">tootest sua função, pressione F5.</span><span class="sxs-lookup"><span data-stu-id="bfc38-133">tootest your function, press F5.</span></span> <span data-ttu-id="bfc38-134">Se solicitado, aceitar solicitação de saudação de toodownload do Visual Studio e instalar as ferramentas de núcleo de funções do Azure (CLI).</span><span class="sxs-lookup"><span data-stu-id="bfc38-134">If prompted, accept hello request from Visual Studio toodownload and install Azure Functions Core (CLI) tools.</span></span>  <span data-ttu-id="bfc38-135">Tooenable uma exceção de firewall também pode ser necessário para que as ferramentas de saudação podem manipular as solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="bfc38-135">You may also need tooenable a firewall exception so that hello tools can handle HTTP requests.</span></span>

2. <span data-ttu-id="bfc38-136">Copiar URL da saudação da sua função do tempo de execução de funções do Azure Olá de saída.</span><span class="sxs-lookup"><span data-stu-id="bfc38-136">Copy hello URL of your function from hello Azure Functions runtime output.</span></span>  

    ![Tempo de execução local do Azure](./media/functions-create-your-first-function-visual-studio/functions-vstools-f5.png)

3. <span data-ttu-id="bfc38-138">Cole a URL de saudação para solicitação HTTP Olá na barra de endereços do navegador.</span><span class="sxs-lookup"><span data-stu-id="bfc38-138">Paste hello URL for hello HTTP request into your browser's address bar.</span></span> <span data-ttu-id="bfc38-139">Acrescente a cadeia de caracteres de consulta Olá `&name=<yourname>` toothis URL e executar a solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="bfc38-139">Append hello query string `&name=<yourname>` toothis URL and execute hello request.</span></span> <span data-ttu-id="bfc38-140">a seguir Olá mostra a resposta de Olá em Olá navegador toohello local solicitação GET retornada pela função hello:</span><span class="sxs-lookup"><span data-stu-id="bfc38-140">hello following shows hello response in hello browser toohello local GET request returned by hello function:</span></span> 

    ![Resposta da função localhost no navegador Olá](./media/functions-create-your-first-function-visual-studio/functions-test-local-browser.png)

4. <span data-ttu-id="bfc38-142">toostop depuração, clique em Olá **parar** botão na barra de ferramentas do Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="bfc38-142">toostop debugging, click hello **Stop** button on hello Visual Studio toolbar.</span></span>

<span data-ttu-id="bfc38-143">Após ter verificado que função hello seja executado corretamente em seu computador local, é hora toopublish Olá projeto tooAzure.</span><span class="sxs-lookup"><span data-stu-id="bfc38-143">After you have verified that hello function runs correctly on your local computer, it's time toopublish hello project tooAzure.</span></span>

## <a name="publish-hello-project-tooazure"></a><span data-ttu-id="bfc38-144">Publicar Olá projeto tooAzure</span><span class="sxs-lookup"><span data-stu-id="bfc38-144">Publish hello project tooAzure</span></span>

<span data-ttu-id="bfc38-145">Você deve ter um aplicativo de funções em sua assinatura do Azure antes de publicar seu projeto.</span><span class="sxs-lookup"><span data-stu-id="bfc38-145">You must have a function app in your Azure subscription before you can publish your project.</span></span> <span data-ttu-id="bfc38-146">Você pode criar um aplicativo de funções diretamente no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bfc38-146">You can create a function app right from Visual Studio.</span></span>

[!INCLUDE [Publish hello project tooAzure](../../includes/functions-vstools-publish.md)]

## <a name="test-your-function-in-azure"></a><span data-ttu-id="bfc38-147">Testar sua função no Azure</span><span class="sxs-lookup"><span data-stu-id="bfc38-147">Test your function in Azure</span></span>

1. <span data-ttu-id="bfc38-148">Copiar Olá URL base do aplicativo de função de saudação da página de perfil de publicação hello.</span><span class="sxs-lookup"><span data-stu-id="bfc38-148">Copy hello base URL of hello function app from hello Publish profile page.</span></span> <span data-ttu-id="bfc38-149">Substituir saudação `localhost:port` parte da URL Olá usados ao testar a função hello localmente com hello nova URL base.</span><span class="sxs-lookup"><span data-stu-id="bfc38-149">Replace hello `localhost:port` portion of hello URL you used when testing hello function locally with hello new base URL.</span></span> <span data-ttu-id="bfc38-150">Como antes, tornar-se de cadeia de consulta Olá tooappend `&name=<yourname>` toothis URL e executar a solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="bfc38-150">As before, make sure tooappend hello query string `&name=<yourname>` toothis URL and execute hello request.</span></span>

    <span data-ttu-id="bfc38-151">Olá URL que chama o HTTP acionado função esta aparência:</span><span class="sxs-lookup"><span data-stu-id="bfc38-151">hello URL that calls your HTTP triggered function looks like this:</span></span>

        http://<functionappname>.azurewebsites.net/api/<functionname>?name=<yourname> 

2. <span data-ttu-id="bfc38-152">Cole esta nova URL para solicitação HTTP de saudação na barra de endereços do navegador.</span><span class="sxs-lookup"><span data-stu-id="bfc38-152">Paste this new URL for hello HTTP request into your browser's address bar.</span></span> <span data-ttu-id="bfc38-153">a seguir Olá mostra a resposta de Olá em Olá navegador toohello remota solicitação GET retornada pela função hello:</span><span class="sxs-lookup"><span data-stu-id="bfc38-153">hello following shows hello response in hello browser toohello remote GET request returned by hello function:</span></span> 

    ![Resposta de função no navegador Olá](./media/functions-create-your-first-function-visual-studio/functions-test-remote-browser.png)
 
## <a name="next-steps"></a><span data-ttu-id="bfc38-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bfc38-155">Next steps</span></span>

<span data-ttu-id="bfc38-156">Você usou o aplicativo de função de toocreate c# do Visual Studio com uma função HTTP disparado simples.</span><span class="sxs-lookup"><span data-stu-id="bfc38-156">You have used Visual Studio toocreate a C# function app with a simple HTTP triggered function.</span></span> 

+ <span data-ttu-id="bfc38-157">toolearn como tooconfigure toosupport seu projeto outros tipos de gatilhos e associações, consulte Olá [configurar o projeto de saudação de desenvolvimento local](functions-develop-vs.md#configure-the-project-for-local-development) seção [ferramentas de funções do Azure para Visual Studio](functions-develop-vs.md).</span><span class="sxs-lookup"><span data-stu-id="bfc38-157">toolearn how tooconfigure your project toosupport other types of triggers and bindings, see hello [Configure hello project for local development](functions-develop-vs.md#configure-the-project-for-local-development) section in [Azure Functions Tools for Visual Studio](functions-develop-vs.md).</span></span>
+ <span data-ttu-id="bfc38-158">toolearn mais sobre o local de teste e depuração usando hello Azure funções principais ferramentas, consulte [código e teste de funções do Azure localmente](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="bfc38-158">toolearn more about local testing and debugging using hello Azure Functions Core Tools, see [Code and test Azure Functions locally](functions-run-local.md).</span></span> 
+ <span data-ttu-id="bfc38-159">toolearn mais sobre como desenvolver funções como bibliotecas de classes do .NET, consulte [bibliotecas de classes do .NET usando com funções do Azure](functions-dotnet-class-library.md).</span><span class="sxs-lookup"><span data-stu-id="bfc38-159">toolearn more about developing functions as .NET class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span> 

