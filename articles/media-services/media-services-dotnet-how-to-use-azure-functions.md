---
title: "Desenvolver o Azure Functions com os Serviços de Mídia"
description: "Este tópico mostra como começar a desenvolver o Azure Functions com os Serviços de Mídia usando o portal do Azure."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 51bdcb01-1846-4e1f-bd90-70020ab471b0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/21/2017
ms.author: juliako
ms.openlocfilehash: 35d539855572fef6c00de614a4e57738a8abd075
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
#<a name="develop-azure-functions-with-media-services"></a><span data-ttu-id="6b392-103">Desenvolver o Azure Functions com os Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="6b392-103">Develop Azure Functions with Media Services</span></span>

<span data-ttu-id="6b392-104">Este tópico mostra como começar a criação de Azure Functions que usam os Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="6b392-104">This topic shows you how to get started with creating Azure Functions that use Media Services.</span></span> <span data-ttu-id="6b392-105">A Azure Function definida neste tópico monitora um contêiner de conta de armazenamento chamado **input** para novos arquivos MP4.</span><span class="sxs-lookup"><span data-stu-id="6b392-105">The Azure Function defined in this topic monitors a storage account container named **input** for new MP4 files.</span></span> <span data-ttu-id="6b392-106">Depois que um arquivo for solto no contêiner de armazenamento, o gatilho de blob executará a função.</span><span class="sxs-lookup"><span data-stu-id="6b392-106">Once a file is dropped into the storage container, the blob trigger will execute the function.</span></span>

