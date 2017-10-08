---
title: "aaaDevelop funções do Azure usando o Visual Studio | Microsoft Docs"
description: "Saiba como funções toodevelop e teste do Azure usando ferramentas de funções do Azure para Visual Studio de 2017."
services: functions
documentationcenter: .net
author: ggailey777
manager: erikre
editor: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: glenga
ms.openlocfilehash: c9baf882bf58068cb9a8930bea337fe51b2a77ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-tools-for-visual-studio"></a><span data-ttu-id="680c0-103">Ferramentas do Azure Functions para Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="680c0-103">Azure Functions Tools for Visual Studio</span></span>  

<span data-ttu-id="680c0-104">Ferramentas de funções do Azure para Visual Studio de 2017 é uma extensão do Visual Studio que permite que você desenvolver, testar e implantar funções tooAzure de c#.</span><span class="sxs-lookup"><span data-stu-id="680c0-104">Azure Functions Tools for Visual Studio 2017 is an extension for Visual Studio that lets you develop, test, and deploy C# functions tooAzure.</span></span> <span data-ttu-id="680c0-105">Se esta for sua primeira experiência com funções do Azure, você pode aprender mais em [tooAzure uma introdução funções](functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="680c0-105">If this is your first experience with Azure Functions, you can learn more at [An introduction tooAzure Functions](functions-overview.md).</span></span>

<span data-ttu-id="680c0-106">Olá ferramentas de funções do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="680c0-106">hello Azure Functions Tools provides hello following benefits:</span></span> 

* <span data-ttu-id="680c0-107">Editar, criar e executar funções em seu computador de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="680c0-107">Edit, build, and run functions on your local development computer.</span></span> 
* <span data-ttu-id="680c0-108">Publicar diretamente de funções do Azure projeto tooAzure.</span><span class="sxs-lookup"><span data-stu-id="680c0-108">Publish your Azure Functions project directly tooAzure.</span></span> 
* <span data-ttu-id="680c0-109">Use associações de função do WebJobs atributos toodeclare diretamente em Olá código c# em vez de manter um function.json separados para definições de associação.</span><span class="sxs-lookup"><span data-stu-id="680c0-109">Use WebJobs attributes toodeclare function bindings directly in hello C# code instead of maintaining a separate function.json for binding definitions.</span></span>
* <span data-ttu-id="680c0-110">Desenvolver e implantar funções de pré-compiladas C#.</span><span class="sxs-lookup"><span data-stu-id="680c0-110">Develop and deploy pre-compiled C# functions.</span></span> <span data-ttu-id="680c0-111">Funções pré-compiladas fornecem um desempenho de inicialização a frio melhor que funções baseadas em script C#.</span><span class="sxs-lookup"><span data-stu-id="680c0-111">Pre-complied functions provide a better cold-start performance than C# script-based functions.</span></span> 
* <span data-ttu-id="680c0-112">Código de funções em c# tendo todos os benefícios de saudação do desenvolvimento do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="680c0-112">Code your functions in C# while having all of hello benefits of Visual Studio development.</span></span> 

<span data-ttu-id="680c0-113">Este tópico mostra como toouse hello ferramentas de funções do Azure para Visual Studio de 2017 toodevelop funções em c#.</span><span class="sxs-lookup"><span data-stu-id="680c0-113">This topic shows you how toouse hello Azure Functions Tools for Visual Studio 2017 toodevelop your functions in C#.</span></span> <span data-ttu-id="680c0-114">Você também aprenderá como toopublish tooAzure seu projeto como um assembly do .NET.</span><span class="sxs-lookup"><span data-stu-id="680c0-114">You also learn how toopublish your project tooAzure as a .NET assembly.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="680c0-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="680c0-115">Prerequisites</span></span>

