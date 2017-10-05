---
title: Como codificar um ativo do Azure usando o Media Encoder Standard | Microsoft Docs
description: "Saiba como usar o Media Encoder Standard para codificar conteúdo de mídia nos Serviços de Mídia do Azure. Exemplos de código usam a API REST."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 2a7273c6-8a22-4f82-9bfe-4509ff32d4a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 796f3b5a4dd56a0160986600cbbcf38faf8add56
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-encode-an-asset-by-using-media-encoder-standard"></a><span data-ttu-id="91d1d-104">Como codificar um ativo usando o Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="91d1d-104">How to encode an asset by using Media Encoder Standard</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="91d1d-105">.NET</span><span class="sxs-lookup"><span data-stu-id="91d1d-105">.NET</span></span>](media-services-dotnet-encode-with-media-encoder-standard.md)
> * [<span data-ttu-id="91d1d-106">REST</span><span class="sxs-lookup"><span data-stu-id="91d1d-106">REST</span></span>](media-services-rest-encode-asset.md)
> * [<span data-ttu-id="91d1d-107">Portal</span><span class="sxs-lookup"><span data-stu-id="91d1d-107">Portal</span></span>](media-services-portal-encode.md)
>
>

## <a name="overview"></a><span data-ttu-id="91d1d-108">Visão geral</span><span class="sxs-lookup"><span data-stu-id="91d1d-108">Overview</span></span>
<span data-ttu-id="91d1d-109">Para fornecer vídeo digital pela Internet, é necessário compactar a mídia.</span><span class="sxs-lookup"><span data-stu-id="91d1d-109">To deliver digital video over the Internet, you must compress the media.</span></span> <span data-ttu-id="91d1d-110">Os arquivos de vídeo digital são muito grandes e podem ser muito grandes para serem fornecidos pela Internet ou exibidos corretamente nos dispositivos dos clientes.</span><span class="sxs-lookup"><span data-stu-id="91d1d-110">Digital video files are large and may be too big to deliver over the Internet, or for your customers’ devices to display properly.</span></span> <span data-ttu-id="91d1d-111">A codificação é o processo de compactação de vídeo e áudio para que seus clientes possam exibir sua mídia.</span><span class="sxs-lookup"><span data-stu-id="91d1d-111">Encoding is the process of compressing video and audio so your customers can view your media.</span></span>

