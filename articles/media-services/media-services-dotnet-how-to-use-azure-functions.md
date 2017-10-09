---
title: "aaaDevelop funções do Azure com os serviços de mídia"
description: "Este tópico mostra como toostart desenvolver funções do Azure com o uso de serviços de mídia Olá portal do Azure."
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
ms.openlocfilehash: 3b2c2fb498fea399c862dfbdb63033d06cabf6d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
#<a name="develop-azure-functions-with-media-services"></a><span data-ttu-id="c1653-103">Desenvolver o Azure Functions com os Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="c1653-103">Develop Azure Functions with Media Services</span></span>

<span data-ttu-id="c1653-104">Este tópico mostra como tooget iniciado com a criação de funções do Azure que usam os serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="c1653-104">This topic shows you how tooget started with creating Azure Functions that use Media Services.</span></span> <span data-ttu-id="c1653-105">Hello Azure função definidos neste tópico monitora um contêiner de conta de armazenamento denominado **entrada** para novos arquivos MP4.</span><span class="sxs-lookup"><span data-stu-id="c1653-105">hello Azure Function defined in this topic monitors a storage account container named **input** for new MP4 files.</span></span> <span data-ttu-id="c1653-106">Depois que um arquivo é deslocado no contêiner de armazenamento Olá, gatilho de blob Olá executará a função hello.</span><span class="sxs-lookup"><span data-stu-id="c1653-106">Once a file is dropped into hello storage container, hello blob trigger will execute hello function.</span></span>