<span data-ttu-id="680c0-116">Ferramentas de funções do Azure está incluída na carga de trabalho de desenvolvimento do Azure de saudação do [Visual Studio 2017 versão 15,3](https://www.visualstudio.com/vs/), ou uma versão posterior.</span><span class="sxs-lookup"><span data-stu-id="680c0-116">Azure Functions Tools is included in hello Azure development workload of [Visual Studio 2017 version 15.3](https://www.visualstudio.com/vs/), or a later version.</span></span> <span data-ttu-id="680c0-117">Certifique-se de incluir Olá **desenvolvimento do Azure** cargas de trabalho em sua instalação de versão 15,3 2017 do Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="680c0-117">Make sure you include hello **Azure development** workload in your Visual Studio 2017 version 15.3 installation:</span></span>

![Instalar o Visual Studio de 2017 com carga de trabalho de desenvolvimento do Azure Olá](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)

<span data-ttu-id="680c0-119">toocreate e implantar funções, você também precisa de:</span><span class="sxs-lookup"><span data-stu-id="680c0-119">toocreate and deploy functions, you also need:</span></span>

* <span data-ttu-id="680c0-120">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="680c0-120">An active Azure subscription.</span></span> <span data-ttu-id="680c0-121">Se você ainda não tiver uma assinatura do Azure, há [contas gratuitas](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) disponíveis.</span><span class="sxs-lookup"><span data-stu-id="680c0-121">If you don't have an Azure subscription, [free accounts](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) are available.</span></span>

* <span data-ttu-id="680c0-122">Uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="680c0-122">An Azure Storage account.</span></span> <span data-ttu-id="680c0-123">toocreate uma conta de armazenamento, consulte [criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="680c0-123">toocreate a storage account, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>  
## <a name="create-an-azure-functions-project"></a><span data-ttu-id="680c0-124">Criar um projeto do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="680c0-124">Create an Azure Functions project</span></span> 

[!INCLUDE [Create a project using hello Azure Functions](../../includes/functions-vstools-create.md)]


## <a name="configure-hello-project-for-local-development"></a><span data-ttu-id="680c0-125">Configurar projeto Olá para desenvolvimento local</span><span class="sxs-lookup"><span data-stu-id="680c0-125">Configure hello project for local development</span></span>

<span data-ttu-id="680c0-126">Quando você cria um novo projeto usando o modelo de funções do Azure hello, você obtém um projeto c# vazio que contém Olá seguintes arquivos:</span><span class="sxs-lookup"><span data-stu-id="680c0-126">When you create a new project using hello Azure Functions template, you get an empty C# project that contains hello following files:</span></span>

* <span data-ttu-id="680c0-127">**host.JSON**: permite que você configure Olá host de funções.</span><span class="sxs-lookup"><span data-stu-id="680c0-127">**host.json**: Lets you configure hello Functions host.</span></span> <span data-ttu-id="680c0-128">Essas configurações se aplicam para execução local e no Azure.</span><span class="sxs-lookup"><span data-stu-id="680c0-128">These settings apply both when running locally and in Azure.</span></span> <span data-ttu-id="680c0-129">Para obter mais informações, consulte o artigo de referência para [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="680c0-129">For more information, see [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) reference article.</span></span>
    
* <span data-ttu-id="680c0-130">**local.Settings.json**: Mantém as configurações usadas ao executar as funções localmente.</span><span class="sxs-lookup"><span data-stu-id="680c0-130">**local.settings.json**: Maintains settings used when running functions locally.</span></span> <span data-ttu-id="680c0-131">Essas configurações não são usadas pelo Azure, eles são usados pelo Olá [Azure funções principais ferramentas](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="680c0-131">These settings are not used by Azure, they are used by hello [Azure Functions Core Tools](functions-run-local.md).</span></span> <span data-ttu-id="680c0-132">Use as configurações toospecify esse arquivo, como tooother de cadeias de caracteres de conexão do Azure services.</span><span class="sxs-lookup"><span data-stu-id="680c0-132">Use this file toospecify settings, such as connection strings tooother Azure services.</span></span> <span data-ttu-id="680c0-133">Adicionar um novo toohello chave **valores** matriz para cada conexão exigido pelas funções em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="680c0-133">Add a new key toohello **Values** array for each connection required by functions in your project.</span></span> <span data-ttu-id="680c0-134">Para obter mais informações, consulte [arquivo de configurações Local](functions-run-local.md#local-settings-file) tópico de ferramentas do Azure funções principais de saudação.</span><span class="sxs-lookup"><span data-stu-id="680c0-134">For more information, see [Local settings file](functions-run-local.md#local-settings-file) in hello Azure Functions Core Tools topic.</span></span>

<span data-ttu-id="680c0-135">tempo de execução de funções Hello usa internamente uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="680c0-135">hello Functions runtime uses an Azure Storage account internally.</span></span> <span data-ttu-id="680c0-136">Todos os disparar tipos diferentes de HTTP e webhooks, você deve definir Olá **Values.AzureWebJobsStorage** chave de cadeia de conexão de conta de armazenamento do Azure válida de tooa.</span><span class="sxs-lookup"><span data-stu-id="680c0-136">For all trigger types other than HTTP and webhooks, you must set hello **Values.AzureWebJobsStorage** key tooa valid Azure Storage account connection string.</span></span>

[!INCLUDE [Note toonot use local storage](../../includes/functions-local-settings-note.md)]

 <span data-ttu-id="680c0-137">cadeia de conexão do conta de armazenamento de saudação tooset:</span><span class="sxs-lookup"><span data-stu-id="680c0-137">tooset hello storage account connection string:</span></span>

1. <span data-ttu-id="680c0-138">No Visual Studio, abra **Cloud Explorer**, expanda **conta de armazenamento** > **sua conta de armazenamento**, em seguida, selecione **propriedades**e cópia hello **cadeia de caracteres de Conexão primária** valor.</span><span class="sxs-lookup"><span data-stu-id="680c0-138">In Visual Studio, open **Cloud Explorer**, expand **Storage Account** > **Your Storage Account**, then select **Properties** and copy hello **Primary Connection String** value.</span></span>   

2. <span data-ttu-id="680c0-139">No seu projeto, abrir o arquivo de projeto local.settings.json hello e definir valor Olá Olá **AzureWebJobsStorage** chave de cadeia de caracteres de conexão toohello você copiou.</span><span class="sxs-lookup"><span data-stu-id="680c0-139">In your project, open hello local.settings.json project file and set hello value of hello **AzureWebJobsStorage** key toohello connection string you copied.</span></span>

3. <span data-ttu-id="680c0-140">Repita Olá anterior etapa tooadd chaves exclusivas toohello **valores** matriz para todas as outras conexões necessária por suas funções.</span><span class="sxs-lookup"><span data-stu-id="680c0-140">Repeat hello previous step tooadd unique keys toohello **Values** array for any other connections required by your functions.</span></span>  

## <a name="create-a-function"></a><span data-ttu-id="680c0-141">Criar uma função</span><span class="sxs-lookup"><span data-stu-id="680c0-141">Create a function</span></span>

<span data-ttu-id="680c0-142">Em funções pré-compilado, associações de saudação usadas pela função hello são definidas aplicando atributos no código de saudação.</span><span class="sxs-lookup"><span data-stu-id="680c0-142">In pre-compiled functions, hello bindings used by hello function are defined by applying attributes in hello code.</span></span> <span data-ttu-id="680c0-143">Quando você usa Olá ferramentas de funções do Azure toocreate suas funções de modelos de saudação fornecido, esses atributos são aplicados para você.</span><span class="sxs-lookup"><span data-stu-id="680c0-143">When you use hello Azure Functions Tools toocreate your functions from hello provided templates, these attributes are applied for you.</span></span> 

1. <span data-ttu-id="680c0-144">No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó do projeto e selecione **Adicionar** > **Novo Item**.</span><span class="sxs-lookup"><span data-stu-id="680c0-144">In **Solution Explorer**, right-click on your project node and select **Add** > **New Item**.</span></span> <span data-ttu-id="680c0-145">Selecione **Azure função**, digite um **nome** para classe hello e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="680c0-145">Select **Azure Function**, type a **Name** for hello class, and click **Add**.</span></span>

2. <span data-ttu-id="680c0-146">Escolha o disparador, definir propriedades de associação de saudação e clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="680c0-146">Choose your trigger, set hello binding properties, and click **Create**.</span></span> <span data-ttu-id="680c0-147">Olá exemplo a seguir mostra as configurações de saudação quando criar um armazenamento de fila disparado função.</span><span class="sxs-lookup"><span data-stu-id="680c0-147">hello following example shows hello settings when creating a Queue storage triggered function.</span></span> 

    ![](./media/functions-develop-vs/functions-vstools-create-queuetrigger.png)
    
    <span data-ttu-id="680c0-148">Uma chave de cadeia de caracteres de conexão chamada **QueueStorage** for fornecido, que é definida no arquivo de local.settings.json hello.</span><span class="sxs-lookup"><span data-stu-id="680c0-148">A connection string key named **QueueStorage** is supplied, which is defined in hello local.settings.json file.</span></span> 
 
3. <span data-ttu-id="680c0-149">Examine Olá recém-adicionado classe.</span><span class="sxs-lookup"><span data-stu-id="680c0-149">Examine hello newly added class.</span></span> <span data-ttu-id="680c0-150">Você verá um estático **executar** método, que é atribuído com hello **FunctionName** atributo.</span><span class="sxs-lookup"><span data-stu-id="680c0-150">You see a static **Run** method, that is attributed with hello **FunctionName** attribute.</span></span> <span data-ttu-id="680c0-151">Esse atributo indica que o método hello é o ponto de entrada hello para função hello.</span><span class="sxs-lookup"><span data-stu-id="680c0-151">This attribute indicates that hello method is hello entry point for hello function.</span></span> 

    <span data-ttu-id="680c0-152">Por exemplo, Olá classe c# a seguir representa uma função de armazenamento disparado fila básica:</span><span class="sxs-lookup"><span data-stu-id="680c0-152">For example, hello following C# class represents a basic Queue storage triggered function:</span></span>

    ````csharp
    using System;
    using Microsoft.Azure.WebJobs;
    using Microsoft.Azure.WebJobs.Host;
    
    namespace FunctionApp1
    {
        public static class Function1
        {
            [FunctionName("QueueTriggerCSharp")]        
            public static void Run([QueueTrigger("myqueue-items", Connection = "QueueStorage")]string myQueueItem, TraceWriter log)
            {
                log.Info($"C# Queue trigger function processed: {myQueueItem}");
            }
        }
    } 
    ````
 
    <span data-ttu-id="680c0-153">Um atributo específico de associação é o método de ponto de entrada tooeach aplicada associação parâmetro fornecido toohello.</span><span class="sxs-lookup"><span data-stu-id="680c0-153">A binding-specific attribute is applied tooeach binding parameter supplied toohello entry point method.</span></span> <span data-ttu-id="680c0-154">atributo de saudação tem informações de associação hello como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="680c0-154">hello attribute takes hello binding information as parameters.</span></span> <span data-ttu-id="680c0-155">No exemplo anterior de saudação, Olá primeiro parâmetro tiver um **QueueTrigger** atributo aplicado, que indica a função de fila disparada.</span><span class="sxs-lookup"><span data-stu-id="680c0-155">In hello previous example, hello first parameter has a **QueueTrigger** attribute applied, indicating queue triggered function.</span></span> <span data-ttu-id="680c0-156">nome da fila de saudação e o nome de configuração de cadeia de caracteres de conexão são passadas como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="680c0-156">hello queue name and connection string setting name are passed as parameters.</span></span>  

## <a name="testing-functions"></a><span data-ttu-id="680c0-157">Funções de teste</span><span class="sxs-lookup"><span data-stu-id="680c0-157">Testing functions</span></span>

<span data-ttu-id="680c0-158">As Ferramentas Principais do Azure Functions permitem executar o projeto do Azure Functions no seu computador de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="680c0-158">Azure Functions Core Tools lets you run Azure Functions project on your local development computer.</span></span> <span data-ttu-id="680c0-159">Você é solicitado tooinstall essas ferramentas Olá a primeira vez que iniciar uma função do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="680c0-159">You are prompted tooinstall these tools hello first time you start a function from Visual Studio.</span></span>  

<span data-ttu-id="680c0-160">tootest sua função, pressione F5.</span><span class="sxs-lookup"><span data-stu-id="680c0-160">tootest your function, press F5.</span></span> <span data-ttu-id="680c0-161">Se solicitado, aceitar solicitação de saudação de toodownload do Visual Studio e instalar as ferramentas de núcleo de funções do Azure (CLI).</span><span class="sxs-lookup"><span data-stu-id="680c0-161">If prompted, accept hello request from Visual Studio toodownload and install Azure Functions Core (CLI) tools.</span></span>  <span data-ttu-id="680c0-162">Tooenable uma exceção de firewall também pode ser necessário para que as ferramentas de saudação podem manipular as solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="680c0-162">You may also need tooenable a firewall exception so that hello tools can handle HTTP requests.</span></span>

<span data-ttu-id="680c0-163">Com projeto de saudação em execução, você pode testar seu código, você deve testar função implantada.</span><span class="sxs-lookup"><span data-stu-id="680c0-163">With hello project running, you can test your code as you would test deployed function.</span></span> <span data-ttu-id="680c0-164">Para saber mais informações, consulte [Estratégias para testar seu código no Azure Functions](functions-test-a-function.md).</span><span class="sxs-lookup"><span data-stu-id="680c0-164">For more information, see [Strategies for testing your code in Azure Functions](functions-test-a-function.md).</span></span> <span data-ttu-id="680c0-165">Quando em execução no modo de depuração, os pontos de interrupção são atingidos no Visual Studio, conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="680c0-165">When running in debug mode, breakpoints are hit in Visual Studio as expected.</span></span> 

<span data-ttu-id="680c0-166">Para obter um exemplo de como uma fila de tootest disparou a função, consulte Olá [tutorial de início rápido de função de fila disparada](functions-create-storage-queue-triggered-function.md#test-the-function).</span><span class="sxs-lookup"><span data-stu-id="680c0-166">For an example of how tootest a queue triggered function, see hello [queue triggered function quickstart tutorial](functions-create-storage-queue-triggered-function.md#test-the-function).</span></span>  

<span data-ttu-id="680c0-167">toolearn mais sobre como usar o hello Azure funções principais ferramentas, consulte [código e teste do Azure funciona localmente](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="680c0-167">toolearn more about using hello Azure Functions Core Tools, see [Code and test Azure functions locally](functions-run-local.md).</span></span>

## <a name="publish-tooazure"></a><span data-ttu-id="680c0-168">Publicar tooAzure</span><span class="sxs-lookup"><span data-stu-id="680c0-168">Publish tooAzure</span></span>

[!INCLUDE [Publish hello project tooAzure](../../includes/functions-vstools-publish.md)]

>[!NOTE]  
><span data-ttu-id="680c0-169">Quaisquer configurações adicionadas no hello local.settings.json devem também ser adicionadas toohello função aplicativo no Azure.</span><span class="sxs-lookup"><span data-stu-id="680c0-169">Any settings you added in hello local.settings.json must be also added toohello function app in Azure.</span></span> <span data-ttu-id="680c0-170">Essas configurações não são adicionadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="680c0-170">These settings are not added automatically.</span></span> <span data-ttu-id="680c0-171">Você pode adicionar o aplicativo de função tooyour configurações necessárias em uma das seguintes maneiras:</span><span class="sxs-lookup"><span data-stu-id="680c0-171">You can add required settings tooyour function app in one of these ways:</span></span>
>
>* <span data-ttu-id="680c0-172">[Usando o portal do Azure de Olá](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="680c0-172">[Using hello Azure portal](functions-how-to-use-azure-function-app-settings.md#settings).</span></span>
>* <span data-ttu-id="680c0-173">[Usando Olá `--publish-local-settings` opção de publicação hello Azure funções principais ferramentas](functions-run-local.md#publish).</span><span class="sxs-lookup"><span data-stu-id="680c0-173">[Using hello `--publish-local-settings` publish option in hello Azure Functions Core Tools](functions-run-local.md#publish).</span></span>
>* <span data-ttu-id="680c0-174">[Usando Olá CLI do Azure](/cli/azure/functionapp/config/appsettings#set).</span><span class="sxs-lookup"><span data-stu-id="680c0-174">[Using hello Azure CLI](/cli/azure/functionapp/config/appsettings#set).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="680c0-175">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="680c0-175">Next steps</span></span>

<span data-ttu-id="680c0-176">Para obter mais informações sobre ferramentas de funções do Azure, consulte Olá seção de perguntas comuns Olá [ferramentas do Visual Studio 2017 para funções do Azure](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/) postagem de blog.</span><span class="sxs-lookup"><span data-stu-id="680c0-176">For more information about Azure Functions Tools, see hello Common Questions section of hello [Visual Studio 2017 Tools for Azure Functions](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/) blog post.</span></span>

<span data-ttu-id="680c0-177">toolearn mais sobre hello Azure funções principais ferramentas, consulte [código e teste do Azure funciona localmente](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="680c0-177">toolearn more about hello Azure Functions Core Tools, see [Code and test Azure functions locally](functions-run-local.md).</span></span>  
<span data-ttu-id="680c0-178">toolearn mais sobre como desenvolver funções como bibliotecas de classes do .NET, consulte [bibliotecas de classes do .NET usando com funções do Azure](functions-dotnet-class-library.md).</span><span class="sxs-lookup"><span data-stu-id="680c0-178">toolearn more about developing functions as .NET class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span> <span data-ttu-id="680c0-179">Este tópico também fornece exemplos de como toouse atributos toodeclare Olá vários tipos de associações com suporte pelas funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="680c0-179">This topic also provides examples of how toouse attributes toodeclare hello various types of bindings supported by Azure Functions.</span></span>    
