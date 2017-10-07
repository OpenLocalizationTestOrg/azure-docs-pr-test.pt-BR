---
title: "arquivos de aaaUpload em uma conta de serviços de mídia usando o .NET | Microsoft Docs"
description: "Saiba como tooget do conteúdo de mídia nos serviços de mídia criando e carregando ativos."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: c9c86380-9395-4db8-acea-507c52066f73
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/12/2017
ms.author: juliako
ms.openlocfilehash: 11c8a359b09efe04b54490fd48ac0cd7c366f8b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-net"></a>Carregar arquivos em uma conta dos Serviços de Mídia usando o .NET
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-upload-files.md)
> * [REST](media-services-rest-upload-files.md)
> * [Portal](media-services-portal-upload-files.md)
> 
> 

No Serviços de Mídia, você carrega (ou ingere) seus arquivos digitais em um ativo. Olá **ativo** entidade pode conter vídeo, áudio, imagens, coleções de miniaturas, texto rastreia e legenda codificada arquivos (e Olá metadados sobre esses arquivos.)  Depois que forem carregados arquivos hello, seu conteúdo é armazenado com segurança na nuvem de saudação para processamento adicional e streaming.

Olá arquivos no ativo de saudação são chamados **arquivos de ativo**. Olá **AssetFile** instância e o arquivo de mídia real Olá são dois objetos distintos. instância de AssetFile Olá contém metadados sobre o arquivo de mídia Olá, enquanto o arquivo de mídia Olá contém conteúdo de mídia real hello.

