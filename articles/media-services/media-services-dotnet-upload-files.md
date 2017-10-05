---
title: "Carregar arquivos em uma conta dos Serviços de Mídia usando o .NET | Microsoft Docs"
description: "Saiba como obter o conteúdo de mídia nos serviços de mídia ao criar e carregar ativos."
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
ms.openlocfilehash: ec8c1da633374ba684f6a0a895c542ee76ef73b8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="upload-files-into-a-media-services-account-using-net"></a><span data-ttu-id="a4eab-103">Carregar arquivos em uma conta dos Serviços de Mídia usando o .NET</span><span class="sxs-lookup"><span data-stu-id="a4eab-103">Upload files into a Media Services account using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a4eab-104">.NET</span><span class="sxs-lookup"><span data-stu-id="a4eab-104">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="a4eab-105">REST</span><span class="sxs-lookup"><span data-stu-id="a4eab-105">REST</span></span>](media-services-rest-upload-files.md)
> * [<span data-ttu-id="a4eab-106">Portal</span><span class="sxs-lookup"><span data-stu-id="a4eab-106">Portal</span></span>](media-services-portal-upload-files.md)
> 
> 

<span data-ttu-id="a4eab-107">No Serviços de Mídia, você carrega (ou ingere) seus arquivos digitais em um ativo.</span><span class="sxs-lookup"><span data-stu-id="a4eab-107">In Media Services, you upload (or ingest) your digital files into an asset.</span></span> <span data-ttu-id="a4eab-108">A entidade **Asset** pode conter vídeo, áudio, imagens, coleções de miniaturas, sequências de texto e arquivos de legendas (e os metadados sobre esses arquivos).  Depois que os arquivos são carregados, o conteúdo é armazenado com segurança na nuvem para processamento adicional e transmissão.</span><span class="sxs-lookup"><span data-stu-id="a4eab-108">The **Asset** entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.)  Once the files are uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span>

<span data-ttu-id="a4eab-109">Os arquivos no ativo são chamados **Arquivos de Ativo**.</span><span class="sxs-lookup"><span data-stu-id="a4eab-109">The files in the asset are called **Asset Files**.</span></span> <span data-ttu-id="a4eab-110">A instância de **AssetFile** e o arquivo de mídia real são dois objetos diferentes.</span><span class="sxs-lookup"><span data-stu-id="a4eab-110">The **AssetFile** instance and the actual media file are two distinct objects.</span></span> <span data-ttu-id="a4eab-111">A instância de AssetFile contém metadados sobre o arquivo de mídia, enquanto o arquivo de mídia contém o conteúdo de mídia real.</span><span class="sxs-lookup"><span data-stu-id="a4eab-111">The AssetFile instance contains metadata about the media file, while the media file contains the actual media content.</span></span>

