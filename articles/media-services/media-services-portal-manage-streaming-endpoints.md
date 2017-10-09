---
title: aaaManage streaming pontos de extremidade com hello portal do Azure | Microsoft Docs
description: "Este tópico mostra como pontos de extremidade de streaming de toomanage com hello portal do Azure."
services: media-services
documentationcenter: 
author: Juliako
writer: juliako
manager: cfowler
editor: 
ms.assetid: bb1aca25-d23a-4520-8c45-44ef3ecd5371
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: dfa9352894d37edb317a6334d7f109419deb362b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-streaming-endpoints-with-hello-azure-portal"></a><span data-ttu-id="4038d-103">Gerenciar pontos de extremidade de streaming com hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4038d-103">Manage streaming endpoints with hello Azure portal</span></span>

<span data-ttu-id="4038d-104">Este tópico mostra como toouse Olá pontos de extremidade de streaming do toomanage portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4038d-104">This topic shows  how toouse hello Azure portal toomanage streaming endpoints.</span></span> 

>[!NOTE]
><span data-ttu-id="4038d-105">Verifique se Olá de tooreview [visão geral](media-services-streaming-endpoints-overview.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="4038d-105">Make sure tooreview hello [overview](media-services-streaming-endpoints-overview.md) topic.</span></span> 

<span data-ttu-id="4038d-106">Para obter informações sobre como tooscale Olá ponto de extremidade de streaming, consulte [isso](media-services-portal-scale-streaming-endpoints.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="4038d-106">For information about how tooscale hello streaming endpoint, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <a name="start-managing-streaming-endpoints"></a><span data-ttu-id="4038d-107">Começar a gerenciar pontos de extremidade de streaming</span><span class="sxs-lookup"><span data-stu-id="4038d-107">Start managing streaming endpoints</span></span> 

<span data-ttu-id="4038d-108">toostart gerenciar pontos de extremidade de streaming para sua conta, Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="4038d-108">toostart managing streaming endpoints for your account, do hello following.</span></span>

1. <span data-ttu-id="4038d-109">Em Olá [portal do Azure](https://portal.azure.com/), selecione sua conta de serviços de mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="4038d-109">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="4038d-110">Em Olá **configurações** folha, selecione **pontos de extremidade de Streaming**.</span><span class="sxs-lookup"><span data-stu-id="4038d-110">In hello **Settings** blade, select **Streaming endpoints**.</span></span>
   
    ![ponto de extremidade de streaming](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints1.png)

> [!NOTE]
> <span data-ttu-id="4038d-112">Você será cobrado apenas quando seu ponto de extremidade de streaming estiver em estado de execução.</span><span class="sxs-lookup"><span data-stu-id="4038d-112">You are only billed when your Streaming Endpoint is in running state.</span></span>

## <a name="adddelete-a-streaming-endpoint"></a><span data-ttu-id="4038d-113">Adicionar/excluir um ponto de extremidade de streaming</span><span class="sxs-lookup"><span data-stu-id="4038d-113">Add/delete a streaming endpoint</span></span>

>[!NOTE]
><span data-ttu-id="4038d-114">padrão de saudação ponto de extremidade de streaming não pode ser excluído.</span><span class="sxs-lookup"><span data-stu-id="4038d-114">hello default streaming endpoint cannot be deleted.</span></span>

<span data-ttu-id="4038d-115">usando o ponto de extremidade de streaming tooadd/excluir Olá portal do Azure, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="4038d-115">tooadd/delete streaming endpoint using hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="4038d-116">tooadd um ponto de extremidade de streaming, clique em Olá **+ Endpoint** na parte superior de saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="4038d-116">tooadd a streaming endpoint, click hello **+ Endpoint** at hello top of hello page.</span></span> 

    <span data-ttu-id="4038d-117">Convém vários pontos de extremidade de Streaming se você planejar toohave CDNs diferentes ou um CDN e acesso direto.</span><span class="sxs-lookup"><span data-stu-id="4038d-117">You might want multiple Streaming Endpoints if you plan toohave different CDNs or a CDN and direct access.</span></span>

2. <span data-ttu-id="4038d-118">toodelete um ponto de extremidade de streaming, pressione **excluir** botão.</span><span class="sxs-lookup"><span data-stu-id="4038d-118">toodelete a streaming endpoint, press **Delete** button.</span></span>      
3. <span data-ttu-id="4038d-119">Clique em Olá **iniciar** saudação do botão toostart ponto de extremidade de streaming.</span><span class="sxs-lookup"><span data-stu-id="4038d-119">Click hello **Start** button toostart hello streaming endpoint.</span></span>
   
    ![ponto de extremidade de streaming](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints2.png)


## <span data-ttu-id="4038d-121"><a id="configure_streaming_endpoints"></a>Configurando Olá ponto de extremidade de Streaming</span><span class="sxs-lookup"><span data-stu-id="4038d-121"><a id="configure_streaming_endpoints"></a>Configuring hello Streaming Endpoint</span></span>
<span data-ttu-id="4038d-122">Ponto de extremidade de streaming permite Olá tooconfigure propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="4038d-122">Streaming Endpoint enables you tooconfigure hello following properties:</span></span>

* <span data-ttu-id="4038d-123">Controle de acesso</span><span class="sxs-lookup"><span data-stu-id="4038d-123">Access control</span></span>
* <span data-ttu-id="4038d-124">Controle de cache</span><span class="sxs-lookup"><span data-stu-id="4038d-124">Cache control</span></span>
* <span data-ttu-id="4038d-125">Políticas de acesso entre sites</span><span class="sxs-lookup"><span data-stu-id="4038d-125">Cross site access policies</span></span>

<span data-ttu-id="4038d-126">Para obter informações detalhadas sobre essas propriedades, consulte [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span><span class="sxs-lookup"><span data-stu-id="4038d-126">For detailed information about these properties, see [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span></span>

<span data-ttu-id="4038d-127">Você pode configurar o ponto de extremidade de streaming fazendo Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="4038d-127">You can configure streaming endpoint by doing hello following:</span></span>

1. <span data-ttu-id="4038d-128">Selecione Olá deseja tooconfigure de ponto de extremidade de streaming.</span><span class="sxs-lookup"><span data-stu-id="4038d-128">Select hello streaming endpoint you want tooconfigure.</span></span>
2. <span data-ttu-id="4038d-129">Clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="4038d-129">Click **Settings**.</span></span>

<span data-ttu-id="4038d-130">Segue uma breve descrição dos campos de saudação.</span><span class="sxs-lookup"><span data-stu-id="4038d-130">A brief description of hello fields follows.</span></span>

![ponto de extremidade de streaming](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints4.png)

1. <span data-ttu-id="4038d-132">Política de cache máximo: tooconfigure usado tempo de vida de ativos atendidas por esse ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="4038d-132">Maximum cache policy: used tooconfigure cache lifetime for assets served through this streaming endpoint.</span></span> <span data-ttu-id="4038d-133">Se nenhum valor for definido, o padrão de saudação é usado.</span><span class="sxs-lookup"><span data-stu-id="4038d-133">If no value is set, hello default is used.</span></span> <span data-ttu-id="4038d-134">valores padrão de saudação também podem ser definidos diretamente no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="4038d-134">hello default values can also be defined directly in Azure storage.</span></span> <span data-ttu-id="4038d-135">Se Azure CDN é habilitado para Olá ponto de extremidade de streaming, você não deve definir tooless de valor de política de cache de saudação de 600 segundos.</span><span class="sxs-lookup"><span data-stu-id="4038d-135">If Azure CDN is enabled for hello streaming endpoint, you should not set hello cache policy value tooless than 600 seconds.</span></span>  
2. <span data-ttu-id="4038d-136">Endereços IP permitidos: usados endereços IP toospecify que seriam permitidos tooconnect toohello publicado o ponto de extremidade de streaming.</span><span class="sxs-lookup"><span data-stu-id="4038d-136">Allowed IP addresses: used toospecify IP addresses that would be allowed tooconnect toohello published streaming endpoint.</span></span> <span data-ttu-id="4038d-137">Se nenhum endereço IP especificado, qualquer endereço IP poderá ser capaz de tooconnect.</span><span class="sxs-lookup"><span data-stu-id="4038d-137">If no IP addresses specified, any IP address would be able tooconnect.</span></span> <span data-ttu-id="4038d-138">Os endereços IP podem ser especificados como um único endereço IP (por exemplo, '10.0.0.1'), um intervalo de IP usando um endereço IP e uma máscara de sub-rede CIDR (por exemplo, '10.0.0.1/22') ou um intervalo de IPs usando um endereço IP e uma máscara de sub-rede em notação decimal com ponto (por exemplo, '10.0.0.1(255.255.255.0)').</span><span class="sxs-lookup"><span data-stu-id="4038d-138">IP addresses can be specified as either a single IP address (for example, '10.0.0.1'), an IP range using an IP address and a CIDR subnet mask (for example, '10.0.0.1/22'), or an IP range using IP address and a dotted decimal subnet mask (for example, '10.0.0.1(255.255.255.0)').</span></span>
3. <span data-ttu-id="4038d-139">Configuração de autenticação de cabeçalho de assinatura do Akamai: usado toospecify como a solicitação de autenticação de cabeçalho de assinatura de servidores Akamai está configurada.</span><span class="sxs-lookup"><span data-stu-id="4038d-139">Configuration for Akamai signature header authentication: used toospecify how signature header authentication request from Akamai servers is configured.</span></span> <span data-ttu-id="4038d-140">A data de validade é no formato UTC.</span><span class="sxs-lookup"><span data-stu-id="4038d-140">Expiration is in UTC.</span></span>

## <a name="scale-your-premium-streaming-endpoint"></a><span data-ttu-id="4038d-141">Dimensionar seu ponto de extremidade de streaming</span><span class="sxs-lookup"><span data-stu-id="4038d-141">Scale your Premium streaming endpoint</span></span>

<span data-ttu-id="4038d-142">Para obter mais informações, consulte [este](media-services-portal-scale-streaming-endpoints.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="4038d-142">For more information, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <span data-ttu-id="4038d-143"><a id="enable_cdn"></a>Habilitar a integração da CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="4038d-143"><a id="enable_cdn"></a>Enable Azure CDN integration</span></span>

<span data-ttu-id="4038d-144">Quando você cria uma nova conta, a integração padrão da CDN do Azure para Ponto de Extremidade de Streaming é habilitada por padrão.</span><span class="sxs-lookup"><span data-stu-id="4038d-144">When you create a new account, default Streaming Endpoint Azure CDN integration is enabled by default.</span></span>

<span data-ttu-id="4038d-145">Se você quiser mais tarde Olá toodisable/habilitar CDN, o ponto de extremidade de streaming deve estar no hello **interrompido** estado.</span><span class="sxs-lookup"><span data-stu-id="4038d-145">If you later want toodisable/enable hello CDN, your streaming endpoint must be in hello **stopped** state.</span></span> <span data-ttu-id="4038d-146">Pode levar horas too2 para tooget de integração do Azure CDN Olá habilitado e Olá alterações toobe ativa em Olá todos os POPs de CDN.</span><span class="sxs-lookup"><span data-stu-id="4038d-146">It could take up too2 hours for hello Azure CDN integration tooget enabled and for hello changes toobe active across all hello CDN POPs.</span></span> <span data-ttu-id="4038d-147">No entanto, você pode iniciar o ponto de extremidade de streaming e fluxo sem interrupções do ponto de extremidade de streaming de saudação e após a conclusão da integração hello, fluxo Olá será entregue de saudação CDN.</span><span class="sxs-lookup"><span data-stu-id="4038d-147">However, your can start your streaming endpoint and stream without interruptions from hello streaming endpoint and once hello integration is complete, hello stream will be delivered from hello CDN.</span></span> <span data-ttu-id="4038d-148">Durante a saudação provisionamento período seu ponto de extremidade de streaming estará em **iniciando** estado e você pode observar degredad desempenho.</span><span class="sxs-lookup"><span data-stu-id="4038d-148">During hello provisioning period your streaming endpoint will be in **starting** state and you might observe degredad performance.</span></span>

<span data-ttu-id="4038d-149">Integração CDN está habilitada em todos os execpt centros de dados do Azure Olá China e Goverment Federal regiões.</span><span class="sxs-lookup"><span data-stu-id="4038d-149">CDN integration is enabled in all hello Azure data centers execpt China and Federal Goverment regions.</span></span>

<span data-ttu-id="4038d-150">Depois de ter habilitado, Olá **controle de acesso**, **nome de host personalizado** e **autenticação da assinatura Akamai** configuração é desabilitada.</span><span class="sxs-lookup"><span data-stu-id="4038d-150">Once it is enabled, hello **Access Control**, **Custom hostname** and **Akamai Signature authentication** configuration gets disabled.</span></span>
 
> [!IMPORTANT]
> <span data-ttu-id="4038d-151">A integração dos Serviços de Mídia do Azure à CDN do Azure é implementada da **Verizon na CDN do Azure** para pontos de extremidade de streaming padrão.</span><span class="sxs-lookup"><span data-stu-id="4038d-151">Azure Media Services integration with Azure CDN is implemented on **Azure CDN from Verizon** for standard streaming endpoints.</span></span> <span data-ttu-id="4038d-152">Os pontos de extremidade de streaming Premium podem ser configurados usando todos os **tipos de preço e provedores da CDN do Azure**.</span><span class="sxs-lookup"><span data-stu-id="4038d-152">Premium streaming endpoints can be configured using all **Azure CDN pricing tiers and providers**.</span></span> <span data-ttu-id="4038d-153">Para obter mais informações sobre os recursos de CDN do Azure, consulte Olá [visão geral da CDN](../cdn/cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4038d-153">For more information about Azure CDN features, see hello [CDN overview](../cdn/cdn-overview.md).</span></span>
 
### <a name="additional-considerations"></a><span data-ttu-id="4038d-154">Considerações adicionais</span><span class="sxs-lookup"><span data-stu-id="4038d-154">Additional considerations</span></span>

* <span data-ttu-id="4038d-155">Quando a CDN é habilitada para um ponto de extremidade de streaming, os clientes não é possível solicitar conteúdo diretamente de origem de saudação.</span><span class="sxs-lookup"><span data-stu-id="4038d-155">When CDN is enabled for a streaming endpoint, clients cannot request content directly from hello origin.</span></span> <span data-ttu-id="4038d-156">Se você precisar Olá capacidade tootest seu conteúdo com ou sem CDN, você pode criar outro ponto de extremidade de streaming que não seja CDN habilitada.</span><span class="sxs-lookup"><span data-stu-id="4038d-156">If you need hello ability tootest your content with or without CDN, you can create another streaming endpoint that isn't CDN enabled.</span></span>
* <span data-ttu-id="4038d-157">Seu permanece de nome de host do ponto de extremidade streaming Olá mesmo depois de habilitar a CDN.</span><span class="sxs-lookup"><span data-stu-id="4038d-157">Your streaming endpoint hostname remains hello same after enabling CDN.</span></span> <span data-ttu-id="4038d-158">Você não precisa toomake qualquer fluxo de trabalho de serviços de mídia do tooyour de alterações depois que a CDN está habilitada.</span><span class="sxs-lookup"><span data-stu-id="4038d-158">You don’t need toomake any changes tooyour media services workflow after CDN is enabled.</span></span> <span data-ttu-id="4038d-159">Por exemplo, se o nome de host do ponto de extremidade streaming é strasbourg.streaming.mediaservices.windows.net, depois de habilitar a CDN, Olá exata mesmo nome de host é usado.</span><span class="sxs-lookup"><span data-stu-id="4038d-159">For example, if your streaming endpoint hostname is strasbourg.streaming.mediaservices.windows.net, after enabling CDN, hello exact same hostname is used.</span></span>
* <span data-ttu-id="4038d-160">Para novos pontos de extremidade de streaming, você pode habilitar CDN criando um novo ponto de extremidade; para pontos de extremidade de streaming existentes, é necessário ponto de extremidade do toofirst parar hello e, em seguida, habilitar/desabilitar Olá CDN.</span><span class="sxs-lookup"><span data-stu-id="4038d-160">For new streaming endpoints, you can enable CDN simply by creating a new endpoint; for existing streaming endpoints, you need toofirst stop hello endpoint and then enable/disable hello CDN.</span></span>
* <span data-ttu-id="4038d-161">O ponto de extremidade de streaming padrão pode ser configurado apenas usando o **provedor de CDN padrão da Verizon** no portal de gerenciamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="4038d-161">Standard streaming endpoint can only be configured using **Verizon Standard CDN provider** using Azure management portal.</span></span> <span data-ttu-id="4038d-162">No entanto, você pode habilitar outros provedores de CDN do Azure usando APIs REST.</span><span class="sxs-lookup"><span data-stu-id="4038d-162">However, you can enable other Azure CDN providers using REST APIs.</span></span>

## <a name="configure-cdn-profile"></a><span data-ttu-id="4038d-163">Configurar perfil de CDN</span><span class="sxs-lookup"><span data-stu-id="4038d-163">Configure CDN profile</span></span>

<span data-ttu-id="4038d-164">Você pode configurar o perfil CDN Olá selecionando Olá **gerenciar CDN** botão na parte superior da saudação.</span><span class="sxs-lookup"><span data-stu-id="4038d-164">You can configure hello CDN profile by selecting hello **Manage CDN** button from hello top.</span></span>

![ponto de extremidade de streaming](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints6.png)

## <a name="next-steps"></a><span data-ttu-id="4038d-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4038d-166">Next steps</span></span>
<span data-ttu-id="4038d-167">Examine os roteiros de aprendizagem dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="4038d-167">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4038d-168">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="4038d-168">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