<span data-ttu-id="6b392-107">Se você quiser explorar e implantar as Azure Functions existentes que usam o Serviços de Mídia do Azure, confira [Azure Functions dos Serviços de Mídia](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span><span class="sxs-lookup"><span data-stu-id="6b392-107">If you want to explore and deploy existing Azure Functions that use Azure Media Services, check out [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span> <span data-ttu-id="6b392-108">Esse repositório contém exemplosque usam os Serviços de Mídia para mostrar os fluxos de trabalho relativos à ingestão de conteúdo diretamente do armazenamento de blobs, à codificação e à gravação do conteúdo de volta no armazenamento de blobs.</span><span class="sxs-lookup"><span data-stu-id="6b392-108">This repository contains examples that use Media Services to show workflows related to ingesting content directly from blob storage, encoding, and writing content back to blob storage.</span></span> <span data-ttu-id="6b392-109">Ele também inclui exemplos de como monitorar as notificações de trabalho por meio de Webhooks e Filas do Azure.</span><span class="sxs-lookup"><span data-stu-id="6b392-109">It also includes examples of how to monitor job notifications via WebHooks and Azure Queues.</span></span> <span data-ttu-id="6b392-110">Você também pode desenvolver as Funções com base em exemplos do repositório [Azure Functions nos Serviços de Mídia](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span><span class="sxs-lookup"><span data-stu-id="6b392-110">You can also develop your Functions based on the examples in the [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) repository.</span></span> <span data-ttu-id="6b392-111">Para implantar as funções, pressione o botão **Implantar no Azure**.</span><span class="sxs-lookup"><span data-stu-id="6b392-111">To deploy the functions, press the **Deploy to Azure** button.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6b392-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6b392-112">Prerequisites</span></span>

- <span data-ttu-id="6b392-113">Antes de criar sua primeira função, você precisará ter uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="6b392-113">Before you can create your first function, you need to have an active Azure account.</span></span> <span data-ttu-id="6b392-114">Se você ainda não tiver uma conta do Azure, [há contas gratuitas disponíveis](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="6b392-114">If you don't already have an Azure account, [free accounts are available](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="6b392-115">Se você pretende criar Azure Functions que executam ações em sua conta do AMS (Serviços de Mídia do Azure) ou escutar eventos enviados pelos Serviços de Mídia, crie uma conta do AMS conforme descrito [aqui](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="6b392-115">If you are going to create Azure Functions that perform actions on your Azure Media Services (AMS) account or listen to events sent by Media Services, you should create an AMS account, as described [here](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="6b392-116">Compreensão de [como usar o Azure Functions](../azure-functions/functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6b392-116">Understanding of [how to use Azure functions](../azure-functions/functions-overview.md).</span></span> <span data-ttu-id="6b392-117">Além disso, examine:</span><span class="sxs-lookup"><span data-stu-id="6b392-117">Also, review:</span></span>
    - [<span data-ttu-id="6b392-118">Associações HTTP e de webhook do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="6b392-118">Azure functions HTTP and webhook bindings</span></span>](../azure-functions/functions-triggers-bindings.md)
    - [<span data-ttu-id="6b392-119">Como definir configurações de aplicativo de uma Azure Function</span><span class="sxs-lookup"><span data-stu-id="6b392-119">How to configure Azure Function app settings</span></span>](../azure-functions/functions-how-to-use-azure-function-app-settings.md)
    
## <a name="considerations"></a><span data-ttu-id="6b392-120">Considerações</span><span class="sxs-lookup"><span data-stu-id="6b392-120">Considerations</span></span>

-  <span data-ttu-id="6b392-121">O Azure Functions em execução no plano de Consumo atingiu o tempo limite de 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="6b392-121">Azure Functions running under the Consumption plan have 5 minutes timeout limit.</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="6b392-122">Criar um aplicativo de funções</span><span class="sxs-lookup"><span data-stu-id="6b392-122">Create a function app</span></span>

1. <span data-ttu-id="6b392-123">Vá para o [portal do Azure](http://portal.azure.com) e entre com sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="6b392-123">Go to the [Azure portal](http://portal.azure.com) and sign-in with your Azure account.</span></span>
2. <span data-ttu-id="6b392-124">Crie um aplicativo de função conforme descrito [aqui](../azure-functions/functions-create-function-app-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6b392-124">Create a function app as described [here](../azure-functions/functions-create-function-app-portal.md).</span></span>

>[!NOTE]
> <span data-ttu-id="6b392-125">Uma conta de armazenamento especificada na variável de ambiente **StorageConnection** (consulte a próxima etapa) deve estar na mesma região do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6b392-125">A storage account that you specify in the **StorageConnection** environment variable (see the next step) should be in the same region as your app.</span></span>

## <a name="configure-function-app-settings"></a><span data-ttu-id="6b392-126">Definir configurações do aplicativo de funções</span><span class="sxs-lookup"><span data-stu-id="6b392-126">Configure function app settings</span></span>

<span data-ttu-id="6b392-127">Ao desenvolver funções dos Serviços de Mídia, é útil adicionar variáveis de ambiente que serão usadas em todas as funções.</span><span class="sxs-lookup"><span data-stu-id="6b392-127">When developing Media Services functions, it is handy to add environment variables that will be used throughout your functions.</span></span> <span data-ttu-id="6b392-128">Para definir as configurações de aplicativo, clique no link Definir configurações de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6b392-128">To configure app settings, click the Configure App Settings link.</span></span> <span data-ttu-id="6b392-129">Para obter mais informações, consulte [Como definir configurações de aplicativo de uma Azure Function](../azure-functions/functions-how-to-use-azure-function-app-settings.md).</span><span class="sxs-lookup"><span data-stu-id="6b392-129">For more information, see  [How to configure Azure Function app settings](../azure-functions/functions-how-to-use-azure-function-app-settings.md).</span></span> 

<span data-ttu-id="6b392-130">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="6b392-130">For example:</span></span>

![Configurações](./media/media-services-azure-functions/media-services-azure-functions001.png)

<span data-ttu-id="6b392-132">A função, definida neste artigo, pressupõe que você tenha as seguintes variáveis de ambiente nas configurações do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="6b392-132">The function, defined in this article, assumes you have the following environment variables in your app settings:</span></span>

<span data-ttu-id="6b392-133">**AMSAccount**: *nome da conta do AMS* (por exemplo, testams)</span><span class="sxs-lookup"><span data-stu-id="6b392-133">**AMSAccount** : *AMS account name* (e.g. testams)</span></span>

<span data-ttu-id="6b392-134">**AMSKey**: *chave da conta do AMS* (por exemplo, IHOySnH+XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM=)</span><span class="sxs-lookup"><span data-stu-id="6b392-134">**AMSKey** : *AMS account key* (e.g. IHOySnH+XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM=)</span></span>

<span data-ttu-id="6b392-135">**MediaServicesStorageAccountName**: *nome da conta de armazenamento* (por exemplo, testamsstorage)</span><span class="sxs-lookup"><span data-stu-id="6b392-135">**MediaServicesStorageAccountName** : *storage account name* (e.g., testamsstorage)</span></span>

<span data-ttu-id="6b392-136">**MediaServicesStorageAccountKey**: *chave da conta de armazenamento* (por exemplo, xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX==)</span><span class="sxs-lookup"><span data-stu-id="6b392-136">**MediaServicesStorageAccountKey** : *storage account key* (e.g., xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX==)</span></span>

<span data-ttu-id="6b392-137">**StorageConnection**: *conexão de armazenamento* (por exemplo, DefaultEndpointsProtocol=https;AccountName=testamsstorage;AccountKey=xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX==)</span><span class="sxs-lookup"><span data-stu-id="6b392-137">**StorageConnection** : *storage connection* (e.g., DefaultEndpointsProtocol=https;AccountName=testamsstorage;AccountKey=xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX==)</span></span>

## <a name="create-a-function"></a><span data-ttu-id="6b392-138">Criar uma função</span><span class="sxs-lookup"><span data-stu-id="6b392-138">Create a function</span></span>

<span data-ttu-id="6b392-139">Depois que o aplicativo de funções for implantado, você poderá encontrá-lo entre os **Serviços de Aplicativos** do Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="6b392-139">Once your function app is deployed, you can find it among **App Services** Azure Functions.</span></span>

1. <span data-ttu-id="6b392-140">Selecione seu aplicativo de funções e clique em **Nova Função**.</span><span class="sxs-lookup"><span data-stu-id="6b392-140">Select your function app and click **New Function**.</span></span>
2. <span data-ttu-id="6b392-141">Escolha a linguagem **C#** e o cenário **Processamento de Dados**.</span><span class="sxs-lookup"><span data-stu-id="6b392-141">Choose the **C#** language and **Data Processing** scenario.</span></span>
3. <span data-ttu-id="6b392-142">Escolha o modelo **BlobTrigger**.</span><span class="sxs-lookup"><span data-stu-id="6b392-142">Choose **BlobTrigger** template.</span></span> <span data-ttu-id="6b392-143">Essa função será disparada sempre que um blob for carregado no contêiner **input**.</span><span class="sxs-lookup"><span data-stu-id="6b392-143">This function will be triggered whenever a blob is uploaded into the **input** container.</span></span> <span data-ttu-id="6b392-144">O nome de **input** é especificado no **Caminho**, na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="6b392-144">The **input** name is specified in the **Path**, in the next step.</span></span>

    ![de entrada](./media/media-services-azure-functions/media-services-azure-functions004.png)

4. <span data-ttu-id="6b392-146">Depois de selecionar **BlobTrigger**, alguns outros controles serão exibidos na página.</span><span class="sxs-lookup"><span data-stu-id="6b392-146">Once you select **BlobTrigger**, some more controls will appear on the page.</span></span>

    ![de entrada](./media/media-services-azure-functions/media-services-azure-functions005.png)

4. <span data-ttu-id="6b392-148">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="6b392-148">Click **Create**.</span></span> 


## <a name="files"></a><span data-ttu-id="6b392-149">Arquivos</span><span class="sxs-lookup"><span data-stu-id="6b392-149">Files</span></span>

<span data-ttu-id="6b392-150">A função do Azure está associada a arquivos de código e a outros arquivos descritos nesta seção.</span><span class="sxs-lookup"><span data-stu-id="6b392-150">Your Azure function is associated with code files and other files that are described in this section.</span></span> <span data-ttu-id="6b392-151">Por padrão, uma função está associada aos arquivos **function.json** e **run.csx** (C#).</span><span class="sxs-lookup"><span data-stu-id="6b392-151">By default, a function is associated with **function.json** and **run.csx** (C#) files.</span></span> <span data-ttu-id="6b392-152">Você precisará adicionar um arquivo **project.json**.</span><span class="sxs-lookup"><span data-stu-id="6b392-152">You will need to add a **project.json** file.</span></span> <span data-ttu-id="6b392-153">O restante desta seção mostra as definições para esses arquivos.</span><span class="sxs-lookup"><span data-stu-id="6b392-153">The rest of this section shows the definitions for these files.</span></span>

![de entrada](./media/media-services-azure-functions/media-services-azure-functions003.png)

### <a name="functionjson"></a><span data-ttu-id="6b392-155">function.json</span><span class="sxs-lookup"><span data-stu-id="6b392-155">function.json</span></span>

<span data-ttu-id="6b392-156">O arquivo function.json define as associações de função e outras definições de configuração.</span><span class="sxs-lookup"><span data-stu-id="6b392-156">The function.json file defines the function bindings and other configuration settings.</span></span> <span data-ttu-id="6b392-157">O tempo de execução usa esse arquivo para determinar os eventos a serem monitorados, bem como para passar e retornar dados da execução da função.</span><span class="sxs-lookup"><span data-stu-id="6b392-157">The runtime uses this file to determine the events to monitor and how to pass data into and return data from function execution.</span></span> <span data-ttu-id="6b392-158">Para obter mais informações, consulte [Associações HTTP e de webhook do Azure Functions](../azure-functions/functions-reference.md#function-code).</span><span class="sxs-lookup"><span data-stu-id="6b392-158">For more information, see [Azure functions HTTP and webhook bindings](../azure-functions/functions-reference.md#function-code).</span></span>

>[!NOTE]
><span data-ttu-id="6b392-159">Defina a propriedade **disabled** como **true** para impedir que a função seja executada.</span><span class="sxs-lookup"><span data-stu-id="6b392-159">Set the **disabled** property to **true** to prevent the function from being executed.</span></span> 


<span data-ttu-id="6b392-160">Aqui está um exemplo de arquivo **function.json**.</span><span class="sxs-lookup"><span data-stu-id="6b392-160">Here is an example of **function.json** file.</span></span>

    {
    "bindings": [
      {
        "name": "myBlob",
        "type": "blobTrigger",
        "direction": "in",
        "path": "input/{fileName}.mp4",
        "connection": "StorageConnection"
      }
    ],
    "disabled": false
    }

### <a name="projectjson"></a><span data-ttu-id="6b392-161">project.json</span><span class="sxs-lookup"><span data-stu-id="6b392-161">project.json</span></span>

<span data-ttu-id="6b392-162">O arquivo project.json contém dependências.</span><span class="sxs-lookup"><span data-stu-id="6b392-162">The project.json file contains dependencies.</span></span> <span data-ttu-id="6b392-163">Este é um exemplo de arquivo **project.json** que inclui os pacotes NuGet necessários dos Serviços de Mídia do Azure do .NET.</span><span class="sxs-lookup"><span data-stu-id="6b392-163">Here is an example of **project.json** file that includes the required .NET Azure Media Services packages from Nuget.</span></span> <span data-ttu-id="6b392-164">Observe que os números de versão serão alterados com as últimas atualizações nos pacotes; portanto, é necessário confirmar as versões mais recentes.</span><span class="sxs-lookup"><span data-stu-id="6b392-164">Note that the version numbers will change with latest updates to the packages, so you should confirm the most recent versions.</span></span> 

    {
      "frameworks": {
        "net46":{
          "dependencies": {
        "windowsazure.mediaservices": "3.8.0.5",
        "windowsazure.mediaservices.extensions": "3.8.0.3"
          }
        }
       }
    }
    
### <a name="runcsx"></a><span data-ttu-id="6b392-165">run.csx</span><span class="sxs-lookup"><span data-stu-id="6b392-165">run.csx</span></span>

<span data-ttu-id="6b392-166">Este é o código C# para sua função.</span><span class="sxs-lookup"><span data-stu-id="6b392-166">This is the C# code for your function.</span></span>  <span data-ttu-id="6b392-167">A função definida abaixo monitora um contêiner de conta de armazenamento chamado **input** (que é o que foi especificado no caminho) para verificar se há novos arquivos MP4.</span><span class="sxs-lookup"><span data-stu-id="6b392-167">The function defined below monitors a storage account container named **input** (that is what was specified in the path) for new MP4 files.</span></span> <span data-ttu-id="6b392-168">Depois que um arquivo for solto no contêiner de armazenamento, o gatilho de blob executará a função.</span><span class="sxs-lookup"><span data-stu-id="6b392-168">Once a file is dropped into the storage container, the blob trigger will execute the function.</span></span>
    
<span data-ttu-id="6b392-169">O exemplo definido nesta seção demonstra</span><span class="sxs-lookup"><span data-stu-id="6b392-169">The example defined in this section demonstrates</span></span> 

1. <span data-ttu-id="6b392-170">como ingerir um ativo em uma conta dos Serviços de Mídia (copiando um blob para um ativo do AMS) e</span><span class="sxs-lookup"><span data-stu-id="6b392-170">how to ingest an asset into a Media Services account (by coping a blob into an AMS asset) and</span></span> 
2. <span data-ttu-id="6b392-171">como enviar um trabalho de codificação que usa a predefinição “Streaming Adaptável” do Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="6b392-171">how to submit an encoding job that uses Media Encoder Standard's "Adaptive Streaming" preset .</span></span>

<span data-ttu-id="6b392-172">No cenário da vida real, provavelmente, você desejará acompanhar o andamento do trabalho e, em seguida, publicar o ativo codificado.</span><span class="sxs-lookup"><span data-stu-id="6b392-172">In the real life scenario, you most likely want to track job progress and then publish your encoded asset.</span></span> <span data-ttu-id="6b392-173">Para obter mais informações, consulte [Usar o Azure WebHooks para monitorar notificações de trabalho dos Serviços de Mídia](media-services-dotnet-check-job-progress-with-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="6b392-173">For more information, see [Use Azure WebHooks to monitor Media Services job notifications](media-services-dotnet-check-job-progress-with-webhooks.md).</span></span> <span data-ttu-id="6b392-174">Para obter mais exemplos, consulte [Azure Functions nos Serviços de Mídia](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span><span class="sxs-lookup"><span data-stu-id="6b392-174">For more examples, see [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span>  

<span data-ttu-id="6b392-175">Depois de definir a função, clique em **Salvar e Executar**.</span><span class="sxs-lookup"><span data-stu-id="6b392-175">Once you are done defining your function click **Save and Run**.</span></span>

    #r "Microsoft.WindowsAzure.Storage"
    #r "Newtonsoft.Json"
    #r "System.Web"

    using System;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Net;
    using System.Threading;
    using System.Threading.Tasks;
    using System.IO;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    using Microsoft.WindowsAzure.Storage.Auth;

    private static readonly string _mediaServicesAccountName = Environment.GetEnvironmentVariable("AMSAccount");
    private static readonly string _mediaServicesAccountKey = Environment.GetEnvironmentVariable("AMSKey");

    static string _storageAccountName = Environment.GetEnvironmentVariable("MediaServicesStorageAccountName");
    static string _storageAccountKey = Environment.GetEnvironmentVariable("MediaServicesStorageAccountKey");

    private static CloudStorageAccount _destinationStorageAccount = null;

    // Field for service context.
    private static CloudMediaContext _context = null;
    private static MediaServicesCredentials _cachedCredentials = null;

    public static void Run(CloudBlockBlob myBlob, string fileName, TraceWriter log)
    {
        // NOTE that the variables {fileName} here come from the path setting in function.json
        // and are passed into the  Run method signature above. We can use this to make decisions on what type of file
        // was dropped into the input container for the function. 

        // No need to do any Retry strategy in this function, By default, the SDK calls a function up to 5 times for a 
        // given blob. If the fifth try fails, the SDK adds a message to a queue named webjobs-blobtrigger-poison.

        log.Info($"C# Blob trigger function processed: {fileName}.mp4");
        log.Info($"Using Azure Media Services account : {_mediaServicesAccountName}");


        try
        {
        // Create and cache the Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(
                _mediaServicesAccountName,
                _mediaServicesAccountKey);

        // Used the chached credentials to create CloudMediaContext.
        _context = new CloudMediaContext(_cachedCredentials);

        // Step 1:  Copy the Blob into a new Input Asset for the Job
        // ***NOTE: Ideally we would have a method to ingest a Blob directly here somehow. 
        // using code from this sample - https://azure.microsoft.com/en-us/documentation/articles/media-services-copying-existing-blob/

        StorageCredentials mediaServicesStorageCredentials =
            new StorageCredentials(_storageAccountName, _storageAccountKey);

        IAsset newAsset = CreateAssetFromBlob(myBlob, fileName, log).GetAwaiter().GetResult();

        // Step 2: Create an Encoding Job

        // Declare a new encoding job with the Standard encoder
        IJob job = _context.Jobs.Create("Azure Function - MES Job");

        // Get a media processor reference, and pass to it the name of the 
        // processor to use for the specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Create a task with the encoding details, using a custom preset
        ITask task = job.Tasks.AddNew("Encode with Adaptive Streaming",
            processor,
            "Adaptive Streaming",
            TaskOptions.None); 

        // Specify the input asset to be encoded.
        task.InputAssets.Add(newAsset);

        // Add an output asset to contain the results of the job. 
        // This output is specified as AssetCreationOptions.None, which 
        // means the output asset is not encrypted. 
        task.OutputAssets.AddNew(fileName, AssetCreationOptions.None);

        job.Submit();
        log.Info("Job Submitted");

        }
        catch (Exception ex)
        {
        log.Error("ERROR: failed.");
        log.Info($"StackTrace : {ex.StackTrace}");
        throw ex;
        }
    }

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


    public static async Task<IAsset> CreateAssetFromBlob(CloudBlockBlob blob, string assetName, TraceWriter log){
        IAsset newAsset = null;

        try{
            Task<IAsset> copyAssetTask = CreateAssetFromBlobAsync(blob, assetName, log);
            newAsset = await copyAssetTask;
            log.Info($"Asset Copied : {newAsset.Id}");
        }
        catch(Exception ex){
            log.Info("Copy Failed");
            log.Info($"ERROR : {ex.Message}");
            throw ex;
        }

        return newAsset;
    }

    /// <summary>
    /// Creates a new asset and copies blobs from the specifed storage account.
    /// </summary>
    /// <param name="blob">The specified blob.</param>
    /// <returns>The new asset.</returns>
    public static async Task<IAsset> CreateAssetFromBlobAsync(CloudBlockBlob blob, string assetName, TraceWriter log)
    {
         //Get a reference to the storage account that is associated with the Media Services account. 
        StorageCredentials mediaServicesStorageCredentials =
        new StorageCredentials(_storageAccountName, _storageAccountKey);
        _destinationStorageAccount = new CloudStorageAccount(mediaServicesStorageCredentials, false);

        // Create a new asset. 
        var asset = _context.Assets.Create(blob.Name, AssetCreationOptions.None);
        log.Info($"Created new asset {asset.Name}");

        IAccessPolicy writePolicy = _context.AccessPolicies.Create("writePolicy",
        TimeSpan.FromHours(4), AccessPermissions.Write);
        ILocator destinationLocator = _context.Locators.CreateLocator(LocatorType.Sas, asset, writePolicy);
        CloudBlobClient destBlobStorage = _destinationStorageAccount.CreateCloudBlobClient();

        // Get the destination asset container reference
        string destinationContainerName = (new Uri(destinationLocator.Path)).Segments[1];
        CloudBlobContainer assetContainer = destBlobStorage.GetContainerReference(destinationContainerName);

        try{
        assetContainer.CreateIfNotExists();
        }
        catch (Exception ex)
        {
        log.Error ("ERROR:" + ex.Message);
        }

        log.Info("Created asset.");

        // Get hold of the destination blob
        CloudBlockBlob destinationBlob = assetContainer.GetBlockBlobReference(blob.Name);

        // Copy Blob
        try
        {
        using (var stream = await blob.OpenReadAsync()) 
        {            
            await destinationBlob.UploadFromStreamAsync(stream);          
        }

        log.Info("Copy Complete.");

        var assetFile = asset.AssetFiles.Create(blob.Name);
        assetFile.ContentFileSize = blob.Properties.Length;
        assetFile.IsPrimary = true;
        assetFile.Update();
        asset.Update();
        }
        catch (Exception ex)
        {
        log.Error(ex.Message);
        log.Info (ex.StackTrace);
        log.Info ("Copy Failed.");
        throw;
        }

        destinationLocator.Delete();
        writePolicy.Delete();

        return asset;
    }
##<a name="test-your-function"></a><span data-ttu-id="6b392-176">Testar a função</span><span class="sxs-lookup"><span data-stu-id="6b392-176">Test your function</span></span>

<span data-ttu-id="6b392-177">Para testar a função, você precisa carregar um arquivo MP4 no contêiner **input** da conta de armazenamento especificada na cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="6b392-177">To test your function, you need to upload an MP4 file into the **input** container of the storage account that you specified in the connection string.</span></span>  

## <a name="next-step"></a><span data-ttu-id="6b392-178">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="6b392-178">Next step</span></span>

<span data-ttu-id="6b392-179">Neste ponto, você está pronto para começar a desenvolver um aplicativo de Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="6b392-179">At this point, you are ready to start developing a Media Services application.</span></span> 
 
<span data-ttu-id="6b392-180">Para obter mais detalhes e amostras/soluções completas de como usar o Azure Functions e os Aplicativos Lógicos com os Serviços de Mídia do Azure para criar fluxos de trabalho de criação de conteúdo personalizados, confira as [Amostras de integração do Functions ao .NET dos Serviços de Mídia no GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)</span><span class="sxs-lookup"><span data-stu-id="6b392-180">For more details and complete samples/solutions of using Azure Functions and Logic Apps with Azure Media Services to create custom content creation workflows, see the [Media Services .NET Functions Integraiton Sample on GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)</span></span>

<span data-ttu-id="6b392-181">Consulte também [Usar o Azure WebHooks para monitorar notificações de trabalho dos Serviços de Mídia com o .NET](media-services-dotnet-check-job-progress-with-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="6b392-181">Also, see [Use Azure WebHooks to monitor Media Services job notifications with .NET](media-services-dotnet-check-job-progress-with-webhooks.md).</span></span> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="6b392-182">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="6b392-182">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6b392-183">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="6b392-183">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