<span data-ttu-id="91d1d-112">Os trabalhos de codificação são uma das operações de processamento mais comuns nos Serviços de Mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="91d1d-112">Encoding jobs are one of the most common processing operations in Azure Media Services.</span></span> <span data-ttu-id="91d1d-113">Você cria trabalhos de codificação para converter arquivos de mídia de uma codificação para outra.</span><span class="sxs-lookup"><span data-stu-id="91d1d-113">You create encoding jobs to convert media files from one encoding to another.</span></span> <span data-ttu-id="91d1d-114">Ao codificar, é possível usar o codificador interno dos Serviços de Mídia (Codificador de Mídia Padrão).</span><span class="sxs-lookup"><span data-stu-id="91d1d-114">When you encode, you can use the Media Services built-in encoder (Media Encoder Standard).</span></span> <span data-ttu-id="91d1d-115">Você também pode usar um codificador fornecido por um parceiro dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="91d1d-115">You can also use an encoder provided by a Media Services partner.</span></span> <span data-ttu-id="91d1d-116">Codificadores de terceiros estão disponíveis por meio do Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="91d1d-116">Third-party encoders are available through the Azure Marketplace.</span></span> <span data-ttu-id="91d1d-117">Você pode especificar os detalhes das tarefas de codificação usando cadeias de caracteres predefinidas para seu codificador ou usando arquivos de configuração predefinidos.</span><span class="sxs-lookup"><span data-stu-id="91d1d-117">You can specify the details of encoding tasks by using preset strings defined for your encoder, or by using preset configuration files.</span></span> <span data-ttu-id="91d1d-118">Para ver os tipos de predefinições disponíveis, confira [Predefinições de tarefa para o Media Encoder Standard](http://msdn.microsoft.com/library/mt269960).</span><span class="sxs-lookup"><span data-stu-id="91d1d-118">To see the types of presets that are available, see [Task Presets for Media Encoder Standard](http://msdn.microsoft.com/library/mt269960).</span></span>

<span data-ttu-id="91d1d-119">Cada trabalho pode ter uma ou mais tarefas, dependendo do tipo de processamento que você deseja realizar.</span><span class="sxs-lookup"><span data-stu-id="91d1d-119">Each job can have one or more tasks depending on the type of processing that you want to accomplish.</span></span> <span data-ttu-id="91d1d-120">Por meio da API REST, é possível criar trabalhos e as tarefas relacionadas de uma destas duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="91d1d-120">Through the REST API, you can create jobs and their related tasks in one of two ways:</span></span>

* <span data-ttu-id="91d1d-121">As tarefas podem ser definidas de forma embutida por meio da propriedade de navegação das Tarefas nas entidades de Trabalho.</span><span class="sxs-lookup"><span data-stu-id="91d1d-121">Tasks can be defined inline through the Tasks navigation property on Job entities.</span></span>
* <span data-ttu-id="91d1d-122">Use o processamento em lotes OData.</span><span class="sxs-lookup"><span data-stu-id="91d1d-122">Use OData batch processing.</span></span>

<span data-ttu-id="91d1d-123">Recomendamos sempre codificar os arquivos de origem em um conjunto de MP4 de taxa de bits adaptável e, em seguida, converter o conjunto no formato desejado usando o [empacotamento dinâmico](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="91d1d-123">We recommend that you always encode your source files into an adaptive bitrate MP4 set, and then convert the set to the desired format by using [dynamic packaging](media-services-dynamic-packaging-overview.md).</span></span>

<span data-ttu-id="91d1d-124">Se o ativo de saída tiver o armazenamento criptografado, você deverá configurar a política de entrega de ativos.</span><span class="sxs-lookup"><span data-stu-id="91d1d-124">If your output asset is storage encrypted, you must configure the asset delivery policy.</span></span> <span data-ttu-id="91d1d-125">Para obter mais informações, consulte [Configurando a política de entrega de ativos](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="91d1d-125">For more information, see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <a name="considerations"></a><span data-ttu-id="91d1d-126">Considerações</span><span class="sxs-lookup"><span data-stu-id="91d1d-126">Considerations</span></span>

<span data-ttu-id="91d1d-127">Ao acessar entidades nos serviços de mídia, você deve definir valores e campos de cabeçalho específicos nas suas solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="91d1d-127">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="91d1d-128">Para obter mais informações, consulte [Configuração para desenvolvimento da API REST dos Serviços de Mídia](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="91d1d-128">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

<span data-ttu-id="91d1d-129">Antes de começar a fazer referência a processadores de mídia, verifique se você tem a ID do processador de mídia correta.</span><span class="sxs-lookup"><span data-stu-id="91d1d-129">Before you start referencing media processors, verify that you have the correct media processor ID.</span></span> <span data-ttu-id="91d1d-130">Para obter mais informações, consulte [Obter processadores de mídia](media-services-rest-get-media-processor.md).</span><span class="sxs-lookup"><span data-stu-id="91d1d-130">For more information, see [Get media processors](media-services-rest-get-media-processor.md).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="91d1d-131">Conectar-se aos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="91d1d-131">Connect to Media Services</span></span>

<span data-ttu-id="91d1d-132">Para saber mais sobre como conectar-se à API do AMS, veja [Acessar a API dos Serviços de Mídia do Azure com a autenticação do Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="91d1d-132">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="91d1d-133">Depois de se conectar com êxito em https://media.windows.net, você receberá um redirecionamento 301 especificando outro URI dos serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="91d1d-133">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="91d1d-134">Você deve fazer chamadas subsequentes para o novo URI.</span><span class="sxs-lookup"><span data-stu-id="91d1d-134">You must make subsequent calls to the new URI.</span></span>

## <a name="create-a-job-with-a-single-encoding-task"></a><span data-ttu-id="91d1d-135">Criar um trabalho com uma única tarefa de codificação</span><span class="sxs-lookup"><span data-stu-id="91d1d-135">Create a job with a single encoding task</span></span>
> [!NOTE]
> <span data-ttu-id="91d1d-136">Ao trabalhar com a API REST dos Serviços de Mídia, as seguintes considerações se aplicam:</span><span class="sxs-lookup"><span data-stu-id="91d1d-136">When you're working with the Media Services REST API, the following considerations apply:</span></span>
>
> <span data-ttu-id="91d1d-137">Ao acessar entidades nos serviços de mídia, você deve definir valores e campos de cabeçalho específicos nas suas solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="91d1d-137">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="91d1d-138">Para obter mais informações, consulte [Configuração para desenvolvimento da API REST dos Serviços de Mídia](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="91d1d-138">For more information, see [Setup for Media Services REST API development](media-services-rest-how-to-use.md).</span></span>
>
> <span data-ttu-id="91d1d-139">Depois de se conectar com êxito em https://media.windows.net, você receberá um redirecionamento 301 especificando outro URI dos serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="91d1d-139">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="91d1d-140">Você deve fazer chamadas subsequentes para o novo URI.</span><span class="sxs-lookup"><span data-stu-id="91d1d-140">You must make subsequent calls to the new URI.</span></span> <span data-ttu-id="91d1d-141">Para saber mais sobre como conectar-se à API do AMS, veja [Acessar a API dos Serviços de Mídia do Azure com a autenticação do Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="91d1d-141">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
>
> <span data-ttu-id="91d1d-142">Ao usar o JSON e especificar o uso da palavra-chave **__metadata** na solicitação (por exemplo, para referenciar um objeto vinculado), é necessário definir o cabeçalho **Accept** como [formato JSON Detalhado](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): Accept: application/json;odata=verbose.</span><span class="sxs-lookup"><span data-stu-id="91d1d-142">When using JSON and specifying to use the **__metadata** keyword in the request (for example, to references a linked object), you must set the **Accept** header to [JSON Verbose format](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): Accept: application/json;odata=verbose.</span></span>
>
>

<span data-ttu-id="91d1d-143">O exemplo a seguir mostra como criar e postar um trabalho com uma tarefa definida para codificar um vídeo em uma resolução e qualidade específicas.</span><span class="sxs-lookup"><span data-stu-id="91d1d-143">The following example shows you how to create and post a job with one task set to encode a video at a specific resolution and quality.</span></span> <span data-ttu-id="91d1d-144">Quando estiver codificando com o Media Encoder Standard, você poderá usar as predefinições de configuração de tarefa especificadas [aqui](http://msdn.microsoft.com/library/mt269960).</span><span class="sxs-lookup"><span data-stu-id="91d1d-144">When you encode with Media Encoder Standard, you can use task configuration presets specified [here](http://msdn.microsoft.com/library/mt269960).</span></span>

<span data-ttu-id="91d1d-145">Solicitação:</span><span class="sxs-lookup"><span data-stu-id="91d1d-145">Request:</span></span>

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
    Host: media.windows.net

    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Aaab7f15b-3136-4ddf-9962-e9ecb28fb9d2')"}}],  "Tasks" : [{"Configuration" : "Adaptive Streaming", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",  "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"}]}

<span data-ttu-id="91d1d-146">Resposta:</span><span class="sxs-lookup"><span data-stu-id="91d1d-146">Response:</span></span>

    HTTP/1.1 201 Created

    . . .

### <a name="set-the-output-assets-name"></a><span data-ttu-id="91d1d-147">Definir nome do ativo de saída</span><span class="sxs-lookup"><span data-stu-id="91d1d-147">Set the output asset's name</span></span>
<span data-ttu-id="91d1d-148">O exemplo a seguir mostra como definir o atributo assetName:</span><span class="sxs-lookup"><span data-stu-id="91d1d-148">The following example shows how to set the assetName attribute:</span></span>

    { "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"}

## <a name="considerations"></a><span data-ttu-id="91d1d-149">Considerações</span><span class="sxs-lookup"><span data-stu-id="91d1d-149">Considerations</span></span>
* <span data-ttu-id="91d1d-150">As propriedades TaskBody devem usar o XML literal para definir o número de entradas ou os ativos de saída que são usados pela tarefa.</span><span class="sxs-lookup"><span data-stu-id="91d1d-150">TaskBody properties must use literal XML to define the number of input, or output assets that are used by the task.</span></span> <span data-ttu-id="91d1d-151">O tópico da tarefa contém a Definição de Esquema XML para o XML.</span><span class="sxs-lookup"><span data-stu-id="91d1d-151">The task topic contains the XML Schema Definition for the XML.</span></span>
* <span data-ttu-id="91d1d-152">Na definição de TaskBody, cada valor interno para <inputAsset> e <outputAsset> deve ser definido como JobInputAsset(value) ou JobOutputAsset(value).</span><span class="sxs-lookup"><span data-stu-id="91d1d-152">In the TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span></span>
* <span data-ttu-id="91d1d-153">Uma tarefa pode ter vários ativos de saída.</span><span class="sxs-lookup"><span data-stu-id="91d1d-153">A task can have multiple output assets.</span></span> <span data-ttu-id="91d1d-154">Um JobOutputAsset(x) só pode ser usado uma vez como uma saída de uma tarefa em um trabalho.</span><span class="sxs-lookup"><span data-stu-id="91d1d-154">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span></span>
* <span data-ttu-id="91d1d-155">Você pode especificar JobInputAsset ou JobOutputAsset como um ativo de entrada de uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="91d1d-155">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span></span>
* <span data-ttu-id="91d1d-156">As tarefas não devem formar um ciclo.</span><span class="sxs-lookup"><span data-stu-id="91d1d-156">Tasks must not form a cycle.</span></span>
* <span data-ttu-id="91d1d-157">O parâmetro de valor passado para JobInputAsset ou JobOutputAsset representa o valor de índice de um ativo.</span><span class="sxs-lookup"><span data-stu-id="91d1d-157">The value parameter that you pass to JobInputAsset or JobOutputAsset represents the index value for an asset.</span></span> <span data-ttu-id="91d1d-158">Os ativos reais são definidos nas propriedades de navegação InputMediaAssets e OutputMediaAssets na definição de entidade do trabalho.</span><span class="sxs-lookup"><span data-stu-id="91d1d-158">The actual assets are defined in the InputMediaAssets and OutputMediaAssets navigation properties on the job entity definition.</span></span>
* <span data-ttu-id="91d1d-159">Como os Serviços de Mídia se baseiam no OData v3, os ativos individuais nas coleções de propriedades de navegação InputMediaAssets e OutputMediaAssets são referenciados por meio de um par nome-valor “__metadata : uri”.</span><span class="sxs-lookup"><span data-stu-id="91d1d-159">Because Media Services is built on OData v3, the individual assets in the InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span></span>
* <span data-ttu-id="91d1d-160">InputMediaAssets são mapeados para um ou mais ativos criados nos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="91d1d-160">InputMediaAssets maps to one or more assets that you created in Media Services.</span></span> <span data-ttu-id="91d1d-161">Os OutputMediaAssets são criados pelo sistema.</span><span class="sxs-lookup"><span data-stu-id="91d1d-161">OutputMediaAssets are created by the system.</span></span> <span data-ttu-id="91d1d-162">Eles não referenciam um ativo existente.</span><span class="sxs-lookup"><span data-stu-id="91d1d-162">They don't reference an existing asset.</span></span>
* <span data-ttu-id="91d1d-163">OutputMediaAssets podem ser nomeados usando o atributo assetName.</span><span class="sxs-lookup"><span data-stu-id="91d1d-163">OutputMediaAssets can be named by using the assetName attribute.</span></span> <span data-ttu-id="91d1d-164">Se esse atributo não estiver presente, então o nome do OutputMediaAsset será tudo o que é o valor de texto interno do elemento <outputAsset> com um sufixo do valor do nome do trabalho ou o valor da ID de trabalho (no caso em que a propriedade Nome não esteja definida).</span><span class="sxs-lookup"><span data-stu-id="91d1d-164">If this attribute is not present, then the name of the OutputMediaAsset is whatever the inner text value of the <outputAsset> element is with a suffix of either the Job Name value, or the Job Id value (in the case where the Name property isn't defined).</span></span> <span data-ttu-id="91d1d-165">Por exemplo, se você definir um valor para assetName como “Sample”, a propriedade Name de OutputMediaAsset deverá ser definida como “Sample”.</span><span class="sxs-lookup"><span data-stu-id="91d1d-165">For example, if you set a value for assetName to "Sample," then the OutputMediaAsset Name property is set to "Sample."</span></span> <span data-ttu-id="91d1d-166">No entanto, se você não definiu um valor para assetName, mas definiu o nome do trabalho como “NewJob”, o Nome do OutputMediaAsset poderá ser “JobOutputAsset(value)_NewJob”.</span><span class="sxs-lookup"><span data-stu-id="91d1d-166">However, if you didn't set a value for assetName, but did set the job name to "NewJob," then the OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob."</span></span>

## <a name="create-a-job-with-chained-tasks"></a><span data-ttu-id="91d1d-167">Criar um trabalho com tarefas encadeadas</span><span class="sxs-lookup"><span data-stu-id="91d1d-167">Create a job with chained tasks</span></span>
<span data-ttu-id="91d1d-168">Em muitos cenários de aplicativo, os desenvolvedores querem criar uma série de tarefas de processamento.</span><span class="sxs-lookup"><span data-stu-id="91d1d-168">In many application scenarios, developers want to create a series of processing tasks.</span></span> <span data-ttu-id="91d1d-169">Nos serviços de mídia, você pode criar uma série de tarefas encadeadas.</span><span class="sxs-lookup"><span data-stu-id="91d1d-169">In Media Services, you can create a series of chained tasks.</span></span> <span data-ttu-id="91d1d-170">Cada tarefa executa etapas de processamento diferentes e pode usar diferentes processadores de mídia.</span><span class="sxs-lookup"><span data-stu-id="91d1d-170">Each task performs different processing steps and can use different media processors.</span></span> <span data-ttu-id="91d1d-171">As tarefas encadeadas podem entregar um ativo de uma tarefa para outra, desempenhando uma sequência linear de tarefas no ativo.</span><span class="sxs-lookup"><span data-stu-id="91d1d-171">The chained tasks can hand off an asset from one task to another, performing a linear sequence of tasks on the asset.</span></span> <span data-ttu-id="91d1d-172">No entanto, as tarefas executadas em um trabalho não precisam estar em uma sequência.</span><span class="sxs-lookup"><span data-stu-id="91d1d-172">However, the tasks performed in a job are not required to be in a sequence.</span></span> <span data-ttu-id="91d1d-173">Quando você cria uma tarefa encadeada, os objetos **ITask** são criados em um único objeto **IJob**.</span><span class="sxs-lookup"><span data-stu-id="91d1d-173">When you create a chained task, the chained **ITask** objects are created in a single **IJob** object.</span></span>

> [!NOTE]
> <span data-ttu-id="91d1d-174">Atualmente, há um limite de 30 tarefas por trabalho.</span><span class="sxs-lookup"><span data-stu-id="91d1d-174">There is currently a limit of 30 tasks per job.</span></span> <span data-ttu-id="91d1d-175">Se você precisa encadear mais de 30 tarefas, crie mais de um trabalho para conter as tarefas.</span><span class="sxs-lookup"><span data-stu-id="91d1d-175">If you need to chain more than 30 tasks, create more than one job to contain the tasks.</span></span>
>
>

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Name":"NewTestJob",
       "InputMediaAssets":[  
          {  
             "__metadata":{  
                "uri":"https://testrest.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A910ffdc1-2e25-4b17-8a42-61ffd4b8914c')"
             }
          }
       ],
       "Tasks":[  
          {  
             "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"
          },
          {  
             "Configuration":"H264 Smooth Streaming 720p",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-16\"?><taskBody><inputAsset>JobOutputAsset(0)</inputAsset><outputAsset>JobOutputAsset(1)</outputAsset></taskBody>"
          }
       ]
    }


### <a name="considerations"></a><span data-ttu-id="91d1d-176">Considerações</span><span class="sxs-lookup"><span data-stu-id="91d1d-176">Considerations</span></span>
<span data-ttu-id="91d1d-177">Para habilitar o encadeamento de tarefas:</span><span class="sxs-lookup"><span data-stu-id="91d1d-177">To enable task chaining:</span></span>

* <span data-ttu-id="91d1d-178">Um trabalho deve ter, pelo menos, duas tarefas.</span><span class="sxs-lookup"><span data-stu-id="91d1d-178">A job must have at least two tasks.</span></span>
* <span data-ttu-id="91d1d-179">Deve haver, pelo menos, uma tarefa cuja entrada é a saída de outra tarefa no trabalho.</span><span class="sxs-lookup"><span data-stu-id="91d1d-179">There must be at least one task whose input is the output of another task in the job.</span></span>

## <a name="use-odata-batch-processing"></a><span data-ttu-id="91d1d-180">Usar o processamento em lotes OData</span><span class="sxs-lookup"><span data-stu-id="91d1d-180">Use OData batch processing</span></span>
<span data-ttu-id="91d1d-181">O exemplo a seguir mostra como usar o processamento em lotes OData para criar um trabalho e tarefas.</span><span class="sxs-lookup"><span data-stu-id="91d1d-181">The following example shows how to use OData batch processing to create a job and tasks.</span></span> <span data-ttu-id="91d1d-182">Para obter informações sobre o processamento em lotes, consulte [Processamento em lote do protocolo OData (Open Data)](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span><span class="sxs-lookup"><span data-stu-id="91d1d-182">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span></span>

    POST https://media.windows.net/api/$batch HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Content-Type: multipart/mixed; boundary=batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Accept: multipart/mixed
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
    Host: media.windows.net


    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Content-Type: multipart/mixed; boundary=changeset_122fb0a4-cd80-4958-820f-346309967e4d

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d
    Content-Type: application/http
    Content-Transfer-Encoding: binary

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-ID: 1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {"Name" : "NewTestJob", "InputMediaAssets@odata.bind":["https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A2a22445d-1500-80c6-4b34-f1e5190d33c6')"]}

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d
    Content-Type: application/http
    Content-Transfer-Encoding: binary

    POST https://media.windows.net/api/$1/Tasks HTTP/1.1
    Content-ID: 2
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
       "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
       "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"Custom output name\">JobOutputAsset(0)</outputAsset></taskBody>"
    }

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d--
    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e--



## <a name="create-a-job-by-using-a-jobtemplate"></a><span data-ttu-id="91d1d-183">Criar um trabalho usando um JobTemplate</span><span class="sxs-lookup"><span data-stu-id="91d1d-183">Create a job by using a JobTemplate</span></span>
<span data-ttu-id="91d1d-184">Ao processar vários ativos usando um conjunto comum de tarefas, use um JobTemplate para especificar as predefinições de tarefa padrão ou para definir a ordem das tarefas.</span><span class="sxs-lookup"><span data-stu-id="91d1d-184">When you process multiple assets by using a common set of tasks, use a JobTemplate to specify the default task presets, or to set the order of tasks.</span></span>

<span data-ttu-id="91d1d-185">O exemplo a seguir mostra como criar um JobTemplate com um TaskTemplate definido de forma embutida.</span><span class="sxs-lookup"><span data-stu-id="91d1d-185">The following example shows how to create a JobTemplate with a TaskTemplate that is defined inline.</span></span> <span data-ttu-id="91d1d-186">O TaskTemplate usa o Media Encoder Standard como o MediaProcessor para codificar o arquivo de ativo.</span><span class="sxs-lookup"><span data-stu-id="91d1d-186">The TaskTemplate uses the Media Encoder Standard as the MediaProcessor to encode the asset file.</span></span> <span data-ttu-id="91d1d-187">No entanto, outros MediaProcessors também podem ser usados.</span><span class="sxs-lookup"><span data-stu-id="91d1d-187">However, other MediaProcessors can be used as well.</span></span>

    POST https://media.windows.net/API/JobTemplates HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewJobTemplate25", "JobTemplateBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><jobTemplate><taskBody taskTemplateId=\"nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789\"><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody></jobTemplate>", "TaskTemplates" : [{"Id" : "nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789", "Configuration" : "H264 Smooth Streaming 720p", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56", "Name" : "SampleTaskTemplate2", "NumberofInputAssets" : 1, "NumberofOutputAssets" : 1}] }


> [!NOTE]
> <span data-ttu-id="91d1d-188">Ao contrário de outras entidades de Serviços de Mídia, você deve definir um novo identificador GUID para cada TaskTemplate e colocá-lo na propriedade taskTemplateId e na propriedade ID no corpo da solicitação.</span><span class="sxs-lookup"><span data-stu-id="91d1d-188">Unlike other Media Services entities, you must define a new GUID identifier for each TaskTemplate and place it in the taskTemplateId and Id property in your request body.</span></span> <span data-ttu-id="91d1d-189">O esquema de identificação de conteúdo deve seguir o esquema descrito em Identificar Entidades de Serviços de Mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="91d1d-189">The content identification scheme must follow the scheme described in Identify Azure Media Services Entities.</span></span> <span data-ttu-id="91d1d-190">Além disso, os JobTemplates não podem ser atualizados.</span><span class="sxs-lookup"><span data-stu-id="91d1d-190">Also, JobTemplates cannot be updated.</span></span> <span data-ttu-id="91d1d-191">Em vez disso, você deve criar um novo com as suas alterações atualizadas.</span><span class="sxs-lookup"><span data-stu-id="91d1d-191">Instead, you must create a new one with your updated changes.</span></span>
>
>

<span data-ttu-id="91d1d-192">Se for bem-sucedido, será retornada a seguinte resposta:</span><span class="sxs-lookup"><span data-stu-id="91d1d-192">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created

    . . .


<span data-ttu-id="91d1d-193">O seguinte exemplo mostra como criar um trabalho que referencia uma ID de JobTemplate:</span><span class="sxs-lookup"><span data-stu-id="91d1d-193">The following example shows how to create a job that references a JobTemplate Id:</span></span>

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A3f1fe4a2-68f5-4190-9557-cd45beccef92')"}}], "TemplateId" : "nb:jtid:UUID:15e6e5e6-ac85-084e-9dc2-db3645fbf0aa"}


<span data-ttu-id="91d1d-194">Se for bem-sucedido, será retornada a seguinte resposta:</span><span class="sxs-lookup"><span data-stu-id="91d1d-194">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created

    . . .



## <a name="media-services-learning-paths"></a><span data-ttu-id="91d1d-195">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="91d1d-195">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="91d1d-196">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="91d1d-196">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="91d1d-197">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="91d1d-197">Next steps</span></span>
<span data-ttu-id="91d1d-198">Agora que você sabe como criar um trabalho para codificar um ativo, consulte [Como verificar o andamento do trabalho com os Serviços de Mídia](media-services-rest-check-job-progress.md).</span><span class="sxs-lookup"><span data-stu-id="91d1d-198">Now that you know how to create a job to encode an asset, see [How to check job progress with Media Services](media-services-rest-check-job-progress.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="91d1d-199">Consulte também</span><span class="sxs-lookup"><span data-stu-id="91d1d-199">See also</span></span>
[<span data-ttu-id="91d1d-200">Obter processadores de mídia</span><span class="sxs-lookup"><span data-stu-id="91d1d-200">Get Media Processors</span></span>](media-services-rest-get-media-processor.md)
