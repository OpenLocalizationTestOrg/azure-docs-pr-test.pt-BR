---
title: "Criar sua primeira função no Azure usando o Visual Studio | Microsoft Docs"
description: "Criar e publicar uma função disparada por HTTP simples no Azure usando Ferramentas do Azure Functions para Visual Studio."
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
ms.openlocfilehash: 04370558725d76ffe83d8aaf5d16c88fd2803ba9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-function-using-visual-studio"></a><span data-ttu-id="3c206-104">Criar sua primeira função usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3c206-104">Create your first function using Visual Studio</span></span>

<span data-ttu-id="3c206-105">O Azure Functions lhe permite executar seu código em um ambiente sem servidor sem que seja preciso primeiro criar uma VM ou publicar um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="3c206-105">Azure Functions lets you execute your code in a serverless environment without having to first create a VM or publish a web application.</span></span>

<span data-ttu-id="3c206-106">Neste tópico, você aprenderá a usar as ferramentas do Visual Studio 2017 para Azure Functions para criar e testar uma função "hello world" localmente.</span><span class="sxs-lookup"><span data-stu-id="3c206-106">In this topic, you learn how to use the Visual Studio 2017 tools for Azure Functions to create and test a "hello world" function locally.</span></span> <span data-ttu-id="3c206-107">Em seguida, você publicará o código de função no Azure.</span><span class="sxs-lookup"><span data-stu-id="3c206-107">You will then publish the function code to Azure.</span></span> <span data-ttu-id="3c206-108">Essas ferramentas estão disponíveis como parte da carga de trabalho de desenvolvimento do Azure no Visual Studio 2017 versão 15.3 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="3c206-108">These tools are available as part of the Azure development workload in Visual Studio 2017 version 15.3, or a later version.</span></span>

![Código do Azure Functions em um projeto do Visual Studio](./media/functions-create-your-first-function-visual-studio/functions-vstools-intro.png)

## <a name="prerequisites"></a><span data-ttu-id="3c206-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3c206-110">Prerequisites</span></span>

<span data-ttu-id="3c206-111">Para concluir este tutorial, instale:</span><span class="sxs-lookup"><span data-stu-id="3c206-111">To complete this tutorial, install:</span></span>

* <span data-ttu-id="3c206-112">[Visual Studio 2017 versão 15.3](https://www.visualstudio.com/vs/preview/), incluindo a carga de trabalho de **desenvolvimento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="3c206-112">[Visual Studio 2017 version 15.3](https://www.visualstudio.com/vs/preview/), including the **Azure development** workload.</span></span>

    ![Instalar o Visual Studio de 2017 com a carga de trabalho de desenvolvimento do Azure](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)
    
    >[!NOTE]  
    <span data-ttu-id="3c206-114">Depois de instalar ou fazer upgrade para o Visual Studio 2017 versão 15,3, talvez você também precise atualizar manualmente as ferramentas do Visual Studio de 2017 para Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="3c206-114">After you install or upgrade to Visual Studio 2017 version 15.3, you might also need to manually update the Visual Studio 2017 tools for Azure Functions.</span></span> <span data-ttu-id="3c206-115">Você pode atualizar as ferramentas no menu **Ferramentas**, em **Extensões e atualizações...** > **Atualizações** > **Visual Studio Marketplace** > **Ferramentas Azure Functions e Trabalhos da Web** > **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="3c206-115">You can update the tools from the **Tools** menu under **Extensions and Updates...** > **Updates** > **Visual Studio Marketplace** > **Azure Functions and Web Jobs Tools** > **Update**.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] 

## <a name="create-an-azure-functions-project-in-visual-studio"></a><span data-ttu-id="3c206-116">Criar um projeto do Azure Functions no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3c206-116">Create an Azure Functions project in Visual Studio</span></span>

[!INCLUDE [Create a project using the Azure Functions template](../../includes/functions-vstools-create.md)]

<span data-ttu-id="3c206-117">Agora que você criou o projeto, poderá criar sua primeira função.</span><span class="sxs-lookup"><span data-stu-id="3c206-117">Now that you have created the project, you can create your first function.</span></span>

## <a name="create-the-function"></a><span data-ttu-id="3c206-118">Criar a função</span><span class="sxs-lookup"><span data-stu-id="3c206-118">Create the function</span></span>

1. <span data-ttu-id="3c206-119">No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó do projeto e selecione **Adicionar** > **Novo Item**.</span><span class="sxs-lookup"><span data-stu-id="3c206-119">In **Solution Explorer**, right-click on your project node and select **Add** > **New Item**.</span></span> <span data-ttu-id="3c206-120">Selecione **Azure Function** e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="3c206-120">Select **Azure Function** and click **Add**.</span></span>

