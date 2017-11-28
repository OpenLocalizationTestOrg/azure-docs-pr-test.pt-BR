---
title: "aaaHow tooencode um ativo do Azure usando o codificador de mídia padrão | Microsoft Docs"
description: "Saiba como toouse codificador de mídia padrão tooencode mídia de conteúdo nos serviços de mídia do Azure. Exemplos de código usam a API REST."
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
ms.openlocfilehash: b766bafded7ee98eda3e6ef149c31d5d8fe406fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencode-an-asset-by-using-media-encoder-standard"></a><span data-ttu-id="8755d-104">Como tooencode um ativo usando o codificador de mídia padrão</span><span class="sxs-lookup"><span data-stu-id="8755d-104">How tooencode an asset by using Media Encoder Standard</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8755d-105">.NET</span><span class="sxs-lookup"><span data-stu-id="8755d-105">.NET</span></span>](media-services-dotnet-encode-with-media-encoder-standard.md)
> * [<span data-ttu-id="8755d-106">REST</span><span class="sxs-lookup"><span data-stu-id="8755d-106">REST</span></span>](media-services-rest-encode-asset.md)
> * [<span data-ttu-id="8755d-107">Portal</span><span class="sxs-lookup"><span data-stu-id="8755d-107">Portal</span></span>](media-services-portal-encode.md)
>
>

## <a name="overview"></a><span data-ttu-id="8755d-108">Visão geral</span><span class="sxs-lookup"><span data-stu-id="8755d-108">Overview</span></span>
<span data-ttu-id="8755d-109">toodeliver vídeo digital pela Olá da Internet, você deve compactar mídia hello.</span><span class="sxs-lookup"><span data-stu-id="8755d-109">toodeliver digital video over hello Internet, you must compress hello media.</span></span> <span data-ttu-id="8755d-110">Arquivos de vídeo digital são grandes e podem ser muito grande toodeliver via Olá da Internet, ou para toodisplay de dispositivos de seus clientes corretamente.</span><span class="sxs-lookup"><span data-stu-id="8755d-110">Digital video files are large and may be too big toodeliver over hello Internet, or for your customers’ devices toodisplay properly.</span></span> <span data-ttu-id="8755d-111">Codificação é o processo de saudação de compactação de vídeo e áudio para que os clientes possam exibir sua mídia.</span><span class="sxs-lookup"><span data-stu-id="8755d-111">Encoding is hello process of compressing video and audio so your customers can view your media.</span></span>

