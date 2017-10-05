---
title: "Como executar a transmissão ao vivo usando os Serviços de Mídia do Azure para criar fluxos de múltiplas taxas de bits com o .NET | Microsoft Docs"
description: "Este tutorial orienta você pelas etapas de criação de um Canal que recebe um fluxo em tempo real de taxa de bits única e o codifica em um fluxo de múltiplas taxas de bits usando o SDK do .NET."
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 4df5e690-ff63-47cc-879b-9c57cb8ec240
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 22d63ff5e9fd33db8711b0c5125ab0882b9f6a74
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-perform-live-streaming-using-azure-media-services-to-create-multi-bitrate-streams-with-net"></a><span data-ttu-id="43174-103">Como executar a transmissão ao vivo usando os Serviços de Mídia do Azure para criar fluxos de múltiplas taxas de bits com o .NET</span><span class="sxs-lookup"><span data-stu-id="43174-103">How to perform live streaming using Azure Media Services to create multi-bitrate streams with .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="43174-104">Portal</span><span class="sxs-lookup"><span data-stu-id="43174-104">Portal</span></span>](media-services-portal-creating-live-encoder-enabled-channel.md)
> * [<span data-ttu-id="43174-105">.NET</span><span class="sxs-lookup"><span data-stu-id="43174-105">.NET</span></span>](media-services-dotnet-creating-live-encoder-enabled-channel.md)
> * [<span data-ttu-id="43174-106">API REST</span><span class="sxs-lookup"><span data-stu-id="43174-106">REST API</span></span>](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> [!NOTE]
> <span data-ttu-id="43174-107">Para concluir este tutorial, você precisa de uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="43174-107">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="43174-108">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="43174-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="43174-109">Visão geral</span><span class="sxs-lookup"><span data-stu-id="43174-109">Overview</span></span>
<span data-ttu-id="43174-110">Este tutorial orienta você pelas etapas de criação de um **Canal** que recebe um fluxo ao vivo de taxa de bits única e o codifica em fluxo de múltiplas taxas de bits.</span><span class="sxs-lookup"><span data-stu-id="43174-110">This tutorial walks you through the steps of creating a **Channel** that receives a single-bitrate live stream and encodes it to multi-bitrate stream.</span></span>

<span data-ttu-id="43174-111">Para obter mais informações conceituais relacionadas aos Canais habilitados para a codificação ao vivo, consulte [Transmissão ao vivo usando os Serviços de Mídia do Azure para criar fluxos de múltiplas taxas de bits](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="43174-111">For more conceptual information related to Channels that are enabled for live encoding, see [Live streaming using Azure Media Services to create multi-bitrate streams](media-services-manage-live-encoder-enabled-channels.md).</span></span>

## <a name="common-live-streaming-scenario"></a><span data-ttu-id="43174-112">Cenário comum de streaming ao vivo</span><span class="sxs-lookup"><span data-stu-id="43174-112">Common Live Streaming Scenario</span></span>
<span data-ttu-id="43174-113">As etapas a seguir descrevem as tarefas envolvidas na criação de aplicativos comuns de transmissão ao vivo.</span><span class="sxs-lookup"><span data-stu-id="43174-113">The following steps describe tasks involved in creating common live streaming applications.</span></span>

> [!NOTE]
> <span data-ttu-id="43174-114">Atualmente, a duração máxima recomendada de um evento ao vivo é de 8 horas.</span><span class="sxs-lookup"><span data-stu-id="43174-114">Currently, the max recommended duration of a live event is 8 hours.</span></span> <span data-ttu-id="43174-115">Entre em contato com amslived na Microsoft.com se precisar executar um Canal por períodos mais longos.</span><span class="sxs-lookup"><span data-stu-id="43174-115">Please contact amslived at Microsoft.com if you need to run a Channel for longer periods of time.</span></span>
> 
> 

1. <span data-ttu-id="43174-116">Conecte uma câmera de vídeo a um computador.</span><span class="sxs-lookup"><span data-stu-id="43174-116">Connect a video camera to a computer.</span></span> <span data-ttu-id="43174-117">Inicie e configure um codificador ao vivo local que possa produzir um fluxo de taxa de bits única em um dos seguintes protocolos: RTMP, Smooth Streaming ou RTP (MPEG-TS).</span><span class="sxs-lookup"><span data-stu-id="43174-117">Launch and configure an on-premises live encoder that can output a single bitrate stream in one of the following protocols: RTMP, Smooth Streaming, or RTP (MPEG-TS).</span></span> <span data-ttu-id="43174-118">Para obter mais informações, consulte [Suporte RTMP dos Serviços de Mídia do Azure e Codificadores ao Vivo](http://go.microsoft.com/fwlink/?LinkId=532824).</span><span class="sxs-lookup"><span data-stu-id="43174-118">For more information, see [Azure Media Services RTMP Support and Live Encoders](http://go.microsoft.com/fwlink/?LinkId=532824).</span></span>

    <span data-ttu-id="43174-119">Essa etapa também pode ser realizada após a criação do canal.</span><span class="sxs-lookup"><span data-stu-id="43174-119">This step could also be performed after you create your Channel.</span></span>

2. <span data-ttu-id="43174-120">Crie e inicie um Canal.</span><span class="sxs-lookup"><span data-stu-id="43174-120">Create and start a Channel.</span></span>
3. <span data-ttu-id="43174-121">Recupere a URL de ingestão do canal.</span><span class="sxs-lookup"><span data-stu-id="43174-121">Retrieve the Channel ingest URL.</span></span>

    <span data-ttu-id="43174-122">A URL de ingestão é usada pelo codificador ao vivo para enviar o fluxo para o canal.</span><span class="sxs-lookup"><span data-stu-id="43174-122">The ingest URL is used by the live encoder to send the stream to the Channel.</span></span>

4. <span data-ttu-id="43174-123">Recupere a URL de visualização do canal.</span><span class="sxs-lookup"><span data-stu-id="43174-123">Retrieve the Channel preview URL.</span></span>

    <span data-ttu-id="43174-124">Use essa URL para verificar se o canal está recebendo corretamente o fluxo ao vivo.</span><span class="sxs-lookup"><span data-stu-id="43174-124">Use this URL to verify that your channel is properly receiving the live stream.</span></span>

5. <span data-ttu-id="43174-125">Crie um ativo.</span><span class="sxs-lookup"><span data-stu-id="43174-125">Create an asset.</span></span>
6. <span data-ttu-id="43174-126">Se você quiser que o ativo seja criptografado dinamicamente durante a reprodução, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="43174-126">If you want for the asset to be dynamically encrypted during playback, do the following:</span></span>
7. <span data-ttu-id="43174-127">Crie uma chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="43174-127">Create a content key.</span></span>
8. <span data-ttu-id="43174-128">Configure a política de autorização da chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="43174-128">Configure the content key's authorization policy.</span></span>
9. <span data-ttu-id="43174-129">Configure a política de entrega de ativos (usada pelo empacotamento dinâmico e criptografia dinâmica).</span><span class="sxs-lookup"><span data-stu-id="43174-129">Configure asset delivery policy (used by dynamic packaging and dynamic encryption).</span></span>
10. <span data-ttu-id="43174-130">Crie um programa e especifique o uso do ativo que você criou.</span><span class="sxs-lookup"><span data-stu-id="43174-130">Create a program and specify to use the asset that you created.</span></span>
11. <span data-ttu-id="43174-131">Publique o ativo associado ao programa criando um localizador OnDemand.</span><span class="sxs-lookup"><span data-stu-id="43174-131">Publish the asset associated with the program by creating an OnDemand locator.</span></span>

    >[!NOTE]
    ><span data-ttu-id="43174-132">Quando sua conta AMS é criada, um ponto de extremidade de streaming **padrão** é adicionado à sua conta em estado **Parado**.</span><span class="sxs-lookup"><span data-stu-id="43174-132">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="43174-133">O ponto de extremidade de streaming do qual você deseja transmitir o conteúdo deve estar no estado **Executando**.</span><span class="sxs-lookup"><span data-stu-id="43174-133">The streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 

12. <span data-ttu-id="43174-134">Inicie o programa quando estiver pronto para iniciar o streaming e o arquivamento.</span><span class="sxs-lookup"><span data-stu-id="43174-134">Start the program when you are ready to start streaming and archiving.</span></span>
13. <span data-ttu-id="43174-135">Opcionalmente, o codificador ao vivo pode ser sinalizado para iniciar um anúncio.</span><span class="sxs-lookup"><span data-stu-id="43174-135">Optionally, the live encoder can be signaled to start an advertisement.</span></span> <span data-ttu-id="43174-136">O anúncio é inserido no fluxo de saída.</span><span class="sxs-lookup"><span data-stu-id="43174-136">The advertisement is inserted in the output stream.</span></span>
14. <span data-ttu-id="43174-137">Interrompa o programa sempre que você deseja parar o streaming e o arquivamento do evento.</span><span class="sxs-lookup"><span data-stu-id="43174-137">Stop the program whenever you want to stop streaming and archiving the event.</span></span>
15. <span data-ttu-id="43174-138">Exclua o programa (e, opcionalmente, exclua o ativo).</span><span class="sxs-lookup"><span data-stu-id="43174-138">Delete the Program (and optionally delete the asset).</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="43174-139">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="43174-139">What you'll learn</span></span>
<span data-ttu-id="43174-140">Este tópico mostra como executar operações diferentes em canais e programas usando o SDK dos Serviços de Mídia para .NET.</span><span class="sxs-lookup"><span data-stu-id="43174-140">This topic shows you how to execute different operations on channels and programs using Media Services .NET SDK.</span></span> <span data-ttu-id="43174-141">Como muitas operações são demoradas, são usadas APIs do .NET que gerenciam operações de execução longa.</span><span class="sxs-lookup"><span data-stu-id="43174-141">Because many operations are long-running .NET APIs that manage long running operations are used.</span></span>

<span data-ttu-id="43174-142">O tópico mostra como fazer o seguinte:</span><span class="sxs-lookup"><span data-stu-id="43174-142">The topic shows how to do the following:</span></span>

1. <span data-ttu-id="43174-143">Crie e inicie um Canal.</span><span class="sxs-lookup"><span data-stu-id="43174-143">Create and start a channel.</span></span> <span data-ttu-id="43174-144">São usadas APIs de execução longa.</span><span class="sxs-lookup"><span data-stu-id="43174-144">Long-running APIs are used.</span></span>
2. <span data-ttu-id="43174-145">Obtenha o ponto de extremidade de ingestão (entrada) dos canais.</span><span class="sxs-lookup"><span data-stu-id="43174-145">Get the channels ingest (input) endpoint.</span></span> <span data-ttu-id="43174-146">Esse ponto de extremidade deve ser fornecido ao codificador que pode enviar um fluxo ao vivo de taxa de bits única.</span><span class="sxs-lookup"><span data-stu-id="43174-146">This endpoint should be provided to the encoder that can send a single bitrate live stream.</span></span>
3. <span data-ttu-id="43174-147">Obtenha o ponto de extremidade de visualização.</span><span class="sxs-lookup"><span data-stu-id="43174-147">Get the preview endpoint.</span></span> <span data-ttu-id="43174-148">Esse ponto de extremidade é usado para visualizar o fluxo.</span><span class="sxs-lookup"><span data-stu-id="43174-148">This endpoint is used to preview your stream.</span></span>
4. <span data-ttu-id="43174-149">Crie um ativo que será usado para armazenar seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="43174-149">Create an asset that will be used to store your content.</span></span> <span data-ttu-id="43174-150">As políticas de entrega de ativos devem ser configuradas, assim, como mostrado neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="43174-150">The asset delivery policies should be configured as well, as shown in this example.</span></span>
5. <span data-ttu-id="43174-151">Crie um programa e especifique o uso do ativo que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="43174-151">Create a program and specify to use the asset that was created earlier.</span></span> <span data-ttu-id="43174-152">Inicie o programa.</span><span class="sxs-lookup"><span data-stu-id="43174-152">Start the program.</span></span> <span data-ttu-id="43174-153">São usadas APIs de execução longa.</span><span class="sxs-lookup"><span data-stu-id="43174-153">Long-running APIs are used.</span></span>
6. <span data-ttu-id="43174-154">Crie um localizador para o ativo, de modo que o conteúdo seja publicado e possa ser transmitido para seus clientes.</span><span class="sxs-lookup"><span data-stu-id="43174-154">Create a locator for the asset, so the content gets published and can be streamed to your clients.</span></span>
7. <span data-ttu-id="43174-155">Mostrar e ocultar slates.</span><span class="sxs-lookup"><span data-stu-id="43174-155">Show and hide slates.</span></span> <span data-ttu-id="43174-156">Iniciar e parar anúncios.</span><span class="sxs-lookup"><span data-stu-id="43174-156">Start and stop advertisements.</span></span> <span data-ttu-id="43174-157">São usadas APIs de execução longa.</span><span class="sxs-lookup"><span data-stu-id="43174-157">Long-running APIs are used.</span></span>
8. <span data-ttu-id="43174-158">Limpe seu canal e todos os recursos associados.</span><span class="sxs-lookup"><span data-stu-id="43174-158">Clean up your channel and all the associated resources.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="43174-159">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="43174-159">Prerequisites</span></span>
<span data-ttu-id="43174-160">Os itens a seguir são necessários para concluir o tutorial.</span><span class="sxs-lookup"><span data-stu-id="43174-160">The following are required to complete the tutorial.</span></span>

* <span data-ttu-id="43174-161">Uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="43174-161">An Azure account.</span></span> <span data-ttu-id="43174-162">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="43174-162">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="43174-163">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="43174-163">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span> <span data-ttu-id="43174-164">Obtenha créditos que possam ser usados para experimentar os serviços pagos do Azure.</span><span class="sxs-lookup"><span data-stu-id="43174-164">You get credits that can be used to try out paid Azure services.</span></span> <span data-ttu-id="43174-165">Mesmo depois que os créditos são usados, você pode manter a conta e usar os serviços e recursos do Azure gratuitos, como o recurso de aplicativos Web do Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="43174-165">Even after the credits are used up, you can keep the account and use free Azure services and features, such as the Web Apps feature in Azure App Service.</span></span>
* <span data-ttu-id="43174-166">Uma conta dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="43174-166">A Media Services account.</span></span> <span data-ttu-id="43174-167">Para criar uma conta de Serviços de Mídia, confira [Criar Conta](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="43174-167">To create a Media Services account, see [Create Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="43174-168">Visual Studio 2010 SP1 (Professional, Premium, Ultimate ou Express) ou versões posteriores.</span><span class="sxs-lookup"><span data-stu-id="43174-168">Visual Studio 2010 SP1 (Professional, Premium, Ultimate, or Express) or later versions.</span></span>
* <span data-ttu-id="43174-169">Você deve usar o Media Services .NET SDK na versão 3.2.0.0 ou mais recente.</span><span class="sxs-lookup"><span data-stu-id="43174-169">You must use Media Services .NET SDK version 3.2.0.0 or newer.</span></span>
* <span data-ttu-id="43174-170">Uma webcam e um codificador que possa enviar um fluxo ao vivo de taxa de bits única.</span><span class="sxs-lookup"><span data-stu-id="43174-170">A webcam and an encoder that can send a single bitrate live stream.</span></span>

## <a name="considerations"></a><span data-ttu-id="43174-171">Considerações</span><span class="sxs-lookup"><span data-stu-id="43174-171">Considerations</span></span>
* <span data-ttu-id="43174-172">Atualmente, a duração máxima recomendada de um evento ao vivo é de 8 horas.</span><span class="sxs-lookup"><span data-stu-id="43174-172">Currently, the max recommended duration of a live event is 8 hours.</span></span> <span data-ttu-id="43174-173">Entre em contato com amslived na Microsoft.com se precisar executar um Canal por períodos mais longos.</span><span class="sxs-lookup"><span data-stu-id="43174-173">Please contact amslived at Microsoft.com if you need to run a Channel for longer periods of time.</span></span>
* <span data-ttu-id="43174-174">Há um limite de 1.000.000 políticas para diferentes políticas de AMS (por exemplo, para política de Localizador ou ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="43174-174">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="43174-175">Use a mesma ID de política, se você estiver sempre usando os mesmos dias/permissões de acesso, por exemplo, políticas de localizadores que devem permanecer no local por um longo período (políticas de não carregamento).</span><span class="sxs-lookup"><span data-stu-id="43174-175">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="43174-176">Para obter mais informações, consulte [este](media-services-dotnet-manage-entities.md#limit-access-policies) tópico.</span><span class="sxs-lookup"><span data-stu-id="43174-176">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

## <a name="download-sample"></a><span data-ttu-id="43174-177">Baixar exemplo</span><span class="sxs-lookup"><span data-stu-id="43174-177">Download sample</span></span>

<span data-ttu-id="43174-178">Você pode baixar o exemplo descrito neste tópico [aqui](https://azure.microsoft.com/documentation/samples/media-services-dotnet-encode-live-stream-with-ams-clear/).</span><span class="sxs-lookup"><span data-stu-id="43174-178">You can download the sample that is described in this topic from [here](https://azure.microsoft.com/documentation/samples/media-services-dotnet-encode-live-stream-with-ams-clear/).</span></span>

## <a name="set-up-for-development-with-media-services-sdk-for-net"></a><span data-ttu-id="43174-179">Configurar para o desenvolvimento com o SDK dos Serviços de Mídia para .NET</span><span class="sxs-lookup"><span data-stu-id="43174-179">Set up for development with Media Services SDK for .NET</span></span>

<span data-ttu-id="43174-180">Configure seu ambiente de desenvolvimento e preencha o arquivo de configuração app.config com as informações de conexão, conforme descrito em [Desenvolvimento de Serviços de Mídia com o .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="43174-180">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="code-example"></a><span data-ttu-id="43174-181">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="43174-181">Code example</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Net;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;

    namespace EncodeLiveStreamWithAmsClear
    {
        class Program
        {
        private const string ChannelName = "channel001";
        private const string AssetlName = "asset001";
        private const string ProgramlName = "program001";

        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            IChannel channel = CreateAndStartChannel();

            // The channel's input endpoint:
            string ingestUrl = channel.Input.Endpoints.FirstOrDefault().Url.ToString();

            Console.WriteLine("Intest URL: {0}", ingestUrl);


            // Use the previewEndpoint to preview and verify 
            // that the input from the encoder is actually reaching the Channel. 
            string previewEndpoint = channel.Preview.Endpoints.FirstOrDefault().Url.ToString();

            Console.WriteLine("Preview URL: {0}", previewEndpoint);

            // When Live Encoding is enabled, you can now get a preview of the live feed as it reaches the Channel. 
            // This can be a valuable tool to check whether your live feed is actually reaching the Channel. 
            // The thumbnail is exposed via the same end-point as the Channel Preview URL.
            string thumbnailUri = new UriBuilder
            {
            Scheme = Uri.UriSchemeHttps,
            Host = channel.Preview.Endpoints.FirstOrDefault().Url.Host,
            Path = "thumbnails/input.jpg"
            }.Uri.ToString();

            Console.WriteLine("Thumbain URL: {0}", thumbnailUri);

            // Once you previewed your stream and verified that it is flowing into your Channel, 
            // you can create an event by creating an Asset, Program, and Streaming Locator. 
            IAsset asset = CreateAndConfigureAsset();

            IProgram program = CreateAndStartProgram(channel, asset);

            ILocator locator = CreateLocatorForAsset(program.Asset, program.ArchiveWindowLength);

            // You can use slates and ads only if the channel type is Standard.  
            StartStopAdsSlates(channel);

            // Once you are done streaming, clean up your resources.
            Cleanup(channel);
        }

        public static IChannel CreateAndStartChannel()
        {
            var channelInput = CreateChannelInput();
            var channePreview = CreateChannelPreview();
            var channelEncoding = CreateChannelEncoding();

            ChannelCreationOptions options = new ChannelCreationOptions
            {
            EncodingType = ChannelEncodingType.Standard,
            Name = ChannelName,
            Input = channelInput,
            Preview = channePreview,
            Encoding = channelEncoding
            };

            Log("Creating channel");
            IOperation channelCreateOperation = _context.Channels.SendCreateOperation(options);
            string channelId = TrackOperation(channelCreateOperation, "Channel create");

            IChannel channel = _context.Channels.Where(c => c.Id == channelId).FirstOrDefault();

            Log("Starting channel");
            var channelStartOperation = channel.SendStartOperation();
            TrackOperation(channelStartOperation, "Channel start");

            return channel;
        }

        /// <summary>
        /// Create channel input, used in channel creation options. 
        /// </summary>
        /// <returns></returns>
        private static ChannelInput CreateChannelInput()
        {
            return new ChannelInput
            {
            StreamingProtocol = StreamingProtocol.RTPMPEG2TS,
            AccessControl = new ChannelAccessControl
            {
                IPAllowList = new List<IPRange>
                {
                    new IPRange
                    {
                    Name = "TestChannelInput001",
                    Address = IPAddress.Parse("0.0.0.0"),
                    SubnetPrefixLength = 0
                    }
                }
            }
            };
        }

        /// <summary>
        /// Create channel preview, used in channel creation options. 
        /// </summary>
        /// <returns></returns>
        private static ChannelPreview CreateChannelPreview()
        {
            return new ChannelPreview
            {
            AccessControl = new ChannelAccessControl
            {
                IPAllowList = new List<IPRange>
                {
                    new IPRange
                    {
                    Name = "TestChannelPreview001",
                    Address = IPAddress.Parse("0.0.0.0"),
                    SubnetPrefixLength = 0
                    }
                }
            }
            };
        }

        /// <summary>
        /// Create channel encoding, used in channel creation options. 
        /// </summary>
        /// <returns></returns>
        private static ChannelEncoding CreateChannelEncoding()
        {
            return new ChannelEncoding
            {
            SystemPreset = "Default720p",
            IgnoreCea708ClosedCaptions = false,
            AdMarkerSource = AdMarkerSource.Api,
            // You can only set audio if streaming protocol is set to StreamingProtocol.RTPMPEG2TS.
            AudioStreams = new List<AudioStream> { new AudioStream { Index = 103, Language = "eng" } }.AsReadOnly()
            };
        }

        /// <summary>
        /// Create an asset and configure asset delivery policies.
        /// </summary>
        /// <returns></returns>
        public static IAsset CreateAndConfigureAsset()
        {
            IAsset asset = _context.Assets.Create(AssetlName, AssetCreationOptions.None);

            IAssetDeliveryPolicy policy =
            _context.AssetDeliveryPolicies.Create("Clear Policy",
            AssetDeliveryPolicyType.NoDynamicEncryption,
            AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.Dash, null);

            asset.DeliveryPolicies.Add(policy);

            return asset;
        }

        /// <summary>
        /// Create a Program on the Channel. You can have multiple Programs that overlap or are sequential;
        /// however each Program must have a unique name within your Media Services account.
        /// </summary>
        /// <param name="channel"></param>
        /// <param name="asset"></param>
        /// <returns></returns>
        public static IProgram CreateAndStartProgram(IChannel channel, IAsset asset)
        {
            IProgram program = channel.Programs.Create(ProgramlName, TimeSpan.FromHours(3), asset.Id);
            Log("Program created", program.Id);

            Log("Starting program");
            var programStartOperation = program.SendStartOperation();
            TrackOperation(programStartOperation, "Program start");

            return program;
        }

        /// <summary>
        /// Create locators in order to be able to publish and stream the video.
        /// </summary>
        /// <param name="asset"></param>
        /// <param name="ArchiveWindowLength"></param>
        /// <returns></returns>
        public static ILocator CreateLocatorForAsset(IAsset asset, TimeSpan ArchiveWindowLength)
        {
            // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            
            var locator = _context.Locators.CreateLocator
            (
                LocatorType.OnDemandOrigin,
                asset,
                _context.AccessPolicies.Create
                (
                    "Live Stream Policy",
                    ArchiveWindowLength,
                    AccessPermissions.Read
                )
            );

            return locator;
        }

        /// <summary>
        /// Perform operations on slates.
        /// </summary>
        /// <param name="channel"></param>
        public static void StartStopAdsSlates(IChannel channel)
        {
            int cueId = new Random().Next(int.MaxValue);
            var path = Path.GetFullPath(Path.Combine(AppDomain.CurrentDomain.BaseDirectory, @"..\\..\\SlateJPG\\DefaultAzurePortalSlate.jpg"));

            Log("Creating asset");
            var slateAsset = _context.Assets.Create("Slate test asset " + DateTime.Now.ToString("yyyy-MM-dd HH-mm"), AssetCreationOptions.None);
            Log("Slate asset created", slateAsset.Id);

            Log("Uploading file");
            var assetFile = slateAsset.AssetFiles.Create("DefaultAzurePortalSlate.jpg");
            assetFile.Upload(path);
            assetFile.IsPrimary = true;
            assetFile.Update();

            Log("Showing slate");
            var showSlateOpeartion = channel.SendShowSlateOperation(TimeSpan.FromMinutes(1), slateAsset.Id);
            TrackOperation(showSlateOpeartion, "Show slate");

            Log("Hiding slate");
            var hideSlateOperation = channel.SendHideSlateOperation();
            TrackOperation(hideSlateOperation, "Hide slate");

            Log("Starting ad");
            var startAdOperation = channel.SendStartAdvertisementOperation(TimeSpan.FromMinutes(1), cueId, false);
            TrackOperation(startAdOperation, "Start ad");

            Log("Ending ad");
            var endAdOperation = channel.SendEndAdvertisementOperation(cueId);
            TrackOperation(endAdOperation, "End ad");

            Log("Deleting slate asset");
            slateAsset.Delete();
        }

        /// <summary>
        /// Clean up resources associated with the channel.
        /// </summary>
        /// <param name="channel"></param>
        public static void Cleanup(IChannel channel)
        {
            IAsset asset;
            if (channel != null)
            {
            foreach (var program in channel.Programs)
            {
                asset = _context.Assets.Where(se => se.Id == program.AssetId)
                            .FirstOrDefault();

                Log("Stopping program");
                var programStopOperation = program.SendStopOperation();
                TrackOperation(programStopOperation, "Program stop");

                program.Delete();

                if (asset != null)
                {
                Log("Deleting locators");
                foreach (var l in asset.Locators)
                    l.Delete();

                Log("Deleting asset");
                asset.Delete();
                }
            }

            Log("Stopping channel");
            var channelStopOperation = channel.SendStopOperation();
            TrackOperation(channelStopOperation, "Channel stop");

            Log("Deleting channel");
            var channelDeleteOperation = channel.SendDeleteOperation();
            TrackOperation(channelDeleteOperation, "Channel delete");
            }
        }

        /// <summary>
        /// Track long running operations.
        /// </summary>
        /// <param name="operation"></param>
        /// <param name="description"></param>
        /// <returns></returns>
        public static string TrackOperation(IOperation operation, string description)
        {
            string entityId = null;
            bool isCompleted = false;

            Log("starting to track ", null, operation.Id);
            while (isCompleted == false)
            {
            operation = _context.Operations.GetOperation(operation.Id);
            isCompleted = IsCompleted(operation, out entityId);
            System.Threading.Thread.Sleep(TimeSpan.FromSeconds(30));
            }
            // If we got here, the operation succeeded.
            Log(description + " in completed", operation.TargetEntityId, operation.Id);

            return entityId;
        }

        /// <summary> 
        /// Checks if the operation has been completed. 
        /// If the operation succeeded, the created entity Id is returned in the out parameter.
        /// </summary> 
        /// <param name="operationId">The operation Id.</param> 
        /// <param name="channel">
        /// If the operation succeeded, 
        /// the entity Id associated with the sucessful operation is returned in the out parameter.</param>
        /// <returns>Returns false if the operation is still in progress; otherwise, true.</returns> 
        private static bool IsCompleted(IOperation operation, out string entityId)
        {
            bool completed = false;

            entityId = null;

            switch (operation.State)
            {
            case OperationState.Failed:
                // Handle the failure. 
                // For example, throw an exception. 
                // Use the following information in the exception: operationId, operation.ErrorMessage.
                Log("operation failed", operation.TargetEntityId, operation.Id);
                break;
            case OperationState.Succeeded:
                completed = true;
                entityId = operation.TargetEntityId;
                break;
            case OperationState.InProgress:
                completed = false;
                Log("operation in progress", operation.TargetEntityId, operation.Id);
                break;
            }
            return completed;
        }

        private static void Log(string action, string entityId = null, string operationId = null)
        {
            Console.WriteLine(
            "{0,-21}{1,-51}{2,-51}{3,-51}",
            DateTime.Now.ToString("yyyy'-'MM'-'dd HH':'mm':'ss"),
            action,
            entityId ?? string.Empty,
            operationId ?? string.Empty);
        }
        }
    }

## <a name="next-step"></a><span data-ttu-id="43174-182">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="43174-182">Next step</span></span>
<span data-ttu-id="43174-183">Revise os roteiros de aprendizagem dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="43174-183">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="43174-184">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="43174-184">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


