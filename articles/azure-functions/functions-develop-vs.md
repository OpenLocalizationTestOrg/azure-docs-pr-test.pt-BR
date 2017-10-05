---
title: Desenvolver Azure Functions usando o Visual Studio | Microsoft Docs
description: Saiba como desenvolver e testar o Azure Functions usando as Ferramentas Azure Functions para o Visual Studio 2017.
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
ms.openlocfilehash: 1e0568bc58e8879cabe409cf8e9b5866f922e7c9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-tools-for-visual-studio"></a><span data-ttu-id="db46a-103">Ferramentas do Azure Functions para Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="db46a-103">Azure Functions Tools for Visual Studio</span></span>  

<span data-ttu-id="db46a-104">As Ferramentas Azure Functions para Visual Studio de 2017 são uma extensão do Visual Studio que permite que você desenvolva, teste e implante funções do C# para o Azure.</span><span class="sxs-lookup"><span data-stu-id="db46a-104">Azure Functions Tools for Visual Studio 2017 is an extension for Visual Studio that lets you develop, test, and deploy C# functions to Azure.</span></span> <span data-ttu-id="db46a-105">Se esta for sua primeira experiência com o Azure Functions, você pode aprender mais em [Uma introdução ao Azure Functions](functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="db46a-105">If this is your first experience with Azure Functions, you can learn more at [An introduction to Azure Functions](functions-overview.md).</span></span>

<span data-ttu-id="db46a-106">As Ferramentas do Azure Functions fornecem os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="db46a-106">The Azure Functions Tools provides the following benefits:</span></span> 

* <span data-ttu-id="db46a-107">Editar, criar e executar funções em seu computador de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="db46a-107">Edit, build, and run functions on your local development computer.</span></span> 
* <span data-ttu-id="db46a-108">Publicar seu projeto do Azure Functions diretamente no Azure.</span><span class="sxs-lookup"><span data-stu-id="db46a-108">Publish your Azure Functions project directly to Azure.</span></span> 
* <span data-ttu-id="db46a-109">Usar atributos do WebJobs para declarar associações de função diretamente no código C# em vez de manter um function.json separado para definições de associação.</span><span class="sxs-lookup"><span data-stu-id="db46a-109">Use WebJobs attributes to declare function bindings directly in the C# code instead of maintaining a separate function.json for binding definitions.</span></span>
* <span data-ttu-id="db46a-110">Desenvolver e implantar funções de pré-compiladas C#.</span><span class="sxs-lookup"><span data-stu-id="db46a-110">Develop and deploy pre-compiled C# functions.</span></span> <span data-ttu-id="db46a-111">Funções pré-compiladas fornecem um desempenho de inicialização a frio melhor que funções baseadas em script C#.</span><span class="sxs-lookup"><span data-stu-id="db46a-111">Pre-complied functions provide a better cold-start performance than C# script-based functions.</span></span> 
* <span data-ttu-id="db46a-112">Codificar suas funções em C# tendo todos os benefícios de desenvolvimento do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="db46a-112">Code your functions in C# while having all of the benefits of Visual Studio development.</span></span> 

<span data-ttu-id="db46a-113">Este tópico mostra como usar as Ferramentas do Azure Functions para Visual Studio 2017 para desenvolver suas funções no C#.</span><span class="sxs-lookup"><span data-stu-id="db46a-113">This topic shows you how to use the Azure Functions Tools for Visual Studio 2017 to develop your functions in C#.</span></span> <span data-ttu-id="db46a-114">Você também aprenderá como publicar seu projeto no Azure como um assembly .NET.</span><span class="sxs-lookup"><span data-stu-id="db46a-114">You also learn how to publish your project to Azure as a .NET assembly.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="db46a-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="db46a-115">Prerequisites</span></span>