<span data-ttu-id="8755d-112">Trabalhos de codificação são uma das operações de processamento mais comuns Olá nos serviços de mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="8755d-112">Encoding jobs are one of hello most common processing operations in Azure Media Services.</span></span> <span data-ttu-id="8755d-113">Criar arquivos de mídia de tooconvert trabalhos codificação de um tooanother de codificação.</span><span class="sxs-lookup"><span data-stu-id="8755d-113">You create encoding jobs tooconvert media files from one encoding tooanother.</span></span> <span data-ttu-id="8755d-114">Ao codificar, você pode usar o codificador interno de serviços de mídia de saudação (padrão de codificador de mídia).</span><span class="sxs-lookup"><span data-stu-id="8755d-114">When you encode, you can use hello Media Services built-in encoder (Media Encoder Standard).</span></span> <span data-ttu-id="8755d-115">Você também pode usar um codificador fornecido por um parceiro dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="8755d-115">You can also use an encoder provided by a Media Services partner.</span></span> <span data-ttu-id="8755d-116">Codificadores de terceiros estão disponíveis por meio de saudação do Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="8755d-116">Third-party encoders are available through hello Azure Marketplace.</span></span> <span data-ttu-id="8755d-117">Você pode especificar os detalhes de saudação de trabalhos de codificação usando cadeias de caracteres predefinidas para o seu codificador ou usando arquivos de configuração predefinidos.</span><span class="sxs-lookup"><span data-stu-id="8755d-117">You can specify hello details of encoding tasks by using preset strings defined for your encoder, or by using preset configuration files.</span></span> <span data-ttu-id="8755d-118">toosee Olá tipos de predefinições disponíveis, consulte [predefinições de tarefa para o codificador de mídia padrão](http://msdn.microsoft.com/library/mt269960).</span><span class="sxs-lookup"><span data-stu-id="8755d-118">toosee hello types of presets that are available, see [Task Presets for Media Encoder Standard](http://msdn.microsoft.com/library/mt269960).</span></span>

<span data-ttu-id="8755d-119">Cada trabalho pode ter um ou mais tarefas dependendo do tipo de saudação de processamento que você deseja tooaccomplish.</span><span class="sxs-lookup"><span data-stu-id="8755d-119">Each job can have one or more tasks depending on hello type of processing that you want tooaccomplish.</span></span> <span data-ttu-id="8755d-120">Por meio de Olá API REST, você pode criar trabalhos e as tarefas relacionadas em uma das duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="8755d-120">Through hello REST API, you can create jobs and their related tasks in one of two ways:</span></span>

* <span data-ttu-id="8755d-121">Tarefas podem ser definidas embutidas por meio da propriedade de navegação Olá tarefas nas entidades de trabalho.</span><span class="sxs-lookup"><span data-stu-id="8755d-121">Tasks can be defined inline through hello Tasks navigation property on Job entities.</span></span>
* <span data-ttu-id="8755d-122">Use o processamento em lotes OData.</span><span class="sxs-lookup"><span data-stu-id="8755d-122">Use OData batch processing.</span></span>

<span data-ttu-id="8755d-123">É recomendável que você sempre codifica arquivos de origem em uma conjunto de MP4 de taxa de bits adaptável e, em seguida, converte o formato desejado do hello conjunto toohello usando [empacotamento dinâmico](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8755d-123">We recommend that you always encode your source files into an adaptive bitrate MP4 set, and then convert hello set toohello desired format by using [dynamic packaging](media-services-dynamic-packaging-overview.md).</span></span>

<span data-ttu-id="8755d-124">Se seu ativo de saída é armazenamento criptografado, você deve configurar política de entrega de ativos de saudação.</span><span class="sxs-lookup"><span data-stu-id="8755d-124">If your output asset is storage encrypted, you must configure hello asset delivery policy.</span></span> <span data-ttu-id="8755d-125">Para obter mais informações, consulte [Configurando a política de entrega de ativos](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="8755d-125">For more information, see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <a name="considerations"></a><span data-ttu-id="8755d-126">Considerações</span><span class="sxs-lookup"><span data-stu-id="8755d-126">Considerations</span></span>

<span data-ttu-id="8755d-127">Ao acessar entidades nos serviços de mídia, você deve definir valores e campos de cabeçalho específicos nas suas solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="8755d-127">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="8755d-128">Para obter mais informações, consulte [Configuração para desenvolvimento da API REST dos Serviços de Mídia](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="8755d-128">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

<span data-ttu-id="8755d-129">Antes de começar a fazer referência a processadores de mídia, verifique se que você tenha Olá ID de processador de mídia correta.</span><span class="sxs-lookup"><span data-stu-id="8755d-129">Before you start referencing media processors, verify that you have hello correct media processor ID.</span></span> <span data-ttu-id="8755d-130">Para obter mais informações, consulte [Obter processadores de mídia](media-services-rest-get-media-processor.md).</span><span class="sxs-lookup"><span data-stu-id="8755d-130">For more information, see [Get media processors](media-services-rest-get-media-processor.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="8755d-131">Conectar os serviços de tooMedia</span><span class="sxs-lookup"><span data-stu-id="8755d-131">Connect tooMedia Services</span></span>

<span data-ttu-id="8755d-132">Para obter informações sobre como tooconnect toohello AMS API, consulte [Olá acesso API de serviços de mídia do Azure com a autenticação do AD do Azure](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="8755d-132">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="8755d-133">Após conectar-se toohttps://media.windows.net, você receberá um redirecionamento 301 que especifica outro URI dos serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="8755d-133">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="8755d-134">Você deve fazer chamadas subsequentes toohello novo URI.</span><span class="sxs-lookup"><span data-stu-id="8755d-134">You must make subsequent calls toohello new URI.</span></span>

## <a name="create-a-job-with-a-single-encoding-task"></a><span data-ttu-id="8755d-135">Criar um trabalho com uma única tarefa de codificação</span><span class="sxs-lookup"><span data-stu-id="8755d-135">Create a job with a single encoding task</span></span>
> [!NOTE]
> <span data-ttu-id="8755d-136">Quando você está trabalhando com hello API de REST de serviços de mídia, hello seguintes considerações se aplicam:</span><span class="sxs-lookup"><span data-stu-id="8755d-136">When you're working with hello Media Services REST API, hello following considerations apply:</span></span>
>
> <span data-ttu-id="8755d-137">Ao acessar entidades nos serviços de mídia, você deve definir valores e campos de cabeçalho específicos nas suas solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="8755d-137">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="8755d-138">Para obter mais informações, consulte [Configuração para desenvolvimento da API REST dos Serviços de Mídia](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="8755d-138">For more information, see [Setup for Media Services REST API development](media-services-rest-how-to-use.md).</span></span>
>
> <span data-ttu-id="8755d-139">Após conectar-se toohttps://media.windows.net, você receberá um redirecionamento 301 que especifica outro URI dos serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="8755d-139">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="8755d-140">Você deve fazer chamadas subsequentes toohello novo URI.</span><span class="sxs-lookup"><span data-stu-id="8755d-140">You must make subsequent calls toohello new URI.</span></span> <span data-ttu-id="8755d-141">Para obter informações sobre como tooconnect toohello AMS API, consulte [Olá acesso API de serviços de mídia do Azure com a autenticação do AD do Azure](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="8755d-141">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
>
> <span data-ttu-id="8755d-142">Quando usando JSON e especificando Olá toouse **Metadata** palavra-chave na solicitação de saudação (por exemplo, tooreferences um objeto vinculado), você deve definir Olá **aceitar** cabeçalho muito[formato JSON detalhado ](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): Aceitar: application/json; odata = verbose.</span><span class="sxs-lookup"><span data-stu-id="8755d-142">When using JSON and specifying toouse hello **__metadata** keyword in hello request (for example, tooreferences a linked object), you must set hello **Accept** header too[JSON Verbose format](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): Accept: application/json;odata=verbose.</span></span>
>
>

<span data-ttu-id="8755d-143">saudação de exemplo a seguir mostra como toocreate e lançar um trabalho com uma tarefa definir tooencode um vídeo em uma resolução e qualidade específicas.</span><span class="sxs-lookup"><span data-stu-id="8755d-143">hello following example shows you how toocreate and post a job with one task set tooencode a video at a specific resolution and quality.</span></span> <span data-ttu-id="8755d-144">Quando estiver codificando com o Media Encoder Standard, você poderá usar as predefinições de configuração de tarefa especificadas [aqui](http://msdn.microsoft.com/library/mt269960).</span><span class="sxs-lookup"><span data-stu-id="8755d-144">When you encode with Media Encoder Standard, you can use task configuration presets specified [here](http://msdn.microsoft.com/library/mt269960).</span></span>

<span data-ttu-id="8755d-145">Solicitação:</span><span class="sxs-lookup"><span data-stu-id="8755d-145">Request:</span></span>

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

<span data-ttu-id="8755d-146">Resposta:</span><span class="sxs-lookup"><span data-stu-id="8755d-146">Response:</span></span>

    HTTP/1.1 201 Created

    . . .

### <a name="set-hello-output-assets-name"></a><span data-ttu-id="8755d-147">Definir nome do ativo de saída Olá</span><span class="sxs-lookup"><span data-stu-id="8755d-147">Set hello output asset's name</span></span>
<span data-ttu-id="8755d-148">saudação de exemplo a seguir mostra como tooset Olá atributo assetName:</span><span class="sxs-lookup"><span data-stu-id="8755d-148">hello following example shows how tooset hello assetName attribute:</span></span>

    { "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"}

## <a name="considerations"></a><span data-ttu-id="8755d-149">Considerações</span><span class="sxs-lookup"><span data-stu-id="8755d-149">Considerations</span></span>
* <span data-ttu-id="8755d-150">Propriedades TaskBody devem usar o número do literal XML toodefine Olá de entrada ou ativos de saída que são usados pela tarefa de saudação.</span><span class="sxs-lookup"><span data-stu-id="8755d-150">TaskBody properties must use literal XML toodefine hello number of input, or output assets that are used by hello task.</span></span> <span data-ttu-id="8755d-151">tópico de tarefa Olá contém hello definição de esquema XML para Olá XML.</span><span class="sxs-lookup"><span data-stu-id="8755d-151">hello task topic contains hello XML Schema Definition for hello XML.</span></span>
* <span data-ttu-id="8755d-152">Olá definição de TaskBody, valor da cada interna de <inputAsset> e <outputAsset> deve ser definido como JobInputAsset(value) ou JobOutputAsset(value).</span><span class="sxs-lookup"><span data-stu-id="8755d-152">In hello TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span></span>
* <span data-ttu-id="8755d-153">Uma tarefa pode ter vários ativos de saída.</span><span class="sxs-lookup"><span data-stu-id="8755d-153">A task can have multiple output assets.</span></span> <span data-ttu-id="8755d-154">Um JobOutputAsset(x) só pode ser usado uma vez como uma saída de uma tarefa em um trabalho.</span><span class="sxs-lookup"><span data-stu-id="8755d-154">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span></span>
* <span data-ttu-id="8755d-155">Você pode especificar JobInputAsset ou JobOutputAsset como um ativo de entrada de uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="8755d-155">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span></span>
* <span data-ttu-id="8755d-156">As tarefas não devem formar um ciclo.</span><span class="sxs-lookup"><span data-stu-id="8755d-156">Tasks must not form a cycle.</span></span>
* <span data-ttu-id="8755d-157">parâmetro de valor Hello que você passe tooJobInputAsset ou JobOutputAsset representa o valor de índice de saudação para um ativo.</span><span class="sxs-lookup"><span data-stu-id="8755d-157">hello value parameter that you pass tooJobInputAsset or JobOutputAsset represents hello index value for an asset.</span></span> <span data-ttu-id="8755d-158">ativos reais Olá são definidos em hello InputMediaAssets e OutputMediaAssets propriedades de navegação na definição de entidade de trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="8755d-158">hello actual assets are defined in hello InputMediaAssets and OutputMediaAssets navigation properties on hello job entity definition.</span></span>
* <span data-ttu-id="8755d-159">Como os serviços de mídia se baseia no OData v3, Olá ativos individuais nas Olá InputMediaAssets e coleções de propriedades de navegação OutputMediaAssets são referenciadas por meio de um " Metadata: uri" par nome-valor.</span><span class="sxs-lookup"><span data-stu-id="8755d-159">Because Media Services is built on OData v3, hello individual assets in hello InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span></span>
* <span data-ttu-id="8755d-160">Os InputMediaAssets mapeiam tooone ou mais ativos que você criou nos serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="8755d-160">InputMediaAssets maps tooone or more assets that you created in Media Services.</span></span> <span data-ttu-id="8755d-161">Os OutputMediaAssets são criados pelo sistema hello.</span><span class="sxs-lookup"><span data-stu-id="8755d-161">OutputMediaAssets are created by hello system.</span></span> <span data-ttu-id="8755d-162">Eles não referenciam um ativo existente.</span><span class="sxs-lookup"><span data-stu-id="8755d-162">They don't reference an existing asset.</span></span>
* <span data-ttu-id="8755d-163">Os OutputMediaAssets podem ser nomeados usando o atributo assetName de saudação.</span><span class="sxs-lookup"><span data-stu-id="8755d-163">OutputMediaAssets can be named by using hello assetName attribute.</span></span> <span data-ttu-id="8755d-164">Se esse atributo não estiver presente, o nome de saudação do hello OutputMediaAsset é qualquer valor de texto interno de saudação do hello <outputAsset> elemento for com um sufixo do valor do nome do trabalho hello, ou valor de Id do trabalho hello (no caso de Olá onde a propriedade de nome de saudação não está definida).</span><span class="sxs-lookup"><span data-stu-id="8755d-164">If this attribute is not present, then hello name of hello OutputMediaAsset is whatever hello inner text value of hello <outputAsset> element is with a suffix of either hello Job Name value, or hello Job Id value (in hello case where hello Name property isn't defined).</span></span> <span data-ttu-id="8755d-165">Por exemplo, se você definir um valor para assetName muito "Exemplo", em seguida, Olá Name de OutputMediaAsset será definida muito "Sample."</span><span class="sxs-lookup"><span data-stu-id="8755d-165">For example, if you set a value for assetName too"Sample," then hello OutputMediaAsset Name property is set too"Sample."</span></span> <span data-ttu-id="8755d-166">No entanto, se não definir um valor para assetName, mas definido o nome do trabalho Olá muito "Novotrabalho" e, em seguida, Olá Name de OutputMediaAsset será "JobOutputAsset (valor) novotrabalho."</span><span class="sxs-lookup"><span data-stu-id="8755d-166">However, if you didn't set a value for assetName, but did set hello job name too"NewJob," then hello OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob."</span></span>

## <a name="create-a-job-with-chained-tasks"></a><span data-ttu-id="8755d-167">Criar um trabalho com tarefas encadeadas</span><span class="sxs-lookup"><span data-stu-id="8755d-167">Create a job with chained tasks</span></span>
<span data-ttu-id="8755d-168">Em muitos cenários de aplicativo, os desenvolvedores desejam toocreate uma série de tarefas de processamento.</span><span class="sxs-lookup"><span data-stu-id="8755d-168">In many application scenarios, developers want toocreate a series of processing tasks.</span></span> <span data-ttu-id="8755d-169">Nos serviços de mídia, você pode criar uma série de tarefas encadeadas.</span><span class="sxs-lookup"><span data-stu-id="8755d-169">In Media Services, you can create a series of chained tasks.</span></span> <span data-ttu-id="8755d-170">Cada tarefa executa etapas de processamento diferentes e pode usar diferentes processadores de mídia.</span><span class="sxs-lookup"><span data-stu-id="8755d-170">Each task performs different processing steps and can use different media processors.</span></span> <span data-ttu-id="8755d-171">tarefas Olá encadeado podem entregar um ativo de uma tarefa tooanother, executando uma sequência linear de tarefas no ativo de saudação.</span><span class="sxs-lookup"><span data-stu-id="8755d-171">hello chained tasks can hand off an asset from one task tooanother, performing a linear sequence of tasks on hello asset.</span></span> <span data-ttu-id="8755d-172">No entanto, tarefas de Olá executadas em um trabalho não são necessário toobe em uma sequência.</span><span class="sxs-lookup"><span data-stu-id="8755d-172">However, hello tasks performed in a job are not required toobe in a sequence.</span></span> <span data-ttu-id="8755d-173">Quando você cria uma tarefa encadeada, Olá encadeados **ITask** objetos são criados em uma única **IJob** objeto.</span><span class="sxs-lookup"><span data-stu-id="8755d-173">When you create a chained task, hello chained **ITask** objects are created in a single **IJob** object.</span></span>

> [!NOTE]
> <span data-ttu-id="8755d-174">Atualmente, há um limite de 30 tarefas por trabalho.</span><span class="sxs-lookup"><span data-stu-id="8755d-174">There is currently a limit of 30 tasks per job.</span></span> <span data-ttu-id="8755d-175">Se você precisar de mais de 30 tarefas toochain, crie mais de um trabalho de tarefas de saudação do toocontain.</span><span class="sxs-lookup"><span data-stu-id="8755d-175">If you need toochain more than 30 tasks, create more than one job toocontain hello tasks.</span></span>
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


### <a name="considerations"></a><span data-ttu-id="8755d-176">Considerações</span><span class="sxs-lookup"><span data-stu-id="8755d-176">Considerations</span></span>
<span data-ttu-id="8755d-177">tooenable encadeamento de tarefas:</span><span class="sxs-lookup"><span data-stu-id="8755d-177">tooenable task chaining:</span></span>

* <span data-ttu-id="8755d-178">Um trabalho deve ter, pelo menos, duas tarefas.</span><span class="sxs-lookup"><span data-stu-id="8755d-178">A job must have at least two tasks.</span></span>
* <span data-ttu-id="8755d-179">Deve haver pelo menos uma tarefa cuja entrada é saída de saudação de outra tarefa no trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="8755d-179">There must be at least one task whose input is hello output of another task in hello job.</span></span>

## <a name="use-odata-batch-processing"></a><span data-ttu-id="8755d-180">Usar o processamento em lotes OData</span><span class="sxs-lookup"><span data-stu-id="8755d-180">Use OData batch processing</span></span>
<span data-ttu-id="8755d-181">saudação de exemplo a seguir mostra como toouse OData em lote toocreate de processamento de um trabalho e tarefas.</span><span class="sxs-lookup"><span data-stu-id="8755d-181">hello following example shows how toouse OData batch processing toocreate a job and tasks.</span></span> <span data-ttu-id="8755d-182">Para obter informações sobre o processamento em lotes, consulte [Processamento em lote do protocolo OData (Open Data)](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span><span class="sxs-lookup"><span data-stu-id="8755d-182">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span></span>

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



## <a name="create-a-job-by-using-a-jobtemplate"></a><span data-ttu-id="8755d-183">Criar um trabalho usando um JobTemplate</span><span class="sxs-lookup"><span data-stu-id="8755d-183">Create a job by using a JobTemplate</span></span>
<span data-ttu-id="8755d-184">Ao processar múltiplos ativos usando um conjunto comum de tarefas, use que uma tarefa de padrão JobTemplate toospecify Olá predefinições ou ordem de saudação tooset das tarefas.</span><span class="sxs-lookup"><span data-stu-id="8755d-184">When you process multiple assets by using a common set of tasks, use a JobTemplate toospecify hello default task presets, or tooset hello order of tasks.</span></span>

<span data-ttu-id="8755d-185">saudação de exemplo a seguir mostra como toocreate um JobTemplate com um TaskTemplate que é definida embutida.</span><span class="sxs-lookup"><span data-stu-id="8755d-185">hello following example shows how toocreate a JobTemplate with a TaskTemplate that is defined inline.</span></span> <span data-ttu-id="8755d-186">Olá TaskTemplate usa Olá codificador de mídia padrão como o arquivo de ativo do hello MediaProcessor tooencode hello.</span><span class="sxs-lookup"><span data-stu-id="8755d-186">hello TaskTemplate uses hello Media Encoder Standard as hello MediaProcessor tooencode hello asset file.</span></span> <span data-ttu-id="8755d-187">No entanto, outros MediaProcessors também podem ser usados.</span><span class="sxs-lookup"><span data-stu-id="8755d-187">However, other MediaProcessors can be used as well.</span></span>

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
> <span data-ttu-id="8755d-188">Ao contrário de outras entidades de serviços de mídia, você deve definir um novo identificador GUID para cada TaskTemplate e colocá-lo em Olá taskTemplateId e a propriedade de Id no corpo da solicitação.</span><span class="sxs-lookup"><span data-stu-id="8755d-188">Unlike other Media Services entities, you must define a new GUID identifier for each TaskTemplate and place it in hello taskTemplateId and Id property in your request body.</span></span> <span data-ttu-id="8755d-189">esquema de conteúdo de identificação de saudação deve seguir o esquema de saudação descrito em identificar entidades de serviços de mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="8755d-189">hello content identification scheme must follow hello scheme described in Identify Azure Media Services Entities.</span></span> <span data-ttu-id="8755d-190">Além disso, os JobTemplates não podem ser atualizados.</span><span class="sxs-lookup"><span data-stu-id="8755d-190">Also, JobTemplates cannot be updated.</span></span> <span data-ttu-id="8755d-191">Em vez disso, você deve criar um novo com as suas alterações atualizadas.</span><span class="sxs-lookup"><span data-stu-id="8755d-191">Instead, you must create a new one with your updated changes.</span></span>
>
>

<span data-ttu-id="8755d-192">Se for bem-sucedido, Olá resposta a seguir será retornada:</span><span class="sxs-lookup"><span data-stu-id="8755d-192">If successful, hello following response is returned:</span></span>

    HTTP/1.1 201 Created

    . . .


<span data-ttu-id="8755d-193">Olá mostrado no exemplo a seguir como toocreate um trabalho que faz referência a uma Id de JobTemplate:</span><span class="sxs-lookup"><span data-stu-id="8755d-193">hello following example shows how toocreate a job that references a JobTemplate Id:</span></span>

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A3f1fe4a2-68f5-4190-9557-cd45beccef92')"}}], "TemplateId" : "nb:jtid:UUID:15e6e5e6-ac85-084e-9dc2-db3645fbf0aa"}


<span data-ttu-id="8755d-194">Se for bem-sucedido, Olá resposta a seguir será retornada:</span><span class="sxs-lookup"><span data-stu-id="8755d-194">If successful, hello following response is returned:</span></span>

    HTTP/1.1 201 Created

    . . .



## <a name="media-services-learning-paths"></a><span data-ttu-id="8755d-195">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="8755d-195">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="8755d-196">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="8755d-196">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="8755d-197">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8755d-197">Next steps</span></span>
<span data-ttu-id="8755d-198">Agora que você sabe como toocreate tooencode um trabalho um ativo, consulte [como toocheck trabalho andamento com os serviços de mídia](media-services-rest-check-job-progress.md).</span><span class="sxs-lookup"><span data-stu-id="8755d-198">Now that you know how toocreate a job tooencode an asset, see [How toocheck job progress with Media Services](media-services-rest-check-job-progress.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="8755d-199">Consulte também</span><span class="sxs-lookup"><span data-stu-id="8755d-199">See also</span></span>
[<span data-ttu-id="8755d-200">Obter processadores de mídia</span><span class="sxs-lookup"><span data-stu-id="8755d-200">Get Media Processors</span></span>](media-services-rest-get-media-processor.md)
