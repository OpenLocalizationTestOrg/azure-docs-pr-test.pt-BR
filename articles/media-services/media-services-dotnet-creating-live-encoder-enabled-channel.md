---
title: "aaaHow tooperform transmissão ao vivo usando fluxos de várias taxas de bits de toocreate de serviços de mídia do Azure com o .NET | Microsoft Docs"
description: "Este tutorial aborda você pelas etapas de saudação de criação de um canal recebe uma transmissão ao vivo de taxa de bits única e codifica o fluxo de taxa de bits toomulti usando o SDK do .NET."
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
ms.openlocfilehash: 22088e6a78a49bd839575614a7c17a411ae8081c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-using-azure-media-services-toocreate-multi-bitrate-streams-with-net"></a><span data-ttu-id="0c7c9-103">Como tooperform transmissão ao vivo usando o Azure Media Services toocreate várias taxas de bits fluxos com .NET</span><span class="sxs-lookup"><span data-stu-id="0c7c9-103">How tooperform live streaming using Azure Media Services toocreate multi-bitrate streams with .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0c7c9-104">Portal</span><span class="sxs-lookup"><span data-stu-id="0c7c9-104">Portal</span></span>](media-services-portal-creating-live-encoder-enabled-channel.md)
> * [<span data-ttu-id="0c7c9-105">.NET</span><span class="sxs-lookup"><span data-stu-id="0c7c9-105">.NET</span></span>](media-services-dotnet-creating-live-encoder-enabled-channel.md)
> * [<span data-ttu-id="0c7c9-106">API REST</span><span class="sxs-lookup"><span data-stu-id="0c7c9-106">REST API</span></span>](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> [!NOTE]
> <span data-ttu-id="0c7c9-107">toocomplete neste tutorial, você precisa de uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-107">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="0c7c9-108">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="0c7c9-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="0c7c9-109">Visão geral</span><span class="sxs-lookup"><span data-stu-id="0c7c9-109">Overview</span></span>
<span data-ttu-id="0c7c9-110">Este tutorial orienta você pelas etapas de saudação de criação de um **Channel** que recebe uma transmissão ao vivo de taxa de bits única e o codifica fluxo toomulti taxas de bits.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-110">This tutorial walks you through hello steps of creating a **Channel** that receives a single-bitrate live stream and encodes it toomulti-bitrate stream.</span></span>

<span data-ttu-id="0c7c9-111">Para obter mais informações conceituais tooChannels relacionados que são habilitados para codificação ao vivo, consulte [transmissão ao vivo usando fluxos de várias taxas de bits do Azure Media Services toocreate](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="0c7c9-111">For more conceptual information related tooChannels that are enabled for live encoding, see [Live streaming using Azure Media Services toocreate multi-bitrate streams](media-services-manage-live-encoder-enabled-channels.md).</span></span>

## <a name="common-live-streaming-scenario"></a><span data-ttu-id="0c7c9-112">Cenário comum de streaming ao vivo</span><span class="sxs-lookup"><span data-stu-id="0c7c9-112">Common Live Streaming Scenario</span></span>
<span data-ttu-id="0c7c9-113">Olá etapas a seguir descreve as tarefas envolvidas na criação de aplicativos comuns de transmissão ao vivo.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-113">hello following steps describe tasks involved in creating common live streaming applications.</span></span>

> [!NOTE]
> <span data-ttu-id="0c7c9-114">Atualmente, Olá máximo recomendado de duração de um evento ao vivo é 8 horas.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-114">Currently, hello max recommended duration of a live event is 8 hours.</span></span> <span data-ttu-id="0c7c9-115">Entre em contato com amslived em Microsoft.com se você precisar toorun um canal para períodos de tempo mais longos.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-115">Please contact amslived at Microsoft.com if you need toorun a Channel for longer periods of time.</span></span>
> 
> 

1. <span data-ttu-id="0c7c9-116">Conecte um computador de tooa de câmera de vídeo.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-116">Connect a video camera tooa computer.</span></span> <span data-ttu-id="0c7c9-117">Inicie e configure um codificador ao vivo no local que pode produzir um fluxo de taxa de bits única em um dos seguintes protocolos de saudação: RTMP, Smooth Streaming ou RTP (MPEG-TS).</span><span class="sxs-lookup"><span data-stu-id="0c7c9-117">Launch and configure an on-premises live encoder that can output a single bitrate stream in one of hello following protocols: RTMP, Smooth Streaming, or RTP (MPEG-TS).</span></span> <span data-ttu-id="0c7c9-118">Para obter mais informações, consulte [Suporte RTMP dos Serviços de Mídia do Azure e Codificadores ao Vivo](http://go.microsoft.com/fwlink/?LinkId=532824).</span><span class="sxs-lookup"><span data-stu-id="0c7c9-118">For more information, see [Azure Media Services RTMP Support and Live Encoders](http://go.microsoft.com/fwlink/?LinkId=532824).</span></span>

    <span data-ttu-id="0c7c9-119">Essa etapa também pode ser realizada após a criação do canal.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-119">This step could also be performed after you create your Channel.</span></span>

2. <span data-ttu-id="0c7c9-120">Crie e inicie um Canal.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-120">Create and start a Channel.</span></span>
3. <span data-ttu-id="0c7c9-121">URL de ingestão recuperar Olá canal.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-121">Retrieve hello Channel ingest URL.</span></span>

    <span data-ttu-id="0c7c9-122">URL de ingestão Olá é usado pelo Olá codificador ao vivo toosend Olá fluxo toohello canal.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-122">hello ingest URL is used by hello live encoder toosend hello stream toohello Channel.</span></span>

4. <span data-ttu-id="0c7c9-123">Recupere a URL de visualização do canal hello.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-123">Retrieve hello Channel preview URL.</span></span>

    <span data-ttu-id="0c7c9-124">Use este tooverify URL que o canal está recebendo corretamente transmissão ao vivo hello.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-124">Use this URL tooverify that your channel is properly receiving hello live stream.</span></span>

5. <span data-ttu-id="0c7c9-125">Crie um ativo.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-125">Create an asset.</span></span>
6. <span data-ttu-id="0c7c9-126">Se você quiser para Olá ativo toobe dinamicamente criptografado durante a reprodução, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="0c7c9-126">If you want for hello asset toobe dynamically encrypted during playback, do hello following:</span></span>
7. <span data-ttu-id="0c7c9-127">Crie uma chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-127">Create a content key.</span></span>
8. <span data-ttu-id="0c7c9-128">Configure a política de autorização da chave de saudação conteúdo.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-128">Configure hello content key's authorization policy.</span></span>
9. <span data-ttu-id="0c7c9-129">Configure a política de entrega de ativos (usada pelo empacotamento dinâmico e criptografia dinâmica).</span><span class="sxs-lookup"><span data-stu-id="0c7c9-129">Configure asset delivery policy (used by dynamic packaging and dynamic encryption).</span></span>
10. <span data-ttu-id="0c7c9-130">Crie um programa e especifique o ativo de saudação toouse que você criou.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-130">Create a program and specify toouse hello asset that you created.</span></span>
11. <span data-ttu-id="0c7c9-131">Publica o ativo de saudação associado ao programa de saudação criando um localizador OnDemand.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-131">Publish hello asset associated with hello program by creating an OnDemand locator.</span></span>

    >[!NOTE]
    ><span data-ttu-id="0c7c9-132">Quando sua conta AMS é criada um **padrão** ponto de extremidade de streaming é adicionada conta tooyour Olá **parado** estado.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-132">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="0c7c9-133">saudação do qual você deseja que o conteúdo de toostream de ponto de extremidade de streaming tem toobe em Olá **executando** estado.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-133">hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 

12. <span data-ttu-id="0c7c9-134">Inicie o programa de hello quando você estiver pronto toostart transmissão e o arquivamento.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-134">Start hello program when you are ready toostart streaming and archiving.</span></span>
13. <span data-ttu-id="0c7c9-135">Opcionalmente, o codificador ao vivo Olá pode ser sinalizado toostart um anúncio.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-135">Optionally, hello live encoder can be signaled toostart an advertisement.</span></span> <span data-ttu-id="0c7c9-136">anúncio de saudação é inserido no fluxo de saída de hello.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-136">hello advertisement is inserted in hello output stream.</span></span>
14. <span data-ttu-id="0c7c9-137">Pare o programa de saudação sempre que quiser toostop streaming e arquivamento evento hello.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-137">Stop hello program whenever you want toostop streaming and archiving hello event.</span></span>
15. <span data-ttu-id="0c7c9-138">Excluir Olá programa (e opcionalmente exclua o ativo de saudação).</span><span class="sxs-lookup"><span data-stu-id="0c7c9-138">Delete hello Program (and optionally delete hello asset).</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="0c7c9-139">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="0c7c9-139">What you'll learn</span></span>
<span data-ttu-id="0c7c9-140">Este tópico mostra como tooexecute diferentes operações com canais e programas usando o SDK do Media Services .NET.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-140">This topic shows you how tooexecute different operations on channels and programs using Media Services .NET SDK.</span></span> <span data-ttu-id="0c7c9-141">Como muitas operações são demoradas, são usadas APIs do .NET que gerenciam operações de execução longa.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-141">Because many operations are long-running .NET APIs that manage long running operations are used.</span></span>

<span data-ttu-id="0c7c9-142">Olá tópico mostra como a seguir Olá toodo:</span><span class="sxs-lookup"><span data-stu-id="0c7c9-142">hello topic shows how toodo hello following:</span></span>

1. <span data-ttu-id="0c7c9-143">Crie e inicie um Canal.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-143">Create and start a channel.</span></span> <span data-ttu-id="0c7c9-144">São usadas APIs de execução longa.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-144">Long-running APIs are used.</span></span>
2. <span data-ttu-id="0c7c9-145">Obter canais Olá ingestão (entrado) do ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-145">Get hello channels ingest (input) endpoint.</span></span> <span data-ttu-id="0c7c9-146">Esse ponto de extremidade deve ser fornecido o codificador toohello que pode enviar um fluxo ao vivo de taxa de bits única.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-146">This endpoint should be provided toohello encoder that can send a single bitrate live stream.</span></span>
3. <span data-ttu-id="0c7c9-147">Obter o ponto de extremidade de visualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-147">Get hello preview endpoint.</span></span> <span data-ttu-id="0c7c9-148">Esse ponto de extremidade é usado toopreview seu fluxo.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-148">This endpoint is used toopreview your stream.</span></span>
4. <span data-ttu-id="0c7c9-149">Crie um ativo que será usado toostore seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-149">Create an asset that will be used toostore your content.</span></span> <span data-ttu-id="0c7c9-150">políticas de entrega de ativos de saudação devem ser configuradas, assim como mostrado neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-150">hello asset delivery policies should be configured as well, as shown in this example.</span></span>
5. <span data-ttu-id="0c7c9-151">Criar um programa e especifique o ativo de saudação toouse criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-151">Create a program and specify toouse hello asset that was created earlier.</span></span> <span data-ttu-id="0c7c9-152">Inicie o programa de saudação.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-152">Start hello program.</span></span> <span data-ttu-id="0c7c9-153">São usadas APIs de execução longa.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-153">Long-running APIs are used.</span></span>
6. <span data-ttu-id="0c7c9-154">Crie um localizador para ativo hello, conteúdo de saudação é publicado e pode ser transmitido tooyour clientes.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-154">Create a locator for hello asset, so hello content gets published and can be streamed tooyour clients.</span></span>
7. <span data-ttu-id="0c7c9-155">Mostrar e ocultar slates.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-155">Show and hide slates.</span></span> <span data-ttu-id="0c7c9-156">Iniciar e parar anúncios.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-156">Start and stop advertisements.</span></span> <span data-ttu-id="0c7c9-157">São usadas APIs de execução longa.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-157">Long-running APIs are used.</span></span>
8. <span data-ttu-id="0c7c9-158">Limpar seu canal e Olá a todos os recursos associados.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-158">Clean up your channel and all hello associated resources.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0c7c9-159">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0c7c9-159">Prerequisites</span></span>
<span data-ttu-id="0c7c9-160">Olá seguem tutorial de saudação toocomplete necessária.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-160">hello following are required toocomplete hello tutorial.</span></span>

* <span data-ttu-id="0c7c9-161">Uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-161">An Azure account.</span></span> <span data-ttu-id="0c7c9-162">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-162">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="0c7c9-163">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="0c7c9-163">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span> <span data-ttu-id="0c7c9-164">Você obtém créditos que podem ser usado tootry out paga serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-164">You get credits that can be used tootry out paid Azure services.</span></span> <span data-ttu-id="0c7c9-165">Mesmo depois de saudação créditos são esgotados, você pode manter Olá conta e usar os serviços do Azure gratuitos e recursos, como recursos de aplicativos Web Olá no serviço de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-165">Even after hello credits are used up, you can keep hello account and use free Azure services and features, such as hello Web Apps feature in Azure App Service.</span></span>
* <span data-ttu-id="0c7c9-166">Uma conta dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-166">A Media Services account.</span></span> <span data-ttu-id="0c7c9-167">toocreate uma conta de serviços de mídia, consulte [criar conta](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="0c7c9-167">toocreate a Media Services account, see [Create Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="0c7c9-168">Visual Studio 2010 SP1 (Professional, Premium, Ultimate ou Express) ou versões posteriores.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-168">Visual Studio 2010 SP1 (Professional, Premium, Ultimate, or Express) or later versions.</span></span>
* <span data-ttu-id="0c7c9-169">Você deve usar o Media Services .NET SDK na versão 3.2.0.0 ou mais recente.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-169">You must use Media Services .NET SDK version 3.2.0.0 or newer.</span></span>
* <span data-ttu-id="0c7c9-170">Uma webcam e um codificador que possa enviar um fluxo ao vivo de taxa de bits única.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-170">A webcam and an encoder that can send a single bitrate live stream.</span></span>

## <a name="considerations"></a><span data-ttu-id="0c7c9-171">Considerações</span><span class="sxs-lookup"><span data-stu-id="0c7c9-171">Considerations</span></span>
* <span data-ttu-id="0c7c9-172">Atualmente, Olá máximo recomendado de duração de um evento ao vivo é 8 horas.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-172">Currently, hello max recommended duration of a live event is 8 hours.</span></span> <span data-ttu-id="0c7c9-173">Entre em contato com amslived em Microsoft.com se você precisar toorun um canal para períodos de tempo mais longos.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-173">Please contact amslived at Microsoft.com if you need toorun a Channel for longer periods of time.</span></span>
* <span data-ttu-id="0c7c9-174">Há um limite de 1.000.000 políticas para diferentes políticas de AMS (por exemplo, para política de Localizador ou ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="0c7c9-174">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="0c7c9-175">Você deve usar Olá Olá a mesma ID de política se você estiver usando sempre mesmo dias acesso permissões, por exemplo, as políticas para localizadores são tooremain desejado no local por um longo período (políticas de carregamento não).</span><span class="sxs-lookup"><span data-stu-id="0c7c9-175">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="0c7c9-176">Para obter mais informações, consulte [este](media-services-dotnet-manage-entities.md#limit-access-policies) tópico.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-176">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

## <a name="download-sample"></a><span data-ttu-id="0c7c9-177">Baixar exemplo</span><span class="sxs-lookup"><span data-stu-id="0c7c9-177">Download sample</span></span>

<span data-ttu-id="0c7c9-178">Você pode baixar o exemplo hello descrito neste tópico de [aqui](https://azure.microsoft.com/documentation/samples/media-services-dotnet-encode-live-stream-with-ams-clear/).</span><span class="sxs-lookup"><span data-stu-id="0c7c9-178">You can download hello sample that is described in this topic from [here](https://azure.microsoft.com/documentation/samples/media-services-dotnet-encode-live-stream-with-ams-clear/).</span></span>

## <a name="set-up-for-development-with-media-services-sdk-for-net"></a><span data-ttu-id="0c7c9-179">Configurar para o desenvolvimento com o SDK dos Serviços de Mídia para .NET</span><span class="sxs-lookup"><span data-stu-id="0c7c9-179">Set up for development with Media Services SDK for .NET</span></span>

<span data-ttu-id="0c7c9-180">Configurar seu ambiente de desenvolvimento e preencher o arquivo App. config de saudação com informações de conexão, conforme descrito em [desenvolvimento de serviços de mídia com o .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="0c7c9-180">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="code-example"></a><span data-ttu-id="0c7c9-181">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="0c7c9-181">Code example</span></span>

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

        // Read values from hello App.config file.
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

            // hello channel's input endpoint:
            string ingestUrl = channel.Input.Endpoints.FirstOrDefault().Url.ToString();

            Console.WriteLine("Intest URL: {0}", ingestUrl);


            // Use hello previewEndpoint toopreview and verify 
            // that hello input from hello encoder is actually reaching hello Channel. 
            string previewEndpoint = channel.Preview.Endpoints.FirstOrDefault().Url.ToString();

            Console.WriteLine("Preview URL: {0}", previewEndpoint);

            // When Live Encoding is enabled, you can now get a preview of hello live feed as it reaches hello Channel. 
            // This can be a valuable tool toocheck whether your live feed is actually reaching hello Channel. 
            // hello thumbnail is exposed via hello same end-point as hello Channel Preview URL.
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

            // You can use slates and ads only if hello channel type is Standard.  
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
            // You can only set audio if streaming protocol is set tooStreamingProtocol.RTPMPEG2TS.
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
        /// Create a Program on hello Channel. You can have multiple Programs that overlap or are sequential;
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
        /// Create locators in order toobe able toopublish and stream hello video.
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
        /// Clean up resources associated with hello channel.
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

            Log("starting tootrack ", null, operation.Id);
            while (isCompleted == false)
            {
            operation = _context.Operations.GetOperation(operation.Id);
            isCompleted = IsCompleted(operation, out entityId);
            System.Threading.Thread.Sleep(TimeSpan.FromSeconds(30));
            }
            // If we got here, hello operation succeeded.
            Log(description + " in completed", operation.TargetEntityId, operation.Id);

            return entityId;
        }

        /// <summary> 
        /// Checks if hello operation has been completed. 
        /// If hello operation succeeded, hello created entity Id is returned in hello out parameter.
        /// </summary> 
        /// <param name="operationId">hello operation Id.</param> 
        /// <param name="channel">
        /// If hello operation succeeded, 
        /// hello entity Id associated with hello sucessful operation is returned in hello out parameter.</param>
        /// <returns>Returns false if hello operation is still in progress; otherwise, true.</returns> 
        private static bool IsCompleted(IOperation operation, out string entityId)
        {
            bool completed = false;

            entityId = null;

            switch (operation.State)
            {
            case OperationState.Failed:
                // Handle hello failure. 
                // For example, throw an exception. 
                // Use hello following information in hello exception: operationId, operation.ErrorMessage.
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

## <a name="next-step"></a><span data-ttu-id="0c7c9-182">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="0c7c9-182">Next step</span></span>
<span data-ttu-id="0c7c9-183">Revise os roteiros de aprendizagem dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="0c7c9-183">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0c7c9-184">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="0c7c9-184">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