<span data-ttu-id="db46a-116">As Ferramentas do Azure Functions estão incluídas na carga de trabalho de desenvolvimento do Azure do [Visual Studio 2017 versão 15.3](https://www.visualstudio.com/vs/) ou uma versão posterior.</span><span class="sxs-lookup"><span data-stu-id="db46a-116">Azure Functions Tools is included in the Azure development workload of [Visual Studio 2017 version 15.3](https://www.visualstudio.com/vs/), or a later version.</span></span> <span data-ttu-id="db46a-117">Certifique-se de incluir a carga de trabalho de **desenvolvimento do Azure** na sua instalação do Visual Studio 2017 versão 15.3:</span><span class="sxs-lookup"><span data-stu-id="db46a-117">Make sure you include the **Azure development** workload in your Visual Studio 2017 version 15.3 installation:</span></span>

![Instalar o Visual Studio de 2017 com a carga de trabalho de desenvolvimento do Azure](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)

<span data-ttu-id="db46a-119">Para criar e implantar funções, você também precisa:</span><span class="sxs-lookup"><span data-stu-id="db46a-119">To create and deploy functions, you also need:</span></span>

* <span data-ttu-id="db46a-120">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="db46a-120">An active Azure subscription.</span></span> <span data-ttu-id="db46a-121">Se você ainda não tiver uma assinatura do Azure, há [contas gratuitas](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) disponíveis.</span><span class="sxs-lookup"><span data-stu-id="db46a-121">If you don't have an Azure subscription, [free accounts](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) are available.</span></span>

* <span data-ttu-id="db46a-122">Uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="db46a-122">An Azure Storage account.</span></span> <span data-ttu-id="db46a-123">Para criar uma conta de armazenamento, consulte [Criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="db46a-123">To create a storage account, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>  
## <a name="create-an-azure-functions-project"></a><span data-ttu-id="db46a-124">Criar um projeto do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="db46a-124">Create an Azure Functions project</span></span> 

[!INCLUDE [Create a project using the Azure Functions](../../includes/functions-vstools-create.md)]


## <a name="configure-the-project-for-local-development"></a><span data-ttu-id="db46a-125">Configurar seu projeto para desenvolvimento local</span><span class="sxs-lookup"><span data-stu-id="db46a-125">Configure the project for local development</span></span>

<span data-ttu-id="db46a-126">Quando você cria um novo projeto usando o modelo do Azure Functions, você obtém um projeto C# vazio que contém os seguintes arquivos:</span><span class="sxs-lookup"><span data-stu-id="db46a-126">When you create a new project using the Azure Functions template, you get an empty C# project that contains the following files:</span></span>

* <span data-ttu-id="db46a-127">**host.json**: Permite que você configure o host do Functions.</span><span class="sxs-lookup"><span data-stu-id="db46a-127">**host.json**: Lets you configure the Functions host.</span></span> <span data-ttu-id="db46a-128">Essas configurações se aplicam para execução local e no Azure.</span><span class="sxs-lookup"><span data-stu-id="db46a-128">These settings apply both when running locally and in Azure.</span></span> <span data-ttu-id="db46a-129">Para obter mais informações, consulte o artigo de referência para [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="db46a-129">For more information, see [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) reference article.</span></span>
    
* <span data-ttu-id="db46a-130">**local.Settings.json**: Mantém as configurações usadas ao executar as funções localmente.</span><span class="sxs-lookup"><span data-stu-id="db46a-130">**local.settings.json**: Maintains settings used when running functions locally.</span></span> <span data-ttu-id="db46a-131">Essas configurações não são usadas pelo Azure, elas são usadas pelas [Ferramentas Básicas do Azure Functions](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="db46a-131">These settings are not used by Azure, they are used by the [Azure Functions Core Tools](functions-run-local.md).</span></span> <span data-ttu-id="db46a-132">Use esse arquivo para especificar as configurações, como cadeias de conexão a outros serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="db46a-132">Use this file to specify settings, such as connection strings to other Azure services.</span></span> <span data-ttu-id="db46a-133">Adicione uma nova chave na matriz **Valores** para cada conexão exigida pelas funções em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="db46a-133">Add a new key to the **Values** array for each connection required by functions in your project.</span></span> <span data-ttu-id="db46a-134">Para obter mais informações, consulte [Arquivo de configurações locais](functions-run-local.md#local-settings-file) no tópico Ferramentas Básicas do Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="db46a-134">For more information, see [Local settings file](functions-run-local.md#local-settings-file) in the Azure Functions Core Tools topic.</span></span>

<span data-ttu-id="db46a-135">O tempo de execução do Functions usa internamente uma conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="db46a-135">The Functions runtime uses an Azure Storage account internally.</span></span> <span data-ttu-id="db46a-136">Para todos os tipos de gatilhos diferentes de HTTP e webhooks, você deve definir a chave **Values.AzureWebJobsStorage** para uma cadeia de conexão de conta de Armazenamento do Azure válida.</span><span class="sxs-lookup"><span data-stu-id="db46a-136">For all trigger types other than HTTP and webhooks, you must set the **Values.AzureWebJobsStorage** key to a valid Azure Storage account connection string.</span></span>

[!INCLUDE [Note to not use local storage](../../includes/functions-local-settings-note.md)]

 <span data-ttu-id="db46a-137">Para definir a cadeia de conexão da conta de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="db46a-137">To set the storage account connection string:</span></span>

1. <span data-ttu-id="db46a-138">No Visual Studio, abra **Cloud Explorer**, expanda **Conta de armazenamento** > **Sua conta de armazenamento**, selecione **Propriedades** e copie o valor da **Cadeia de conexão primária**.</span><span class="sxs-lookup"><span data-stu-id="db46a-138">In Visual Studio, open **Cloud Explorer**, expand **Storage Account** > **Your Storage Account**, then select **Properties** and copy the **Primary Connection String** value.</span></span>   

2. <span data-ttu-id="db46a-139">Em seu projeto, abra o arquivo de projeto local.settings.json e defina o valor da chave **AzureWebJobsStorage** na cadeia de conexão que você copiou.</span><span class="sxs-lookup"><span data-stu-id="db46a-139">In your project, open the local.settings.json project file and set the value of the **AzureWebJobsStorage** key to the connection string you copied.</span></span>

3. <span data-ttu-id="db46a-140">Repita a etapa anterior para adicionar as chaves exclusivas para a matriz de **Valores** para todas as outras conexões necessárias para as suas funções.</span><span class="sxs-lookup"><span data-stu-id="db46a-140">Repeat the previous step to add unique keys to the **Values** array for any other connections required by your functions.</span></span>  

## <a name="create-a-function"></a><span data-ttu-id="db46a-141">Criar uma função</span><span class="sxs-lookup"><span data-stu-id="db46a-141">Create a function</span></span>

<span data-ttu-id="db46a-142">Em funções pré-compiladas, as associações usadas pela função são definidas aplicando atributos no código.</span><span class="sxs-lookup"><span data-stu-id="db46a-142">In pre-compiled functions, the bindings used by the function are defined by applying attributes in the code.</span></span> <span data-ttu-id="db46a-143">Quando você usar as Ferramentas do Azure Functions para criar suas funções a partir de modelos fornecidos, esses atributos são aplicados para você.</span><span class="sxs-lookup"><span data-stu-id="db46a-143">When you use the Azure Functions Tools to create your functions from the provided templates, these attributes are applied for you.</span></span> 

1. <span data-ttu-id="db46a-144">No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó do projeto e selecione **Adicionar** > **Novo Item**.</span><span class="sxs-lookup"><span data-stu-id="db46a-144">In **Solution Explorer**, right-click on your project node and select **Add** > **New Item**.</span></span> <span data-ttu-id="db46a-145">Selecione **Azure Function**, digite um **Nome** para a classe e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="db46a-145">Select **Azure Function**, type a **Name** for the class, and click **Add**.</span></span>

2. <span data-ttu-id="db46a-146">Escolha o gatilho, defina as propriedades de associação e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="db46a-146">Choose your trigger, set the binding properties, and click **Create**.</span></span> <span data-ttu-id="db46a-147">O exemplo a seguir mostra as configurações ao criar uma função disparada por armazenamento de filas.</span><span class="sxs-lookup"><span data-stu-id="db46a-147">The following example shows the settings when creating a Queue storage triggered function.</span></span> 

    ![](./media/functions-develop-vs/functions-vstools-create-queuetrigger.png)
    
    <span data-ttu-id="db46a-148">Uma chave de cadeia de conexão chamada **QueueStorage** é fornecida, que é definida no arquivo local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="db46a-148">A connection string key named **QueueStorage** is supplied, which is defined in the local.settings.json file.</span></span> 
 
3. <span data-ttu-id="db46a-149">Examine a classe recém-adicionada.</span><span class="sxs-lookup"><span data-stu-id="db46a-149">Examine the newly added class.</span></span> <span data-ttu-id="db46a-150">Você verá um método estático **Run**, que é atribuído ao atributo **FunctionName**.</span><span class="sxs-lookup"><span data-stu-id="db46a-150">You see a static **Run** method, that is attributed with the **FunctionName** attribute.</span></span> <span data-ttu-id="db46a-151">Esse atributo indica que o método é o ponto de entrada para a função.</span><span class="sxs-lookup"><span data-stu-id="db46a-151">This attribute indicates that the method is the entry point for the function.</span></span> 

    <span data-ttu-id="db46a-152">Por exemplo, a classe C# a seguir representa uma função básica disparada pelo armazenamento de filas:</span><span class="sxs-lookup"><span data-stu-id="db46a-152">For example, the following C# class represents a basic Queue storage triggered function:</span></span>

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
 
    <span data-ttu-id="db46a-153">Um atributo específico de associação é aplicado a cada parâmetro de associação fornecido ao método do ponto de entrada.</span><span class="sxs-lookup"><span data-stu-id="db46a-153">A binding-specific attribute is applied to each binding parameter supplied to the entry point method.</span></span> <span data-ttu-id="db46a-154">O atributo utiliza as informações de associação como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="db46a-154">The attribute takes the binding information as parameters.</span></span> <span data-ttu-id="db46a-155">No exemplo anterior, o primeiro parâmetro possui um atributo **QueueTrigger** aplicado, que indica a função disparada por fila.</span><span class="sxs-lookup"><span data-stu-id="db46a-155">In the previous example, The first parameter has a **QueueTrigger** attribute applied, indicating queue triggered function.</span></span> <span data-ttu-id="db46a-156">O nome da fila e o nome de configuração da cadeia de conexão são passadas como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="db46a-156">The queue name and connection string setting name are passed as parameters.</span></span>  

## <a name="testing-functions"></a><span data-ttu-id="db46a-157">Funções de teste</span><span class="sxs-lookup"><span data-stu-id="db46a-157">Testing functions</span></span>

<span data-ttu-id="db46a-158">As Ferramentas Principais do Azure Functions permitem executar o projeto do Azure Functions no seu computador de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="db46a-158">Azure Functions Core Tools lets you run Azure Functions project on your local development computer.</span></span> <span data-ttu-id="db46a-159">Você precisa instalar essas ferramentas na primeira vez em que inicia uma função no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="db46a-159">You are prompted to install these tools the first time you start a function from Visual Studio.</span></span>  

<span data-ttu-id="db46a-160">Para testar sua função, pressione F5.</span><span class="sxs-lookup"><span data-stu-id="db46a-160">To test your function, press F5.</span></span> <span data-ttu-id="db46a-161">Se solicitado, aceite a solicitação do Visual Studio para baixar e instalar as ferramentas principais (CLI) do Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="db46a-161">If prompted, accept the request from Visual Studio to download and install Azure Functions Core (CLI) tools.</span></span>  <span data-ttu-id="db46a-162">Você também precisará habilitar a exceção de firewall de forma que as ferramentas possam lidar com solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="db46a-162">You may also need to enable a firewall exception so that the tools can handle HTTP requests.</span></span>

<span data-ttu-id="db46a-163">Com o projeto em execução, você pode testar seu código da mesma forma que você testaria a função implantada.</span><span class="sxs-lookup"><span data-stu-id="db46a-163">With the project running, you can test your code as you would test deployed function.</span></span> <span data-ttu-id="db46a-164">Para saber mais informações, consulte [Estratégias para testar seu código no Azure Functions](functions-test-a-function.md).</span><span class="sxs-lookup"><span data-stu-id="db46a-164">For more information, see [Strategies for testing your code in Azure Functions](functions-test-a-function.md).</span></span> <span data-ttu-id="db46a-165">Quando em execução no modo de depuração, os pontos de interrupção são atingidos no Visual Studio, conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="db46a-165">When running in debug mode, breakpoints are hit in Visual Studio as expected.</span></span> 

<span data-ttu-id="db46a-166">Para obter um exemplo de como testar uma função disparada por fila, consulte o [tutorial de início rápido de função disparada por fila](functions-create-storage-queue-triggered-function.md#test-the-function).</span><span class="sxs-lookup"><span data-stu-id="db46a-166">For an example of how to test a queue triggered function, see the [queue triggered function quickstart tutorial](functions-create-storage-queue-triggered-function.md#test-the-function).</span></span>  

<span data-ttu-id="db46a-167">Para saber mais sobre o uso das Ferramentas Básicas do Azure Functions, consulte [Codificar e testar o Azure Functions localmente](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="db46a-167">To learn more about using the Azure Functions Core Tools, see [Code and test Azure functions locally](functions-run-local.md).</span></span>

## <a name="publish-to-azure"></a><span data-ttu-id="db46a-168">Publicar no Azure</span><span class="sxs-lookup"><span data-stu-id="db46a-168">Publish to Azure</span></span>

[!INCLUDE [Publish the project to Azure](../../includes/functions-vstools-publish.md)]

>[!NOTE]  
><span data-ttu-id="db46a-169">As configurações que você adicionou no local.settings.json também devem ser adicionadas ao aplicativo de funções no Azure.</span><span class="sxs-lookup"><span data-stu-id="db46a-169">Any settings you added in the local.settings.json must be also added to the function app in Azure.</span></span> <span data-ttu-id="db46a-170">Essas configurações não são adicionadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="db46a-170">These settings are not added automatically.</span></span> <span data-ttu-id="db46a-171">Você pode adicionar as configurações necessárias ao seu aplicativo de funções de uma dessas maneiras:</span><span class="sxs-lookup"><span data-stu-id="db46a-171">You can add required settings to your function app in one of these ways:</span></span>
>
>* <span data-ttu-id="db46a-172">[Usando o Portal do Azure](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="db46a-172">[Using the Azure portal](functions-how-to-use-azure-function-app-settings.md#settings).</span></span>
>* <span data-ttu-id="db46a-173">[Usando a opção de publicação `--publish-local-settings` nas ferramentas básicas do Azure Functions](functions-run-local.md#publish).</span><span class="sxs-lookup"><span data-stu-id="db46a-173">[Using the `--publish-local-settings` publish option in the Azure Functions Core Tools](functions-run-local.md#publish).</span></span>
>* <span data-ttu-id="db46a-174">[Usando a CLI do Azure](/cli/azure/functionapp/config/appsettings#set).</span><span class="sxs-lookup"><span data-stu-id="db46a-174">[Using the Azure CLI](/cli/azure/functionapp/config/appsettings#set).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="db46a-175">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="db46a-175">Next steps</span></span>

<span data-ttu-id="db46a-176">Para obter mais informações sobre as Ferramentas do Azure Functions, consulte a seção de Perguntas Comuns da postagem de blog [Ferramentas do Visual Studio 2017 para o Azure Functions](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span><span class="sxs-lookup"><span data-stu-id="db46a-176">For more information about Azure Functions Tools, see the Common Questions section of the [Visual Studio 2017 Tools for Azure Functions](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/) blog post.</span></span>

<span data-ttu-id="db46a-177">Para saber mais sobre as Ferramentas Básicas do Azure Functions, consulte [Codificar e testar o Azure Functions localmente](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="db46a-177">To learn more about the Azure Functions Core Tools, see [Code and test Azure functions locally](functions-run-local.md).</span></span>  
<span data-ttu-id="db46a-178">Para saber mais sobre como desenvolver funções como bibliotecas de classes do .NET, veja [Como usar bibliotecas de classes do .NET com o Azure Functions](functions-dotnet-class-library.md).</span><span class="sxs-lookup"><span data-stu-id="db46a-178">To learn more about developing functions as .NET class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span> <span data-ttu-id="db46a-179">Este tópico também fornece exemplos de como usar atributos para declarar os vários tipos de associações com suporte pelo Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="db46a-179">This topic also provides examples of how to use attributes to declare the various types of bindings supported by Azure Functions.</span></span>    
