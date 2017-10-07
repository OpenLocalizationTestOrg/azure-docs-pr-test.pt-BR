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
# <a name="upload-files-into-a-media-services-account-using-net"></a><span data-ttu-id="4573f-103">Carregar arquivos em uma conta dos Serviços de Mídia usando o .NET</span><span class="sxs-lookup"><span data-stu-id="4573f-103">Upload files into a Media Services account using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4573f-104">.NET</span><span class="sxs-lookup"><span data-stu-id="4573f-104">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="4573f-105">REST</span><span class="sxs-lookup"><span data-stu-id="4573f-105">REST</span></span>](media-services-rest-upload-files.md)
> * [<span data-ttu-id="4573f-106">Portal</span><span class="sxs-lookup"><span data-stu-id="4573f-106">Portal</span></span>](media-services-portal-upload-files.md)
> 
> 

<span data-ttu-id="4573f-107">No Serviços de Mídia, você carrega (ou ingere) seus arquivos digitais em um ativo.</span><span class="sxs-lookup"><span data-stu-id="4573f-107">In Media Services, you upload (or ingest) your digital files into an asset.</span></span> <span data-ttu-id="4573f-108">Olá **ativo** entidade pode conter vídeo, áudio, imagens, coleções de miniaturas, texto rastreia e legenda codificada arquivos (e Olá metadados sobre esses arquivos.)  Depois que forem carregados arquivos hello, seu conteúdo é armazenado com segurança na nuvem de saudação para processamento adicional e streaming.</span><span class="sxs-lookup"><span data-stu-id="4573f-108">hello **Asset** entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.)  Once hello files are uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span>

<span data-ttu-id="4573f-109">Olá arquivos no ativo de saudação são chamados **arquivos de ativo**.</span><span class="sxs-lookup"><span data-stu-id="4573f-109">hello files in hello asset are called **Asset Files**.</span></span> <span data-ttu-id="4573f-110">Olá **AssetFile** instância e o arquivo de mídia real Olá são dois objetos distintos.</span><span class="sxs-lookup"><span data-stu-id="4573f-110">hello **AssetFile** instance and hello actual media file are two distinct objects.</span></span> <span data-ttu-id="4573f-111">instância de AssetFile Olá contém metadados sobre o arquivo de mídia Olá, enquanto o arquivo de mídia Olá contém conteúdo de mídia real hello.</span><span class="sxs-lookup"><span data-stu-id="4573f-111">hello AssetFile instance contains metadata about hello media file, while hello media file contains hello actual media content.</span></span>

