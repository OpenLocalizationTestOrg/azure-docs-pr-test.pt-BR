---
title: aaaGetting iniciado com a CDN do Azure | Microsoft Docs
description: "Este tópico mostra como tooenable hello Azure Content Delivery Network (CDN). tutorial de saudação orienta na criação de saudação de um novo perfil CDN e o ponto de extremidade."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 4ca51224-5423-419b-98cf-89860ef516d2
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 0ce9802bfd7b60e70a9a62330f5593fc17ea07d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-cdn"></a><span data-ttu-id="5ab25-104">Introdução à CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="5ab25-104">Getting started with Azure CDN</span></span>
<span data-ttu-id="5ab25-105">Este tópico explica a habilitação do Azure CDN por meio da criação de um novo perfil e um ponto de extremidade CDN.</span><span class="sxs-lookup"><span data-stu-id="5ab25-105">This topic walks through enabling Azure CDN by creating a new CDN profile and endpoint.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5ab25-106">Para um Introdução toohow o CDN works, bem como uma lista de recursos, consulte Olá [visão geral da CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5ab25-106">For an introduction toohow CDN works, as well as a list of features, see hello [CDN Overview](cdn-overview.md).</span></span>
> 
> 

## <a name="create-a-new-cdn-profile"></a><span data-ttu-id="5ab25-107">Criar um novo perfil CDN</span><span class="sxs-lookup"><span data-stu-id="5ab25-107">Create a new CDN profile</span></span>
<span data-ttu-id="5ab25-108">Um perfil CDN é um conjunto de pontos de extremidade CDN.</span><span class="sxs-lookup"><span data-stu-id="5ab25-108">A CDN profile is a collection of CDN endpoints.</span></span>  <span data-ttu-id="5ab25-109">Cada perfil contém um ou mais pontos de extremidade CDN.</span><span class="sxs-lookup"><span data-stu-id="5ab25-109">Each profile contains one or more CDN endpoints.</span></span>  <span data-ttu-id="5ab25-110">Você poderá toouse tooorganize de vários perfis seus pontos de extremidade CDN, o domínio da internet, aplicativo web ou algum outro critério.</span><span class="sxs-lookup"><span data-stu-id="5ab25-110">You may wish toouse multiple profiles tooorganize your CDN endpoints by internet domain, web application, or some other criteria.</span></span>

> [!NOTE]
> <span data-ttu-id="5ab25-111">Por padrão, uma única assinatura do Azure é limitado tooeight perfis CDN.</span><span class="sxs-lookup"><span data-stu-id="5ab25-111">By default, a single Azure subscription is limited tooeight CDN profiles.</span></span> <span data-ttu-id="5ab25-112">Cada perfil CDN é limitado tooten pontos de extremidade CDN.</span><span class="sxs-lookup"><span data-stu-id="5ab25-112">Each CDN profile is limited tooten CDN endpoints.</span></span>
> 
> <span data-ttu-id="5ab25-113">Preços de CDN é aplicada no nível de perfil CDN hello.</span><span class="sxs-lookup"><span data-stu-id="5ab25-113">CDN pricing is applied at hello CDN profile level.</span></span> <span data-ttu-id="5ab25-114">Se você desejar toouse uma mistura de CDN do Azure camadas de preços, você precisará vários perfis CDN.</span><span class="sxs-lookup"><span data-stu-id="5ab25-114">If you wish toouse a mix of Azure CDN pricing tiers, you will need multiple CDN profiles.</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a><span data-ttu-id="5ab25-115">Criar um novo ponto final de CDN</span><span class="sxs-lookup"><span data-stu-id="5ab25-115">Create a new CDN endpoint</span></span>
<span data-ttu-id="5ab25-116">**toocreate um novo ponto de extremidade CDN**</span><span class="sxs-lookup"><span data-stu-id="5ab25-116">**toocreate a new CDN endpoint**</span></span>