2. <span data-ttu-id="3c206-121">Selecione **HttpTrigger**, digite um **Nome da Função**, selecione **Anônimo** para **Direitos de Acesso**e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3c206-121">Select **HttpTrigger**, type a **Function Name**, select **Anonymous** for **Access Rights**, and click **Create**.</span></span> <span data-ttu-id="3c206-122">A função criada é acessada por uma solicitação HTTP de qualquer cliente.</span><span class="sxs-lookup"><span data-stu-id="3c206-122">The function created is accessed by an HTTP request from any client.</span></span> 

    ![Criar uma nova função do Azure](./media/functions-create-your-first-function-visual-studio/functions-vstools-add-new-function-2.png)

    <span data-ttu-id="3c206-124">Um arquivo de código é adicionado ao seu projeto que contém uma classe que implementa o código de função.</span><span class="sxs-lookup"><span data-stu-id="3c206-124">A code file is added to your project that contains a class that implements your function code.</span></span> <span data-ttu-id="3c206-125">Esse código é baseado em um modelo, que recebe um valor de nome e ecoa esse valor novamente.</span><span class="sxs-lookup"><span data-stu-id="3c206-125">This code is based on a template, which receives a name value and echos it back.</span></span> <span data-ttu-id="3c206-126">O atributo **FunctionName** define o nome da sua função.</span><span class="sxs-lookup"><span data-stu-id="3c206-126">The **FunctionName** attribute sets the name of your function.</span></span> <span data-ttu-id="3c206-127">O atributo **HttpTrigger** indica a mensagem que dispara a função.</span><span class="sxs-lookup"><span data-stu-id="3c206-127">The **HttpTrigger** attribute indicates the message that triggers the function.</span></span> 

    ![Arquivo do código de função](./media/functions-create-your-first-function-visual-studio/functions-code-page.png)

<span data-ttu-id="3c206-129">Agora que você criou uma função disparada por HTTP, poderá testá-la em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="3c206-129">Now that you have created an HTTP-triggered function, you can test it on your local computer.</span></span>

## <a name="test-the-function-locally"></a><span data-ttu-id="3c206-130">Testar a função localmente</span><span class="sxs-lookup"><span data-stu-id="3c206-130">Test the function locally</span></span>

<span data-ttu-id="3c206-131">As Ferramentas Principais do Azure Functions permitem executar o projeto do Azure Functions no seu computador de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="3c206-131">Azure Functions Core Tools lets you run Azure Functions project on your local development computer.</span></span> <span data-ttu-id="3c206-132">Você precisa instalar essas ferramentas na primeira vez em que inicia uma função no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3c206-132">You are prompted to install these tools the first time you start a function from Visual Studio.</span></span>  

1. <span data-ttu-id="3c206-133">Para testar sua função, pressione F5.</span><span class="sxs-lookup"><span data-stu-id="3c206-133">To test your function, press F5.</span></span> <span data-ttu-id="3c206-134">Se solicitado, aceite a solicitação do Visual Studio para baixar e instalar as ferramentas principais (CLI) do Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="3c206-134">If prompted, accept the request from Visual Studio to download and install Azure Functions Core (CLI) tools.</span></span>  <span data-ttu-id="3c206-135">Você também precisará habilitar a exceção de firewall de forma que as ferramentas possam lidar com solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="3c206-135">You may also need to enable a firewall exception so that the tools can handle HTTP requests.</span></span>

2. <span data-ttu-id="3c206-136">Copie a URL da sua função da saída de tempo de execução do Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="3c206-136">Copy the URL of your function from the Azure Functions runtime output.</span></span>  

    ![Tempo de execução local do Azure](./media/functions-create-your-first-function-visual-studio/functions-vstools-f5.png)

3. <span data-ttu-id="3c206-138">Cole a URL para a solicitação HTTP na barra de endereços do navegador.</span><span class="sxs-lookup"><span data-stu-id="3c206-138">Paste the URL for the HTTP request into your browser's address bar.</span></span> <span data-ttu-id="3c206-139">Acrescente o valor de cadeia de consulta `&name=<yourname>` a essa URL e execute a solicitação.</span><span class="sxs-lookup"><span data-stu-id="3c206-139">Append the query string `&name=<yourname>` to this URL and execute the request.</span></span> <span data-ttu-id="3c206-140">O exemplo a seguir mostra a resposta no navegador à solicitação GET local retornada pela função:</span><span class="sxs-lookup"><span data-stu-id="3c206-140">The following shows the response in the browser to the local GET request returned by the function:</span></span> 

    ![Resposta da função localhost no navegador](./media/functions-create-your-first-function-visual-studio/functions-test-local-browser.png)

4. <span data-ttu-id="3c206-142">Para interromper a depuração, clique no botão **Parar** na barra de ferramentas do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3c206-142">To stop debugging, click the **Stop** button on the Visual Studio toolbar.</span></span>

