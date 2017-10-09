---
title: "aaaUsing PlayReady e/ou Widevine comuns criptografia dinâmica | Microsoft Docs"
description: "Serviços de mídia do Microsoft Azure permite que você toodeliver MPEG-DASH, Smooth Streaming e Http-Live-Streaming (HLS) fluxos protegidos com o Microsoft PlayReady DRM. Ele também permite que você toodelivery DASH criptografado com Widevine DRM. Este tópico mostra como toodynamically criptografar com PlayReady e Widevine DRM."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 548d1a12-e2cb-45fe-9307-4ec0320567a2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 0475e6ec80dcf39eb4e5c4ad4d17f821502951bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-playready-andor-widevine-dynamic-common-encryption"></a><span data-ttu-id="739cf-105">Usando a criptografia comum dinâmica PlayReady e/ou Widevine</span><span class="sxs-lookup"><span data-stu-id="739cf-105">Using PlayReady and/or Widevine dynamic common encryption</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="739cf-106">.NET</span><span class="sxs-lookup"><span data-stu-id="739cf-106">.NET</span></span>](media-services-protect-with-drm.md)
> * [<span data-ttu-id="739cf-107">Java</span><span class="sxs-lookup"><span data-stu-id="739cf-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="739cf-108">PHP</span><span class="sxs-lookup"><span data-stu-id="739cf-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
>
>

<span data-ttu-id="739cf-109">Serviços de mídia do Microsoft Azure permite que você toodeliver MPEG-DASH, Smooth Streaming e fluxos de HTTP-Live-Streaming (HLS) protegidos com [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span><span class="sxs-lookup"><span data-stu-id="739cf-109">Microsoft Azure Media Services enables you toodeliver MPEG-DASH, Smooth Streaming, and HTTP-Live-Streaming (HLS) streams protected with [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span></span> <span data-ttu-id="739cf-110">Ele também permite fluxos de traço toodeliver criptografado com licenças Widevine DRM.</span><span class="sxs-lookup"><span data-stu-id="739cf-110">It also enables you toodeliver encrypted DASH streams with Widevine DRM licenses.</span></span> <span data-ttu-id="739cf-111">PlayReady e Widevine são criptografados por Olá especificação de criptografia comum (ISO/IEC 23001-7 CENC).</span><span class="sxs-lookup"><span data-stu-id="739cf-111">Both PlayReady and Widevine are encrypted per hello Common Encryption (ISO/IEC 23001-7 CENC) specification.</span></span> <span data-ttu-id="739cf-112">Você pode usar [AMS .NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices/) (começando com a versão de hello 3.5.1) ou REST API tooconfigure seu toouse AssetDeliveryConfiguration Widevine.</span><span class="sxs-lookup"><span data-stu-id="739cf-112">You can use [AMS .NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices/) (starting with hello version 3.5.1) or REST API tooconfigure your AssetDeliveryConfiguration toouse Widevine.</span></span>

<span data-ttu-id="739cf-113">Os Serviços de Mídia fornecem um serviço para entregar licenças DRM do PlayReady e do Widevine.</span><span class="sxs-lookup"><span data-stu-id="739cf-113">Media Services provides a service for delivering PlayReady and Widevine DRM licenses.</span></span> <span data-ttu-id="739cf-114">Serviços de mídia oferecem APIs que permitem que você configure direitos hello e restrições que você deseja para Olá tooenforce de tempo de execução PlayReady ou Widevine DRM quando um usuário é reproduzido conteúdo protegido.</span><span class="sxs-lookup"><span data-stu-id="739cf-114">Media Services also provides APIs that let you configure hello rights and restrictions that you want for hello PlayReady or Widevine DRM runtime tooenforce when a user plays back protected content.</span></span> <span data-ttu-id="739cf-115">Quando um usuário solicita um conteúdo protegido por DRM, o aplicativo de player hello solicitará uma licença do serviço de licença Olá AMS.</span><span class="sxs-lookup"><span data-stu-id="739cf-115">When a user requests a DRM protected content, hello player application will request a license from hello AMS license service.</span></span> <span data-ttu-id="739cf-116">serviço de licença AMS Olá emitirá um player de toohello de licença se ele está autorizado.</span><span class="sxs-lookup"><span data-stu-id="739cf-116">hello AMS license service will issue a license toohello player if it is authorized.</span></span> <span data-ttu-id="739cf-117">Uma licença do PlayReady ou Widevine contém a chave de descriptografia de saudação que pode ser usado por Olá cliente player toodecrypt e fluxo Olá conteúdo.</span><span class="sxs-lookup"><span data-stu-id="739cf-117">A PlayReady or Widevine license contains hello decryption key that can be used by hello client player toodecrypt and stream hello content.</span></span>

<span data-ttu-id="739cf-118">Você também pode usar o hello AMS parceiros toohelp fornecer licenças Widevine a seguir: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="739cf-118">You can also use hello following AMS partners toohelp you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span> <span data-ttu-id="739cf-119">Para saber mais, consulte: integração com [Axinom](media-services-axinom-integration.md) e [castLabs](media-services-castlabs-integration.md).</span><span class="sxs-lookup"><span data-stu-id="739cf-119">For more information, see: integration with [Axinom](media-services-axinom-integration.md) and [castLabs](media-services-castlabs-integration.md).</span></span>

<span data-ttu-id="739cf-120">Os serviços de mídia oferecem suporte a várias maneiras de autorizar os usuários que fazem solicitações de chave.</span><span class="sxs-lookup"><span data-stu-id="739cf-120">Media Services supports multiple ways of authorizing users who make key requests.</span></span> <span data-ttu-id="739cf-121">Olá política de autorização da chave de conteúdo pode ter uma ou mais restrições de autorização: abrir ou restrição de token.</span><span class="sxs-lookup"><span data-stu-id="739cf-121">hello content key authorization policy could have one or more authorization restrictions: open or token restriction.</span></span> <span data-ttu-id="739cf-122">política de restrição de token de saudação deve ser acompanhada por um token emitido por um Token STS (serviço seguro).</span><span class="sxs-lookup"><span data-stu-id="739cf-122">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="739cf-123">Serviços de mídia oferece suporte a tokens no hello [Simple Web Tokens](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) formato (SWT) e [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) formato (JWT).</span><span class="sxs-lookup"><span data-stu-id="739cf-123">Media Services supports tokens in hello [Simple Web Tokens](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (SWT) format and [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT) format.</span></span> <span data-ttu-id="739cf-124">Para obter mais informações, consulte a política de autorização de configurar Olá da chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="739cf-124">For more information, see Configure hello content key’s authorization policy.</span></span>

<span data-ttu-id="739cf-125">tootake vantagem da criptografia dinâmica, você precisa toohave um ativo que contenha um conjunto de arquivos MP4 com múltiplas taxas de bits ou arquivos de origem de Smooth Streaming de várias taxas de bits.</span><span class="sxs-lookup"><span data-stu-id="739cf-125">tootake advantage of dynamic encryption, you need toohave an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="739cf-126">Você também precisa políticas de entrega Olá tooconfigure ativo hello (descrita posteriormente neste tópico).</span><span class="sxs-lookup"><span data-stu-id="739cf-126">You also need tooconfigure hello delivery policies for hello asset (described later in this topic).</span></span> <span data-ttu-id="739cf-127">Em seguida, com base no formato de saudação especificado na URL de streaming de hello, Olá Streaming sob demanda servidor garantirá que fluxo Olá é fornecido no protocolo de saudação escolhida.</span><span class="sxs-lookup"><span data-stu-id="739cf-127">Then, based on hello format specified in hello streaming URL, hello On-Demand Streaming server will ensure that hello stream is delivered in hello protocol you have chosen.</span></span> <span data-ttu-id="739cf-128">Como resultado, você só precisa toostore e pagamento para arquivos de saudação em um único formato de armazenamento e os serviços de mídia criará e enviará a resposta HTTP apropriada Olá com base em cada solicitação de um cliente.</span><span class="sxs-lookup"><span data-stu-id="739cf-128">As a result, you only need toostore and pay for hello files in a single storage format and Media Services will build and serve hello appropriate HTTP response based on each request from a client.</span></span>

<span data-ttu-id="739cf-129">Este tópico seria útil toodevelopers que funcionam em aplicativos que distribuem mídia protegida com vários DRMs, como o PlayReady e Widevine.</span><span class="sxs-lookup"><span data-stu-id="739cf-129">This topic would be useful toodevelopers that work on applications that deliver media protected with multiple DRMs, such as PlayReady and Widevine.</span></span> <span data-ttu-id="739cf-130">tópico de saudação mostra como tooconfigure Olá o serviço de entrega de licenças do PlayReady com as políticas de autorização para que somente clientes autorizados recebam licenças do PlayReady ou Widevine.</span><span class="sxs-lookup"><span data-stu-id="739cf-130">hello topic shows you how tooconfigure hello PlayReady license delivery service with authorization policies so that only authorized clients could receive PlayReady or Widevine licenses.</span></span> <span data-ttu-id="739cf-131">Ele também mostra como criptografia de criptografia dinâmica toouse com PlayReady ou Widevine DRM sobre traço.</span><span class="sxs-lookup"><span data-stu-id="739cf-131">It also shows how toouse dynamic encryption encryption with PlayReady or Widevine DRM over DASH.</span></span>

>[!NOTE]
><span data-ttu-id="739cf-132">Quando sua conta AMS é criada um **padrão** ponto de extremidade de streaming é adicionada conta tooyour Olá **parado** estado.</span><span class="sxs-lookup"><span data-stu-id="739cf-132">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="739cf-133">toostart streaming seu conteúdo e execute aproveitar o empacotamento dinâmico e criptografia dinâmica, Olá ponto de extremidade de streaming do qual você deseja toostream conteúdo tem toobe em Olá **executando** estado.</span><span class="sxs-lookup"><span data-stu-id="739cf-133">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 

## <a name="download-sample"></a><span data-ttu-id="739cf-134">Baixar exemplo</span><span class="sxs-lookup"><span data-stu-id="739cf-134">Download sample</span></span>
<span data-ttu-id="739cf-135">Você pode baixar o exemplo hello descrito neste artigo do [aqui](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm).</span><span class="sxs-lookup"><span data-stu-id="739cf-135">You can download hello sample described in this article from [here](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm).</span></span>

## <a name="configuring-dynamic-common-encryption-and-drm-license-delivery-services"></a><span data-ttu-id="739cf-136">Configurando a Criptografia Dinâmica Comum e Serviços de Distribuição de Licenças de DRM</span><span class="sxs-lookup"><span data-stu-id="739cf-136">Configuring Dynamic Common Encryption and DRM License Delivery Services</span></span>

<span data-ttu-id="739cf-137">Olá seguem etapas gerais que você precisaria tooperform para proteger seus ativos com o PlayReady, usando o serviço de entrega de licença de serviços de mídia hello e também usando criptografia dinâmica.</span><span class="sxs-lookup"><span data-stu-id="739cf-137">hello following are general steps that you would need tooperform when protecting your assets with PlayReady, using hello Media Services license delivery service, and also using dynamic encryption.</span></span>

1. <span data-ttu-id="739cf-138">Criar um ativo e carregar arquivos no ativo de saudação.</span><span class="sxs-lookup"><span data-stu-id="739cf-138">Create an asset and upload files into hello asset.</span></span>
2. <span data-ttu-id="739cf-139">Codifica Olá ativo contendo Olá arquivo toohello taxa de bits adaptável que MP4 definido.</span><span class="sxs-lookup"><span data-stu-id="739cf-139">Encode hello asset containing hello file toohello adaptive bitrate MP4 set.</span></span>
3. <span data-ttu-id="739cf-140">Criar uma chave de conteúdo e associá-lo com ativo Olá codificado.</span><span class="sxs-lookup"><span data-stu-id="739cf-140">Create a content key and associate it with hello encoded asset.</span></span> <span data-ttu-id="739cf-141">Nos serviços de mídia, a chave de conteúdo de saudação contém chave de criptografia do ativo hello.</span><span class="sxs-lookup"><span data-stu-id="739cf-141">In Media Services, hello content key contains hello asset’s encryption key.</span></span>
4. <span data-ttu-id="739cf-142">Configure a política de autorização da chave de saudação conteúdo.</span><span class="sxs-lookup"><span data-stu-id="739cf-142">Configure hello content key’s authorization policy.</span></span> <span data-ttu-id="739cf-143">política de autorização da chave de conteúdo Olá deve ser configurada por você e cliente Olá para Olá conteúdo toobe chave toohello entregue cliente.</span><span class="sxs-lookup"><span data-stu-id="739cf-143">hello content key authorization policy must be configured by you and met by hello client in order for hello content key toobe delivered toohello client.</span></span>

    <span data-ttu-id="739cf-144">Ao criar a política de autorização da chave de conteúdo hello, você precisa fazer toospecify Olá seguinte: método (PlayReady ou Widevine), restrições de entrega (abertas ou token) e tipo de entrega de chave de toohello específicos de informações que define como chave Olá é entregue cliente de toohello ([PlayReady](media-services-playready-license-template-overview.md) ou [Widevine](media-services-widevine-license-template-overview.md) modelo de licença).</span><span class="sxs-lookup"><span data-stu-id="739cf-144">When creating hello content key authorization policy, you need toospecify hello following: delivery method (PlayReady or Widevine), restrictions (open or token), and information specific toohello key delivery type that defines how hello key is delivered toohello client ([PlayReady](media-services-playready-license-template-overview.md) or [Widevine](media-services-widevine-license-template-overview.md) license template).</span></span>

5. <span data-ttu-id="739cf-145">Configure a política de distribuição de saudação para um ativo.</span><span class="sxs-lookup"><span data-stu-id="739cf-145">Configure hello delivery policy for an asset.</span></span> <span data-ttu-id="739cf-146">configuração de política de entrega de saudação inclui: Olá de protocolo de entrega (por exemplo, MPEG DASH, HLS, Smooth Streaming ou todos), tipo de criptografia dinâmica (por exemplo, criptografia comum), PlayReady ou URL de aquisição de licenças Widevine.</span><span class="sxs-lookup"><span data-stu-id="739cf-146">hello delivery policy configuration includes: delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all), hello type of dynamic encryption (for example, Common Encryption), PlayReady or Widevine license acquisition URL.</span></span>

    <span data-ttu-id="739cf-147">Você pode aplicar o protocolo de tooeach política diferente em Olá mesmo ativo.</span><span class="sxs-lookup"><span data-stu-id="739cf-147">You could apply different policy tooeach protocol on hello same asset.</span></span> <span data-ttu-id="739cf-148">Por exemplo, você pode aplicar PlayReady criptografia tooSmooth/DASH e Envelope AES tooHLS.</span><span class="sxs-lookup"><span data-stu-id="739cf-148">For example, you could apply PlayReady encryption tooSmooth/DASH and AES Envelope tooHLS.</span></span> <span data-ttu-id="739cf-149">Todos os protocolos que não estão definidos em uma política de entrega (por exemplo, você adiciona uma única política que só especifica HLS como protocolo de saudação) serão impedidos de streaming.</span><span class="sxs-lookup"><span data-stu-id="739cf-149">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as hello protocol) will be blocked from streaming.</span></span> <span data-ttu-id="739cf-150">Olá toothis de exceção é se você não tiver nenhuma política de entrega de ativo definida.</span><span class="sxs-lookup"><span data-stu-id="739cf-150">hello exception toothis is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="739cf-151">Em seguida, todos os protocolos poderão ser em Olá clara.</span><span class="sxs-lookup"><span data-stu-id="739cf-151">Then, all protocols will be allowed in hello clear.</span></span>

6. <span data-ttu-id="739cf-152">Crie um localizador OnDemand em ordem tooget uma URL de streaming.</span><span class="sxs-lookup"><span data-stu-id="739cf-152">Create an OnDemand locator in order tooget a streaming URL.</span></span>

<span data-ttu-id="739cf-153">Você encontrará um exemplo completo de .NET final Olá Olá tópico.</span><span class="sxs-lookup"><span data-stu-id="739cf-153">You will find a complete .NET example at hello end of hello topic.</span></span>

<span data-ttu-id="739cf-154">Olá a imagem a seguir demonstra o fluxo de trabalho de saudação descrito acima.</span><span class="sxs-lookup"><span data-stu-id="739cf-154">hello following image demonstrates hello workflow described above.</span></span> <span data-ttu-id="739cf-155">Aqui o token de saudação é usado para autenticação.</span><span class="sxs-lookup"><span data-stu-id="739cf-155">Here hello token is used for authentication.</span></span>

![Proteger com o PlayReady](./media/media-services-content-protection-overview/media-services-content-protection-with-drm.png)

<span data-ttu-id="739cf-157">restante deste tópico Olá fornece explicações detalhadas, exemplos de código e tootopics links que mostram como tooachieve Olá as tarefas descritas acima.</span><span class="sxs-lookup"><span data-stu-id="739cf-157">hello rest of this topic provides detailed explanations, code examples, and links tootopics that show you how tooachieve hello tasks described above.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="739cf-158">Limitações atuais</span><span class="sxs-lookup"><span data-stu-id="739cf-158">Current limitations</span></span>
<span data-ttu-id="739cf-159">Se você adicionar ou atualizar uma política de entrega de ativos, você deve excluir o localizador de saudação associada (se houver) e criar um novo.</span><span class="sxs-lookup"><span data-stu-id="739cf-159">If you add or update an asset delivery policy, you must delete hello associated locator (if any) and create a new locator.</span></span>

<span data-ttu-id="739cf-160">Limitação ao criptografar com o Widevine com os Serviços de Mídia do Azure: atualmente, não há suporte para várias chaves de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="739cf-160">Limitation when encrypting with Widevine with Azure Media Services: currently, multiple content keys are not supported.</span></span>

## <a name="create-an-asset-and-upload-files-into-hello-asset"></a><span data-ttu-id="739cf-161">Criar um ativo e carregar arquivos no ativo de saudação</span><span class="sxs-lookup"><span data-stu-id="739cf-161">Create an asset and upload files into hello asset</span></span>
<span data-ttu-id="739cf-162">Em ordem toomanage, codificar e transmitir seus vídeos, primeiro você deve carregar o conteúdo nos serviços de mídia do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="739cf-162">In order toomanage, encode, and stream your videos, you must first upload your content into Microsoft Azure Media Services.</span></span> <span data-ttu-id="739cf-163">Uma vez carregado, seu conteúdo é armazenado com segurança na nuvem Olá para processamento e streaming.</span><span class="sxs-lookup"><span data-stu-id="739cf-163">Once uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span>

<span data-ttu-id="739cf-164">Para obter informações detalhadas, consulte [Carregar arquivos em uma conta dos Serviços de Mídia](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="739cf-164">For detailed information, see [Upload Files into a Media Services account](media-services-dotnet-upload-files.md).</span></span>

## <a name="encode-hello-asset-containing-hello-file-toohello-adaptive-bitrate-mp4-set"></a><span data-ttu-id="739cf-165">Codificar Olá ativo contendo Olá arquivo toohello taxa de bits adaptável que MP4 set</span><span class="sxs-lookup"><span data-stu-id="739cf-165">Encode hello asset containing hello file toohello adaptive bitrate MP4 set</span></span>
<span data-ttu-id="739cf-166">Com criptografia dinâmica, tudo o que você precisa é toocreate um ativo que contenha um conjunto de arquivos MP4 com múltiplas taxas de bits ou arquivos de origem de Smooth Streaming de várias taxas de bits.</span><span class="sxs-lookup"><span data-stu-id="739cf-166">With dynamic encryption all you need is toocreate an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="739cf-167">Em seguida, com base no formato de saudação especificado no manifesto de saudação e solicitação de fragmento, Olá sob demanda de Streaming server irá garantir que você receba o fluxo de saudação no protocolo hello escolhido.</span><span class="sxs-lookup"><span data-stu-id="739cf-167">Then, based on hello specified format in hello manifest and fragment request, hello On-Demand Streaming server will ensure that you receive hello stream in hello protocol you have chosen.</span></span> <span data-ttu-id="739cf-168">Como resultado, você só precisa toostore e pagamento para arquivos de saudação em único formato de armazenamento e serviços de mídia criará e enviará a resposta apropriada hello, com base nas solicitações de um cliente.</span><span class="sxs-lookup"><span data-stu-id="739cf-168">As a result, you only need toostore and pay for hello files in single storage format and Media Services service will build and serve hello appropriate response based on requests from a client.</span></span> <span data-ttu-id="739cf-169">Para obter mais informações, consulte Olá [visão geral do empacotamento dinâmico](media-services-dynamic-packaging-overview.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="739cf-169">For more information, see hello [Dynamic Packaging Overview](media-services-dynamic-packaging-overview.md) topic.</span></span>

<span data-ttu-id="739cf-170">Para obter instruções sobre como tooencode, consulte [como tooencode um ativo usando o codificador de mídia padrão](media-services-dotnet-encode-with-media-encoder-standard.md).</span><span class="sxs-lookup"><span data-stu-id="739cf-170">For instructions on how tooencode, see [How tooencode an asset using Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>

## <span data-ttu-id="739cf-171"><a id="create_contentkey"></a>Criar uma chave de conteúdo e associá-lo com ativo Olá codificado</span><span class="sxs-lookup"><span data-stu-id="739cf-171"><a id="create_contentkey"></a>Create a content key and associate it with hello encoded asset</span></span>
<span data-ttu-id="739cf-172">Nos serviços de mídia, a chave de conteúdo de saudação contém chave Olá que você deseja tooencrypt um ativo com.</span><span class="sxs-lookup"><span data-stu-id="739cf-172">In Media Services, hello content key contains hello key that you want tooencrypt an asset with.</span></span>

<span data-ttu-id="739cf-173">Para obter informações detalhadas, consulte [Criar chave de conteúdo](media-services-dotnet-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="739cf-173">For detailed information, see [Create content key](media-services-dotnet-create-contentkey.md).</span></span>

## <span data-ttu-id="739cf-174"><a id="configure_key_auth_policy"></a>Configurar política de autorização da chave de saudação conteúdo</span><span class="sxs-lookup"><span data-stu-id="739cf-174"><a id="configure_key_auth_policy"></a>Configure hello content key’s authorization policy</span></span>
<span data-ttu-id="739cf-175">Os serviços de mídia oferecem suporte a várias maneiras de autenticar os usuários que fazem solicitações de chave.</span><span class="sxs-lookup"><span data-stu-id="739cf-175">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="739cf-176">política de autorização da chave de conteúdo Olá deve ser configurada por você e Olá cliente (player) em ordem para Olá toobe chave entregue toohello cliente.</span><span class="sxs-lookup"><span data-stu-id="739cf-176">hello content key authorization policy must be configured by you and met by hello client (player) in order for hello key toobe delivered toohello client.</span></span> <span data-ttu-id="739cf-177">Olá política de autorização da chave de conteúdo pode ter uma ou mais restrições de autorização: abrir ou restrição de token.</span><span class="sxs-lookup"><span data-stu-id="739cf-177">hello content key authorization policy could have one or more authorization restrictions: open or token restriction.</span></span>

<span data-ttu-id="739cf-178">Para obter informações detalhadas, consulte [Configurar política de autorização de chave de conteúdo](media-services-dotnet-configure-content-key-auth-policy.md#playready-dynamic-encryption).</span><span class="sxs-lookup"><span data-stu-id="739cf-178">For detailed information, see [Configure Content Key Authorization Policy](media-services-dotnet-configure-content-key-auth-policy.md#playready-dynamic-encryption).</span></span>

## <span data-ttu-id="739cf-179"><a id="configure_asset_delivery_policy"></a>Configurar política de entrega de ativos</span><span class="sxs-lookup"><span data-stu-id="739cf-179"><a id="configure_asset_delivery_policy"></a>Configure asset delivery policy</span></span>
<span data-ttu-id="739cf-180">Configure a política de distribuição de saudação para seu ativo.</span><span class="sxs-lookup"><span data-stu-id="739cf-180">Configure hello delivery policy for your asset.</span></span> <span data-ttu-id="739cf-181">Algumas coisas que Olá a configuração de política de entrega de ativos inclui:</span><span class="sxs-lookup"><span data-stu-id="739cf-181">Some things that hello asset delivery policy configuration includes:</span></span>

* <span data-ttu-id="739cf-182">Olá DRM URL de aquisição de licença.</span><span class="sxs-lookup"><span data-stu-id="739cf-182">hello DRM license acquisition URL.</span></span>
* <span data-ttu-id="739cf-183">Olá ativo protocolo de entrega (por exemplo, MPEG DASH, HLS, Smooth Streaming ou todos).</span><span class="sxs-lookup"><span data-stu-id="739cf-183">hello asset delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all).</span></span>
* <span data-ttu-id="739cf-184">tipo de saudação de criptografia dinâmica (neste caso, criptografia comum).</span><span class="sxs-lookup"><span data-stu-id="739cf-184">hello type of dynamic encryption (in this case, Common Encryption).</span></span>

<span data-ttu-id="739cf-185">Para obter informações detalhadas, consulte [Configurar política de entrega de ativos ](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="739cf-185">For detailed information, see [Configure asset delivery policy ](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <span data-ttu-id="739cf-186"><a id="create_locator"></a>Criar um OnDemand streaming localizador de ordem tooget uma URL de streaming</span><span class="sxs-lookup"><span data-stu-id="739cf-186"><a id="create_locator"></a>Create an OnDemand streaming locator in order tooget a streaming URL</span></span>
<span data-ttu-id="739cf-187">Você precisará tooprovide seu usuário com hello streaming URL para Smooth, DASH ou HLS.</span><span class="sxs-lookup"><span data-stu-id="739cf-187">You will need tooprovide your user with hello streaming URL for Smooth, DASH or HLS.</span></span>

> [!NOTE]
> <span data-ttu-id="739cf-188">Se você adicionar ou atualizar a política de fornecimento do ativo, você deve excluir um localizador existente (se houver) e criar um novo localizador.</span><span class="sxs-lookup"><span data-stu-id="739cf-188">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
>
>

<span data-ttu-id="739cf-189">Para obter instruções sobre como toopublish um ativo e compilar uma URL de streaming, consulte [construir uma URL de streaming](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="739cf-189">For instructions on how toopublish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="get-a-test-token"></a><span data-ttu-id="739cf-190">Obter um token de teste</span><span class="sxs-lookup"><span data-stu-id="739cf-190">Get a test token</span></span>
<span data-ttu-id="739cf-191">Obtenha um teste de token com base na restrição de token de saudação que foi usada para a política de autorização da chave de saudação.</span><span class="sxs-lookup"><span data-stu-id="739cf-191">Get a test token based on hello token restriction that was used for hello key authorization policy.</span></span>

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate =
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on hello data in hello given TokenRestrictionTemplate.
    //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
    //so you have tooadd it in front of hello token string.
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate);
    Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);


<span data-ttu-id="739cf-192">Você pode usar o hello [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tootest seu fluxo.</span><span class="sxs-lookup"><span data-stu-id="739cf-192">You can use hello [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tootest your stream.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="739cf-193">Criar e configurar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="739cf-193">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="739cf-194">Configurar seu ambiente de desenvolvimento e preencher o arquivo App. config de saudação com informações de conexão, conforme descrito em [desenvolvimento de serviços de mídia com o .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="739cf-194">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="739cf-195">Adicionar Olá elementos a seguir muito**appSettings** definido no seu arquivo App. config:</span><span class="sxs-lookup"><span data-stu-id="739cf-195">Add hello following elements too**appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a><span data-ttu-id="739cf-196">Exemplo</span><span class="sxs-lookup"><span data-stu-id="739cf-196">Example</span></span>

<span data-ttu-id="739cf-197">Olá exemplo a seguir demonstra a funcionalidade que foi introduzida no SDK de serviços de mídia do Azure para .net-versão 3.5.2 (especificamente, Olá capacidade toodefine um Widevine modelo de licença e solicitam uma licença de Widevine dos serviços de mídia do Azure).</span><span class="sxs-lookup"><span data-stu-id="739cf-197">hello following sample demonstrates functionality that was introduced in Azure Media Services SDK for .Net -Version 3.5.2 (specifically, hello ability toodefine a Widevine license template and request a Widevine license from Azure Media Services).</span></span>

<span data-ttu-id="739cf-198">Substitua o código de saudação no arquivo Program.cs pelo código Olá mostrado nesta seção.</span><span class="sxs-lookup"><span data-stu-id="739cf-198">Overwrite hello code in your Program.cs file with hello code shown in this section.</span></span>

>[!NOTE]
><span data-ttu-id="739cf-199">Há um limite de 1.000.000 políticas para diferentes políticas de AMS (por exemplo, para política de Localizador ou ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="739cf-199">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="739cf-200">Você deve usar Olá Olá a mesma ID de política se você estiver usando sempre mesmo dias acesso permissões, por exemplo, as políticas para localizadores são tooremain desejado no local por um longo período (políticas de carregamento não).</span><span class="sxs-lookup"><span data-stu-id="739cf-200">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="739cf-201">Para obter mais informações, consulte [este](media-services-dotnet-manage-entities.md#limit-access-policies) tópico.</span><span class="sxs-lookup"><span data-stu-id="739cf-201">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="739cf-202">Certifique-se de que variáveis de tooupdate toopoint toofolders onde se encontram os arquivos de entrada.</span><span class="sxs-lookup"><span data-stu-id="739cf-202">Make sure tooupdate variables toopoint toofolders where your input files are located.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;
    using Microsoft.WindowsAzure.MediaServices.Client.Widevine;
    using Newtonsoft.Json;

    namespace DynamicEncryptionWithDRM
    {
        class Program
        {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static readonly Uri _sampleIssuer =
            new Uri(ConfigurationManager.AppSettings["Issuer"]);
        private static readonly Uri _sampleAudience =
            new Uri(ConfigurationManager.AppSettings["Audience"]);

        // Field for service context.
        private static CloudMediaContext _context = null;

        private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

        private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            bool tokenRestriction = false;
            string tokenTemplateString = null;

            IAsset asset = UploadFileAndCreateAsset(_singleMP4File);
            Console.WriteLine("Uploaded asset: {0}", asset.Id);

            IAsset encodedAsset = EncodeToAdaptiveBitrateMP4Set(asset);
            Console.WriteLine("Encoded asset: {0}", encodedAsset.Id);

            IContentKey key = CreateCommonTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine("PlayReady License Key delivery URL: {0}", key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense));
            Console.WriteLine();

            if (tokenRestriction)
            tokenTemplateString = AddTokenRestrictedAuthorizationPolicy(key);
            else
            AddOpenAuthorizationPolicy(key);

            Console.WriteLine("Added authorization policy: {0}", key.AuthorizationPolicyId);
            Console.WriteLine();

            CreateAssetDeliveryPolicy(encodedAsset, key);
            Console.WriteLine("Created asset delivery policy. \n");
            Console.WriteLine();

            if (tokenRestriction && !String.IsNullOrEmpty(tokenTemplateString))
            {
            // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
            // back into a TokenRestrictionTemplate class instance.
            TokenRestrictionTemplate tokenTemplate =
                TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

            // Generate a test token based on hello hello data in hello given TokenRestrictionTemplate.
            // Note, you need toopass hello key id Guid because we specified
            // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey,
                                        DateTime.UtcNow.AddDays(365));
            Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            // You can use hello http://amsplayer.azurewebsites.net/azuremediaplayer.html player tootest streams.
            // Note that DASH works on IE 11 (via PlayReady), Edge (via PlayReady), Chrome (via Widevine).

            string url = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Encrypted DASH URL: {0}/manifest(format=mpd-time-csf)", url);

            Console.ReadLine();
        }

        static public IAsset UploadFileAndCreateAsset(string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
            Console.WriteLine("File does not exist.");
            return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.None);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset inputAsset)
        {
            var encodingPreset = "Adaptive Streaming";

            IJob job = _context.Jobs.Create(String.Format("Encoding into Mp4 {0} too{1}",
                        inputAsset.Name,
                        encodingPreset));

            var mediaProcessors =
            _context.MediaProcessors.Where(p => p.Name.Contains("Media Encoder Standard")).ToList();

            var latestMediaProcessor =
            mediaProcessors.OrderBy(mp => new Version(mp.Version)).LastOrDefault();

            ITask encodeTask = job.Tasks.AddNew("Encoding", latestMediaProcessor, encodingPreset, TaskOptions.None);
            encodeTask.InputAssets.Add(inputAsset);
            encodeTask.OutputAssets.AddNew(String.Format("{0} as {1}", inputAsset.Name, encodingPreset), AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }


        static public IContentKey CreateCommonTypeContentKey(IAsset asset)
        {

            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                        keyId,
                        contentKey,
                        "ContentKey",
                        ContentKeyType.CommonEncryption);

            // Associate hello key with hello asset.
            asset.ContentKeys.Add(key);

            return key;
        }

        static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
        {

            // Create ContentKeyAuthorizationPolicy with Open restrictions
            // and create authorization policy          

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                {
                new ContentKeyAuthorizationPolicyRestriction
                {
                    Name = "Open",
                    KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
                    Requirements = null
                }
                };

            // Configure PlayReady and Widevine license templates.
            string PlayReadyLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

            string WidevineLicenseTemplate = ConfigureWidevineLicenseTemplate();

            IContentKeyAuthorizationPolicyOption PlayReadyPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
                ContentKeyDeliveryType.PlayReadyLicense,
                restrictions, PlayReadyLicenseTemplate);

            IContentKeyAuthorizationPolicyOption WidevinePolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
                ContentKeyDeliveryType.Widevine,
                restrictions, WidevineLicenseTemplate);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common Content Key with no restrictions").
                Result;


            contentKeyAuthorizationPolicy.Options.Add(PlayReadyPolicy);
            contentKeyAuthorizationPolicy.Options.Add(WidevinePolicy);
            // Associate hello content key authorization policy with hello content key.
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;
        }

        public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
        {
            string tokenTemplateString = GenerateTokenRequirements();

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                {
                new ContentKeyAuthorizationPolicyRestriction
                {
                    Name = "Token Authorization Policy",
                    KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                    Requirements = tokenTemplateString,
                }
                };

            // Configure PlayReady and Widevine license templates.
            string PlayReadyLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

            string WidevineLicenseTemplate = ConfigureWidevineLicenseTemplate();

            IContentKeyAuthorizationPolicyOption PlayReadyPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                ContentKeyDeliveryType.PlayReadyLicense,
                restrictions, PlayReadyLicenseTemplate);

            IContentKeyAuthorizationPolicyOption WidevinePolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                ContentKeyDeliveryType.Widevine,
                restrictions, WidevineLicenseTemplate);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common Content Key with token restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(PlayReadyPolicy);
            contentKeyAuthorizationPolicy.Options.Add(WidevinePolicy);

            // Associate hello content key authorization policy with hello content key
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
        }

        static private string GenerateTokenRequirements()
        {
            TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

            template.PrimaryVerificationKey = new SymmetricVerificationKey();
            template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
            template.Audience = _sampleAudience.ToString();
            template.Issuer = _sampleIssuer.ToString();
            template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

            return TokenRestrictionTemplateSerializer.Serialize(template);
        }

        static private string ConfigurePlayReadyLicenseTemplate()
        {
            // hello following code configures PlayReady License Template using .NET classes
            // and returns hello XML string.

            //hello PlayReadyLicenseResponseTemplate class represents hello template for hello response sent back toohello end user.
            //It contains a field for a custom data string between hello license server and hello application
            //(may be useful for custom app logic) as well as a list of one or more license templates.
            PlayReadyLicenseResponseTemplate responseTemplate = new PlayReadyLicenseResponseTemplate();

            // hello PlayReadyLicenseTemplate class represents a license template for creating PlayReady licenses
            // toobe returned toohello end users.
            //It contains hello data on hello content key in hello license and any rights or restrictions toobe
            //enforced by hello PlayReady DRM runtime when using hello content key.
            PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();
            //Configure whether hello license is persistent (saved in persistent storage on hello client)
            //or non-persistent (only held in memory while hello player is using hello license).  
            licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

            // AllowTestDevices controls whether test devices can use hello license or not.  
            // If true, hello MinimumSecurityLevel property of hello license
            // is set too150.  If false (hello default), hello MinimumSecurityLevel property of hello license is set too2000.
            licenseTemplate.AllowTestDevices = true;

            // You can also configure hello Play Right in hello PlayReady license by using hello PlayReadyPlayRight class.
            // It grants hello user hello ability tooplayback hello content subject toohello zero or more restrictions
            // configured in hello license and on hello PlayRight itself (for playback specific policy).
            // Much of hello policy on hello PlayRight has toodo with output restrictions
            // which control hello types of outputs that hello content can be played over and
            // any restrictions that must be put in place when using a given output.
            // For example, if hello DigitalVideoOnlyContentRestriction is enabled,
            //then hello DRM runtime will only allow hello video toobe displayed over digital outputs
            //(analog video outputs won’t be allowed toopass hello content).

            //IMPORTANT: These types of restrictions can be very powerful but can also affect hello consumer experience.
            // If hello output protections are configured too restrictive,
            // hello content might be unplayable on some clients. For more information, see hello PlayReady Compliance Rules document.

            // For example:
            //licenseTemplate.PlayRight.AgcAndColorStripeRestriction = new AgcAndColorStripeRestriction(1);

            responseTemplate.LicenseTemplates.Add(licenseTemplate);

            return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
        }

        private static string ConfigureWidevineLicenseTemplate()
        {
            var template = new WidevineMessage
            {
            allowed_track_types = AllowedTrackTypes.SD_HD,
            content_key_specs = new[]
            {
                    new ContentKeySpecs
                    {
                    required_output_protection = new RequiredOutputProtection { hdcp = Hdcp.HDCP_NONE},
                    security_level = 1,
                    track_type = "SD"
                    }
                },
            policy_overrides = new
            {
                can_play = true,
                can_persist = true,
                can_renew = false
            }
            };

            string configuration = JsonConvert.SerializeObject(template);
            return configuration;
        }

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            // Get hello PlayReady license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);

            // GetKeyDeliveryUrl for Widevine attaches hello KID toohello URL.
            // For example: https://amsaccount1.keydelivery.mediaservices.windows.net/Widevine/?KID=268a6dcb-18c8-4648-8c95-f46429e4927c.  
            // hello WidevineBaseLicenseAcquisitionUrl (used below) also tells Dynamaic Encryption
            // tooappend /? KID =< keyId > toohello end of hello url when creating hello manifest.
            // As a result Widevine license acquisition URL will have KID appended twice,
            // so we need tooremove hello KID that in hello URL when we call GetKeyDeliveryUrl.

            Uri widevineUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.Widevine);
            UriBuilder uriBuilder = new UriBuilder(widevineUrl);
            uriBuilder.Query = String.Empty;
            widevineUrl = uriBuilder.Uri;

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                    {AssetDeliveryPolicyConfigurationKey.PlayReadyLicenseAcquisitionUrl, acquisitionUrl.ToString()},
                    {AssetDeliveryPolicyConfigurationKey.WidevineBaseLicenseAcquisitionUrl, widevineUrl.ToString()}

            };

            // In this case we only specify Dash streaming protocol in hello delivery policy,
            // All other protocols will be blocked from streaming.
            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryption,
            AssetDeliveryProtocol.Dash,
            assetDeliveryPolicyConfiguration);


            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        }

        /// <summary>
        /// Gets hello streaming origin locator.
        /// </summary>
        /// <param name="assets"></param>
        /// <returns></returns>
        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset.

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                         EndsWith(".ism")).
                         FirstOrDefault();

            // Create a 30-day readonly access policy.
            IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

            // Create a locator toohello streaming content on an origin.
            ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

            // Create a URL toohello manifest file.
            return originLocator.Path + assetFile.Name;
        }

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
        }

        static private byte[] GetRandomBuffer(int length)
        {
            var returnValue = new byte[length];

            using (var rng =
            new System.Security.Cryptography.RNGCryptoServiceProvider())
            {
            rng.GetBytes(returnValue);
            }

            return returnValue;
        }
        }
    }


## <a name="next-step"></a><span data-ttu-id="739cf-203">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="739cf-203">Next step</span></span>
<span data-ttu-id="739cf-204">Revise os roteiros de aprendizagem dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="739cf-204">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="739cf-205">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="739cf-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="739cf-206">Confira também</span><span class="sxs-lookup"><span data-stu-id="739cf-206">See also</span></span>
[<span data-ttu-id="739cf-207">CENC com DRM múltiplo e controle de acesso</span><span class="sxs-lookup"><span data-stu-id="739cf-207">CENC with Multi-DRM and Access Control</span></span>](media-services-cenc-with-multidrm-access-control.md)

[<span data-ttu-id="739cf-208">Configurar o empacotamento Widevine com AMS</span><span class="sxs-lookup"><span data-stu-id="739cf-208">Configure Widevine packaging with AMS</span></span>](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services)

[<span data-ttu-id="739cf-209">Anunciando os serviços de entrega de licenças do Google Widevine nos Serviços de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="739cf-209">Announcing Google Widevine license delivery services in Azure Media Services</span></span>](https://azure.microsoft.com/blog/announcing-general-availability-of-google-widevine-license-services/)