1. <span data-ttu-id="5ab25-117">Em Olá [Portal do Azure](https://portal.azure.com), navegar tooyour perfil CDN.</span><span class="sxs-lookup"><span data-stu-id="5ab25-117">In hello [Azure Portal](https://portal.azure.com), navigate tooyour CDN profile.</span></span>  <span data-ttu-id="5ab25-118">Você pode ter-fixado toohello painel na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="5ab25-118">You may have pinned it toohello dashboard in hello previous step.</span></span>  <span data-ttu-id="5ab25-119">Se você não, você pode encontrá-lo clicando **procurar**, em seguida, **perfis CDN**, e clicando no perfil Olá planejar tooadd seu ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="5ab25-119">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on hello profile you plan tooadd your endpoint to.</span></span>
   
    <span data-ttu-id="5ab25-120">folha de perfil CDN Olá aparece.</span><span class="sxs-lookup"><span data-stu-id="5ab25-120">hello CDN profile blade appears.</span></span>
   
    ![Perfil CDN][cdn-profile-settings]
2. <span data-ttu-id="5ab25-122">Clique em Olá **Adicionar ponto de extremidade** botão.</span><span class="sxs-lookup"><span data-stu-id="5ab25-122">Click hello **Add Endpoint** button.</span></span>
   
    ![Adicionar botão de ponto de extremidade][cdn-new-endpoint-button]
   
    <span data-ttu-id="5ab25-124">Olá **adicionar um ponto de extremidade** folha é exibida.</span><span class="sxs-lookup"><span data-stu-id="5ab25-124">hello **Add an endpoint** blade appears.</span></span>
   
    ![Adicionar folha de ponto de extremidade][cdn-add-endpoint]
3. <span data-ttu-id="5ab25-126">Insira um **Nome** para esse ponto de extremidade CDN.</span><span class="sxs-lookup"><span data-stu-id="5ab25-126">Enter a **Name** for this CDN endpoint.</span></span>  <span data-ttu-id="5ab25-127">Esse nome será usado tooaccess seus recursos armazenados em cache no domínio Olá `<endpointname>.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="5ab25-127">This name will be used tooaccess your cached resources at hello domain `<endpointname>.azureedge.net`.</span></span>
4. <span data-ttu-id="5ab25-128">Em Olá **tipo de origem** lista suspensa, selecione o tipo de origem.</span><span class="sxs-lookup"><span data-stu-id="5ab25-128">In hello **Origin type** dropdown, select your origin type.</span></span>  <span data-ttu-id="5ab25-129">Selecione **Armazenamento** para uma conta de armazenamento do Azure, **Serviço de nuvem** para um Serviço de Nuvem do Azure, **Aplicativo Web** para um Aplicativo Web do Azure ou **Origem personalizada** para qualquer outra origem de servidor Web acessível publicamente (hospedado no Azure ou em outro lugar).</span><span class="sxs-lookup"><span data-stu-id="5ab25-129">Select **Storage** for an Azure Storage account, **Cloud service** for an Azure Cloud Service, **Web App** for an Azure Web App, or **Custom origin** for any other publicly accessible web server origin (hosted in Azure or elsewhere).</span></span>
   
    ![Tipo de origem CDN](./media/cdn-create-new-endpoint/cdn-origin-type.png)
5. <span data-ttu-id="5ab25-131">Em Olá **nome de host de origem** lista suspensa, selecione ou digite o domínio de origem.</span><span class="sxs-lookup"><span data-stu-id="5ab25-131">In hello **Origin hostname** dropdown, select or type your origin domain.</span></span>  <span data-ttu-id="5ab25-132">Olá suspensa listará todas as origens disponíveis do tipo hello especificada na etapa 4.</span><span class="sxs-lookup"><span data-stu-id="5ab25-132">hello dropdown will list all available origins of hello type you specified in step 4.</span></span>  <span data-ttu-id="5ab25-133">Se você selecionou *origem personalizado* como seu **tipo de origem**, você digitará no domínio de saudação de sua origem personalizada.</span><span class="sxs-lookup"><span data-stu-id="5ab25-133">If you selected *Custom origin* as your **Origin type**, you will type in hello domain of your custom origin.</span></span>
6. <span data-ttu-id="5ab25-134">Em Olá **caminho de origem** texto, digite Olá caminho toohello recursos desejados toocache ou deixe em branco tooallow cache qualquer recurso no domínio Olá especificado na etapa 5.</span><span class="sxs-lookup"><span data-stu-id="5ab25-134">In hello **Origin path** text box, enter hello path toohello resources you want toocache, or leave blank tooallow cache any resource at hello domain you specified in step 5.</span></span>
7. <span data-ttu-id="5ab25-135">Em Olá **cabeçalho de host de origem**, insira o cabeçalho de host Olá deseja Olá CDN toosend com cada solicitação ou deixe o padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="5ab25-135">In hello **Origin host header**, enter hello host header you want hello CDN toosend with each request, or leave hello default.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="5ab25-136">Alguns tipos de origens, como o armazenamento do Azure e os aplicativos Web, exigem domínio Olá host cabeçalho toomatch Olá de origem hello.</span><span class="sxs-lookup"><span data-stu-id="5ab25-136">Some types of origins, such as Azure Storage and Web Apps, require hello host header toomatch hello domain of hello origin.</span></span> <span data-ttu-id="5ab25-137">A menos que você tenha uma origem que requer um cabeçalho de host diferente do seu domínio, você deve deixar o valor padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="5ab25-137">Unless you have an origin that requires a host header different from its domain, you should leave hello default value.</span></span>
   > 
   > 
8. <span data-ttu-id="5ab25-138">Para **protocolo** e **porta de origem**, especificar Olá protocolos e portas tooaccess usado seus recursos na origem de saudação.</span><span class="sxs-lookup"><span data-stu-id="5ab25-138">For **Protocol** and **Origin port**, specify hello protocols and ports used tooaccess your resources at hello origin.</span></span>  <span data-ttu-id="5ab25-139">É necessário selecionar pelo menos um protocolo (HTTP ou HTTPS).</span><span class="sxs-lookup"><span data-stu-id="5ab25-139">At least one protocol (HTTP or HTTPS) must be selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5ab25-140">Olá **porta de origem** afeta somente o ponto de extremidade de saudação de porta usa as informações de tooretrieve de origem hello.</span><span class="sxs-lookup"><span data-stu-id="5ab25-140">hello **Origin port** only affects what port hello endpoint uses tooretrieve information from hello origin.</span></span>  <span data-ttu-id="5ab25-141">Olá ponto de extremidade em si será apenas clientes tooend disponível em saudação padrão portas HTTP e HTTPS (80 e 443), independentemente de saudação **porta de origem**.</span><span class="sxs-lookup"><span data-stu-id="5ab25-141">hello endpoint itself will only be available tooend clients on hello default HTTP and HTTPS ports (80 and 443), regardless of hello **Origin port**.</span></span>  
   > 
   > <span data-ttu-id="5ab25-142">**Azure CDN do Akamai** pontos de extremidade não permitem a gama porta TCP de saudação completa para origens.</span><span class="sxs-lookup"><span data-stu-id="5ab25-142">**Azure CDN from Akamai** endpoints do not allow hello full TCP port range for origins.</span></span>  <span data-ttu-id="5ab25-143">Para obter uma lista das portas de origem que não são permitidas, confira [CDN do Azure das Portas de Origem Permitidas Akamai](https://msdn.microsoft.com/library/mt757337.aspx).</span><span class="sxs-lookup"><span data-stu-id="5ab25-143">For a list of origin ports that are not allowed, see [Azure CDN from Akamai Allowed Origin Ports](https://msdn.microsoft.com/library/mt757337.aspx).</span></span>  
   > 
   > <span data-ttu-id="5ab25-144">Acessar o CDN conteúdo usando HTTPS tem Olá restrições a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ab25-144">Accessing CDN content using HTTPS has hello following constraints:</span></span>
   > 
   > * <span data-ttu-id="5ab25-145">Você deve usar o certificado SSL Olá fornecido pelo Olá CDN.</span><span class="sxs-lookup"><span data-stu-id="5ab25-145">You must use hello SSL certificate provided by hello CDN.</span></span> <span data-ttu-id="5ab25-146">Não há suporte a certificados de terceiros.</span><span class="sxs-lookup"><span data-stu-id="5ab25-146">Third party certificates are not supported.</span></span>
   > * <span data-ttu-id="5ab25-147">Você deve usar o domínio fornecido CDN de saudação (`<endpointname>.azureedge.net`) tooaccess conteúdo em HTTPS.</span><span class="sxs-lookup"><span data-stu-id="5ab25-147">You must use hello CDN-provided domain (`<endpointname>.azureedge.net`) tooaccess HTTPS content.</span></span> <span data-ttu-id="5ab25-148">Suporte ao protocolo HTTPS não está disponível para nomes de domínio personalizados (CNAMEs) como Olá CDN não oferece suporte a certificados personalizados no momento.</span><span class="sxs-lookup"><span data-stu-id="5ab25-148">HTTPS support is not available for custom domain names (CNAMEs) since hello CDN does not support custom certificates at this time.</span></span>
   > 
   > 
9. <span data-ttu-id="5ab25-149">Clique em Olá **adicionar** toocreate botão Olá novo ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="5ab25-149">Click hello **Add** button toocreate hello new endpoint.</span></span>
10. <span data-ttu-id="5ab25-150">Depois que o ponto de extremidade de saudação é criado, ele aparece em uma lista de pontos de extremidade para o perfil de saudação.</span><span class="sxs-lookup"><span data-stu-id="5ab25-150">Once hello endpoint is created, it appears in a list of endpoints for hello profile.</span></span> <span data-ttu-id="5ab25-151">modo de exibição de lista Olá mostra Olá URL toouse tooaccess em cache o conteúdo, bem como domínio de origem de saudação.</span><span class="sxs-lookup"><span data-stu-id="5ab25-151">hello list view shows hello URL toouse tooaccess cached content, as well as hello origin domain.</span></span>
    
    ![Ponto de extremidade CDN][cdn-endpoint-success]
    
    > [!IMPORTANT]
    > <span data-ttu-id="5ab25-153">ponto de extremidade de saudação não estará disponível imediatamente para uso, como demora Olá toopropagate de registro por meio de saudação CDN.</span><span class="sxs-lookup"><span data-stu-id="5ab25-153">hello endpoint will not immediately be available for use, as it takes time for hello registration toopropagate through hello CDN.</span></span>  <span data-ttu-id="5ab25-154">Para <b>Azure CDN do Akamai</b> , a propagação geralmente é concluída em um minuto.</span><span class="sxs-lookup"><span data-stu-id="5ab25-154">For <b>Azure CDN from Akamai</b> profiles, propagation will usually complete within one minute.</span></span>  <span data-ttu-id="5ab25-155">Para perfis da <b>CDN do Azure da Verizon</b>, a propagação geralmente é concluída em 90 minutos, mas em alguns casos pode levar mais tempo.</span><span class="sxs-lookup"><span data-stu-id="5ab25-155">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
    > 
    > <span data-ttu-id="5ab25-156">Os usuários que tentarem nome de domínio toouse Olá CDN antes de configuração de ponto de extremidade Olá propagou toohello POPs receberá códigos de resposta HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="5ab25-156">Users who try toouse hello CDN domain name before hello endpoint configuration has propagated toohello POPs will receive HTTP 404 response codes.</span></span>  <span data-ttu-id="5ab25-157">Se passaram várias horas desde que você criou o ponto de extremidade e ainda está recebendo respostas 404, consulte [Solucionando problemas dos pontos de extremidade CDN retornando status 404](cdn-troubleshoot-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="5ab25-157">If it's been several hours since you created your endpoint and you're still receiving 404 responses, please see [Troubleshooting CDN endpoints returning 404 statuses](cdn-troubleshoot-endpoint.md).</span></span>
    > 
    > 

## <a name="see-also"></a><span data-ttu-id="5ab25-158">Consulte também</span><span class="sxs-lookup"><span data-stu-id="5ab25-158">See Also</span></span>
* [<span data-ttu-id="5ab25-159">Controle do comportamento do cache de solicitações com cadeias de caracteres de consulta</span><span class="sxs-lookup"><span data-stu-id="5ab25-159">Controlling caching behavior of requests with query strings</span></span>](cdn-query-string.md)
* [<span data-ttu-id="5ab25-160">Como tooMap conteúdo CDN tooa domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="5ab25-160">How tooMap CDN Content tooa Custom Domain</span></span>](cdn-map-content-to-custom-domain.md)
* [<span data-ttu-id="5ab25-161">Pré-carregar ativos em um ponto de extremidade da CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="5ab25-161">Pre-load assets on an Azure CDN endpoint</span></span>](cdn-preload-endpoint.md)
* [<span data-ttu-id="5ab25-162">Limpar um ponto de extremidade CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="5ab25-162">Purge an Azure CDN Endpoint</span></span>](cdn-purge-endpoint.md)
* [<span data-ttu-id="5ab25-163">Solucionando problemas dos pontos de extremidade CDN retornando status 404</span><span class="sxs-lookup"><span data-stu-id="5ab25-163">Troubleshooting CDN endpoints returning 404 statuses</span></span>](cdn-troubleshoot-endpoint.md)

[cdn-profile-settings]: ./media/cdn-create-new-endpoint/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-create-new-endpoint/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-create-new-endpoint/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-create-new-endpoint/cdn-endpoint-success.png