> [!NOTE]
> Olá considerações a seguir se aplicam:
> 
> * Serviços de mídia usa o valor de saudação do hello IAssetFile.Name propriedade ao criar URLs para Olá streaming de conteúdo (por exemplo, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Por esse motivo, não é permitida a codificação por porcentagem. Olá valor Olá **nome** propriedade não pode ter qualquer um dos seguintes Olá [%-caracteres reservados codificados](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # [] ". Além disso, só pode haver um '.' para a extensão de nome de arquivo hello.
> * comprimento de saudação do nome de saudação não deve ser maior do que 260 caracteres.
> * Há um limite toohello tamanho máximo com suporte para o processamento de serviços de mídia. Consulte [isso](media-services-quotas-and-limitations.md) tópico para obter detalhes sobre a limitação de tamanho de arquivo hello.
> * Há um limite de 1.000.000 políticas para diferentes políticas de AMS (por exemplo, para política de Localizador ou ContentKeyAuthorizationPolicy). Você deve usar Olá Olá a mesma ID de política se você estiver usando sempre mesmo dias acesso permissões, por exemplo, as políticas para localizadores são tooremain desejado no local por um longo período (políticas de carregamento não). Para obter mais informações, consulte [este](media-services-dotnet-manage-entities.md#limit-access-policies) tópico.
> 

Ao criar ativos, você pode especificar Olá as opções de criptografia a seguir. 

* **None** - nenhuma criptografia é usada. Este é o valor padrão de saudação. Observe que, ao usar essa opção, seu conteúdo não será protegido quando estiver em trânsito ou em repouso no armazenamento.
  Se você planejar toodeliver um MP4 usando o download progressivo, use essa opção. 
* **CommonEncryption** - use essa opção se você estiver carregando conteúdo que já foi criptografado e protegido com criptografia comum ou DRM PlayReady (por exemplo, Smooth Streaming protegido com DRM PlayReady).
* **EnvelopeEncrypted** – use essa opção se você estiver carregando HLS criptografado com AES. Observe que arquivos Olá devem ter sido codificados e criptografados pelo Transform Manager.
* **StorageEncrypted** - criptografa o conteúdo limpo localmente usando a criptografia AES de 256 bits e, em seguida, carrega tooAzure armazenamento onde ele está armazenado criptografado em repouso. Ativos protegidos pela criptografia de armazenamento são descriptografados automaticamente e posicionados em um tooencoding anterior do sistema de arquivos criptografados e, opcionalmente, criptografada novamente toouploading anterior como um novo ativo de saída. caso de uso primário Olá para criptografia de armazenamento é quando você deseja toosecure seus arquivos de mídia de entrada de alta qualidade com criptografia forte em rest no disco.
  
    Os Serviços de Mídia fornecem criptografia para armazenamento em disco para seus ativos, não por conexão, como o DRM (Gerenciador de Direitos Digitais).
  
    Se seu ativo tiver o armazenamento criptografado, você deverá configurar a política de entrega de ativos. Para obter mais informações, consulte [Configurando a política de entrega de ativos](media-services-dotnet-configure-asset-delivery-policy.md).

Se você especificar para toobe seu ativo criptografado com uma **CommonEncrypted** opção, ou um **EnvelopeEncypted** opção, você precisará tooassociate seu ativo com um **ContentKey**. Para obter mais informações, consulte [como toocreate um ContentKey](media-services-dotnet-create-contentkey.md). 

Se você especificar para toobe seu ativo criptografado com uma **StorageEncrypted** opção, Olá SDK do Media Services para .NET criará uma **StorateEncrypted** **ContentKey** para seu ativo.

Este tópico mostra como os serviços de mídia toouse .NET SDK, bem como arquivos de tooupload de extensões do SDK do Media Services .NET em um ativo de serviços de mídia.

## <a name="upload-a-single-file-with-media-services-net-sdk"></a>Carregar um único arquivo com o SDK do .NET dos Serviços de Mídia
código de exemplo Hello abaixo usa tooupload .NET SDK um único arquivo. Olá AccessPolicy e localizador são criados e destruídos pela função de carregamento de saudação. 


        static public IAsset CreateAssetAndUploadSingleFile(AssetCreationOptions assetCreationOptions, string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
                Console.WriteLine("File does not exist.");
                return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, assetCreationOptions);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }


## <a name="upload-multiple-files-with-media-services-net-sdk"></a>Carregar vários arquivos com o SDK do .NET dos Serviços de Mídia
Olá mostrado no código a seguir como toocreate um ativo e carregar vários arquivos.

código de Olá Olá a seguir:

* Cria um ativo vazio usando Olá CreateEmptyAsset método definido na etapa anterior hello.
* Cria um **AccessPolicy** instância que define permissões de saudação e a duração do ativo de toohello de acesso.
* Cria um **localizador** instância que fornece o ativo de toohello de acesso.
* Cria uma instância de **BlobTransferClient** . Esse tipo representa um cliente que opera em Olá que BLOBs do Azure. Neste exemplo, usamos o progresso de carregamento do hello cliente toomonitor hello. 
* Enumera os arquivos no diretório especificado hello e cria um **AssetFile** instância para cada arquivo.
* Carregamentos Olá arquivos nos serviços de mídia usando Olá **UploadAsync** método. 

> [!NOTE]
> Use Olá UploadAsync método tooensure Olá chamadas não estão bloqueando e Olá arquivos são carregados em paralelo.
> 
> 

        static public IAsset CreateAssetAndUploadMultipleFiles(AssetCreationOptions assetCreationOptions, string folderPath)
        {
            var assetName = "UploadMultipleFiles_" + DateTime.UtcNow.ToString();

            IAsset asset = _context.Assets.Create(assetName, assetCreationOptions);

            var accessPolicy = _context.AccessPolicies.Create(assetName, TimeSpan.FromDays(30),
                                                                AccessPermissions.Write | AccessPermissions.List);

            var locator = _context.Locators.CreateLocator(LocatorType.Sas, asset, accessPolicy);

            var blobTransferClient = new BlobTransferClient();
            blobTransferClient.NumberOfConcurrentTransfers = 20;
            blobTransferClient.ParallelTransferThreadCount = 20;

            blobTransferClient.TransferProgressChanged += blobTransferClient_TransferProgressChanged;

            var filePaths = Directory.EnumerateFiles(folderPath);

            Console.WriteLine("There are {0} files in {1}", filePaths.Count(), folderPath);

            if (!filePaths.Any())
            {
                throw new FileNotFoundException(String.Format("No files in directory, check folderPath: {0}", folderPath));
            }

            var uploadTasks = new List<Task>();
            foreach (var filePath in filePaths)
            {
                var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
                Console.WriteLine("Created assetFile {0}", assetFile.Name);

                // It is recommended toovalidate AccestFiles before upload. 
                Console.WriteLine("Start uploading of {0}", assetFile.Name);
                uploadTasks.Add(assetFile.UploadAsync(filePath, blobTransferClient, locator, CancellationToken.None));
            }

            Task.WaitAll(uploadTasks.ToArray());
            Console.WriteLine("Done uploading hello files");

            blobTransferClient.TransferProgressChanged -= blobTransferClient_TransferProgressChanged;

            locator.Delete();
            accessPolicy.Delete();

            return asset;
        }

    static void  blobTransferClient_TransferProgressChanged(object sender, BlobTransferProgressChangedEventArgs e)
    {
        if (e.ProgressPercentage > 4) // Avoid startup jitter, as hello upload tasks are added.
        {
            Console.WriteLine("{0}% upload competed for {1}.", e.ProgressPercentage, e.LocalFile);
        }
    }



Ao carregar um grande número de ativos, considere o seguinte de saudação.

* Criar um novo objeto **CloudMediaContext** por thread. Olá **CloudMediaContext** a classe não é thread-safe.
* Aumente NumberOfConcurrentTransfers do valor padrão de saudação do valor mais alto de 2 tooa como 5. Configurar essa propriedade afeta todas as instâncias de **CloudMediaContext**. 
* Manter ParallelTransferThreadCount com seu valor padrão de 10 hello.

## <a id="ingest_in_bulk"></a>Ingestão de ativos em massa usando o SDK do .NET dos Serviços de Mídia
O carregamento de grandes arquivos de ativo pode ser um afunilamento durante a criação do ativo. Ingestão de ativos em massa ou "Ingestão em massa", envolve separar a criação do ativo do processo de carregamento de saudação. toouse uma abordagem de ingestão em massa, crie um manifesto (IngestManifest) que descreve o ativo de saudação e seus arquivos associados. Em seguida, use o método de carregamento de saudação do contêiner de blob de sua escolha tooupload Olá arquivos associados toohello do manifesto. Serviços de mídia do Microsoft Azure observa o contêiner de blob de saudação associado manifesto hello. Depois de um arquivo carregado toohello contêiner de blob, serviços de mídia do Microsoft Azure conclui a criação do ativo Olá com base na configuração de saudação do ativo Olá no manifesto de saudação (IngestManifestAsset).

toocreate um novo IngestManifest chamar o método de criar hello exposto pelo Olá coleta os IngestManifests em Olá CloudMediaContext. Esse método criará um novo IngestManifest com o nome do manifesto Olá que você fornecer.

    IIngestManifest manifest = context.IngestManifests.Create(name);

Crie ativos Olá que serão associados em massa de saudação IngestManifest. Configure opções de criptografia de saudação desejada ativo Olá para ingestão em massa.

    // Create hello assets that will be associated with this bulk ingest manifest
    IAsset destAsset1 = _context.Assets.Create(name + "_asset_1", AssetCreationOptions.None);
    IAsset destAsset2 = _context.Assets.Create(name + "_asset_2", AssetCreationOptions.None);

Um IngestManifestAsset associa um ativo a um IngestManifest em massa para ingestão em massa. Ele também associa Olá AssetFiles que comporá cada ativo. toocreate um IngestManifestAsset, use o método de criação de Olá no contexto do servidor de saudação.

Olá exemplo a seguir demonstra adicionando dois novos os IngestManifestAssets que associam os dois ativos de saudação criado anteriormente em massa de toohello ingestmanifest. Cada IngestManifestAsset associa também um conjunto de arquivos que serão carregados para cada ativo durante a ingestão em massa.  

    string filename1 = _singleInputMp4Path;
    string filename2 = _primaryFilePath;
    string filename3 = _singleInputFilePath;

    IIngestManifestAsset bulkAsset1 =  manifest.IngestManifestAssets.Create(destAsset1, new[] { filename1 });
    IIngestManifestAsset bulkAsset2 =  manifest.IngestManifestAssets.Create(destAsset2, new[] { filename2, filename3 });

Você pode usar qualquer aplicativo cliente de alta velocidade capaz de carregar o contêiner de armazenamento do blob da arquivos para ativo Olá toohello URI fornecido pelo Olá **IIngestManifest.BlobStorageUriForUpload** propriedade Olá IngestManifest. Um serviço de carregamento de alta velocidade notável é [Aspera sob demanda para o aplicativo do Azure](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6). Você também pode escrever código de arquivos de ativos de saudação tooupload conforme Olá exemplo de código a seguir.

    static void UploadBlobFile(string destBlobURI, string filename)
    {
        Task copytask = new Task(() =>
        {
            var storageaccount = new CloudStorageAccount(new StorageCredentials(_storageAccountName, _storageAccountKey), true);
            CloudBlobClient blobClient = storageaccount.CreateCloudBlobClient();
            CloudBlobContainer blobContainer = blobClient.GetContainerReference(destBlobURI);

            string[] splitfilename = filename.Split('\\');
            var blob = blobContainer.GetBlockBlobReference(splitfilename[splitfilename.Length - 1]);

            using (var stream = System.IO.File.OpenRead(filename))
                blob.UploadFromStream(stream);

            lock (consoleWriteLock)
            {
                Console.WriteLine("Upload for {0} completed.", filename);
            }
        });

        copytask.Start();
    }

código de saudação para carregar arquivos de ativo Olá para o exemplo hello usados neste tópico é mostrado no hello exemplo de código a seguir.

    UploadBlobFile(manifest.BlobStorageUriForUpload, filename1);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename2);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename3);