> [!NOTE]
> <span data-ttu-id="4573f-112">Olá considerações a seguir se aplicam:</span><span class="sxs-lookup"><span data-stu-id="4573f-112">hello following considerations apply:</span></span>
> 
> * <span data-ttu-id="4573f-113">Serviços de mídia usa o valor de saudação do hello IAssetFile.Name propriedade ao criar URLs para Olá streaming de conteúdo (por exemplo, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Por esse motivo, não é permitida a codificação por porcentagem.</span><span class="sxs-lookup"><span data-stu-id="4573f-113">Media Services uses hello value of hello IAssetFile.Name property when building URLs for hello streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="4573f-114">Olá valor Olá **nome** propriedade não pode ter qualquer um dos seguintes Olá [%-caracteres reservados codificados](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # [] ".</span><span class="sxs-lookup"><span data-stu-id="4573f-114">hello value of hello **Name** property cannot have any of hello following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="4573f-115">Além disso, só pode haver um '.' para a extensão de nome de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="4573f-115">Also, there can only be one '.' for hello file name extension.</span></span>
> * <span data-ttu-id="4573f-116">comprimento de saudação do nome de saudação não deve ser maior do que 260 caracteres.</span><span class="sxs-lookup"><span data-stu-id="4573f-116">hello length of hello name should not be greater than 260 characters.</span></span>
> * <span data-ttu-id="4573f-117">Há um limite toohello tamanho máximo com suporte para o processamento de serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="4573f-117">There is a limit toohello maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="4573f-118">Consulte [isso](media-services-quotas-and-limitations.md) tópico para obter detalhes sobre a limitação de tamanho de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="4573f-118">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
> * <span data-ttu-id="4573f-119">Há um limite de 1.000.000 políticas para diferentes políticas de AMS (por exemplo, para política de Localizador ou ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="4573f-119">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="4573f-120">Você deve usar Olá Olá a mesma ID de política se você estiver usando sempre mesmo dias acesso permissões, por exemplo, as políticas para localizadores são tooremain desejado no local por um longo período (políticas de carregamento não).</span><span class="sxs-lookup"><span data-stu-id="4573f-120">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="4573f-121">Para obter mais informações, consulte [este](media-services-dotnet-manage-entities.md#limit-access-policies) tópico.</span><span class="sxs-lookup"><span data-stu-id="4573f-121">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>
> 

<span data-ttu-id="4573f-122">Ao criar ativos, você pode especificar Olá as opções de criptografia a seguir.</span><span class="sxs-lookup"><span data-stu-id="4573f-122">When you create assets, you can specify hello following encryption options.</span></span> 

* <span data-ttu-id="4573f-123">**None** - nenhuma criptografia é usada.</span><span class="sxs-lookup"><span data-stu-id="4573f-123">**None** - No encryption is used.</span></span> <span data-ttu-id="4573f-124">Este é o valor padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="4573f-124">This is hello default value.</span></span> <span data-ttu-id="4573f-125">Observe que, ao usar essa opção, seu conteúdo não será protegido quando estiver em trânsito ou em repouso no armazenamento.</span><span class="sxs-lookup"><span data-stu-id="4573f-125">Note that when using this option your content is not protected in transit or at rest in storage.</span></span>
  <span data-ttu-id="4573f-126">Se você planejar toodeliver um MP4 usando o download progressivo, use essa opção.</span><span class="sxs-lookup"><span data-stu-id="4573f-126">If you plan toodeliver an MP4 using progressive download, use this option.</span></span> 
* <span data-ttu-id="4573f-127">**CommonEncryption** - use essa opção se você estiver carregando conteúdo que já foi criptografado e protegido com criptografia comum ou DRM PlayReady (por exemplo, Smooth Streaming protegido com DRM PlayReady).</span><span class="sxs-lookup"><span data-stu-id="4573f-127">**CommonEncryption** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="4573f-128">**EnvelopeEncrypted** – use essa opção se você estiver carregando HLS criptografado com AES.</span><span class="sxs-lookup"><span data-stu-id="4573f-128">**EnvelopeEncrypted** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="4573f-129">Observe que arquivos Olá devem ter sido codificados e criptografados pelo Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="4573f-129">Note that hello files must have been encoded and encrypted by Transform Manager.</span></span>
* <span data-ttu-id="4573f-130">**StorageEncrypted** - criptografa o conteúdo limpo localmente usando a criptografia AES de 256 bits e, em seguida, carrega tooAzure armazenamento onde ele está armazenado criptografado em repouso.</span><span class="sxs-lookup"><span data-stu-id="4573f-130">**StorageEncrypted** - Encrypts your clear content locally using AES-256 bit encryption and then uploads it tooAzure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="4573f-131">Ativos protegidos pela criptografia de armazenamento são descriptografados automaticamente e posicionados em um tooencoding anterior do sistema de arquivos criptografados e, opcionalmente, criptografada novamente toouploading anterior como um novo ativo de saída.</span><span class="sxs-lookup"><span data-stu-id="4573f-131">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior tooencoding, and optionally re-encrypted prior toouploading back as a new output asset.</span></span> <span data-ttu-id="4573f-132">caso de uso primário Olá para criptografia de armazenamento é quando você deseja toosecure seus arquivos de mídia de entrada de alta qualidade com criptografia forte em rest no disco.</span><span class="sxs-lookup"><span data-stu-id="4573f-132">hello primary use case for Storage Encryption is when you want toosecure your high quality input media files with strong encryption at rest on disk.</span></span>
  
    <span data-ttu-id="4573f-133">Os Serviços de Mídia fornecem criptografia para armazenamento em disco para seus ativos, não por conexão, como o DRM (Gerenciador de Direitos Digitais).</span><span class="sxs-lookup"><span data-stu-id="4573f-133">Media Services provides on-disk storage encryption for your assets, not over-the-wire like Digital Rights Manager (DRM).</span></span>
  
    <span data-ttu-id="4573f-134">Se seu ativo tiver o armazenamento criptografado, você deverá configurar a política de entrega de ativos.</span><span class="sxs-lookup"><span data-stu-id="4573f-134">If your asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="4573f-135">Para obter mais informações, consulte [Configurando a política de entrega de ativos](media-services-dotnet-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="4573f-135">For more information see [Configuring asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span></span>

<span data-ttu-id="4573f-136">Se você especificar para toobe seu ativo criptografado com uma **CommonEncrypted** opção, ou um **EnvelopeEncypted** opção, você precisará tooassociate seu ativo com um **ContentKey**.</span><span class="sxs-lookup"><span data-stu-id="4573f-136">If you specify for your asset toobe encrypted with a **CommonEncrypted** option, or an **EnvelopeEncypted** option, you will need tooassociate your asset with a **ContentKey**.</span></span> <span data-ttu-id="4573f-137">Para obter mais informações, consulte [como toocreate um ContentKey](media-services-dotnet-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="4573f-137">For more information, see [How toocreate a ContentKey](media-services-dotnet-create-contentkey.md).</span></span> 

<span data-ttu-id="4573f-138">Se você especificar para toobe seu ativo criptografado com uma **StorageEncrypted** opção, Olá SDK do Media Services para .NET criará uma **StorateEncrypted** **ContentKey** para seu ativo.</span><span class="sxs-lookup"><span data-stu-id="4573f-138">If you specify for your asset toobe encrypted with a **StorageEncrypted** option, hello Media Services SDK for .NET will create a **StorateEncrypted** **ContentKey** for your asset.</span></span>

<span data-ttu-id="4573f-139">Este tópico mostra como os serviços de mídia toouse .NET SDK, bem como arquivos de tooupload de extensões do SDK do Media Services .NET em um ativo de serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="4573f-139">This topic shows how toouse Media Services .NET SDK as well as Media Services .NET SDK extensions tooupload files into a Media Services asset.</span></span>

## <a name="upload-a-single-file-with-media-services-net-sdk"></a><span data-ttu-id="4573f-140">Carregar um único arquivo com o SDK do .NET dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="4573f-140">Upload a single file with Media Services .NET SDK</span></span>
<span data-ttu-id="4573f-141">código de exemplo Hello abaixo usa tooupload .NET SDK um único arquivo.</span><span class="sxs-lookup"><span data-stu-id="4573f-141">hello sample code below uses .NET SDK tooupload a single file.</span></span> <span data-ttu-id="4573f-142">Olá AccessPolicy e localizador são criados e destruídos pela função de carregamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="4573f-142">hello AccessPolicy and Locator are created and destroyed by hello Upload function.</span></span> 


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


## <a name="upload-multiple-files-with-media-services-net-sdk"></a><span data-ttu-id="4573f-143">Carregar vários arquivos com o SDK do .NET dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="4573f-143">Upload multiple files with Media Services .NET SDK</span></span>
<span data-ttu-id="4573f-144">Olá mostrado no código a seguir como toocreate um ativo e carregar vários arquivos.</span><span class="sxs-lookup"><span data-stu-id="4573f-144">hello following code shows how toocreate an asset and upload multiple files.</span></span>

<span data-ttu-id="4573f-145">código de Olá Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="4573f-145">hello code does hello following:</span></span>

* <span data-ttu-id="4573f-146">Cria um ativo vazio usando Olá CreateEmptyAsset método definido na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="4573f-146">Creates an empty asset using hello CreateEmptyAsset method defined in hello previous step.</span></span>
* <span data-ttu-id="4573f-147">Cria um **AccessPolicy** instância que define permissões de saudação e a duração do ativo de toohello de acesso.</span><span class="sxs-lookup"><span data-stu-id="4573f-147">Creates an **AccessPolicy** instance that defines hello permissions and duration of access toohello asset.</span></span>
* <span data-ttu-id="4573f-148">Cria um **localizador** instância que fornece o ativo de toohello de acesso.</span><span class="sxs-lookup"><span data-stu-id="4573f-148">Creates a **Locator** instance that provides access toohello asset.</span></span>
* <span data-ttu-id="4573f-149">Cria uma instância de **BlobTransferClient** .</span><span class="sxs-lookup"><span data-stu-id="4573f-149">Creates a **BlobTransferClient** instance.</span></span> <span data-ttu-id="4573f-150">Esse tipo representa um cliente que opera em Olá que BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="4573f-150">This type represents a client that operates on hello Azure blobs.</span></span> <span data-ttu-id="4573f-151">Neste exemplo, usamos o progresso de carregamento do hello cliente toomonitor hello.</span><span class="sxs-lookup"><span data-stu-id="4573f-151">In this example we use hello client toomonitor hello upload progress.</span></span> 
* <span data-ttu-id="4573f-152">Enumera os arquivos no diretório especificado hello e cria um **AssetFile** instância para cada arquivo.</span><span class="sxs-lookup"><span data-stu-id="4573f-152">Enumerates through files in hello specified directory and creates an **AssetFile** instance for each file.</span></span>
* <span data-ttu-id="4573f-153">Carregamentos Olá arquivos nos serviços de mídia usando Olá **UploadAsync** método.</span><span class="sxs-lookup"><span data-stu-id="4573f-153">Uploads hello files into Media Services using hello **UploadAsync** method.</span></span> 

> [!NOTE]
> <span data-ttu-id="4573f-154">Use Olá UploadAsync método tooensure Olá chamadas não estão bloqueando e Olá arquivos são carregados em paralelo.</span><span class="sxs-lookup"><span data-stu-id="4573f-154">Use hello UploadAsync method tooensure that hello calls are not blocking and hello files are uploaded in parallel.</span></span>
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



<span data-ttu-id="4573f-155">Ao carregar um grande número de ativos, considere o seguinte de saudação.</span><span class="sxs-lookup"><span data-stu-id="4573f-155">When uploading a large number of assets, consider hello following.</span></span>

* <span data-ttu-id="4573f-156">Criar um novo objeto **CloudMediaContext** por thread.</span><span class="sxs-lookup"><span data-stu-id="4573f-156">Create a new **CloudMediaContext** object per thread.</span></span> <span data-ttu-id="4573f-157">Olá **CloudMediaContext** a classe não é thread-safe.</span><span class="sxs-lookup"><span data-stu-id="4573f-157">hello **CloudMediaContext** class is not thread safe.</span></span>
* <span data-ttu-id="4573f-158">Aumente NumberOfConcurrentTransfers do valor padrão de saudação do valor mais alto de 2 tooa como 5.</span><span class="sxs-lookup"><span data-stu-id="4573f-158">Increase NumberOfConcurrentTransfers from hello default value of 2 tooa higher value like 5.</span></span> <span data-ttu-id="4573f-159">Configurar essa propriedade afeta todas as instâncias de **CloudMediaContext**.</span><span class="sxs-lookup"><span data-stu-id="4573f-159">Setting this property affects all instances of **CloudMediaContext**.</span></span> 
* <span data-ttu-id="4573f-160">Manter ParallelTransferThreadCount com seu valor padrão de 10 hello.</span><span class="sxs-lookup"><span data-stu-id="4573f-160">Keep ParallelTransferThreadCount at hello default value of 10.</span></span>

## <span data-ttu-id="4573f-161"><a id="ingest_in_bulk"></a>Ingestão de ativos em massa usando o SDK do .NET dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="4573f-161"><a id="ingest_in_bulk"></a>Ingesting Assets in Bulk using Media Services .NET SDK</span></span>
<span data-ttu-id="4573f-162">O carregamento de grandes arquivos de ativo pode ser um afunilamento durante a criação do ativo.</span><span class="sxs-lookup"><span data-stu-id="4573f-162">Uploading large asset files can be a bottleneck during asset creation.</span></span> <span data-ttu-id="4573f-163">Ingestão de ativos em massa ou "Ingestão em massa", envolve separar a criação do ativo do processo de carregamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="4573f-163">Ingesting Assets in Bulk or “Bulk Ingesting”, involves decoupling asset creation from hello upload process.</span></span> <span data-ttu-id="4573f-164">toouse uma abordagem de ingestão em massa, crie um manifesto (IngestManifest) que descreve o ativo de saudação e seus arquivos associados.</span><span class="sxs-lookup"><span data-stu-id="4573f-164">toouse a bulk ingesting approach, create a manifest (IngestManifest) that describes hello asset and its associated files.</span></span> <span data-ttu-id="4573f-165">Em seguida, use o método de carregamento de saudação do contêiner de blob de sua escolha tooupload Olá arquivos associados toohello do manifesto.</span><span class="sxs-lookup"><span data-stu-id="4573f-165">Then use hello upload method of your choice tooupload hello associated files toohello manifest’s blob container.</span></span> <span data-ttu-id="4573f-166">Serviços de mídia do Microsoft Azure observa o contêiner de blob de saudação associado manifesto hello.</span><span class="sxs-lookup"><span data-stu-id="4573f-166">Microsoft Azure Media Services watches hello blob container associated with hello manifest.</span></span> <span data-ttu-id="4573f-167">Depois de um arquivo carregado toohello contêiner de blob, serviços de mídia do Microsoft Azure conclui a criação do ativo Olá com base na configuração de saudação do ativo Olá no manifesto de saudação (IngestManifestAsset).</span><span class="sxs-lookup"><span data-stu-id="4573f-167">Once a file is uploaded toohello blob container, Microsoft Azure Media Services completes hello asset creation based on hello configuration of hello asset in hello manifest (IngestManifestAsset).</span></span>

<span data-ttu-id="4573f-168">toocreate um novo IngestManifest chamar o método de criar hello exposto pelo Olá coleta os IngestManifests em Olá CloudMediaContext.</span><span class="sxs-lookup"><span data-stu-id="4573f-168">toocreate a new IngestManifest call hello Create method exposed by hello IngestManifests collection on hello CloudMediaContext.</span></span> <span data-ttu-id="4573f-169">Esse método criará um novo IngestManifest com o nome do manifesto Olá que você fornecer.</span><span class="sxs-lookup"><span data-stu-id="4573f-169">This method will create a new IngestManifest with hello manifest name you provide.</span></span>

    IIngestManifest manifest = context.IngestManifests.Create(name);

<span data-ttu-id="4573f-170">Crie ativos Olá que serão associados em massa de saudação IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="4573f-170">Create hello assets that will be associated with hello bulk IngestManifest.</span></span> <span data-ttu-id="4573f-171">Configure opções de criptografia de saudação desejada ativo Olá para ingestão em massa.</span><span class="sxs-lookup"><span data-stu-id="4573f-171">Configure hello desired encryption options on hello asset for bulk ingesting.</span></span>

    // Create hello assets that will be associated with this bulk ingest manifest
    IAsset destAsset1 = _context.Assets.Create(name + "_asset_1", AssetCreationOptions.None);
    IAsset destAsset2 = _context.Assets.Create(name + "_asset_2", AssetCreationOptions.None);

<span data-ttu-id="4573f-172">Um IngestManifestAsset associa um ativo a um IngestManifest em massa para ingestão em massa.</span><span class="sxs-lookup"><span data-stu-id="4573f-172">An IngestManifestAsset associates an Asset with a bulk IngestManifest for bulk ingesting.</span></span> <span data-ttu-id="4573f-173">Ele também associa Olá AssetFiles que comporá cada ativo.</span><span class="sxs-lookup"><span data-stu-id="4573f-173">It also associates hello AssetFiles that will make up each Asset.</span></span> <span data-ttu-id="4573f-174">toocreate um IngestManifestAsset, use o método de criação de Olá no contexto do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="4573f-174">toocreate an IngestManifestAsset, use hello Create method on hello server context.</span></span>

<span data-ttu-id="4573f-175">Olá exemplo a seguir demonstra adicionando dois novos os IngestManifestAssets que associam os dois ativos de saudação criado anteriormente em massa de toohello ingestmanifest.</span><span class="sxs-lookup"><span data-stu-id="4573f-175">hello following example demonstrates adding two new IngestManifestAssets that associate hello two assets previously created toohello bulk ingest manifest.</span></span> <span data-ttu-id="4573f-176">Cada IngestManifestAsset associa também um conjunto de arquivos que serão carregados para cada ativo durante a ingestão em massa.</span><span class="sxs-lookup"><span data-stu-id="4573f-176">Each IngestManifestAsset also associates a set of files that will be uploaded for each asset during bulk ingesting.</span></span>  

    string filename1 = _singleInputMp4Path;
    string filename2 = _primaryFilePath;
    string filename3 = _singleInputFilePath;

    IIngestManifestAsset bulkAsset1 =  manifest.IngestManifestAssets.Create(destAsset1, new[] { filename1 });
    IIngestManifestAsset bulkAsset2 =  manifest.IngestManifestAssets.Create(destAsset2, new[] { filename2, filename3 });

<span data-ttu-id="4573f-177">Você pode usar qualquer aplicativo cliente de alta velocidade capaz de carregar o contêiner de armazenamento do blob da arquivos para ativo Olá toohello URI fornecido pelo Olá **IIngestManifest.BlobStorageUriForUpload** propriedade Olá IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="4573f-177">You can use any high speed client application capable of uploading hello asset files toohello blob storage container URI provided by hello **IIngestManifest.BlobStorageUriForUpload** property of hello IngestManifest.</span></span> <span data-ttu-id="4573f-178">Um serviço de carregamento de alta velocidade notável é [Aspera sob demanda para o aplicativo do Azure](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6).</span><span class="sxs-lookup"><span data-stu-id="4573f-178">One notable high speed upload service is [Aspera On Demand for Azure Application](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6).</span></span> <span data-ttu-id="4573f-179">Você também pode escrever código de arquivos de ativos de saudação tooupload conforme Olá exemplo de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="4573f-179">You can also write code tooupload hello assets files as shown in hello following code example.</span></span>

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

<span data-ttu-id="4573f-180">código de saudação para carregar arquivos de ativo Olá para o exemplo hello usados neste tópico é mostrado no hello exemplo de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="4573f-180">hello code for uploading hello asset files for hello sample used in this topic is shown in hello following code example.</span></span>

    UploadBlobFile(manifest.BlobStorageUriForUpload, filename1);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename2);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename3);


<span data-ttu-id="4573f-181">Você pode determinar o progresso de saudação de ingestão em massa de Olá para todos os ativos associados um **IngestManifest** consultando a propriedade de estatísticas de saudação do hello **IngestManifest**.</span><span class="sxs-lookup"><span data-stu-id="4573f-181">You can determine hello progress of hello bulk ingesting for all assets associated with an **IngestManifest** by polling hello Statistics property of hello **IngestManifest**.</span></span> <span data-ttu-id="4573f-182">Em ordem tooupdate informações sobre o andamento, você deve usar um novo **CloudMediaContext** cada vez que você pesquisar propriedades de estatísticas de saudação.</span><span class="sxs-lookup"><span data-stu-id="4573f-182">In order tooupdate progress information, you must use a new **CloudMediaContext** each time you poll hello Statistics property.</span></span>

<span data-ttu-id="4573f-183">Olá exemplo a seguir demonstra sondagem um IngestManifest por seu **Id**.</span><span class="sxs-lookup"><span data-stu-id="4573f-183">hello following example demonstrates polling an IngestManifest by its **Id**.</span></span>

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



## <a name="upload-files-using-net-sdk-extensions"></a><span data-ttu-id="4573f-184">Carregar arquivos usando as extensões do SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="4573f-184">Upload files using .NET SDK Extensions</span></span>
<span data-ttu-id="4573f-185">exemplo Hello abaixo mostra como tooupload um único arquivo usando as extensões do SDK do .NET.</span><span class="sxs-lookup"><span data-stu-id="4573f-185">hello example below shows how tooupload a single file using .NET SDK Extensions.</span></span> <span data-ttu-id="4573f-186">Nesse caso Olá **CreateFromFile** método é usado, mas a versão assíncrona Olá também está disponível (**CreateFromFileAsync**).</span><span class="sxs-lookup"><span data-stu-id="4573f-186">In this case hello **CreateFromFile** method is used, but hello asynchronous version is also available (**CreateFromFileAsync**).</span></span> <span data-ttu-id="4573f-187">Olá **CreateFromFile** método permite que você especifique o nome do arquivo hello, opção de criptografia e um retorno de chamada de saudação do pedido tooreport carregar progresso do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="4573f-187">hello **CreateFromFile** method lets you specify hello file name, encryption option, and a callback in order tooreport hello upload progress of hello file.</span></span>

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

<span data-ttu-id="4573f-188">Olá exemplo a seguir chama a função UploadFile e especifica a criptografia de armazenamento como a opção de criação de ativos de saudação.</span><span class="sxs-lookup"><span data-stu-id="4573f-188">hello following example calls UploadFile function and specifies storage encryption as hello asset creation option.</span></span>  

    var asset = UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.StorageEncrypted);

## <a name="next-steps"></a><span data-ttu-id="4573f-189">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4573f-189">Next steps</span></span>

<span data-ttu-id="4573f-190">Agora você pode codificar seus ativos carregados.</span><span class="sxs-lookup"><span data-stu-id="4573f-190">You can now encode your uploaded assets.</span></span> <span data-ttu-id="4573f-191">Para saber mais, veja [Codificar ativos](media-services-portal-encode.md).</span><span class="sxs-lookup"><span data-stu-id="4573f-191">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="4573f-192">Você também pode usar as funções do Azure tootrigger um trabalho de codificação com base em um arquivo que chegam no contêiner de saudação configurada.</span><span class="sxs-lookup"><span data-stu-id="4573f-192">You can also use Azure Functions tootrigger an encoding job based on a file arriving in hello configured container.</span></span> <span data-ttu-id="4573f-193">Para obter mais informações, confira [este exemplo](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span><span class="sxs-lookup"><span data-stu-id="4573f-193">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="4573f-194">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="4573f-194">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4573f-195">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="4573f-195">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="4573f-196">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="4573f-196">Next step</span></span>
<span data-ttu-id="4573f-197">Agora que você carregou um ativo tooMedia serviços, vá toohello [como tooGet um processador de mídia] [ How tooGet a Media Processor] tópico.</span><span class="sxs-lookup"><span data-stu-id="4573f-197">Now that you have uploaded an asset tooMedia Services, go toohello [How tooGet a Media Processor][How tooGet a Media Processor] topic.</span></span>

[How tooGet a Media Processor]: media-services-get-media-processor.md