> [!NOTE]
> <span data-ttu-id="a4eab-112">As seguintes considerações se aplicam:</span><span class="sxs-lookup"><span data-stu-id="a4eab-112">The following considerations apply:</span></span>
> 
> * <span data-ttu-id="a4eab-113">Os serviços de mídia usam o valor da propriedade IAssetFile.Name ao construir URLs para o conteúdo de streaming (por exemplo, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Por esse motivo, não é permitida a codificação por porcentagem.</span><span class="sxs-lookup"><span data-stu-id="a4eab-113">Media Services uses the value of the IAssetFile.Name property when building URLs for the streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="a4eab-114">O valor da propriedade **Name** não pode ter quaisquer dos seguintes [caracteres reservados para codificação de percentual](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span><span class="sxs-lookup"><span data-stu-id="a4eab-114">The value of the **Name** property cannot have any of the following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="a4eab-115">Além disso, pode haver somente um '.' para a extensão de nome de arquivo.</span><span class="sxs-lookup"><span data-stu-id="a4eab-115">Also, there can only be one '.' for the file name extension.</span></span>
> * <span data-ttu-id="a4eab-116">O comprimento do nome não deve ser maior do que 260 caracteres.</span><span class="sxs-lookup"><span data-stu-id="a4eab-116">The length of the name should not be greater than 260 characters.</span></span>
> * <span data-ttu-id="a4eab-117">Há um limite no tamanho máximo de arquivo com suporte para o processamento nos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="a4eab-117">There is a limit to the maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="a4eab-118">Confira [este](media-services-quotas-and-limitations.md) tópico para obter detalhes sobre a limitação de tamanho de arquivo.</span><span class="sxs-lookup"><span data-stu-id="a4eab-118">Please see [this](media-services-quotas-and-limitations.md) topic for details about the file size limitation.</span></span>
> * <span data-ttu-id="a4eab-119">Há um limite de 1.000.000 políticas para diferentes políticas de AMS (por exemplo, para política de Localizador ou ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="a4eab-119">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="a4eab-120">Use a mesma ID de política, se você estiver sempre usando os mesmos dias/permissões de acesso, por exemplo, políticas de localizadores que devem permanecer no local por um longo período (políticas de não carregamento).</span><span class="sxs-lookup"><span data-stu-id="a4eab-120">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="a4eab-121">Para obter mais informações, consulte [este](media-services-dotnet-manage-entities.md#limit-access-policies) tópico.</span><span class="sxs-lookup"><span data-stu-id="a4eab-121">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>
> 

<span data-ttu-id="a4eab-122">Quando você cria ativos, você pode especificar as seguintes opções de criptografia.</span><span class="sxs-lookup"><span data-stu-id="a4eab-122">When you create assets, you can specify the following encryption options.</span></span> 

* <span data-ttu-id="a4eab-123">**None** - nenhuma criptografia é usada.</span><span class="sxs-lookup"><span data-stu-id="a4eab-123">**None** - No encryption is used.</span></span> <span data-ttu-id="a4eab-124">Esse é o valor padrão.</span><span class="sxs-lookup"><span data-stu-id="a4eab-124">This is the default value.</span></span> <span data-ttu-id="a4eab-125">Observe que, ao usar essa opção, seu conteúdo não será protegido quando estiver em trânsito ou em repouso no armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a4eab-125">Note that when using this option your content is not protected in transit or at rest in storage.</span></span>
  <span data-ttu-id="a4eab-126">Se você pretende enviar um MP4 usando o download progressivo, use essa opção.</span><span class="sxs-lookup"><span data-stu-id="a4eab-126">If you plan to deliver an MP4 using progressive download, use this option.</span></span> 
* <span data-ttu-id="a4eab-127">**CommonEncryption** - use essa opção se você estiver carregando conteúdo que já foi criptografado e protegido com criptografia comum ou DRM PlayReady (por exemplo, Smooth Streaming protegido com DRM PlayReady).</span><span class="sxs-lookup"><span data-stu-id="a4eab-127">**CommonEncryption** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="a4eab-128">**EnvelopeEncrypted** – use essa opção se você estiver carregando HLS criptografado com AES.</span><span class="sxs-lookup"><span data-stu-id="a4eab-128">**EnvelopeEncrypted** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="a4eab-129">Observe que os arquivos devem ter sido codificados e criptografados pelo Gerenciador de Transformação.</span><span class="sxs-lookup"><span data-stu-id="a4eab-129">Note that the files must have been encoded and encrypted by Transform Manager.</span></span>
* <span data-ttu-id="a4eab-130">**StorageEncrypted** - criptografa o conteúdo limpo localmente usando a criptografia AES de 256 bits e, em seguida, carrega-o para o armazenamento do Azure, onde ele é armazenado, criptografado em rest.</span><span class="sxs-lookup"><span data-stu-id="a4eab-130">**StorageEncrypted** - Encrypts your clear content locally using AES-256 bit encryption and then uploads it to Azure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="a4eab-131">Ativos protegidos pela criptografia de armazenamento são descriptografados automaticamente e posicionados em um sistema de arquivos criptografado antes da codificação, então opcionalmente criptografados novamente antes do carregamento como um novo ativo de saída.</span><span class="sxs-lookup"><span data-stu-id="a4eab-131">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span></span> <span data-ttu-id="a4eab-132">O caso de uso primário para criptografia de armazenamento é quando você deseja proteger seus arquivos de mídia de entrada de alta qualidade com criptografia forte em repouso no disco.</span><span class="sxs-lookup"><span data-stu-id="a4eab-132">The primary use case for Storage Encryption is when you want to secure your high quality input media files with strong encryption at rest on disk.</span></span>
  
    <span data-ttu-id="a4eab-133">Os Serviços de Mídia fornecem criptografia para armazenamento em disco para seus ativos, não por conexão, como o DRM (Gerenciador de Direitos Digitais).</span><span class="sxs-lookup"><span data-stu-id="a4eab-133">Media Services provides on-disk storage encryption for your assets, not over-the-wire like Digital Rights Manager (DRM).</span></span>
  
    <span data-ttu-id="a4eab-134">Se seu ativo tiver o armazenamento criptografado, você deverá configurar a política de entrega de ativos.</span><span class="sxs-lookup"><span data-stu-id="a4eab-134">If your asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="a4eab-135">Para obter mais informações, consulte [Configurando a política de entrega de ativos](media-services-dotnet-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="a4eab-135">For more information see [Configuring asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span></span>

<span data-ttu-id="a4eab-136">Se você especificar para o ativo a ser criptografado com uma opção **CommonEncrypted** ou uma opção **EnvelopeEncypted**, você precisará associar seu ativo a um **ContentKey**.</span><span class="sxs-lookup"><span data-stu-id="a4eab-136">If you specify for your asset to be encrypted with a **CommonEncrypted** option, or an **EnvelopeEncypted** option, you will need to associate your asset with a **ContentKey**.</span></span> <span data-ttu-id="a4eab-137">Para obter mais informações, consulte [Como criar uma ContentKey](media-services-dotnet-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="a4eab-137">For more information, see [How to create a ContentKey](media-services-dotnet-create-contentkey.md).</span></span> 

<span data-ttu-id="a4eab-138">Se você especificar que o ativo deve ser criptografado com uma opção **StorageEncrypted**, o SDK dos Serviços de Mídia para .NET criará um **StorateEncrypted** **ContentKey** para o ativo.</span><span class="sxs-lookup"><span data-stu-id="a4eab-138">If you specify for your asset to be encrypted with a **StorageEncrypted** option, the Media Services SDK for .NET will create a **StorateEncrypted** **ContentKey** for your asset.</span></span>

<span data-ttu-id="a4eab-139">Este tópico mostra como usar o SDK do .NET dos Serviços de Mídia, bem como extensões do SDK do .NET dos Serviços de Mídia para carregar arquivos em um ativo dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="a4eab-139">This topic shows how to use Media Services .NET SDK as well as Media Services .NET SDK extensions to upload files into a Media Services asset.</span></span>

## <a name="upload-a-single-file-with-media-services-net-sdk"></a><span data-ttu-id="a4eab-140">Carregar um único arquivo com o SDK do .NET dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="a4eab-140">Upload a single file with Media Services .NET SDK</span></span>
<span data-ttu-id="a4eab-141">O código de exemplo abaixo usa o SDK do .NET para carregar um único arquivo.</span><span class="sxs-lookup"><span data-stu-id="a4eab-141">The sample code below uses .NET SDK to upload a single file.</span></span> <span data-ttu-id="a4eab-142">O AccessPolicy e Localizador são criados e destruídos pela função de Carregamento.</span><span class="sxs-lookup"><span data-stu-id="a4eab-142">The AccessPolicy and Locator are created and destroyed by the Upload function.</span></span> 


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


## <a name="upload-multiple-files-with-media-services-net-sdk"></a><span data-ttu-id="a4eab-143">Carregar vários arquivos com o SDK do .NET dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="a4eab-143">Upload multiple files with Media Services .NET SDK</span></span>
<span data-ttu-id="a4eab-144">O código a seguir mostra como criar um ativo e carregar vários arquivos.</span><span class="sxs-lookup"><span data-stu-id="a4eab-144">The following code shows how to create an asset and upload multiple files.</span></span>

<span data-ttu-id="a4eab-145">O código faz o seguinte:</span><span class="sxs-lookup"><span data-stu-id="a4eab-145">The code does the following:</span></span>

* <span data-ttu-id="a4eab-146">Cria um ativo vazio usando o método CreateEmptyAsset definido na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="a4eab-146">Creates an empty asset using the CreateEmptyAsset method defined in the previous step.</span></span>
* <span data-ttu-id="a4eab-147">Cria uma instância de **AccessPolicy** que define as permissões e a duração do acesso ao ativo.</span><span class="sxs-lookup"><span data-stu-id="a4eab-147">Creates an **AccessPolicy** instance that defines the permissions and duration of access to the asset.</span></span>
* <span data-ttu-id="a4eab-148">Cria uma instância de **Locator** que fornece acesso ao ativo.</span><span class="sxs-lookup"><span data-stu-id="a4eab-148">Creates a **Locator** instance that provides access to the asset.</span></span>
* <span data-ttu-id="a4eab-149">Cria uma instância de **BlobTransferClient** .</span><span class="sxs-lookup"><span data-stu-id="a4eab-149">Creates a **BlobTransferClient** instance.</span></span> <span data-ttu-id="a4eab-150">Esse tipo representa um cliente que opera nos blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="a4eab-150">This type represents a client that operates on the Azure blobs.</span></span> <span data-ttu-id="a4eab-151">Neste exemplo, usamos o cliente para monitorar o progresso do carregamento.</span><span class="sxs-lookup"><span data-stu-id="a4eab-151">In this example we use the client to monitor the upload progress.</span></span> 
* <span data-ttu-id="a4eab-152">Enumere os arquivos no diretório especificado e cria uma instância de **AssetFile** para cada arquivo.</span><span class="sxs-lookup"><span data-stu-id="a4eab-152">Enumerates through files in the specified directory and creates an **AssetFile** instance for each file.</span></span>
* <span data-ttu-id="a4eab-153">Carregue os arquivos para os serviços de mídia usando o método **UploadAsync** .</span><span class="sxs-lookup"><span data-stu-id="a4eab-153">Uploads the files into Media Services using the **UploadAsync** method.</span></span> 

> [!NOTE]
> <span data-ttu-id="a4eab-154">Use o método UploadAsync para garantir que as chamadas não estejam bloqueadas e os arquivos sejam carregados em paralelo.</span><span class="sxs-lookup"><span data-stu-id="a4eab-154">Use the UploadAsync method to ensure that the calls are not blocking and the files are uploaded in parallel.</span></span>
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

                // It is recommended to validate AccestFiles before upload. 
                Console.WriteLine("Start uploading of {0}", assetFile.Name);
                uploadTasks.Add(assetFile.UploadAsync(filePath, blobTransferClient, locator, CancellationToken.None));
            }

            Task.WaitAll(uploadTasks.ToArray());
            Console.WriteLine("Done uploading the files");

            blobTransferClient.TransferProgressChanged -= blobTransferClient_TransferProgressChanged;

            locator.Delete();
            accessPolicy.Delete();

            return asset;
        }

    static void  blobTransferClient_TransferProgressChanged(object sender, BlobTransferProgressChangedEventArgs e)
    {
        if (e.ProgressPercentage > 4) // Avoid startup jitter, as the upload tasks are added.
        {
            Console.WriteLine("{0}% upload competed for {1}.", e.ProgressPercentage, e.LocalFile);
        }
    }



<span data-ttu-id="a4eab-155">Ao carregar um grande número de ativos, considere o seguinte.</span><span class="sxs-lookup"><span data-stu-id="a4eab-155">When uploading a large number of assets, consider the following.</span></span>

* <span data-ttu-id="a4eab-156">Criar um novo objeto **CloudMediaContext** por thread.</span><span class="sxs-lookup"><span data-stu-id="a4eab-156">Create a new **CloudMediaContext** object per thread.</span></span> <span data-ttu-id="a4eab-157">A classe **CloudMediaContext** não é thread-safe.</span><span class="sxs-lookup"><span data-stu-id="a4eab-157">The **CloudMediaContext** class is not thread safe.</span></span>
* <span data-ttu-id="a4eab-158">Aumente NumberOfConcurrentTransfers do valor padrão de 2 para um valor maior como 5.</span><span class="sxs-lookup"><span data-stu-id="a4eab-158">Increase NumberOfConcurrentTransfers from the default value of 2 to a higher value like 5.</span></span> <span data-ttu-id="a4eab-159">Configurar essa propriedade afeta todas as instâncias de **CloudMediaContext**.</span><span class="sxs-lookup"><span data-stu-id="a4eab-159">Setting this property affects all instances of **CloudMediaContext**.</span></span> 
* <span data-ttu-id="a4eab-160">Mantenha ParallelTransferThreadCount no valor padrão de 10.</span><span class="sxs-lookup"><span data-stu-id="a4eab-160">Keep ParallelTransferThreadCount at the default value of 10.</span></span>

## <span data-ttu-id="a4eab-161"><a id="ingest_in_bulk"></a>Ingestão de ativos em massa usando o SDK do .NET dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="a4eab-161"><a id="ingest_in_bulk"></a>Ingesting Assets in Bulk using Media Services .NET SDK</span></span>
<span data-ttu-id="a4eab-162">O carregamento de grandes arquivos de ativo pode ser um afunilamento durante a criação do ativo.</span><span class="sxs-lookup"><span data-stu-id="a4eab-162">Uploading large asset files can be a bottleneck during asset creation.</span></span> <span data-ttu-id="a4eab-163">A ingestão de ativos em massa, ou "Ingestão em massa", envolve a dissociação da criação do ativo do processo de carregamento.</span><span class="sxs-lookup"><span data-stu-id="a4eab-163">Ingesting Assets in Bulk or “Bulk Ingesting”, involves decoupling asset creation from the upload process.</span></span> <span data-ttu-id="a4eab-164">Para usar uma abordagem de ingestão em massa, crie um manifesto (IngestManifest) que descreve o ativo e seus arquivos associados.</span><span class="sxs-lookup"><span data-stu-id="a4eab-164">To use a bulk ingesting approach, create a manifest (IngestManifest) that describes the asset and its associated files.</span></span> <span data-ttu-id="a4eab-165">Em seguida, use o método de carregamento de sua escolha para carregar os arquivos associados ao contêiner de blob do manifesto.</span><span class="sxs-lookup"><span data-stu-id="a4eab-165">Then use the upload method of your choice to upload the associated files to the manifest’s blob container.</span></span> <span data-ttu-id="a4eab-166">Os serviços de mídia do Microsoft Azure observa o contêiner de blob associado ao manifesto.</span><span class="sxs-lookup"><span data-stu-id="a4eab-166">Microsoft Azure Media Services watches the blob container associated with the manifest.</span></span> <span data-ttu-id="a4eab-167">Depois que um arquivo é carregado para o contêiner de blob, os serviços de mídia do Microsoft Azure concluem a criação do ativo com base na configuração do ativo no manifesto (IngestManifestAsset).</span><span class="sxs-lookup"><span data-stu-id="a4eab-167">Once a file is uploaded to the blob container, Microsoft Azure Media Services completes the asset creation based on the configuration of the asset in the manifest (IngestManifestAsset).</span></span>

<span data-ttu-id="a4eab-168">Para criar um novo IngestManifest chame o método Criar exposto pela coleção IngestManifests no CloudMediaContext.</span><span class="sxs-lookup"><span data-stu-id="a4eab-168">To create a new IngestManifest call the Create method exposed by the IngestManifests collection on the CloudMediaContext.</span></span> <span data-ttu-id="a4eab-169">Esse método criará um novo IngestManifest com o nome manifesto fornecido.</span><span class="sxs-lookup"><span data-stu-id="a4eab-169">This method will create a new IngestManifest with the manifest name you provide.</span></span>

    IIngestManifest manifest = context.IngestManifests.Create(name);

<span data-ttu-id="a4eab-170">Crie os ativos que serão associados a IngestManifest em massa.</span><span class="sxs-lookup"><span data-stu-id="a4eab-170">Create the assets that will be associated with the bulk IngestManifest.</span></span> <span data-ttu-id="a4eab-171">Configure as opções de criptografia desejadas no ativo para a ingestão em massa.</span><span class="sxs-lookup"><span data-stu-id="a4eab-171">Configure the desired encryption options on the asset for bulk ingesting.</span></span>

    // Create the assets that will be associated with this bulk ingest manifest
    IAsset destAsset1 = _context.Assets.Create(name + "_asset_1", AssetCreationOptions.None);
    IAsset destAsset2 = _context.Assets.Create(name + "_asset_2", AssetCreationOptions.None);

<span data-ttu-id="a4eab-172">Um IngestManifestAsset associa um ativo a um IngestManifest em massa para ingestão em massa.</span><span class="sxs-lookup"><span data-stu-id="a4eab-172">An IngestManifestAsset associates an Asset with a bulk IngestManifest for bulk ingesting.</span></span> <span data-ttu-id="a4eab-173">Ele também associa os AssetFiles que formarão cada ativo.</span><span class="sxs-lookup"><span data-stu-id="a4eab-173">It also associates the AssetFiles that will make up each Asset.</span></span> <span data-ttu-id="a4eab-174">Para criar um IngestManifestAsset, use o método Criar no contexto do servidor.</span><span class="sxs-lookup"><span data-stu-id="a4eab-174">To create an IngestManifestAsset, use the Create method on the server context.</span></span>

<span data-ttu-id="a4eab-175">O exemplo a seguir demonstra a adição de dois novos IngestManifestAssets que associam os dois ativos criados anteriormente no manifesto de ingestão em massa.</span><span class="sxs-lookup"><span data-stu-id="a4eab-175">The following example demonstrates adding two new IngestManifestAssets that associate the two assets previously created to the bulk ingest manifest.</span></span> <span data-ttu-id="a4eab-176">Cada IngestManifestAsset associa também um conjunto de arquivos que serão carregados para cada ativo durante a ingestão em massa.</span><span class="sxs-lookup"><span data-stu-id="a4eab-176">Each IngestManifestAsset also associates a set of files that will be uploaded for each asset during bulk ingesting.</span></span>  

    string filename1 = _singleInputMp4Path;
    string filename2 = _primaryFilePath;
    string filename3 = _singleInputFilePath;

    IIngestManifestAsset bulkAsset1 =  manifest.IngestManifestAssets.Create(destAsset1, new[] { filename1 });
    IIngestManifestAsset bulkAsset2 =  manifest.IngestManifestAssets.Create(destAsset2, new[] { filename2, filename3 });

<span data-ttu-id="a4eab-177">Você pode usar qualquer aplicativo de cliente de alta velocidade capaz de carregar os arquivos de ativo para o URI do contêiner de armazenamento de blobs fornecido pela propriedade **IIngestManifest.BlobStorageUriForUpload** do IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="a4eab-177">You can use any high speed client application capable of uploading the asset files to the blob storage container URI provided by the **IIngestManifest.BlobStorageUriForUpload** property of the IngestManifest.</span></span> <span data-ttu-id="a4eab-178">Um serviço de carregamento de alta velocidade notável é [Aspera sob demanda para o aplicativo do Azure](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6).</span><span class="sxs-lookup"><span data-stu-id="a4eab-178">One notable high speed upload service is [Aspera On Demand for Azure Application](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6).</span></span> <span data-ttu-id="a4eab-179">Você também pode escrever o código para carregar os arquivos de ativos conforme mostrado no exemplo de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="a4eab-179">You can also write code to upload the assets files as shown in the following code example.</span></span>

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

<span data-ttu-id="a4eab-180">O código para carregar os arquivos de ativo para o exemplo usado neste tópico é mostrado no exemplo de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="a4eab-180">The code for uploading the asset files for the sample used in this topic is shown in the following code example.</span></span>

    UploadBlobFile(manifest.BlobStorageUriForUpload, filename1);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename2);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename3);


<span data-ttu-id="a4eab-181">Você pode determinar o progresso da ingestão em massa para todos os ativos associados com um **IngestManifest** sondando a propriedade Estatística do **IngestManifest**.</span><span class="sxs-lookup"><span data-stu-id="a4eab-181">You can determine the progress of the bulk ingesting for all assets associated with an **IngestManifest** by polling the Statistics property of the **IngestManifest**.</span></span> <span data-ttu-id="a4eab-182">Para atualizar informações sobre o andamento, você deve usar um novo **CloudMediaContext** sempre que sondar a propriedade Estatísticas.</span><span class="sxs-lookup"><span data-stu-id="a4eab-182">In order to update progress information, you must use a new **CloudMediaContext** each time you poll the Statistics property.</span></span>

<span data-ttu-id="a4eab-183">O exemplo a seguir demonstra a sondagem em um IngestManifest pela sua **Id**.</span><span class="sxs-lookup"><span data-stu-id="a4eab-183">The following example demonstrates polling an IngestManifest by its **Id**.</span></span>

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



## <a name="upload-files-using-net-sdk-extensions"></a><span data-ttu-id="a4eab-184">Carregar arquivos usando as extensões do SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="a4eab-184">Upload files using .NET SDK Extensions</span></span>
<span data-ttu-id="a4eab-185">O exemplo a seguir mostra como carregar um único arquivo usando as extensões do SDK do .NET.</span><span class="sxs-lookup"><span data-stu-id="a4eab-185">The example below shows how to upload a single file using .NET SDK Extensions.</span></span> <span data-ttu-id="a4eab-186">Nesse caso, o método **CreateFromFile** é usado, mas a versão assíncrona também está disponível (**CreateFromFileAsync**).</span><span class="sxs-lookup"><span data-stu-id="a4eab-186">In this case the **CreateFromFile** method is used, but the asynchronous version is also available (**CreateFromFileAsync**).</span></span> <span data-ttu-id="a4eab-187">O método **CreateFromFile** permite que você especifique o nome do arquivo, a opção de criptografia e um retorno de chamada para relatar o progresso do carregamento do arquivo.</span><span class="sxs-lookup"><span data-stu-id="a4eab-187">The **CreateFromFile** method lets you specify the file name, encryption option, and a callback in order to report the upload progress of the file.</span></span>

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

<span data-ttu-id="a4eab-188">O exemplo a seguir chama a função UploadFile e especifica a criptografia de armazenamento como a opção de criação de ativos.</span><span class="sxs-lookup"><span data-stu-id="a4eab-188">The following example calls UploadFile function and specifies storage encryption as the asset creation option.</span></span>  

    var asset = UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.StorageEncrypted);

## <a name="next-steps"></a><span data-ttu-id="a4eab-189">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a4eab-189">Next steps</span></span>

<span data-ttu-id="a4eab-190">Agora você pode codificar seus ativos carregados.</span><span class="sxs-lookup"><span data-stu-id="a4eab-190">You can now encode your uploaded assets.</span></span> <span data-ttu-id="a4eab-191">Para saber mais, veja [Codificar ativos](media-services-portal-encode.md).</span><span class="sxs-lookup"><span data-stu-id="a4eab-191">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="a4eab-192">Você também pode usar as Azure Functions para disparar um trabalho de codificação baseado em um arquivo que chega no contêiner configurado.</span><span class="sxs-lookup"><span data-stu-id="a4eab-192">You can also use Azure Functions to trigger an encoding job based on a file arriving in the configured container.</span></span> <span data-ttu-id="a4eab-193">Para obter mais informações, confira [este exemplo](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span><span class="sxs-lookup"><span data-stu-id="a4eab-193">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="a4eab-194">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="a4eab-194">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a4eab-195">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="a4eab-195">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="a4eab-196">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="a4eab-196">Next step</span></span>
<span data-ttu-id="a4eab-197">Agora que você carregou um ativo nos Serviços de Mídia, acesse o tópico [Como obter um processador de mídia][How to Get a Media Processor].</span><span class="sxs-lookup"><span data-stu-id="a4eab-197">Now that you have uploaded an asset to Media Services, go to the [How to Get a Media Processor][How to Get a Media Processor] topic.</span></span>

[How to Get a Media Processor]: media-services-get-media-processor.md