Você pode determinar o progresso de saudação de ingestão em massa de Olá para todos os ativos associados um **IngestManifest** consultando a propriedade de estatísticas de saudação do hello **IngestManifest**. Em ordem tooupdate informações sobre o andamento, você deve usar um novo **CloudMediaContext** cada vez que você pesquisar propriedades de estatísticas de saudação.

Olá exemplo a seguir demonstra sondagem um IngestManifest por seu **Id**.

    static void MonitorBulkManifest(string manifestID)
    {
       bool bContinue = true;
       while (bContinue)
       {
          CloudMediaContext context = GetContext();
          IIngestManifest manifest = context.IngestManifests.Where(m => m.Id == manifestID).FirstOrDefault();

          if (manifest != null)
          {
             lock(consoleWriteLock)
             {
                Console.WriteLine("\nWaiting on all file uploads.");
                Console.WriteLine("PendingFilesCount  : {0}", manifest.Statistics.PendingFilesCount);
                Console.WriteLine("FinishedFilesCount : {0}", manifest.Statistics.FinishedFilesCount);
                Console.WriteLine("{0}% complete.\n", (float)manifest.Statistics.FinishedFilesCount / (float)(manifest.Statistics.FinishedFilesCount + manifest.Statistics.PendingFilesCount) * 100);

                if (manifest.Statistics.PendingFilesCount == 0)
                {
                   Console.WriteLine("Completed\n");
                   bContinue = false;
                }
             }

             if (manifest.Statistics.FinishedFilesCount < manifest.Statistics.PendingFilesCount)
                Thread.Sleep(60000);
          }
          else // Manifest is null
             bContinue = false;
       }
    }



