---
title: "aaaUsing AES-128 dinâmico criptografia e a chave de serviço de entrega | Microsoft Docs"
description: "Serviços de mídia do Microsoft Azure permite que você toodeliver seu conteúdo criptografado com chaves de criptografia AES de 128 bits. Serviços de mídia também fornece o serviço de entrega de chave de saudação que oferece aos usuários tooauthorized de chaves de criptografia. Este tópico mostra como toodynamically criptografar com AES-128 e usar o serviço de distribuição de chaves de saudação."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 4d2c10af-9ee0-408f-899b-33fa4c1d89b9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: juliako
ms.openlocfilehash: cb1b413ec2ba79f7437464099cf72236ab93f312
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-aes-128-dynamic-encryption-and-key-delivery-service"></a><span data-ttu-id="4a010-105">Uso da criptografia dinâmica AES-128 e serviço de distribuição de chaves</span><span class="sxs-lookup"><span data-stu-id="4a010-105">Using AES-128 dynamic encryption and key delivery service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4a010-106">.NET</span><span class="sxs-lookup"><span data-stu-id="4a010-106">.NET</span></span>](media-services-protect-with-aes128.md)
> * [<span data-ttu-id="4a010-107">Java</span><span class="sxs-lookup"><span data-stu-id="4a010-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="4a010-108">PHP</span><span class="sxs-lookup"><span data-stu-id="4a010-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="4a010-109">Visão geral</span><span class="sxs-lookup"><span data-stu-id="4a010-109">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="4a010-110">Consulte [isso](https://channel9.msdn.com/Shows/Azure-Friday/Azure-Media-Services-Protecting-your-Media-Content-with-AES-Encryption) vídeo para obter uma visão geral de como tooprotect seu conteúdo de mídia com a criptografia AES.</span><span class="sxs-lookup"><span data-stu-id="4a010-110">See [this](https://channel9.msdn.com/Shows/Azure-Friday/Azure-Media-Services-Protecting-your-Media-Content-with-AES-Encryption) video for an overview of how tooprotect your Media Content with AES encryption.</span></span>
> 
> 

<span data-ttu-id="4a010-111">Serviços de mídia do Microsoft Azure permite que você toodeliver Http-Live-Streaming (HLS) e Smooth Streams criptografados com Advanced Encryption Standard (AES) (usando chaves de criptografia de 128 bits).</span><span class="sxs-lookup"><span data-stu-id="4a010-111">Microsoft Azure Media Services enables you toodeliver Http-Live-Streaming (HLS) and Smooth Streams encrypted with Advanced Encryption Standard (AES) (using 128-bit encryption keys).</span></span> <span data-ttu-id="4a010-112">Serviços de mídia também fornece o serviço de entrega de chave de saudação que oferece aos usuários tooauthorized de chaves de criptografia.</span><span class="sxs-lookup"><span data-stu-id="4a010-112">Media Services also provides hello Key Delivery service that delivers encryption keys tooauthorized users.</span></span> <span data-ttu-id="4a010-113">Se você quiser para serviços de mídia tooencrypt um ativo, você precisa tooassociate uma chave de criptografia com ativo hello e também configurar políticas de autorização para a chave de saudação.</span><span class="sxs-lookup"><span data-stu-id="4a010-113">If you want for Media Services tooencrypt an asset, you need tooassociate an encryption key with hello asset and also configure authorization policies for hello key.</span></span> <span data-ttu-id="4a010-114">Quando um fluxo é solicitado por um player, o Media Services usa Olá especificado toodynamically chave criptografar seu conteúdo usando a criptografia AES.</span><span class="sxs-lookup"><span data-stu-id="4a010-114">When a stream is requested by a player, Media Services uses hello specified key toodynamically encrypt your content using AES encryption.</span></span> <span data-ttu-id="4a010-115">fluxo de saudação toodecrypt, player Olá solicitar chave Olá do serviço de distribuição de chaves de saudação.</span><span class="sxs-lookup"><span data-stu-id="4a010-115">toodecrypt hello stream, hello player will request hello key from hello key delivery service.</span></span> <span data-ttu-id="4a010-116">toodecide ou não usuário Olá é autorizado chave de saudação tooget, serviço Olá avalia as políticas de autorização de saudação que você especificou para a chave de saudação.</span><span class="sxs-lookup"><span data-stu-id="4a010-116">toodecide whether or not hello user is authorized tooget hello key, hello service evaluates hello authorization policies that you specified for hello key.</span></span>

<span data-ttu-id="4a010-117">Os serviços de mídia oferecem suporte a várias maneiras de autenticar os usuários que fazem solicitações de chave.</span><span class="sxs-lookup"><span data-stu-id="4a010-117">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="4a010-118">Olá política de autorização da chave de conteúdo pode ter uma ou mais restrições de autorização: abrir ou restrição de token.</span><span class="sxs-lookup"><span data-stu-id="4a010-118">hello content key authorization policy could have one or more authorization restrictions: open or token restriction.</span></span> <span data-ttu-id="4a010-119">política de restrição de token de saudação deve ser acompanhada por um token emitido por um Token STS (serviço seguro).</span><span class="sxs-lookup"><span data-stu-id="4a010-119">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="4a010-120">Serviços de mídia oferece suporte a tokens no hello [Simple Web Tokens](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) formato (SWT) e [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) formato (JWT).</span><span class="sxs-lookup"><span data-stu-id="4a010-120">Media Services supports tokens in hello [Simple Web Tokens](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (SWT) format and [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT) format.</span></span> <span data-ttu-id="4a010-121">Para obter mais informações, consulte [configurar política de autorização da chave de saudação conteúdo](media-services-protect-with-aes128.md#configure_key_auth_policy).</span><span class="sxs-lookup"><span data-stu-id="4a010-121">For more information, see [Configure hello content key’s authorization policy](media-services-protect-with-aes128.md#configure_key_auth_policy).</span></span>

<span data-ttu-id="4a010-122">tootake vantagem da criptografia dinâmica, você precisa toohave um ativo que contenha um conjunto de arquivos MP4 com múltiplas taxas de bits ou arquivos de origem de Smooth Streaming de várias taxas de bits.</span><span class="sxs-lookup"><span data-stu-id="4a010-122">tootake advantage of dynamic encryption, you need toohave an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="4a010-123">Você também precisa tooconfigure política de entrega de saudação para ativo hello (descrito posteriormente neste tópico).</span><span class="sxs-lookup"><span data-stu-id="4a010-123">You also need tooconfigure hello delivery policy for hello asset (described later in this topic).</span></span> <span data-ttu-id="4a010-124">Em seguida, com base no formato de saudação especificado na URL de streaming de hello, Olá Streaming sob demanda servidor garantirá que fluxo Olá é fornecido no protocolo de saudação escolhida.</span><span class="sxs-lookup"><span data-stu-id="4a010-124">Then, based on hello format specified in hello streaming URL, hello On-Demand Streaming server will ensure that hello stream is delivered in hello protocol you have chosen.</span></span> <span data-ttu-id="4a010-125">Como resultado, você só precisa toostore e pagamento para arquivos de saudação em único formato de armazenamento e serviços de mídia criará e enviará a resposta apropriada hello, com base nas solicitações de um cliente.</span><span class="sxs-lookup"><span data-stu-id="4a010-125">As a result, you only need toostore and pay for hello files in single storage format and Media Services service will build and serve hello appropriate response based on requests from a client.</span></span>

<span data-ttu-id="4a010-126">Este tópico seria útil toodevelopers que trabalham em aplicativos que distribuem mídia protegida.</span><span class="sxs-lookup"><span data-stu-id="4a010-126">This topic would be useful toodevelopers that work on applications that deliver protected media.</span></span> <span data-ttu-id="4a010-127">tópico de saudação mostra como tooconfigure Olá o serviço de entrega de chave com políticas de autorização para que somente clientes autorizados recebam as chaves de criptografia de saudação.</span><span class="sxs-lookup"><span data-stu-id="4a010-127">hello topic shows you how tooconfigure hello key delivery service with authorization policies so that only authorized clients could receive hello encryption keys.</span></span> <span data-ttu-id="4a010-128">Ele também mostra como criptografia dinâmica toouse.</span><span class="sxs-lookup"><span data-stu-id="4a010-128">It also shows how toouse dynamic encryption.</span></span>


## <a name="aes-128-dynamic-encryption-and-key-delivery-service-workflow"></a><span data-ttu-id="4a010-129">Criptografia dinâmica AES-128 e fluxo de trabalho de serviço de distribuição de chaves</span><span class="sxs-lookup"><span data-stu-id="4a010-129">AES-128 Dynamic Encryption and Key Delivery Service Workflow</span></span>

<span data-ttu-id="4a010-130">Olá seguem etapas gerais que você precisaria tooperform ao criptografar seus ativos com AES, usando o serviço de distribuição de chaves de serviços de mídia hello e também usar criptografia dinâmica.</span><span class="sxs-lookup"><span data-stu-id="4a010-130">hello following are general steps that you would need tooperform when encrypting your assets with AES, using hello Media Services key delivery service, and also using dynamic encryption.</span></span>

1. <span data-ttu-id="4a010-131">[Criar um ativo e carregar arquivos no ativo Olá](media-services-protect-with-aes128.md#create_asset).</span><span class="sxs-lookup"><span data-stu-id="4a010-131">[Create an asset and upload files into hello asset](media-services-protect-with-aes128.md#create_asset).</span></span>
2. <span data-ttu-id="4a010-132">[Codificar Olá ativo que contém a saudação arquivo toohello taxa de bits adaptável MP4 conjunto](media-services-protect-with-aes128.md#encode_asset).</span><span class="sxs-lookup"><span data-stu-id="4a010-132">[Encode hello asset containing hello file toohello adaptive bitrate MP4 set](media-services-protect-with-aes128.md#encode_asset).</span></span>
3. <span data-ttu-id="4a010-133">[Criar uma chave de conteúdo e associá-lo com ativo Olá codificado](media-services-protect-with-aes128.md#create_contentkey).</span><span class="sxs-lookup"><span data-stu-id="4a010-133">[Create a content key and associate it with hello encoded asset](media-services-protect-with-aes128.md#create_contentkey).</span></span> <span data-ttu-id="4a010-134">Nos serviços de mídia, a chave de conteúdo de saudação contém chave de criptografia do ativo hello.</span><span class="sxs-lookup"><span data-stu-id="4a010-134">In Media Services, hello content key contains hello asset’s encryption key.</span></span>
4. <span data-ttu-id="4a010-135">[Configurar política de autorização da chave de saudação conteúdo](media-services-protect-with-aes128.md#configure_key_auth_policy).</span><span class="sxs-lookup"><span data-stu-id="4a010-135">[Configure hello content key’s authorization policy](media-services-protect-with-aes128.md#configure_key_auth_policy).</span></span> <span data-ttu-id="4a010-136">política de autorização da chave de conteúdo Olá deve ser configurada por você e cliente Olá para Olá conteúdo toobe chave toohello entregue cliente.</span><span class="sxs-lookup"><span data-stu-id="4a010-136">hello content key authorization policy must be configured by you and met by hello client in order for hello content key toobe delivered toohello client.</span></span>
5. <span data-ttu-id="4a010-137">[Configurar a política de entrega Olá para um ativo](media-services-protect-with-aes128.md#configure_asset_delivery_policy).</span><span class="sxs-lookup"><span data-stu-id="4a010-137">[Configure hello delivery policy for an asset](media-services-protect-with-aes128.md#configure_asset_delivery_policy).</span></span> <span data-ttu-id="4a010-138">configuração de política de entrega de saudação inclui: URL de aquisição e o vetor de inicialização (IV) de chave (AES 128 exigem hello mesmo toobe de IV fornecido ao criptografar e descriptografar), protocolo de entrega (por exemplo, MPEG DASH, HLS, Smooth Streaming ou todos), Olá tipo de criptografia dinâmica (por exemplo, envelope ou nenhuma criptografia dinâmica).</span><span class="sxs-lookup"><span data-stu-id="4a010-138">hello delivery policy configuration includes: key acquisition URL and Initialization Vector (IV) (AES 128 requires hello same IV toobe supplied when encrypting and decrypting), delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all), hello type of dynamic encryption (for example, envelope or no dynamic encryption).</span></span>

    <span data-ttu-id="4a010-139">Você pode aplicar o protocolo de tooeach política diferente em Olá mesmo ativo.</span><span class="sxs-lookup"><span data-stu-id="4a010-139">You could apply different policy tooeach protocol on hello same asset.</span></span> <span data-ttu-id="4a010-140">Por exemplo, você pode aplicar PlayReady criptografia tooSmooth/DASH e Envelope AES tooHLS.</span><span class="sxs-lookup"><span data-stu-id="4a010-140">For example, you could apply PlayReady encryption tooSmooth/DASH and AES Envelope tooHLS.</span></span> <span data-ttu-id="4a010-141">Todos os protocolos que não estão definidos em uma política de entrega (por exemplo, você adiciona uma única política que só especifica HLS como protocolo de saudação) serão impedidos de streaming.</span><span class="sxs-lookup"><span data-stu-id="4a010-141">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as hello protocol) will be blocked from streaming.</span></span> <span data-ttu-id="4a010-142">Olá toothis de exceção é se você não tiver nenhuma política de entrega de ativo definida.</span><span class="sxs-lookup"><span data-stu-id="4a010-142">hello exception toothis is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="4a010-143">Em seguida, todos os protocolos poderão ser em Olá clara.</span><span class="sxs-lookup"><span data-stu-id="4a010-143">Then, all protocols will be allowed in hello clear.</span></span>

6. <span data-ttu-id="4a010-144">[Criar um localizador OnDemand](media-services-protect-with-aes128.md#create_locator) em ordem tooget uma URL de streaming.</span><span class="sxs-lookup"><span data-stu-id="4a010-144">[Create an OnDemand locator](media-services-protect-with-aes128.md#create_locator) in order tooget a streaming URL.</span></span>

<span data-ttu-id="4a010-145">Olá tópico também mostra [como um aplicativo cliente pode solicitar uma chave de serviço de distribuição de chaves Olá](media-services-protect-with-aes128.md#client_request).</span><span class="sxs-lookup"><span data-stu-id="4a010-145">hello topic also shows [how a client application can request a key from hello key delivery service](media-services-protect-with-aes128.md#client_request).</span></span>

<span data-ttu-id="4a010-146">Você encontrará um .NET completo [exemplo](media-services-protect-with-aes128.md#example) final Olá Olá tópico.</span><span class="sxs-lookup"><span data-stu-id="4a010-146">You will find a complete .NET [example](media-services-protect-with-aes128.md#example) at hello end of hello topic.</span></span>

<span data-ttu-id="4a010-147">Olá a imagem a seguir demonstra o fluxo de trabalho de saudação descrito acima.</span><span class="sxs-lookup"><span data-stu-id="4a010-147">hello following image demonstrates hello workflow described above.</span></span> <span data-ttu-id="4a010-148">Aqui o token de saudação é usado para autenticação.</span><span class="sxs-lookup"><span data-stu-id="4a010-148">Here hello token is used for authentication.</span></span>

![Proteger com o AES-128](./media/media-services-content-protection-overview/media-services-content-protection-with-aes.png)

<span data-ttu-id="4a010-150">restante deste tópico Olá fornece explicações detalhadas, exemplos de código e tootopics links que mostram como tooachieve Olá as tarefas descritas acima.</span><span class="sxs-lookup"><span data-stu-id="4a010-150">hello rest of this topic provides detailed explanations, code examples, and links tootopics that show you how tooachieve hello tasks described above.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="4a010-151">Limitações atuais</span><span class="sxs-lookup"><span data-stu-id="4a010-151">Current limitations</span></span>
<span data-ttu-id="4a010-152">Se você adicionar ou atualizar a política de fornecimento do ativo, você deve excluir um localizador existente (se houver) e criar um novo localizador.</span><span class="sxs-lookup"><span data-stu-id="4a010-152">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>

## <span data-ttu-id="4a010-153"><a id="create_asset"></a>Criar um ativo e carregar arquivos no ativo de saudação</span><span class="sxs-lookup"><span data-stu-id="4a010-153"><a id="create_asset"></a>Create an asset and upload files into hello asset</span></span>
<span data-ttu-id="4a010-154">Em ordem toomanage, codificar e transmitir seus vídeos, primeiro você deve carregar o conteúdo nos serviços de mídia do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="4a010-154">In order toomanage, encode, and stream your videos, you must first upload your content into Microsoft Azure Media Services.</span></span> <span data-ttu-id="4a010-155">Uma vez carregado, seu conteúdo é armazenado com segurança na nuvem Olá para processamento e streaming.</span><span class="sxs-lookup"><span data-stu-id="4a010-155">Once uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span> 

<span data-ttu-id="4a010-156">Para obter informações detalhadas, consulte [Carregar arquivos em uma conta dos Serviços de Mídia](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="4a010-156">For detailed information, see [Upload Files into a Media Services account](media-services-dotnet-upload-files.md).</span></span>

## <span data-ttu-id="4a010-157"><a id="encode_asset"></a>Codificar Olá ativo contendo Olá arquivo toohello taxa de bits adaptável que MP4 set</span><span class="sxs-lookup"><span data-stu-id="4a010-157"><a id="encode_asset"></a>Encode hello asset containing hello file toohello adaptive bitrate MP4 set</span></span>
<span data-ttu-id="4a010-158">Com criptografia dinâmica, tudo o que você precisa é toocreate um ativo que contenha um conjunto de arquivos MP4 com múltiplas taxas de bits ou arquivos de origem de Smooth Streaming de várias taxas de bits.</span><span class="sxs-lookup"><span data-stu-id="4a010-158">With dynamic encryption all you need is toocreate an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="4a010-159">Em seguida, com base no formato de saudação especificado no manifesto de saudação ou solicitação de fragmento, Olá sob demanda de Streaming server irá garantir que você receba o fluxo de saudação no protocolo hello escolhido.</span><span class="sxs-lookup"><span data-stu-id="4a010-159">Then, based on hello specified format in hello manifest or fragment request, hello On-Demand Streaming server will ensure that you receive hello stream in hello protocol you have chosen.</span></span> <span data-ttu-id="4a010-160">Como resultado, você só precisa toostore e pagamento para arquivos de saudação em único formato de armazenamento e serviços de mídia criará e enviará a resposta apropriada hello, com base nas solicitações de um cliente.</span><span class="sxs-lookup"><span data-stu-id="4a010-160">As a result, you only need toostore and pay for hello files in single storage format and Media Services service will build and serve hello appropriate response based on requests from a client.</span></span> <span data-ttu-id="4a010-161">Para obter mais informações, consulte Olá [visão geral do empacotamento dinâmico](media-services-dynamic-packaging-overview.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="4a010-161">For more information, see hello [Dynamic Packaging Overview](media-services-dynamic-packaging-overview.md) topic.</span></span>

>[!NOTE]
><span data-ttu-id="4a010-162">Quando sua conta AMS é criada um **padrão** ponto de extremidade de streaming é adicionada conta tooyour Olá **parado** estado.</span><span class="sxs-lookup"><span data-stu-id="4a010-162">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="4a010-163">toostart streaming seu conteúdo e execute aproveitar o empacotamento dinâmico e criptografia dinâmica, Olá ponto de extremidade de streaming do qual você deseja toostream conteúdo tem toobe em Olá **executando** estado.</span><span class="sxs-lookup"><span data-stu-id="4a010-163">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 
>
><span data-ttu-id="4a010-164">Além disso, o empacotamento dinâmico capaz de toouse toobe e criptografia dinâmica seu ativo deve conter um conjunto de MP4s de taxa de bits adaptável ou arquivos de Smooth Streaming de taxa de bits adaptável.</span><span class="sxs-lookup"><span data-stu-id="4a010-164">Also, toobe able toouse dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>

<span data-ttu-id="4a010-165">Para obter instruções sobre como tooencode, consulte [como tooencode um ativo usando o codificador de mídia padrão](media-services-dotnet-encode-with-media-encoder-standard.md).</span><span class="sxs-lookup"><span data-stu-id="4a010-165">For instructions on how tooencode, see [How tooencode an asset using Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>

## <span data-ttu-id="4a010-166"><a id="create_contentkey"></a>Criar uma chave de conteúdo e associá-lo com ativo Olá codificado</span><span class="sxs-lookup"><span data-stu-id="4a010-166"><a id="create_contentkey"></a>Create a content key and associate it with hello encoded asset</span></span>
<span data-ttu-id="4a010-167">Nos serviços de mídia, a chave de conteúdo de saudação contém chave Olá que você deseja tooencrypt um ativo com.</span><span class="sxs-lookup"><span data-stu-id="4a010-167">In Media Services, hello content key contains hello key that you want tooencrypt an asset with.</span></span>

<span data-ttu-id="4a010-168">Para obter informações detalhadas, consulte [Criar chave de conteúdo](media-services-dotnet-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="4a010-168">For detailed information, see [Create content key](media-services-dotnet-create-contentkey.md).</span></span>

## <span data-ttu-id="4a010-169"><a id="configure_key_auth_policy"></a>Configurar política de autorização da chave de saudação conteúdo</span><span class="sxs-lookup"><span data-stu-id="4a010-169"><a id="configure_key_auth_policy"></a>Configure hello content key’s authorization policy</span></span>
<span data-ttu-id="4a010-170">Os serviços de mídia oferecem suporte a várias maneiras de autenticar os usuários que fazem solicitações de chave.</span><span class="sxs-lookup"><span data-stu-id="4a010-170">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="4a010-171">política de autorização da chave de conteúdo Olá deve ser configurada por você e Olá cliente (player) em ordem para Olá toobe chave entregue toohello cliente.</span><span class="sxs-lookup"><span data-stu-id="4a010-171">hello content key authorization policy must be configured by you and met by hello client (player) in order for hello key toobe delivered toohello client.</span></span> <span data-ttu-id="4a010-172">Olá política de autorização da chave de conteúdo pode ter uma ou mais restrições de autorização: aberta, restrição de token ou restrição de IP.</span><span class="sxs-lookup"><span data-stu-id="4a010-172">hello content key authorization policy could have one or more authorization restrictions: open, token restriction, or IP restriction.</span></span>

<span data-ttu-id="4a010-173">Para obter informações detalhadas, consulte [Configurar política de autorização de chave de conteúdo](media-services-dotnet-configure-content-key-auth-policy.md).</span><span class="sxs-lookup"><span data-stu-id="4a010-173">For detailed information, see [Configure Content Key Authorization Policy](media-services-dotnet-configure-content-key-auth-policy.md).</span></span>

## <span data-ttu-id="4a010-174"><a id="configure_asset_delivery_policy"></a>Configurar política de entrega de ativos</span><span class="sxs-lookup"><span data-stu-id="4a010-174"><a id="configure_asset_delivery_policy"></a>Configure asset delivery policy</span></span>
<span data-ttu-id="4a010-175">Configure a política de distribuição de saudação para seu ativo.</span><span class="sxs-lookup"><span data-stu-id="4a010-175">Configure hello delivery policy for your asset.</span></span> <span data-ttu-id="4a010-176">Algumas coisas que Olá a configuração de política de entrega de ativos inclui:</span><span class="sxs-lookup"><span data-stu-id="4a010-176">Some things that hello asset delivery policy configuration includes:</span></span>

* <span data-ttu-id="4a010-177">Olá URL de aquisição de chave.</span><span class="sxs-lookup"><span data-stu-id="4a010-177">hello Key acquisition URL.</span></span> 
* <span data-ttu-id="4a010-178">Olá toouse de vetor de inicialização (IV) para criptografia de envelope hello.</span><span class="sxs-lookup"><span data-stu-id="4a010-178">hello Initialization Vector (IV) toouse for hello envelope encryption.</span></span> <span data-ttu-id="4a010-179">AES 128 exigem Olá mesmo toobe de IV fornecido ao criptografar e descriptografar.</span><span class="sxs-lookup"><span data-stu-id="4a010-179">AES 128 requires hello same IV toobe supplied when encrypting and decrypting.</span></span> 
* <span data-ttu-id="4a010-180">Olá ativo protocolo de entrega (por exemplo, MPEG DASH, HLS, Smooth Streaming ou todos).</span><span class="sxs-lookup"><span data-stu-id="4a010-180">hello asset delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all).</span></span>
* <span data-ttu-id="4a010-181">tipo de saudação de criptografia dinâmica (por exemplo, envelope AES) ou nenhuma criptografia dinâmica.</span><span class="sxs-lookup"><span data-stu-id="4a010-181">hello type of dynamic encryption (for example, AES envelope) or no dynamic encryption.</span></span> 

<span data-ttu-id="4a010-182">Para obter informações detalhadas, consulte [Configurar política de entrega de ativos ](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="4a010-182">For detailed information, see [Configure asset delivery policy ](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <span data-ttu-id="4a010-183"><a id="create_locator"></a>Criar um OnDemand streaming localizador de ordem tooget uma URL de streaming</span><span class="sxs-lookup"><span data-stu-id="4a010-183"><a id="create_locator"></a>Create an OnDemand streaming locator in order tooget a streaming URL</span></span>
<span data-ttu-id="4a010-184">Você precisará tooprovide seu usuário com hello streaming URL para Smooth, DASH ou HLS.</span><span class="sxs-lookup"><span data-stu-id="4a010-184">You will need tooprovide your user with hello streaming URL for Smooth, DASH or HLS.</span></span>

> [!NOTE]
> <span data-ttu-id="4a010-185">Se você adicionar ou atualizar a política de fornecimento do ativo, você deve excluir um localizador existente (se houver) e criar um novo localizador.</span><span class="sxs-lookup"><span data-stu-id="4a010-185">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
> 
> 

<span data-ttu-id="4a010-186">Para obter instruções sobre como toopublish um ativo e compilar uma URL de streaming, consulte [construir uma URL de streaming](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="4a010-186">For instructions on how toopublish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="get-a-test-token"></a><span data-ttu-id="4a010-187">Obter um token de teste</span><span class="sxs-lookup"><span data-stu-id="4a010-187">Get a test token</span></span>
<span data-ttu-id="4a010-188">Obtenha um teste de token com base na restrição de token de saudação que foi usada para a política de autorização da chave de saudação.</span><span class="sxs-lookup"><span data-stu-id="4a010-188">Get a test token based on hello token restriction that was used for hello key authorization policy.</span></span>

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate = 
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on hello data in hello given TokenRestrictionTemplate.
    //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
    //so you have tooadd it in front of hello token string. 
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate);
    Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);

<span data-ttu-id="4a010-189">Você pode usar o hello [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tootest seu fluxo.</span><span class="sxs-lookup"><span data-stu-id="4a010-189">You can use hello [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tootest your stream.</span></span>

## <span data-ttu-id="4a010-190"><a id="client_request"></a>Como o seu cliente pode solicitar uma chave de serviço de distribuição de chaves Olá?</span><span class="sxs-lookup"><span data-stu-id="4a010-190"><a id="client_request"></a>How can your client request a key from hello key delivery service?</span></span>
<span data-ttu-id="4a010-191">Na etapa anterior de saudação, é construída Olá URL que aponta o arquivo de manifesto tooa.</span><span class="sxs-lookup"><span data-stu-id="4a010-191">In hello previous step, you constructed hello URL that points tooa manifest file.</span></span> <span data-ttu-id="4a010-192">Seu cliente precisa tooextract Olá informações necessárias Olá streaming de arquivos de manifesto na ordem toomake um serviço de entrega de chave de toohello de solicitação.</span><span class="sxs-lookup"><span data-stu-id="4a010-192">Your client needs tooextract hello necessary information from hello streaming manifest files in order toomake a request toohello key delivery service.</span></span>

### <a name="manifest-files"></a><span data-ttu-id="4a010-193">Arquivos de manifesto</span><span class="sxs-lookup"><span data-stu-id="4a010-193">Manifest files</span></span>
<span data-ttu-id="4a010-194">cliente de saudação precisa tooextract Olá URL (que também contém a chave de conteúdo Id (kid)) valor do arquivo de manifesto hello.</span><span class="sxs-lookup"><span data-stu-id="4a010-194">hello client needs tooextract hello URL (that also contains content key Id (kid)) value from hello manifest file.</span></span> <span data-ttu-id="4a010-195">cliente Olá tente tooget chave de criptografia de saudação do serviço de distribuição de chaves de saudação.</span><span class="sxs-lookup"><span data-stu-id="4a010-195">hello client will then try tooget hello encryption key from hello key delivery service.</span></span> <span data-ttu-id="4a010-196">Olá cliente também precisa tooextract Olá IV valor e use-lo para descriptografar stream.hello Olá trecho de código a seguir mostra Olá <Protection> elemento do manifesto de Smooth Streaming hello.</span><span class="sxs-lookup"><span data-stu-id="4a010-196">hello client also needs tooextract hello IV value and use it do decrypt hello stream.hello following snippet shows hello <Protection> element of hello Smooth Streaming manifest.</span></span>

    <Protection>
      <ProtectionHeader SystemID="B47B251A-2409-4B42-958E-08DBAE7B4EE9">
        <ContentProtection xmlns:sea="urn:mpeg:dash:schema:sea:2012" schemeIdUri="urn:mpeg:dash:sea:2012">
          <sea:SegmentEncryption schemeIdUri="urn:mpeg:dash:sea:aes128-cbc:2013"/>
          <sea:KeySystem keySystemUri="urn:mpeg:dash:sea:keysys:http:2013"/>
          <sea:CryptoPeriod IV="0xD7D7D7D7D7D7D7D7D7D7D7D7D7D7D7D7" 
                            keyUriTemplate="https://wamsbayclus001kd-hs.cloudapp.net/HlsHandler.ashx?
                                            kid=da3813af-55e6-48e7-aa9f-a4d6031f7b4d"/>
        </ContentProtection>
      </ProtectionHeader>
    </Protection>

<span data-ttu-id="4a010-197">No caso de saudação do HLS, o manifesto de raiz de saudação é dividido em arquivos de segmento.</span><span class="sxs-lookup"><span data-stu-id="4a010-197">In hello case of HLS, hello root manifest is broken into segment files.</span></span> 

<span data-ttu-id="4a010-198">Por exemplo, o manifesto de raiz de saudação é: http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/manifest(format=m3u8-aapl) que contém uma lista de nomes de arquivo de segmento.</span><span class="sxs-lookup"><span data-stu-id="4a010-198">For example, hello root manifest is: http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/manifest(format=m3u8-aapl) and it contains a list of segment file names.</span></span>

    . . . 
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=630133,RESOLUTION=424x240,CODECS="avc1.4d4015,mp4a.40.2",AUDIO="audio"
    QualityLevels(514369)/Manifest(video,format=m3u8-aapl)
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=965441,RESOLUTION=636x356,CODECS="avc1.4d401e,mp4a.40.2",AUDIO="audio"
    QualityLevels(842459)/Manifest(video,format=m3u8-aapl)
    …

<span data-ttu-id="4a010-199">Se você abrir um dos arquivos de segmento Olá no editor de texto (por exemplo, http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/QualityLevels(514369)/Manifest(video,format=m3u8-aapl), it should conter #EXT-X-chave que indica que esse arquivo hello está criptografado.</span><span class="sxs-lookup"><span data-stu-id="4a010-199">If you open one of hello segment files in text editor (for example, http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/QualityLevels(514369)/Manifest(video,format=m3u8-aapl), it should contain #EXT-X-KEY which indicates that hello file is encrypted.</span></span>

    #EXTM3U
    #EXT-X-VERSION:4
    #EXT-X-ALLOW-CACHE:NO
    #EXT-X-MEDIA-SEQUENCE:0
    #EXT-X-TARGETDURATION:9
    #EXT-X-KEY:METHOD=AES-128,
    URI="https://wamsbayclus001kd-hs.cloudapp.net/HlsHandler.ashx?
         kid=da3813af-55e6-48e7-aa9f-a4d6031f7b4d",
            IV=0XD7D7D7D7D7D7D7D7D7D7D7D7D7D7D7D7
    #EXT-X-PROGRAM-DATE-TIME:1970-01-01T00:00:00.000+00:00
    #EXTINF:8.425708,no-desc
    Fragments(video=0,format=m3u8-aapl)
    #EXT-X-ENDLIST

>[!NOTE] 
><span data-ttu-id="4a010-200">Se você estiver planejando tooplay um AES criptografado HLS no Safari, consulte [este blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span><span class="sxs-lookup"><span data-stu-id="4a010-200">If you are planning tooplay an AES encrypted HLS in Safari, see [this blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span></span>

### <a name="request-hello-key-from-hello-key-delivery-service"></a><span data-ttu-id="4a010-201">Solicitar a chave de saudação do serviço de distribuição de chaves Olá</span><span class="sxs-lookup"><span data-stu-id="4a010-201">Request hello key from hello key delivery service</span></span>

<span data-ttu-id="4a010-202">Olá código a seguir mostra como toosend toohello uma solicitação do Media Services chave de serviço de entrega usando uma Uri (que foi extraído do manifesto de saudação) de entrega de chave e um token (Este tópico não fala sobre como tooget Simple Web Tokens de um serviço de Token seguro).</span><span class="sxs-lookup"><span data-stu-id="4a010-202">hello following code shows how toosend a request toohello Media Services key delivery service using a key delivery Uri (that was extracted from hello manifest) and a token (this topic does not talk about how tooget Simple Web Tokens from a Secure Token Service).</span></span>

    private byte[] GetDeliveryKey(Uri keyDeliveryUri, string token)
    {
        HttpWebRequest request = (HttpWebRequest)WebRequest.Create(keyDeliveryUri);

        request.Method = "POST";
        request.ContentType = "text/xml";
        if (!string.IsNullOrEmpty(token))
        {
            request.Headers[AuthorizationHeader] = token;
        }
        request.ContentLength = 0;

        var response = request.GetResponse();

        var stream = response.GetResponseStream();
        if (stream == null)
        {
            throw new NullReferenceException("Response stream is null");
        }

        var buffer = new byte[256];
        var length = 0;
        while (stream.CanRead && length <= buffer.Length)
        {
            var nexByte = stream.ReadByte();
            if (nexByte == -1)
            {
                break;
            }
            buffer[length] = (byte)nexByte;
            length++;
        }
        response.Close();

        // AES keys must be exactly 16 bytes (128 bits).
        var key = new byte[length];
        Array.Copy(buffer, key, length);
        return key;
    }

## <a name="protect-your-content-with-aes-128-using-net"></a><span data-ttu-id="4a010-203">Proteger o conteúdo com o AES-128 usando o .NET</span><span class="sxs-lookup"><span data-stu-id="4a010-203">Protect your content with AES-128 using .NET</span></span>

### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="4a010-204">Criar e configurar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4a010-204">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="4a010-205">Configurar seu ambiente de desenvolvimento e preencher o arquivo App. config de saudação com informações de conexão, conforme descrito em [desenvolvimento de serviços de mídia com o .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="4a010-205">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="4a010-206">Adicionar Olá elementos a seguir muito**appSettings** definido no seu arquivo App. config:</span><span class="sxs-lookup"><span data-stu-id="4a010-206">Add hello following elements too**appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

### <span data-ttu-id="4a010-207"><a id="example"></a>Exemplo</span><span class="sxs-lookup"><span data-stu-id="4a010-207"><a id="example"></a>Example</span></span>

<span data-ttu-id="4a010-208">Substitua o código de saudação no arquivo Program.cs pelo código Olá mostrado nesta seção.</span><span class="sxs-lookup"><span data-stu-id="4a010-208">Overwrite hello code in your Program.cs file with hello code shown in this section.</span></span>
 
>[!NOTE]
><span data-ttu-id="4a010-209">Há um limite de 1.000.000 políticas para diferentes políticas de AMS (por exemplo, para política de Localizador ou ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="4a010-209">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="4a010-210">Você deve usar Olá Olá a mesma ID de política se você estiver usando sempre mesmo dias acesso permissões, por exemplo, as políticas para localizadores são tooremain desejado no local por um longo período (políticas de carregamento não).</span><span class="sxs-lookup"><span data-stu-id="4a010-210">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="4a010-211">Para obter mais informações, consulte [este](media-services-dotnet-manage-entities.md#limit-access-policies) tópico.</span><span class="sxs-lookup"><span data-stu-id="4a010-211">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="4a010-212">Certifique-se de que variáveis de tooupdate toopoint toofolders onde se encontram os arquivos de entrada.</span><span class="sxs-lookup"><span data-stu-id="4a010-212">Make sure tooupdate variables toopoint toofolders where your input files are located.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Security.Cryptography;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;

    namespace AESDynamicEncryptionAndKeyDeliverySvc
    {
        class Program
        {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // A Uri describing hello issuer of hello token.  
        // Must match hello value in hello token for hello token toobe considered valid.
        private static readonly Uri _sampleIssuer =
            new Uri(ConfigurationManager.AppSettings["Issuer"]);
        // hello Audience or Scope of hello token.  
        // Must match hello value in hello token for hello token toobe considered valid.
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

            IContentKey key = CreateEnvelopeTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
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

            // Generate a test token based on hello data in hello given TokenRestrictionTemplate.
            // Note, you need toopass hello key id Guid because we specified 
            // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);

            //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
            //so you have tooadd it in front of hello token string. 
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey);
            Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            // You can use hello bit.ly/aesplayer Flash player tootest hello URL 
            // (with open authorization policy). 
            // Paste hello URL and click hello Update button tooplay hello video. 
            //
            string URL = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Smooth Streaming Url: {0}/manifest", URL);
            Console.WriteLine();
            Console.WriteLine("HLS Url: {0}/manifest(format=m3u8-aapl)", URL);
            Console.WriteLine();

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
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.StorageEncrypted);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);


            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");
            // Get a media processor reference, and pass tooit hello name of hello 
            // processor toouse for hello specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with hello encoding details, using a string preset.
            // In this case "Adaptive Streaming" preset is used.
            ITask task = job.Tasks.AddNew("My encoding task",
            processor,
            "Adaptive Streaming",
            TaskOptions.None);

            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);
            // Add an output asset toocontain hello results of hello job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means hello output asset is not encrypted. 
            task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }

        private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
            ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }

        static public IContentKey CreateEnvelopeTypeContentKey(IAsset asset)
        {
            // Create envelope encryption content key
            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                keyId,
                contentKey,
                "ContentKey",
                ContentKeyType.EnvelopeEncryption);

            // Associate hello key with hello asset.
            asset.ContentKeys.Add(key);

            return key;
        }

        static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
        {
            // Create ContentKeyAuthorizationPolicy with Open restrictions 
            // and create authorization policy             
            IContentKeyAuthorizationPolicy policy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Open Authorization Policy").Result;

            List<ContentKeyAuthorizationPolicyRestriction> restrictions =
            new List<ContentKeyAuthorizationPolicyRestriction>();

            ContentKeyAuthorizationPolicyRestriction restriction =
            new ContentKeyAuthorizationPolicyRestriction
            {
            Name = "HLS Open Authorization Policy",
            KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
            Requirements = null // no requirements needed for HLS
        };

            restrictions.Add(restriction);

            IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
            "policy",
            ContentKeyDeliveryType.BaselineHttp,
            restrictions,
            "");

            policy.Options.Add(policyOption);

            // Add ContentKeyAutorizationPolicy tooContentKey
            contentKey.AuthorizationPolicyId = policy.Id;
            IContentKey updatedKey = contentKey.UpdateAsync().Result;
            Console.WriteLine("Adding Key tooAsset: Key ID is " + updatedKey.Id);
        }

        public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
        {
            string tokenTemplateString = GenerateTokenRequirements();

            IContentKeyAuthorizationPolicy policy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("HLS token restricted authorization policy").Result;

            List<ContentKeyAuthorizationPolicyRestriction> restrictions =
            new List<ContentKeyAuthorizationPolicyRestriction>();

            ContentKeyAuthorizationPolicyRestriction restriction =
            new ContentKeyAuthorizationPolicyRestriction
            {
                Name = "Token Authorization Policy",
                KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                Requirements = tokenTemplateString
            };

            restrictions.Add(restriction);

            //You could have multiple options 
            IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
            "Token option for HLS",
            ContentKeyDeliveryType.BaselineHttp,
            restrictions,
            null  // no key delivery data is needed for HLS
            );

            policy.Options.Add(policyOption);

            // Add ContentKeyAutorizationPolicy tooContentKey
            contentKey.AuthorizationPolicyId = policy.Id;
            IContentKey updatedKey = contentKey.UpdateAsync().Result;
            Console.WriteLine("Adding Key tooAsset: Key ID is " + updatedKey.Id);

            return tokenTemplateString;
        }

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            Uri keyAcquisitionUri = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.BaselineHttp);

            string envelopeEncryptionIV = Convert.ToBase64String(GetRandomBuffer(16));

            // When configuring delivery policy, you can choose tooassociate it
            // with a key acquisition URL that has a KID appended or
            // or a key acquisition URL that does not have a KID appended  
            // in which case a content key can be reused. 

            // EnvelopeKeyAcquisitionUrl:  contains a key ID in hello key URL.
            // EnvelopeBaseKeyAcquisitionUrl:  hello URL does not contains a key ID

            // hello following policy configuration specifies: 
            // key url that will have KID=<Guid> appended toohello envelope and
            // hello Initialization Vector (IV) toouse for hello envelope encryption.

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
            {AssetDeliveryPolicyConfigurationKey.EnvelopeKeyAcquisitionUrl, keyAcquisitionUri.ToString()}
            };

            IAssetDeliveryPolicy assetDeliveryPolicy =
            _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
                AssetDeliveryPolicyType.DynamicEnvelopeEncryption,
                AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.Dash,
                assetDeliveryPolicyConfiguration);

            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);
            Console.WriteLine();
            Console.WriteLine("Adding Asset Delivery Policy: " +
            assetDeliveryPolicy.AssetDeliveryPolicyType);
        }

        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset. 

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                EndsWith(".ism")).
                FirstOrDefault();

            // Create a 30-day readonly access policy. 
            // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            
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

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
        }

        static private byte[] GetRandomBuffer(int size)
        {
            byte[] randomBytes = new byte[size];
            using (RNGCryptoServiceProvider rng = new RNGCryptoServiceProvider())
            {
            rng.GetBytes(randomBytes);
            }

            return randomBytes;
        }
        }
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="4a010-213">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="4a010-213">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4a010-214">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="4a010-214">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

