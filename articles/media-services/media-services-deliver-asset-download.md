---
title: "Baixar ativos de Serviços de Mídia em seu computador - Azure | Microsoft Docs"
description: "Aprenda a baixar ativos para seu computador. Os exemplos de código são escritos em C# e usam a SDK dos Serviços de Mídia para .NET."
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
ms.openlocfilehash: d8e740e969f68c85842f42c109328423da1b4414
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-deliver-an-asset-by-download"></a><span data-ttu-id="9000c-104">Como fornecer um ativo por Download</span><span class="sxs-lookup"><span data-stu-id="9000c-104">How to: Deliver an Asset by Download</span></span>
<span data-ttu-id="9000c-105">Este tópico descreve as opções para entregar os ativos de mídia carregados nos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="9000c-105">This topic discusses options for delivering media assets uploaded to Media Services.</span></span> <span data-ttu-id="9000c-106">Você pode entregar conteúdo dos Serviços de Mídia em vários cenários de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="9000c-106">You can deliver Media Services content in numerous application scenarios.</span></span> <span data-ttu-id="9000c-107">Você pode baixar ativos de mídia ou acessá-los usando um localizador.</span><span class="sxs-lookup"><span data-stu-id="9000c-107">You can download media assets, or access them by using a locator.</span></span> <span data-ttu-id="9000c-108">Você pode enviar conteúdo de mídia para outro aplicativo ou para outro provedor de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="9000c-108">You can send media content to another application or to another content provider.</span></span> <span data-ttu-id="9000c-109">Para melhor desempenho e escalabilidade, você também pode fornecer conteúdo usando uma CDN (Rede de Entrega de Conteúdo).</span><span class="sxs-lookup"><span data-stu-id="9000c-109">For improved performance and scalability, you can also deliver content by using a Content Delivery Network (CDN).</span></span>

<span data-ttu-id="9000c-110">Este exemplo mostra como baixar ativos de mídia dos Serviços de Mídia no computador local.</span><span class="sxs-lookup"><span data-stu-id="9000c-110">This example shows how to download media assets from Media Services to your local computer.</span></span> <span data-ttu-id="9000c-111">O código consulta os trabalhos associados à conta dos Serviços de Mídia por ID do trabalho e acessa sua coleção **OutputMediaAssets** (que é o conjunto de um ou mais ativos de mídia de saída que resulta da execução de um trabalho).</span><span class="sxs-lookup"><span data-stu-id="9000c-111">The code queries the jobs associated with the Media Services account by job ID and accesses its **OutputMediaAssets** collection (which is the set of one or more output media assets that results from running a job).</span></span> <span data-ttu-id="9000c-112">Este exemplo mostra como baixar os ativos de mídia da saída de um trabalho, mas você pode aplicar a mesma abordagem para baixar outros ativos.</span><span class="sxs-lookup"><span data-stu-id="9000c-112">This  example shows how to download output media assets from a job, but you can apply the same approach to download other assets.</span></span>

>[!NOTE]
><span data-ttu-id="9000c-113">Há um limite de 1.000.000 políticas para diferentes políticas de AMS (por exemplo, para política de Localizador ou ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="9000c-113">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="9000c-114">Use a mesma ID de política, se você estiver sempre usando os mesmos dias/permissões de acesso, por exemplo, políticas de localizadores que devem permanecer no local por um longo período (políticas de não carregamento).</span><span class="sxs-lookup"><span data-stu-id="9000c-114">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="9000c-115">Para obter mais informações, consulte [este](media-services-dotnet-manage-entities.md#limit-access-policies) tópico.</span><span class="sxs-lookup"><span data-stu-id="9000c-115">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

    // Download the output asset of the specified job to a local folder.
    static IAsset DownloadAssetToLocal( string jobId, string outputFolder)
    {
        // This method illustrates how to download a single asset. 
        // However, you can iterate through the OutputAssets
        // collection, and download all assets if there are many. 

        // Get a reference to the job. 
        IJob job = GetJob(jobId);

        // Get a reference to the first output asset. If there were multiple 
        // output media assets you could iterate and handle each one.
        IAsset outputAsset = job.OutputMediaAssets[0];

        // Create a SAS locator to download the asset
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
            // Use the following event handler to check download progress.
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



## <a name="media-services-learning-paths"></a><span data-ttu-id="9000c-116">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="9000c-116">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9000c-117">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="9000c-117">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="9000c-118">Consulte também</span><span class="sxs-lookup"><span data-stu-id="9000c-118">See Also</span></span>
[<span data-ttu-id="9000c-119">Fornecer conteúdo de streaming</span><span class="sxs-lookup"><span data-stu-id="9000c-119">Deliver streaming content</span></span>](media-services-deliver-streaming-content.md)