## <a name="upload-files-using-net-sdk-extensions"></a>Carregar arquivos usando as extensões do SDK do .NET
exemplo Hello abaixo mostra como tooupload um único arquivo usando as extensões do SDK do .NET. Nesse caso Olá **CreateFromFile** método é usado, mas a versão assíncrona Olá também está disponível (**CreateFromFileAsync**). Olá **CreateFromFile** método permite que você especifique o nome do arquivo hello, opção de criptografia e um retorno de chamada de saudação do pedido tooreport carregar progresso do arquivo hello.

    static public IAsset UploadFile(string fileName, AssetCreationOptions options)
    {
        IAsset inputAsset = _context.Assets.CreateFromFile(
            fileName,
            options,
            (af, p) =>
            {
                Console.WriteLine("Uploading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Asset {0} created.", inputAsset.Id);

        return inputAsset;
    }

Olá exemplo a seguir chama a função UploadFile e especifica a criptografia de armazenamento como a opção de criação de ativos de saudação.  

    var asset = UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.StorageEncrypted);

## <a name="next-steps"></a>Próximas etapas

Agora você pode codificar seus ativos carregados. Para saber mais, veja [Codificar ativos](media-services-portal-encode.md).

Você também pode usar as funções do Azure tootrigger um trabalho de codificação com base em um arquivo que chegam no contêiner de saudação configurada. Para obter mais informações, confira [este exemplo](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a>Próxima etapa
Agora que você carregou um ativo tooMedia serviços, vá toohello [como tooGet um processador de mídia] [ How tooGet a Media Processor] tópico.

[How tooGet a Media Processor]: media-services-get-media-processor.md

