---
title: aaaHow toocreate e publicar um produto no gerenciamento de API do Azure
description: Saiba como toocreate e publicar produtos no gerenciamento de API do Azure.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 31de55cb-9384-490b-a2f2-6dfcf83da764
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: f0a37f08b4e29ca68be9caec4c7604e3b4b6aaa6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-publish-a-product-in-azure-api-management"></a><span data-ttu-id="0eb16-103">Como toocreate e publicar um produto no gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="0eb16-103">How toocreate and publish a product in Azure API Management</span></span>
<span data-ttu-id="0eb16-104">No gerenciamento de API do Azure, um produto contém um ou mais APIs, bem como em termos de cota e hello de uso de uso.</span><span class="sxs-lookup"><span data-stu-id="0eb16-104">In Azure API Management, a product contains one or more APIs as well as a usage quota and hello terms of use.</span></span> <span data-ttu-id="0eb16-105">Depois que um produto é publicado, os desenvolvedores podem assinar toohello produto e começar a APIs do produto do toouse hello.</span><span class="sxs-lookup"><span data-stu-id="0eb16-105">Once a product is published, developers can subscribe toohello product and begin toouse hello product's APIs.</span></span> <span data-ttu-id="0eb16-106">tópico de Olá fornece um guia toocreating um produto, a adição de uma API e publicá-la para desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="0eb16-106">hello topic provides a guide toocreating a product, adding an API, and publishing it for developers.</span></span>

## <span data-ttu-id="0eb16-107"><a name="create-product"> </a>Criar um produto</span><span class="sxs-lookup"><span data-stu-id="0eb16-107"><a name="create-product"> </a>Create a product</span></span>
<span data-ttu-id="0eb16-108">As operações são adicionadas e configurados tooan API no portal do publicador Olá.</span><span class="sxs-lookup"><span data-stu-id="0eb16-108">Operations are added and configured tooan API in hello publisher portal.</span></span> <span data-ttu-id="0eb16-109">tooaccess Olá clique portal, publisher **portal do publicador** em hello Portal do Azure para seu serviço de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="0eb16-109">tooaccess hello publisher portal, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![Portal do editor][api-management-management-console]