<span data-ttu-id="c1653-107">Se você quiser tooexplore e implanta funções do Azure existentes que usam o Azure Media Services, confira [funções do Azure de serviços de mídia](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span><span class="sxs-lookup"><span data-stu-id="c1653-107">If you want tooexplore and deploy existing Azure Functions that use Azure Media Services, check out [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span> <span data-ttu-id="c1653-108">Esse repositório contém exemplos que usam os serviços de mídia tooshow fluxos de trabalho relacionado tooingesting conteúdo diretamente do armazenamento de blob, codificação e gravar o conteúdo de volta tooblob armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c1653-108">This repository contains examples that use Media Services tooshow workflows related tooingesting content directly from blob storage, encoding, and writing content back tooblob storage.</span></span> <span data-ttu-id="c1653-109">Ele também inclui exemplos de como toomonitor trabalho notificações via WebHooks e filas do Azure.</span><span class="sxs-lookup"><span data-stu-id="c1653-109">It also includes examples of how toomonitor job notifications via WebHooks and Azure Queues.</span></span> <span data-ttu-id="c1653-110">Você também pode desenvolver funções, com base em exemplos Olá Olá [funções do Azure de serviços de mídia](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) repositório.</span><span class="sxs-lookup"><span data-stu-id="c1653-110">You can also develop your Functions based on hello examples in hello [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) repository.</span></span> <span data-ttu-id="c1653-111">funções de saudação toodeploy, pressione Olá **implantar tooAzure** botão.</span><span class="sxs-lookup"><span data-stu-id="c1653-111">toodeploy hello functions, press hello **Deploy tooAzure** button.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1653-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c1653-112">Prerequisites</span></span>

- <span data-ttu-id="c1653-113">Antes de criar sua primeira função, é necessário toohave uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="c1653-113">Before you can create your first function, you need toohave an active Azure account.</span></span> <span data-ttu-id="c1653-114">Se você ainda não tiver uma conta do Azure, [há contas gratuitas disponíveis](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="c1653-114">If you don't already have an Azure account, [free accounts are available](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="c1653-115">Se você for toocreate Azure funções que executam ações em sua conta de serviços de mídia do Azure (AMS) ou escutar tooevents enviadas pelos serviços de mídia, você deve criar uma conta de AMS, conforme descrito [aqui](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="c1653-115">If you are going toocreate Azure Functions that perform actions on your Azure Media Services (AMS) account or listen tooevents sent by Media Services, you should create an AMS account, as described [here](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="c1653-116">Compreensão de [como toouse Azure funções](../azure-functions/functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c1653-116">Understanding of [how toouse Azure functions](../azure-functions/functions-overview.md).</span></span> <span data-ttu-id="c1653-117">Além disso, examine:</span><span class="sxs-lookup"><span data-stu-id="c1653-117">Also, review:</span></span>
    - [<span data-ttu-id="c1653-118">Associações HTTP e de webhook do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="c1653-118">Azure functions HTTP and webhook bindings</span></span>](../azure-functions/functions-triggers-bindings.md)
    - [<span data-ttu-id="c1653-119">Como configurações de aplicativo do Azure função tooconfigure</span><span class="sxs-lookup"><span data-stu-id="c1653-119">How tooconfigure Azure Function app settings</span></span>](../azure-functions/functions-how-to-use-azure-function-app-settings.md)
    
## <a name="considerations"></a><span data-ttu-id="c1653-120">Considerações</span><span class="sxs-lookup"><span data-stu-id="c1653-120">Considerations</span></span>

-  <span data-ttu-id="c1653-121">As funções do Azure em execução no plano de consumo Olá atingiu o tempo limite de 5 minutos limitar.</span><span class="sxs-lookup"><span data-stu-id="c1653-121">Azure Functions running under hello Consumption plan have 5 minutes timeout limit.</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="c1653-122">Criar um aplicativo de funções</span><span class="sxs-lookup"><span data-stu-id="c1653-122">Create a function app</span></span>

1. <span data-ttu-id="c1653-123">Vá toohello [portal do Azure](http://portal.azure.com) e entrar com sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="c1653-123">Go toohello [Azure portal](http://portal.azure.com) and sign-in with your Azure account.</span></span>
2. <span data-ttu-id="c1653-124">Crie um aplicativo de função conforme descrito [aqui](../azure-functions/functions-create-function-app-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c1653-124">Create a function app as described [here](../azure-functions/functions-create-function-app-portal.md).</span></span>

>[!NOTE]
> <span data-ttu-id="c1653-125">Uma conta de armazenamento que você especificar na Olá **StorageConnection** variável de ambiente (consulte a próxima etapa de saudação) deve estar no hello mesma região do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c1653-125">A storage account that you specify in hello **StorageConnection** environment variable (see hello next step) should be in hello same region as your app.</span></span>

## <a name="configure-function-app-settings"></a><span data-ttu-id="c1653-126">Definir configurações do aplicativo de funções</span><span class="sxs-lookup"><span data-stu-id="c1653-126">Configure function app settings</span></span>

<span data-ttu-id="c1653-127">Ao desenvolver funções dos serviços de mídia, é tooadd útil variáveis de ambiente que serão utilizados durante suas funções.</span><span class="sxs-lookup"><span data-stu-id="c1653-127">When developing Media Services functions, it is handy tooadd environment variables that will be used throughout your functions.</span></span> <span data-ttu-id="c1653-128">tooconfigure configurações do aplicativo, clique em Olá link de definir configurações de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c1653-128">tooconfigure app settings, click hello Configure App Settings link.</span></span> <span data-ttu-id="c1653-129">Para obter mais informações, consulte [como configurações de aplicativo do Azure função tooconfigure](../azure-functions/functions-how-to-use-azure-function-app-settings.md).</span><span class="sxs-lookup"><span data-stu-id="c1653-129">For more information, see  [How tooconfigure Azure Function app settings](../azure-functions/functions-how-to-use-azure-function-app-settings.md).</span></span> 

<span data-ttu-id="c1653-130">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1653-130">For example:</span></span>

![Configurações](./media/media-services-azure-functions/media-services-azure-functions001.png)

<span data-ttu-id="c1653-132">função Hello, definida neste artigo supõe que você tenha Olá variáveis de ambiente em suas configurações de aplicativo a seguir:</span><span class="sxs-lookup"><span data-stu-id="c1653-132">hello function, defined in this article, assumes you have hello following environment variables in your app settings:</span></span>

<span data-ttu-id="c1653-133">**AMSAccount**: *nome da conta do AMS* (por exemplo, testams)</span><span class="sxs-lookup"><span data-stu-id="c1653-133">**AMSAccount** : *AMS account name* (e.g. testams)</span></span>

<span data-ttu-id="c1653-134">**AMSKey**: *chave da conta do AMS* (por exemplo, IHOySnH+XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM=)</span><span class="sxs-lookup"><span data-stu-id="c1653-134">**AMSKey** : *AMS account key* (e.g. IHOySnH+XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM=)</span></span>

<span data-ttu-id="c1653-135">**MediaServicesStorageAccountName**: *nome da conta de armazenamento* (por exemplo, testamsstorage)</span><span class="sxs-lookup"><span data-stu-id="c1653-135">**MediaServicesStorageAccountName** : *storage account name* (e.g., testamsstorage)</span></span>

<span data-ttu-id="c1653-136">**MediaServicesStorageAccountKey**: *chave da conta de armazenamento* (por exemplo, xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX==)</span><span class="sxs-lookup"><span data-stu-id="c1653-136">**MediaServicesStorageAccountKey** : *storage account key* (e.g., xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX==)</span></span>

<span data-ttu-id="c1653-137">**StorageConnection**: *conexão de armazenamento* (por exemplo, DefaultEndpointsProtocol=https;AccountName=testamsstorage;AccountKey=xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX==)</span><span class="sxs-lookup"><span data-stu-id="c1653-137">**StorageConnection** : *storage connection* (e.g., DefaultEndpointsProtocol=https;AccountName=testamsstorage;AccountKey=xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX==)</span></span>

## <a name="create-a-function"></a><span data-ttu-id="c1653-138">Criar uma função</span><span class="sxs-lookup"><span data-stu-id="c1653-138">Create a function</span></span>

<span data-ttu-id="c1653-139">Depois que o aplicativo de funções for implantado, você poderá encontrá-lo entre os **Serviços de Aplicativos** do Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="c1653-139">Once your function app is deployed, you can find it among **App Services** Azure Functions.</span></span>

1. <span data-ttu-id="c1653-140">Selecione seu aplicativo de funções e clique em **Nova Função**.</span><span class="sxs-lookup"><span data-stu-id="c1653-140">Select your function app and click **New Function**.</span></span>
2. <span data-ttu-id="c1653-141">Escolha Olá **c#** idioma e **processamento de dados** cenário.</span><span class="sxs-lookup"><span data-stu-id="c1653-141">Choose hello **C#** language and **Data Processing** scenario.</span></span>
3. <span data-ttu-id="c1653-142">Escolha o modelo **BlobTrigger**.</span><span class="sxs-lookup"><span data-stu-id="c1653-142">Choose **BlobTrigger** template.</span></span> <span data-ttu-id="c1653-143">Essa função será disparada sempre que um blob é carregado no hello **entrada** contêiner.</span><span class="sxs-lookup"><span data-stu-id="c1653-143">This function will be triggered whenever a blob is uploaded into hello **input** container.</span></span> <span data-ttu-id="c1653-144">Olá **entrada** nome é especificado no hello **caminho**, na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="c1653-144">hello **input** name is specified in hello **Path**, in hello next step.</span></span>

    ![de entrada](./media/media-services-azure-functions/media-services-azure-functions004.png)

4. <span data-ttu-id="c1653-146">Depois de selecionar **BlobTrigger**, alguns controles mais serão exibidos na página de saudação.</span><span class="sxs-lookup"><span data-stu-id="c1653-146">Once you select **BlobTrigger**, some more controls will appear on hello page.</span></span>

    ![de entrada](./media/media-services-azure-functions/media-services-azure-functions005.png)

4. <span data-ttu-id="c1653-148">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c1653-148">Click **Create**.</span></span> 


## <a name="files"></a><span data-ttu-id="c1653-149">Arquivos</span><span class="sxs-lookup"><span data-stu-id="c1653-149">Files</span></span>

<span data-ttu-id="c1653-150">A função do Azure está associada a arquivos de código e a outros arquivos descritos nesta seção.</span><span class="sxs-lookup"><span data-stu-id="c1653-150">Your Azure function is associated with code files and other files that are described in this section.</span></span> <span data-ttu-id="c1653-151">Por padrão, uma função está associada aos arquivos **function.json** e **run.csx** (C#).</span><span class="sxs-lookup"><span data-stu-id="c1653-151">By default, a function is associated with **function.json** and **run.csx** (C#) files.</span></span> <span data-ttu-id="c1653-152">Você precisará tooadd um **Project** arquivo.</span><span class="sxs-lookup"><span data-stu-id="c1653-152">You will need tooadd a **project.json** file.</span></span> <span data-ttu-id="c1653-153">restante Olá desta seção mostra as definições de saudação para esses arquivos.</span><span class="sxs-lookup"><span data-stu-id="c1653-153">hello rest of this section shows hello definitions for these files.</span></span>

![de entrada](./media/media-services-azure-functions/media-services-azure-functions003.png)

### <a name="functionjson"></a><span data-ttu-id="c1653-155">function.json</span><span class="sxs-lookup"><span data-stu-id="c1653-155">function.json</span></span>

<span data-ttu-id="c1653-156">arquivo de function.json Olá define associações de função hello e outras definições de configuração.</span><span class="sxs-lookup"><span data-stu-id="c1653-156">hello function.json file defines hello function bindings and other configuration settings.</span></span> <span data-ttu-id="c1653-157">saudação de tempo de execução usa toomonitor de eventos neste arquivo toodetermine hello e como toopass dados e retornar dados de função execução.</span><span class="sxs-lookup"><span data-stu-id="c1653-157">hello runtime uses this file toodetermine hello events toomonitor and how toopass data into and return data from function execution.</span></span> <span data-ttu-id="c1653-158">Para obter mais informações, consulte [Associações HTTP e de webhook do Azure Functions](../azure-functions/functions-reference.md#function-code).</span><span class="sxs-lookup"><span data-stu-id="c1653-158">For more information, see [Azure functions HTTP and webhook bindings](../azure-functions/functions-reference.md#function-code).</span></span>

>[!NOTE]
><span data-ttu-id="c1653-159">Saudação de conjunto **desabilitado** propriedade muito**true** tooprevent função de saudação do que está sendo executada.</span><span class="sxs-lookup"><span data-stu-id="c1653-159">Set hello **disabled** property too**true** tooprevent hello function from being executed.</span></span> 


<span data-ttu-id="c1653-160">Aqui está um exemplo de arquivo **function.json**.</span><span class="sxs-lookup"><span data-stu-id="c1653-160">Here is an example of **function.json** file.</span></span>

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

### <a name="projectjson"></a><span data-ttu-id="c1653-161">project.json</span><span class="sxs-lookup"><span data-stu-id="c1653-161">project.json</span></span>

<span data-ttu-id="c1653-162">arquivo do Project Olá contém dependências.</span><span class="sxs-lookup"><span data-stu-id="c1653-162">hello project.json file contains dependencies.</span></span> <span data-ttu-id="c1653-163">Aqui está um exemplo de **Project** arquivo que inclui Olá necessário .NET do Azure Media Services pacotes do Nuget.</span><span class="sxs-lookup"><span data-stu-id="c1653-163">Here is an example of **project.json** file that includes hello required .NET Azure Media Services packages from Nuget.</span></span> <span data-ttu-id="c1653-164">Observe que os números de versão de hello serão alteradas com atualizações mais recentes toohello pacotes, portanto você deve confirmar versões mais recentes de saudação.</span><span class="sxs-lookup"><span data-stu-id="c1653-164">Note that hello version numbers will change with latest updates toohello packages, so you should confirm hello most recent versions.</span></span> 

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
    
### <a name="runcsx"></a><span data-ttu-id="c1653-165">run.csx</span><span class="sxs-lookup"><span data-stu-id="c1653-165">run.csx</span></span>

<span data-ttu-id="c1653-166">Este é o código c# Olá para sua função.</span><span class="sxs-lookup"><span data-stu-id="c1653-166">This is hello C# code for your function.</span></span>  <span data-ttu-id="c1653-167">função Hello definido abaixo monitores um contêiner de conta de armazenamento denominado **entrada** (que é o que foi especificado no caminho de saudação) para novos arquivos MP4.</span><span class="sxs-lookup"><span data-stu-id="c1653-167">hello function defined below monitors a storage account container named **input** (that is what was specified in hello path) for new MP4 files.</span></span> <span data-ttu-id="c1653-168">Depois que um arquivo é deslocado no contêiner de armazenamento Olá, gatilho de blob Olá executará a função hello.</span><span class="sxs-lookup"><span data-stu-id="c1653-168">Once a file is dropped into hello storage container, hello blob trigger will execute hello function.</span></span>
    
<span data-ttu-id="c1653-169">exemplo Hello definido nesta seção demonstra</span><span class="sxs-lookup"><span data-stu-id="c1653-169">hello example defined in this section demonstrates</span></span> 

1. <span data-ttu-id="c1653-170">como a conta tooingest um ativo para os serviços de mídia (copiando um blob em um ativo de AMS) e</span><span class="sxs-lookup"><span data-stu-id="c1653-170">how tooingest an asset into a Media Services account (by coping a blob into an AMS asset) and</span></span> 
2. <span data-ttu-id="c1653-171">como toosubmit um trabalho de codificação que usa "Streaming adaptável" mídia codificador padrão predefinido.</span><span class="sxs-lookup"><span data-stu-id="c1653-171">how toosubmit an encoding job that uses Media Encoder Standard's "Adaptive Streaming" preset .</span></span>

<span data-ttu-id="c1653-172">No cenário do mundo real hello, você provavelmente deseja tootrack o andamento do trabalho e, em seguida, publique o ativo codificado.</span><span class="sxs-lookup"><span data-stu-id="c1653-172">In hello real life scenario, you most likely want tootrack job progress and then publish your encoded asset.</span></span> <span data-ttu-id="c1653-173">Para obter mais informações, consulte [notificações de trabalho de serviços de mídia do Azure de usar ganchos toomonitor](media-services-dotnet-check-job-progress-with-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="c1653-173">For more information, see [Use Azure WebHooks toomonitor Media Services job notifications](media-services-dotnet-check-job-progress-with-webhooks.md).</span></span> <span data-ttu-id="c1653-174">Para obter mais exemplos, consulte [Azure Functions nos Serviços de Mídia](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span><span class="sxs-lookup"><span data-stu-id="c1653-174">For more examples, see [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span>  

<span data-ttu-id="c1653-175">Depois de definir a função, clique em **Salvar e Executar**.</span><span class="sxs-lookup"><span data-stu-id="c1653-175">Once you are done defining your function click **Save and Run**.</span></span>

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
        // NOTE that hello variables {fileName} here come from hello path setting in function.json
        // and are passed into hello  Run method signature above. We can use this toomake decisions on what type of file
        // was dropped into hello input container for hello function. 

        // No need toodo any Retry strategy in this function, By default, hello SDK calls a function up too5 times for a 
        // given blob. If hello fifth try fails, hello SDK adds a message tooa queue named webjobs-blobtrigger-poison.

        log.Info($"C# Blob trigger function processed: {fileName}.mp4");
        log.Info($"Using Azure Media Services account : {_mediaServicesAccountName}");


        try
        {
        // Create and cache hello Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(
                _mediaServicesAccountName,
                _mediaServicesAccountKey);

        // Used hello chached credentials toocreate CloudMediaContext.
        _context = new CloudMediaContext(_cachedCredentials);

        // Step 1:  Copy hello Blob into a new Input Asset for hello Job
        // ***NOTE: Ideally we would have a method tooingest a Blob directly here somehow. 
        // using code from this sample - https://azure.microsoft.com/en-us/documentation/articles/media-services-copying-existing-blob/

        StorageCredentials mediaServicesStorageCredentials =
            new StorageCredentials(_storageAccountName, _storageAccountKey);

        IAsset newAsset = CreateAssetFromBlob(myBlob, fileName, log).GetAwaiter().GetResult();

        // Step 2: Create an Encoding Job

        // Declare a new encoding job with hello Standard encoder
        IJob job = _context.Jobs.Create("Azure Function - MES Job");

        // Get a media processor reference, and pass tooit hello name of hello 
        // processor toouse for hello specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Create a task with hello encoding details, using a custom preset
        ITask task = job.Tasks.AddNew("Encode with Adaptive Streaming",
            processor,
            "Adaptive Streaming",
            TaskOptions.None); 

        // Specify hello input asset toobe encoded.
        task.InputAssets.Add(newAsset);

        // Add an output asset toocontain hello results of hello job. 
        // This output is specified as AssetCreationOptions.None, which 
        // means hello output asset is not encrypted. 
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
    /// Creates a new asset and copies blobs from hello specifed storage account.
    /// </summary>
    /// <param name="blob">hello specified blob.</param>
    /// <returns>hello new asset.</returns>
    public static async Task<IAsset> CreateAssetFromBlobAsync(CloudBlockBlob blob, string assetName, TraceWriter log)
    {
         //Get a reference toohello storage account that is associated with hello Media Services account. 
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

        // Get hello destination asset container reference
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

        // Get hold of hello destination blob
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
##<a name="test-your-function"></a><span data-ttu-id="c1653-176">Testar a função</span><span class="sxs-lookup"><span data-stu-id="c1653-176">Test your function</span></span>

<span data-ttu-id="c1653-177">tootest sua função, você precisa tooupload um arquivo MP4 em Olá **entrada** contêiner Olá da conta de armazenamento que você especificou na cadeia de caracteres de conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="c1653-177">tootest your function, you need tooupload an MP4 file into hello **input** container of hello storage account that you specified in hello connection string.</span></span>  

## <a name="next-step"></a><span data-ttu-id="c1653-178">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="c1653-178">Next step</span></span>

<span data-ttu-id="c1653-179">Neste ponto, você está pronto toostart desenvolvendo um aplicativo de serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="c1653-179">At this point, you are ready toostart developing a Media Services application.</span></span> 
 
<span data-ttu-id="c1653-180">Para obter mais detalhes e exemplos/soluções completas do uso de funções do Azure e os aplicativos lógicos com fluxos de trabalho de criação de conteúdo personalizado do Azure Media Services toocreate, consulte Olá [exemplo de integração de funções Media Services .NET no GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)</span><span class="sxs-lookup"><span data-stu-id="c1653-180">For more details and complete samples/solutions of using Azure Functions and Logic Apps with Azure Media Services toocreate custom content creation workflows, see hello [Media Services .NET Functions Integraiton Sample on GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)</span></span>

<span data-ttu-id="c1653-181">Além disso, consulte [notificações com .NET de trabalho de serviços de mídia do Azure de usar ganchos toomonitor](media-services-dotnet-check-job-progress-with-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="c1653-181">Also, see [Use Azure WebHooks toomonitor Media Services job notifications with .NET](media-services-dotnet-check-job-progress-with-webhooks.md).</span></span> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="c1653-182">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="c1653-182">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c1653-183">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="c1653-183">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