<span data-ttu-id="3c206-143">Após verificar se a função foi executada corretamente no computador local, é hora de publicar o projeto no Azure.</span><span class="sxs-lookup"><span data-stu-id="3c206-143">After you have verified that the function runs correctly on your local computer, it's time to publish the project to Azure.</span></span>

## <a name="publish-the-project-to-azure"></a><span data-ttu-id="3c206-144">Publicar o projeto no Azure</span><span class="sxs-lookup"><span data-stu-id="3c206-144">Publish the project to Azure</span></span>

<span data-ttu-id="3c206-145">Você deve ter um aplicativo de funções em sua assinatura do Azure antes de publicar seu projeto.</span><span class="sxs-lookup"><span data-stu-id="3c206-145">You must have a function app in your Azure subscription before you can publish your project.</span></span> <span data-ttu-id="3c206-146">Você pode criar um aplicativo de funções diretamente no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3c206-146">You can create a function app right from Visual Studio.</span></span>

[!INCLUDE [Publish the project to Azure](../../includes/functions-vstools-publish.md)]

## <a name="test-your-function-in-azure"></a><span data-ttu-id="3c206-147">Testar sua função no Azure</span><span class="sxs-lookup"><span data-stu-id="3c206-147">Test your function in Azure</span></span>

1. <span data-ttu-id="3c206-148">Copie a URL base do aplicativo de funções da página de perfil de publicação.</span><span class="sxs-lookup"><span data-stu-id="3c206-148">Copy the base URL of the function app from the Publish profile page.</span></span> <span data-ttu-id="3c206-149">Substitua a parte `localhost:port` da URL que você usou ao testar a função localmente pela nova URL base.</span><span class="sxs-lookup"><span data-stu-id="3c206-149">Replace the `localhost:port` portion of the URL you used when testing the function locally with the new base URL.</span></span> <span data-ttu-id="3c206-150">Como anteriormente, acrescente o valor de cadeia de consulta `&name=<yourname>` a essa URL e execute a solicitação.</span><span class="sxs-lookup"><span data-stu-id="3c206-150">As before, make sure to append the query string `&name=<yourname>` to this URL and execute the request.</span></span>

    <span data-ttu-id="3c206-151">A URL que chama a função disparada por HTTP é mais ou menos assim:</span><span class="sxs-lookup"><span data-stu-id="3c206-151">The URL that calls your HTTP triggered function looks like this:</span></span>

        http://<functionappname>.azurewebsites.net/api/<functionname>?name=<yourname> 

2. <span data-ttu-id="3c206-152">Cole essa nova URL para a solicitação HTTP na barra de endereços do navegador.</span><span class="sxs-lookup"><span data-stu-id="3c206-152">Paste this new URL for the HTTP request into your browser's address bar.</span></span> <span data-ttu-id="3c206-153">O exemplo a seguir mostra a resposta no navegador à solicitação GET remota retornada pela função:</span><span class="sxs-lookup"><span data-stu-id="3c206-153">The following shows the response in the browser to the remote GET request returned by the function:</span></span> 

    ![Resposta da função no navegador](./media/functions-create-your-first-function-visual-studio/functions-test-remote-browser.png)
 
## <a name="next-steps"></a><span data-ttu-id="3c206-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3c206-155">Next steps</span></span>

<span data-ttu-id="3c206-156">Você usou o Visual Studio para criar um aplicativo de funções C# com uma função disparada por HTTP simples.</span><span class="sxs-lookup"><span data-stu-id="3c206-156">You have used Visual Studio to create a C# function app with a simple HTTP triggered function.</span></span> 

+ <span data-ttu-id="3c206-157">Para saber como configurar seu projeto para dar suporte a outros tipos de gatilhos e associações, consulte a seção [Configurar o projeto para desenvolvimento local](functions-develop-vs.md#configure-the-project-for-local-development) em [Ferramentas do Azure Functions para Visual Studio](functions-develop-vs.md).</span><span class="sxs-lookup"><span data-stu-id="3c206-157">To learn how to configure your project to support other types of triggers and bindings, see the [Configure the project for local development](functions-develop-vs.md#configure-the-project-for-local-development) section in [Azure Functions Tools for Visual Studio](functions-develop-vs.md).</span></span>
+ <span data-ttu-id="3c206-158">Para saber mais sobre o local de teste e a depuração usando as Ferramentas Principais do Azure Functions, confira [Codificar e testar o Azure Functions localmente](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="3c206-158">To learn more about local testing and debugging using the Azure Functions Core Tools, see [Code and test Azure Functions locally](functions-run-local.md).</span></span> 
+ <span data-ttu-id="3c206-159">Para saber mais sobre como desenvolver funções como bibliotecas de classes do .NET, veja [Como usar bibliotecas de classes do .NET com o Azure Functions](functions-dotnet-class-library.md).</span><span class="sxs-lookup"><span data-stu-id="3c206-159">To learn more about developing functions as .NET class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span> 