> <span data-ttu-id="0eb16-111">Se você ainda não tiver criado uma instância do serviço de gerenciamento de API, consulte [criar uma instância do serviço de gerenciamento de API] [ Create an API Management service instance] em Olá [Introdução ao gerenciamento de API do Azure] [ Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="0eb16-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="0eb16-112">Clique em **produtos** na menu Olá Olá toodisplay esquerdo Olá **produtos** página e, em seguida, clique em **adicionar produto**.</span><span class="sxs-lookup"><span data-stu-id="0eb16-112">Click on **Products** in hello menu on hello left toodisplay hello **Products** page, and click **Add Product**.</span></span>

![Produtos][api-management-products]

![Novo produto][api-management-add-new-product]

<span data-ttu-id="0eb16-115">Insira um nome descritivo para o produto de saudação em Olá **nome** campo e uma descrição de produto Olá Olá **descrição** campo.</span><span class="sxs-lookup"><span data-stu-id="0eb16-115">Enter a descriptive name for hello product in hello **Name** field and a description of hello product in hello **Description** field.</span></span>

<span data-ttu-id="0eb16-116">Produtos de Gerenciamento de API podem ser **Livres** ou **Protegidos**.</span><span class="sxs-lookup"><span data-stu-id="0eb16-116">Products in API Management can be **Open** or **Protected**.</span></span> <span data-ttu-id="0eb16-117">Produtos protegidos devem ser assinado toobefore, eles podem ser usados, ao abrir produtos podem ser usados sem uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="0eb16-117">Protected products must be subscribed toobefore they can be used, while open products can be used without a subscription.</span></span> <span data-ttu-id="0eb16-118">Verificar **exigir assinatura** toocreate um produto protegido que requer uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="0eb16-118">Check **Require subscription** toocreate a protected product that requires a subscription.</span></span> <span data-ttu-id="0eb16-119">Essa é a configuração de padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="0eb16-119">This is hello default setting.</span></span>

<span data-ttu-id="0eb16-120">Verificar **exigirem a aprovação de assinatura** se você deseja que um administrador tooreview e aceitar ou rejeitar assinatura tentativas toothis produto.</span><span class="sxs-lookup"><span data-stu-id="0eb16-120">Check **Require subscription approval** if you want an administrator tooreview and accept or reject subscription attempts toothis product.</span></span> <span data-ttu-id="0eb16-121">Se Olá caixa está desmarcada, tentativas de assinatura serão aprovadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="0eb16-121">If hello box is unchecked, subscription attempts will be auto-approved.</span></span> <span data-ttu-id="0eb16-122">Para obter mais informações sobre assinaturas, consulte [produto do modo de exibição assinantes tooa][View subscribers tooa product].</span><span class="sxs-lookup"><span data-stu-id="0eb16-122">For more information on subscriptions, see [View subscribers tooa product][View subscribers tooa product].</span></span>

<span data-ttu-id="0eb16-123">toosubscribe contas de desenvolvedor tooallow produto de toohello várias vezes, verifique Olá **permitir várias assinaturas** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="0eb16-123">tooallow developer accounts toosubscribe multiple times toohello product, check hello **Allow multiple subscriptions** check box.</span></span> <span data-ttu-id="0eb16-124">Se essa caixa não estiver marcada, cada conta de desenvolvedor pode inscrever-se apenas um produto de toohello única vez.</span><span class="sxs-lookup"><span data-stu-id="0eb16-124">If this box is not checked, each developer account can subscribe only a single time toohello product.</span></span>

![Várias assinaturas ilimitadas][api-management-unlimited-multiple-subscriptions]

<span data-ttu-id="0eb16-126">Contagem de saudação toolimit de várias assinaturas simultâneas, verifique Olá **limitar o número de assinaturas simultâneas para** caixa de seleção e insira o limite de assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="0eb16-126">toolimit hello count of multiple simultaneous subscriptions, check hello **Limit number of simultaneous subscriptions to** check box and enter hello subscription limit.</span></span> <span data-ttu-id="0eb16-127">Em Olá exemplo a seguir, assinaturas simultâneas são toofour limitado por conta de desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="0eb16-127">In hello following example, simultaneous subscriptions are limited toofour per developer account.</span></span>

![Quatro assinaturas][api-management-four-multiple-subscriptions]

<span data-ttu-id="0eb16-129">Depois que todas as novas opções de produto são configuradas, clique em **salvar** novo produto do toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="0eb16-129">Once all new product options are configured, click **Save** toocreate hello new product.</span></span>

![Produtos][api-management-products-page]

> <span data-ttu-id="0eb16-131">Por padrão novos produtos são não publicados e são visível toohello somente **administradores** grupo.</span><span class="sxs-lookup"><span data-stu-id="0eb16-131">By default new products are unpublished, and are visible only toohello  **Administrators** group.</span></span>
> 
> 

<span data-ttu-id="0eb16-132">tooconfigure um produto, clique no nome do produto de saudação em Olá **produtos** guia.</span><span class="sxs-lookup"><span data-stu-id="0eb16-132">tooconfigure a product, click on hello product name in hello **Products** tab.</span></span>

## <span data-ttu-id="0eb16-133"><a name="add-apis"></a>Produto de tooa adicionar APIs</span><span class="sxs-lookup"><span data-stu-id="0eb16-133"><a name="add-apis"> </a>Add APIs tooa product</span></span>
<span data-ttu-id="0eb16-134">Olá **produtos** página contém quatro links para a configuração: **resumo**, **configurações**, **visibilidade**, e  **Os assinantes**.</span><span class="sxs-lookup"><span data-stu-id="0eb16-134">hello **Products** page contains four links for configuration: **Summary**, **Settings**, **Visibility**, and **Subscribers**.</span></span> <span data-ttu-id="0eb16-135">Olá **resumo** guia é onde você pode adicionar APIs e publicar ou cancelar a publicação de um produto.</span><span class="sxs-lookup"><span data-stu-id="0eb16-135">hello **Summary** tab is where you can add APIs and publish or unpublish a product.</span></span>

![Resumo][api-management-new-product-summary]

<span data-ttu-id="0eb16-137">Antes de publicar seu produto é necessário tooadd uma ou mais APIs.</span><span class="sxs-lookup"><span data-stu-id="0eb16-137">Before publishing your product you need tooadd one or more APIs.</span></span> <span data-ttu-id="0eb16-138">toodo, clique **tooproduct adicionar API**.</span><span class="sxs-lookup"><span data-stu-id="0eb16-138">toodo this, click **Add API tooproduct**.</span></span>

![Adicionar APIs][api-management-add-apis-to-product]

<span data-ttu-id="0eb16-140">Selecione Olá desejado APIs e clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="0eb16-140">Select hello desired APIs and click **Save**.</span></span>

## <span data-ttu-id="0eb16-141"><a name="add-description"></a>Produto do adicionar informações descritivas tooa</span><span class="sxs-lookup"><span data-stu-id="0eb16-141"><a name="add-description"> </a>Add descriptive information tooa product</span></span>
<span data-ttu-id="0eb16-142">Olá **configurações** guia permite que você tooprovide informações detalhadas sobre o produto hello como sua finalidade, Olá APIs que fornece acesso a e outras informações úteis.</span><span class="sxs-lookup"><span data-stu-id="0eb16-142">hello **Settings** tab allows you tooprovide detailed information about hello product such as its purpose, hello APIs it provides access to, and other useful information.</span></span> <span data-ttu-id="0eb16-143">conteúdo de saudação é destinado a desenvolvedores Olá que serão chamado hello API e podem ser gravados em texto sem formatação ou marcação HTML.</span><span class="sxs-lookup"><span data-stu-id="0eb16-143">hello content is targeted at hello developers that will be calling hello API and can be written in plain text or HTML markup.</span></span>

![Configurações do produto][api-management-product-settings]

<span data-ttu-id="0eb16-145">Verificar **exigir assinatura** toocreate um produto protegido que requer um toobe de assinatura usado ou desmarque Olá toocreate da caixa de seleção um produto aberto que pode ser chamado sem uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="0eb16-145">Check **Require subscription** toocreate a protected product that requires a subscription toobe used, or clear hello checkbox toocreate an open product that can be called without a subscription.</span></span>

<span data-ttu-id="0eb16-146">Selecione **exigirem a aprovação de assinatura** se você quiser toomanually aprovar todas as solicitações de assinatura de produto.</span><span class="sxs-lookup"><span data-stu-id="0eb16-146">Select **Require subscription approval** if you want toomanually approve all product subscription requests.</span></span> <span data-ttu-id="0eb16-147">Por padrão, todas as assinaturas de produto são aprovadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="0eb16-147">By default all product subscriptions are granted automatically.</span></span>

<span data-ttu-id="0eb16-148">toosubscribe contas de desenvolvedor tooallow produto de toohello várias vezes, verifique Olá **permitir várias assinaturas** caixa de seleção e, opcionalmente, especificar um limite.</span><span class="sxs-lookup"><span data-stu-id="0eb16-148">tooallow developer accounts toosubscribe multiple times toohello product, check hello **Allow multiple subscriptions** check box and optionally specify a limit.</span></span> <span data-ttu-id="0eb16-149">Se essa caixa não estiver marcada, cada conta de desenvolvedor pode inscrever-se apenas um produto de toohello única vez.</span><span class="sxs-lookup"><span data-stu-id="0eb16-149">If this box is not checked, each developer account can subscribe only a single time toohello product.</span></span>

<span data-ttu-id="0eb16-150">Opcionalmente, preencha Olá **termos de uso** campo que descreve os termos de saudação de uso de produto de saudação que os assinantes devem aceitar no produto de saudação do pedido toouse.</span><span class="sxs-lookup"><span data-stu-id="0eb16-150">Optionally fill in hello **Terms of use** field describing hello terms of use for hello product which subscribers must accept in order toouse hello product.</span></span>

## <span data-ttu-id="0eb16-151"><a name="publish-product"> </a>Publicar um produto</span><span class="sxs-lookup"><span data-stu-id="0eb16-151"><a name="publish-product"> </a>Publish a product</span></span>
<span data-ttu-id="0eb16-152">Antes de saudação APIs em um produto pode ser chamada, produto Olá deve ser publicado.</span><span class="sxs-lookup"><span data-stu-id="0eb16-152">Before hello APIs in a product can be called, hello product must be published.</span></span> <span data-ttu-id="0eb16-153">Em Olá **resumo** produto hello, clique em **publicar**e, em seguida, clique em **Sim, publicá-lo** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="0eb16-153">On hello **Summary** tab for hello product, click **Publish**, and then click **Yes, publish it** tooconfirm.</span></span> <span data-ttu-id="0eb16-154">toomake privado um produto publicada anteriormente, clique em **Cancelar publicação**.</span><span class="sxs-lookup"><span data-stu-id="0eb16-154">toomake a previously published product private, click **Unpublish**.</span></span>

![Publicar produto][api-management-publish-product]

## <span data-ttu-id="0eb16-156"><a name="make-visible"></a>Fazer um toodevelopers visível do produto</span><span class="sxs-lookup"><span data-stu-id="0eb16-156"><a name="make-visible"> </a>Make a product visible toodevelopers</span></span>
<span data-ttu-id="0eb16-157">Olá **visibilidade** guia permite que você toochoose quais funções são capazes de toosee Olá produto no portal do desenvolvedor hello e assinar toohello produto.</span><span class="sxs-lookup"><span data-stu-id="0eb16-157">hello **Visibility** tab allows you toochoose which roles are able toosee hello product on hello developer portal and subscribe toohello product.</span></span>

![Visibilidade do produto][api-management-product-visiblity]

<span data-ttu-id="0eb16-159">tooenable ou desativar visibilidade de um produto para desenvolvedores de saudação em um grupo, marque ou desmarque Olá a caixa de seleção ao lado do grupo de saudação e, em seguida, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="0eb16-159">tooenable or disable visibility of a product for hello developers in a group, check or uncheck hello check box beside hello group and then click **Save**.</span></span>

> <span data-ttu-id="0eb16-160">Para obter mais informações, consulte [como desenvolvedor de toomanage grupos toocreate e usar contas no gerenciamento de API do Azure][How toocreate and use groups toomanage developer accounts in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="0eb16-160">For more information, see [How toocreate and use groups toomanage developer accounts in Azure API Management][How toocreate and use groups toomanage developer accounts in Azure API Management].</span></span>
> 
> 

## <span data-ttu-id="0eb16-161"><a name="view-subscribers"></a>Produto de tooa de assinantes do modo de exibição</span><span class="sxs-lookup"><span data-stu-id="0eb16-161"><a name="view-subscribers"> </a>View subscribers tooa product</span></span>
<span data-ttu-id="0eb16-162">Olá **assinantes** guia lista os desenvolvedores de saudação que assinaram toohello produto.</span><span class="sxs-lookup"><span data-stu-id="0eb16-162">hello **Subscribers** tab lists hello developers who have subscribed toohello product.</span></span> <span data-ttu-id="0eb16-163">Olá detalhes e as configurações para cada desenvolvedor podem ser exibidas clicando no nome do desenvolvedor hello.</span><span class="sxs-lookup"><span data-stu-id="0eb16-163">hello details and settings for each developer can be viewed by clicking on hello developer's name.</span></span> <span data-ttu-id="0eb16-164">Neste exemplo não desenvolvedores inscreveu ainda toohello produto.</span><span class="sxs-lookup"><span data-stu-id="0eb16-164">In this example no developers have yet subscribed toohello product.</span></span>

![Desenvolvedores][api-management-developer-list]

## <span data-ttu-id="0eb16-166"><a name="next-steps"> </a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0eb16-166"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="0eb16-167">Uma vez Olá desejado APIs foram adicionadas e produto Olá publicado, os desenvolvedores podem assinar toohello produto e começar a saudação toocall APIs.</span><span class="sxs-lookup"><span data-stu-id="0eb16-167">Once hello desired APIs are added and hello product published, developers can subscribe toohello product and begin toocall hello APIs.</span></span> <span data-ttu-id="0eb16-168">Para ver um tutorial que demonstra esses itens, bem como a configuração avançada do produto, consulte [Como criar e definir configurações avançadas no Gerenciamento de API do Azure][How create and configure advanced product settings in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="0eb16-168">For a tutorial that demonstrates these items as well as advanced product configuration see [How create and configure advanced product settings in Azure API Management][How create and configure advanced product settings in Azure API Management].</span></span>

<span data-ttu-id="0eb16-169">Para obter mais informações sobre como trabalhar com produtos, consulte Olá vídeo a seguir.</span><span class="sxs-lookup"><span data-stu-id="0eb16-169">For more information about working with products, see hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

[Create a product]: #create-product
[Add APIs tooa product]: #add-apis
[Add descriptive information tooa product]: #add-description
[Publish a product]: #publish-product
[Make a product visible toodevelopers]: #make-visible
[View subscribers tooa product]: #view-subscribers
[Next steps]: #next-steps

[api-management-management-console]: ./media/api-management-howto-add-products/api-management-management-console.png
[api-management-add-product]: ./media/api-management-howto-add-products/api-management-add-product.png
[api-management-add-new-product]: ./media/api-management-howto-add-products/api-management-add-new-product.png
[api-management-unlimited-multiple-subscriptions]: ./media/api-management-howto-add-products/api-management-unlimited-multiple-subscriptions.png
[api-management-four-multiple-subscriptions]: ./media/api-management-howto-add-products/api-management-four-multiple-subscriptions.png
[api-management-products-page]: ./media/api-management-howto-add-products/api-management-products-page.png
[api-management-new-product-summary]: ./media/api-management-howto-add-products/api-management-new-product-summary.png
[api-management-add-apis-to-product]: ./media/api-management-howto-add-products/api-management-add-apis-to-product.png
[api-management-product-settings]: ./media/api-management-howto-add-products/api-management-product-settings.png
[api-management-publish-product]: ./media/api-management-howto-add-products/api-management-publish-product.png
[api-management-product-visiblity]: ./media/api-management-howto-add-products/api-management-product-visibility.png
[api-management-developer-list]: ./media/api-management-howto-add-products/api-management-developer-list.png



[api-management-products]: ./media/api-management-howto-add-products/api-management-products.png
[api-management-]: ./media/api-management-howto-add-products/
[api-management-]: ./media/api-management-howto-add-products/


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps
[How toocreate and use groups toomanage developer accounts in Azure API Management]: api-management-howto-create-groups.md
[How create and configure advanced product settings in Azure API Management]: api-management-howto-product-with-rules.md 
