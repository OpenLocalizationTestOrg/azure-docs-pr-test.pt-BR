---
title: "computador de tooyour de ativos de serviços de mídia aaaDownload - Azure | Microsoft Docs"
description: "Saiba mais sobre o computador de tooyour ativos toodownload. Exemplos de código são escritos em c# e usam Olá SDK do Media Services para .NET."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 8908a1dd-3ffb-4f18-955d-4c8e2d82fc5d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 6c6e764720caa59d8371178a2682700345f7bc57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-deliver-an-asset-by-download"></a><span data-ttu-id="cf78e-104">Como fornecer um ativo por Download</span><span class="sxs-lookup"><span data-stu-id="cf78e-104">How to: Deliver an Asset by Download</span></span>
<span data-ttu-id="cf78e-105">Este tópico discute as opções para entrega de ativos de mídia carregado tooMedia serviços.</span><span class="sxs-lookup"><span data-stu-id="cf78e-105">This topic discusses options for delivering media assets uploaded tooMedia Services.</span></span> <span data-ttu-id="cf78e-106">Você pode entregar conteúdo dos Serviços de Mídia em vários cenários de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="cf78e-106">You can deliver Media Services content in numerous application scenarios.</span></span> <span data-ttu-id="cf78e-107">Você pode baixar ativos de mídia ou acessá-los usando um localizador.</span><span class="sxs-lookup"><span data-stu-id="cf78e-107">You can download media assets, or access them by using a locator.</span></span> <span data-ttu-id="cf78e-108">Você pode enviar o aplicativo de tooanother conteúdo de mídia ou tooanother provedor de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="cf78e-108">You can send media content tooanother application or tooanother content provider.</span></span> <span data-ttu-id="cf78e-109">Para melhor desempenho e escalabilidade, você também pode fornecer conteúdo usando uma CDN (Rede de Entrega de Conteúdo).</span><span class="sxs-lookup"><span data-stu-id="cf78e-109">For improved performance and scalability, you can also deliver content by using a Content Delivery Network (CDN).</span></span>

<span data-ttu-id="cf78e-110">Este exemplo mostra como ativos de mídia toodownload do computador local do Media Services tooyour.</span><span class="sxs-lookup"><span data-stu-id="cf78e-110">This example shows how toodownload media assets from Media Services tooyour local computer.</span></span> <span data-ttu-id="cf78e-111">consultas de código Olá Olá trabalhos associados à conta de serviços de mídia do hello, ID do trabalho e acessar seu **OutputMediaAssets** coleção (que é o conjunto de saudação de um ou mais ativos de mídia de saída que é o resultado da execução de um trabalho).</span><span class="sxs-lookup"><span data-stu-id="cf78e-111">hello code queries hello jobs associated with hello Media Services account by job ID and accesses its **OutputMediaAssets** collection (which is hello set of one or more output media assets that results from running a job).</span></span> <span data-ttu-id="cf78e-112">Este exemplo mostra como mídia de saída toodownload ativos de um trabalho, mas você podem aplicar Olá mesmo toodownload de abordagem outros ativos.</span><span class="sxs-lookup"><span data-stu-id="cf78e-112">This  example shows how toodownload output media assets from a job, but you can apply hello same approach toodownload other assets.</span></span>

>[!NOTE]
><span data-ttu-id="cf78e-113">Há um limite de 1.000.000 políticas para diferentes políticas de AMS (por exemplo, para política de Localizador ou ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="cf78e-113">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="cf78e-114">Você deve usar Olá Olá a mesma ID de política se você estiver usando sempre mesmo dias acesso permissões, por exemplo, as políticas para localizadores são tooremain desejado no local por um longo período (políticas de carregamento não).</span><span class="sxs-lookup"><span data-stu-id="cf78e-114">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="cf78e-115">Para obter mais informações, consulte [este](media-services-dotnet-manage-entities.md#limit-access-policies) tópico.</span><span class="sxs-lookup"><span data-stu-id="cf78e-115">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

    // Download hello output asset of hello specified job tooa local folder.
    static IAsset DownloadAssetToLocal( string jobId, string outputFolder)
    {
        // This method illustrates how toodownload a single asset. 
        // However, you can iterate through hello OutputAssets
        // collection, and download all assets if there are many. 

        // Get a reference toohello job. 
        IJob job = GetJob(jobId);

        // Get a reference toohello first output asset. If there were multiple 
        // output media assets you could iterate and handle each one.
        IAsset outputAsset = job.OutputMediaAssets[0];

        // Create a SAS locator toodownload hello asset
        IAccessPolicy accessPolicy = _context.AccessPolicies.Create("File Download Policy", TimeSpan.FromDays(30), AccessPermissions.Read);
        ILocator locator = _context.Locators.CreateLocator(LocatorType.Sas, outputAsset, accessPolicy);

        BlobTransferClient blobTransfer = new BlobTransferClient
        {
            NumberOfConcurrentTransfers = 20,
            ParallelTransferThreadCount = 20
        };

        var downloadTasks = new List<Task>();
        foreach (IAssetFile outputFile in outputAsset.AssetFiles)
        {
            // Use hello following event handler toocheck download progress.
            outputFile.DownloadProgressChanged += DownloadProgress;

            string localDownloadPath = Path.Combine(outputFolder, outputFile.Name);

            Console.WriteLine("File download path:  " + localDownloadPath);

            downloadTasks.Add(outputFile.DownloadAsync(Path.GetFullPath(localDownloadPath), blobTransfer, locator, CancellationToken.None));

            outputFile.DownloadProgressChanged -= DownloadProgress;
        }

        Task.WaitAll(downloadTasks.ToArray());

        return outputAsset;
    }

    static void DownloadProgress(object sender, DownloadProgressChangedEventArgs e)
    {
        Console.WriteLine(string.Format("{0} % download progress. ", e.Progress));
    }



## <a name="media-services-learning-paths"></a><span data-ttu-id="cf78e-116">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="cf78e-116">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="cf78e-117">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="cf78e-117">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="cf78e-118">Consulte também</span><span class="sxs-lookup"><span data-stu-id="cf78e-118">See Also</span></span>
[<span data-ttu-id="cf78e-119">Fornecer conteúdo de streaming</span><span class="sxs-lookup"><span data-stu-id="cf78e-119">Deliver streaming content</span></span>](media-services-deliver-streaming-content.md)

