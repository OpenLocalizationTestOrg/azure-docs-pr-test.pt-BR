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
#<a name="develop-azure-functions-with-media-services"></a>Desenvolver o Azure Functions com os Serviços de Mídia

Este tópico mostra como tooget iniciado com a criação de funções do Azure que usam os serviços de mídia. Hello Azure função definidos neste tópico monitora um contêiner de conta de armazenamento denominado **entrada** para novos arquivos MP4. Depois que um arquivo é deslocado no contêiner de armazenamento Olá, gatilho de blob Olá executará a função hello.

Se você quiser tooexplore e implanta funções do Azure existentes que usam o Azure Media Services, confira [funções do Azure de serviços de mídia](https://github.com/Azure-Samples/media-services-dotnet-functions-integration). Esse repositório contém exemplos que usam os serviços de mídia tooshow fluxos de trabalho relacionado tooingesting conteúdo diretamente do armazenamento de blob, codificação e gravar o conteúdo de volta tooblob armazenamento. Ele também inclui exemplos de como toomonitor trabalho notificações via WebHooks e filas do Azure. Você também pode desenvolver funções, com base em exemplos Olá Olá [funções do Azure de serviços de mídia](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) repositório. funções de saudação toodeploy, pressione Olá **implantar tooAzure** botão.

## <a name="prerequisites"></a>Pré-requisitos

- Antes de criar sua primeira função, é necessário toohave uma conta ativa do Azure. Se você ainda não tiver uma conta do Azure, [há contas gratuitas disponíveis](https://azure.microsoft.com/free/).
- Se você for toocreate Azure funções que executam ações em sua conta de serviços de mídia do Azure (AMS) ou escutar tooevents enviadas pelos serviços de mídia, você deve criar uma conta de AMS, conforme descrito [aqui](media-services-portal-create-account.md).
- Compreensão de [como toouse Azure funções](../azure-functions/functions-overview.md). Além disso, examine:
    - [Associações HTTP e de webhook do Azure Functions](../azure-functions/functions-triggers-bindings.md)
    - [Como configurações de aplicativo do Azure função tooconfigure](../azure-functions/functions-how-to-use-azure-function-app-settings.md)
    
## <a name="considerations"></a>Considerações

-  As funções do Azure em execução no plano de consumo Olá atingiu o tempo limite de 5 minutos limitar.

## <a name="create-a-function-app"></a>Criar um aplicativo de funções

1. Vá toohello [portal do Azure](http://portal.azure.com) e entrar com sua conta do Azure.
2. Crie um aplicativo de função conforme descrito [aqui](../azure-functions/functions-create-function-app-portal.md).

>[!NOTE]
> Uma conta de armazenamento que você especificar na Olá **StorageConnection** variável de ambiente (consulte a próxima etapa de saudação) deve estar no hello mesma região do seu aplicativo.

## <a name="configure-function-app-settings"></a>Definir configurações do aplicativo de funções

Ao desenvolver funções dos serviços de mídia, é tooadd útil variáveis de ambiente que serão utilizados durante suas funções. tooconfigure configurações do aplicativo, clique em Olá link de definir configurações de aplicativo. Para obter mais informações, consulte [como configurações de aplicativo do Azure função tooconfigure](../azure-functions/functions-how-to-use-azure-function-app-settings.md). 

Por exemplo:

![Configurações](./media/media-services-azure-functions/media-services-azure-functions001.png)

função Hello, definida neste artigo supõe que você tenha Olá variáveis de ambiente em suas configurações de aplicativo a seguir:

**AMSAccount**: *nome da conta do AMS* (por exemplo, testams)

**AMSKey**: *chave da conta do AMS* (por exemplo, IHOySnH+XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM=)

**MediaServicesStorageAccountName**: *nome da conta de armazenamento* (por exemplo, testamsstorage)

**MediaServicesStorageAccountKey**: *chave da conta de armazenamento* (por exemplo, xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX==)

**StorageConnection**: *conexão de armazenamento* (por exemplo, DefaultEndpointsProtocol=https;AccountName=testamsstorage;AccountKey=xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX==)

## <a name="create-a-function"></a>Criar uma função

Depois que o aplicativo de funções for implantado, você poderá encontrá-lo entre os **Serviços de Aplicativos** do Azure Functions.

1. Selecione seu aplicativo de funções e clique em **Nova Função**.
2. Escolha Olá **c#** idioma e **processamento de dados** cenário.
3. Escolha o modelo **BlobTrigger**. Essa função será disparada sempre que um blob é carregado no hello **entrada** contêiner. Olá **entrada** nome é especificado no hello **caminho**, na próxima etapa do hello.

    ![de entrada](./media/media-services-azure-functions/media-services-azure-functions004.png)

4. Depois de selecionar **BlobTrigger**, alguns controles mais serão exibidos na página de saudação.

    ![de entrada](./media/media-services-azure-functions/media-services-azure-functions005.png)

4. Clique em **Criar**. 


## <a name="files"></a>Arquivos

A função do Azure está associada a arquivos de código e a outros arquivos descritos nesta seção. Por padrão, uma função está associada aos arquivos **function.json** e **run.csx** (C#). Você precisará tooadd um **Project** arquivo. restante Olá desta seção mostra as definições de saudação para esses arquivos.

![de entrada](./media/media-services-azure-functions/media-services-azure-functions003.png)

### <a name="functionjson"></a>function.json

arquivo de function.json Olá define associações de função hello e outras definições de configuração. saudação de tempo de execução usa toomonitor de eventos neste arquivo toodetermine hello e como toopass dados e retornar dados de função execução. Para obter mais informações, consulte [Associações HTTP e de webhook do Azure Functions](../azure-functions/functions-reference.md#function-code).

>[!NOTE]
>Saudação de conjunto **desabilitado** propriedade muito**true** tooprevent função de saudação do que está sendo executada. 


Aqui está um exemplo de arquivo **function.json**.

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

### <a name="projectjson"></a>project.json

arquivo do Project Olá contém dependências. Aqui está um exemplo de **Project** arquivo que inclui Olá necessário .NET do Azure Media Services pacotes do Nuget. Observe que os números de versão de hello serão alteradas com atualizações mais recentes toohello pacotes, portanto você deve confirmar versões mais recentes de saudação. 

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
    
### <a name="runcsx"></a>run.csx

Este é o código c# Olá para sua função.  função Hello definido abaixo monitores um contêiner de conta de armazenamento denominado **entrada** (que é o que foi especificado no caminho de saudação) para novos arquivos MP4. Depois que um arquivo é deslocado no contêiner de armazenamento Olá, gatilho de blob Olá executará a função hello.
    
exemplo Hello definido nesta seção demonstra 

1. como a conta tooingest um ativo para os serviços de mídia (copiando um blob em um ativo de AMS) e 
2. como toosubmit um trabalho de codificação que usa "Streaming adaptável" mídia codificador padrão predefinido.

No cenário do mundo real hello, você provavelmente deseja tootrack o andamento do trabalho e, em seguida, publique o ativo codificado. Para obter mais informações, consulte [notificações de trabalho de serviços de mídia do Azure de usar ganchos toomonitor](media-services-dotnet-check-job-progress-with-webhooks.md). Para obter mais exemplos, consulte [Azure Functions nos Serviços de Mídia](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).  

Depois de definir a função, clique em **Salvar e Executar**.

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
##<a name="test-your-function"></a>Testar a função

tootest sua função, você precisa tooupload um arquivo MP4 em Olá **entrada** contêiner Olá da conta de armazenamento que você especificou na cadeia de caracteres de conexão de saudação.  

## <a name="next-step"></a>Próxima etapa

Neste ponto, você está pronto toostart desenvolvendo um aplicativo de serviços de mídia. 
 
Para obter mais detalhes e exemplos/soluções completas do uso de funções do Azure e os aplicativos lógicos com fluxos de trabalho de criação de conteúdo personalizado do Azure Media Services toocreate, consulte Olá [exemplo de integração de funções Media Services .NET no GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)

Além disso, consulte [notificações com .NET de trabalho de serviços de mídia do Azure de usar ganchos toomonitor](media-services-dotnet-check-job-progress-with-webhooks.md). 

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

