---
title: Como criar e publicar um produto no Gerenciamento de API do Azure
description: Aprenda a criar e publicar produtos no Gerenciamento de API do Azure.
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
ms.openlocfilehash: 73bf4451ba1b71807e22440beecc73a7e8045c5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-publish-a-product-in-azure-api-management"></a><span data-ttu-id="f4add-103">Como criar e publicar um produto no Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="f4add-103">How to create and publish a product in Azure API Management</span></span>
<span data-ttu-id="f4add-104">No Gerenciamento de API, um produto contém uma ou mais APIs, bem como uma quota de uso e os termos de uso.</span><span class="sxs-lookup"><span data-stu-id="f4add-104">In Azure API Management, a product contains one or more APIs as well as a usage quota and the terms of use.</span></span> <span data-ttu-id="f4add-105">Uma vez publicado o produto, os desenvolvedores podem assinar o produto e começar a usar as APIs dele.</span><span class="sxs-lookup"><span data-stu-id="f4add-105">Once a product is published, developers can subscribe to the product and begin to use the product's APIs.</span></span> <span data-ttu-id="f4add-106">Este tópico fornece um guia para criar um produto, adicionar uma API e publicá-la para os desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="f4add-106">The topic provides a guide to creating a product, adding an API, and publishing it for developers.</span></span>

## <span data-ttu-id="f4add-107"><a name="create-product"> </a>Criar um produto</span><span class="sxs-lookup"><span data-stu-id="f4add-107"><a name="create-product"> </a>Create a product</span></span>
<span data-ttu-id="f4add-108">Operações são adicionadas e configuradas em uma API no Portal do editor.</span><span class="sxs-lookup"><span data-stu-id="f4add-108">Operations are added and configured to an API in the publisher portal.</span></span> <span data-ttu-id="f4add-109">Para acessar o portal do editor, clique em **Portal do editor** no Portal do Azure para acessar o serviço Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="f4add-109">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![Portal do editor][api-management-management-console]

> <span data-ttu-id="f4add-111">Se ainda não criou uma instância de serviço de Gerenciamento de API, confira [Criar uma instância de serviço de Gerenciamento de API][Create an API Management service instance] no tutorial [Introdução ao Gerenciamento de API do Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="f4add-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="f4add-112">Clique em **Produtos** no menu à esquerda para exibir a página **Produtos** e clique em **Adicionar Produto**.</span><span class="sxs-lookup"><span data-stu-id="f4add-112">Click on **Products** in the menu on the left to display the **Products** page, and click **Add Product**.</span></span>

![Produtos][api-management-products]

![Novo produto][api-management-add-new-product]

<span data-ttu-id="f4add-115">Insira um nome descritivo para o produto no campo **Nome** e uma descrição do produto no campo **Descrição**.</span><span class="sxs-lookup"><span data-stu-id="f4add-115">Enter a descriptive name for the product in the **Name** field and a description of the product in the **Description** field.</span></span>

<span data-ttu-id="f4add-116">Produtos de Gerenciamento de API podem ser **Livres** ou **Protegidos**.</span><span class="sxs-lookup"><span data-stu-id="f4add-116">Products in API Management can be **Open** or **Protected**.</span></span> <span data-ttu-id="f4add-117">Produtos protegidos devem ser assinados antes que possam ser usados, enquanto produtos abertos podem ser usados sem uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="f4add-117">Protected products must be subscribed to before they can be used, while open products can be used without a subscription.</span></span> <span data-ttu-id="f4add-118">Marque **Exigir assinatura** para criar um produto protegido que requer uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="f4add-118">Check **Require subscription** to create a protected product that requires a subscription.</span></span> <span data-ttu-id="f4add-119">Esta é a configuração padrão.</span><span class="sxs-lookup"><span data-stu-id="f4add-119">This is the default setting.</span></span>

<span data-ttu-id="f4add-120">Marque **Requerer aprovação de assinatura** se desejar que um administrador revise e aceite ou rejeite as tentativas de assinatura para o produto.</span><span class="sxs-lookup"><span data-stu-id="f4add-120">Check **Require subscription approval** if you want an administrator to review and accept or reject subscription attempts to this product.</span></span> <span data-ttu-id="f4add-121">Se a caixa não estiver marcada, as tentativas de assinatura serão aprovadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="f4add-121">If the box is unchecked, subscription attempts will be auto-approved.</span></span> <span data-ttu-id="f4add-122">Para obter mais informações sobre assinaturas, consulte [Exibir os assinantes de um produto][View subscribers to a product].</span><span class="sxs-lookup"><span data-stu-id="f4add-122">For more information on subscriptions, see [View subscribers to a product][View subscribers to a product].</span></span>

<span data-ttu-id="f4add-123">Para permitir que contas de desenvolvedor assinem o produto várias vezes, marque a caixa de seleção **Permitir várias assinaturas** .</span><span class="sxs-lookup"><span data-stu-id="f4add-123">To allow developer accounts to subscribe multiple times to the product, check the **Allow multiple subscriptions** check box.</span></span> <span data-ttu-id="f4add-124">Se essa caixa não estiver marcada, cada conta de desenvolvedor poderá assinar o produto uma única vez.</span><span class="sxs-lookup"><span data-stu-id="f4add-124">If this box is not checked, each developer account can subscribe only a single time to the product.</span></span>

![Várias assinaturas ilimitadas][api-management-unlimited-multiple-subscriptions]

<span data-ttu-id="f4add-126">Para limitar a contagem de várias assinaturas simultâneas, marque a caixa de seleção **Limitar o número de assinaturas simultâneas a** e insira o limite de assinaturas.</span><span class="sxs-lookup"><span data-stu-id="f4add-126">To limit the count of multiple simultaneous subscriptions, check the **Limit number of simultaneous subscriptions to** check box and enter the subscription limit.</span></span> <span data-ttu-id="f4add-127">No exemplo a seguir, as assinaturas simultâneas são limitadas a quatro por conta de desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="f4add-127">In the following example, simultaneous subscriptions are limited to four per developer account.</span></span>

![Quatro assinaturas][api-management-four-multiple-subscriptions]

<span data-ttu-id="f4add-129">Depois que todas as novas opções de produto forem configuradas, clique em **Salvar** para criar o novo produto.</span><span class="sxs-lookup"><span data-stu-id="f4add-129">Once all new product options are configured, click **Save** to create the new product.</span></span>

![Produtos][api-management-products-page]

> <span data-ttu-id="f4add-131">Por padrão, novos produtos não são publicados e ficam visíveis somente para o grupo **Administradores** .</span><span class="sxs-lookup"><span data-stu-id="f4add-131">By default new products are unpublished, and are visible only to the  **Administrators** group.</span></span>
> 
> 

<span data-ttu-id="f4add-132">Para configurar um produto, clique o nome do produto na guia **Produtos** .</span><span class="sxs-lookup"><span data-stu-id="f4add-132">To configure a product, click on the product name in the **Products** tab.</span></span>

## <span data-ttu-id="f4add-133"><a name="add-apis"> </a>Adicionar APIs a um produto</span><span class="sxs-lookup"><span data-stu-id="f4add-133"><a name="add-apis"> </a>Add APIs to a product</span></span>
<span data-ttu-id="f4add-134">A página **Produtos** contém quatro links para configuração: **Resumo**, **Configurações**, **Visibilidade** e **Assinantes**.</span><span class="sxs-lookup"><span data-stu-id="f4add-134">The **Products** page contains four links for configuration: **Summary**, **Settings**, **Visibility**, and **Subscribers**.</span></span> <span data-ttu-id="f4add-135">A guia **Resumo** é onde você pode adicionar APIs e publicar ou cancelar a publicação de um produto.</span><span class="sxs-lookup"><span data-stu-id="f4add-135">The **Summary** tab is where you can add APIs and publish or unpublish a product.</span></span>

![Resumo][api-management-new-product-summary]

<span data-ttu-id="f4add-137">Antes de publicar o produto, você precisa adicionar uma ou mais APIs.</span><span class="sxs-lookup"><span data-stu-id="f4add-137">Before publishing your product you need to add one or more APIs.</span></span> <span data-ttu-id="f4add-138">Para fazer isso, clique em **Adicionar API ao produto**.</span><span class="sxs-lookup"><span data-stu-id="f4add-138">To do this, click **Add API to product**.</span></span>

![Adicionar APIs][api-management-add-apis-to-product]

<span data-ttu-id="f4add-140">Selecione as APIs desejadas e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="f4add-140">Select the desired APIs and click **Save**.</span></span>

## <span data-ttu-id="f4add-141"><a name="add-description"> </a>Adicionar informações descritivas a um produto</span><span class="sxs-lookup"><span data-stu-id="f4add-141"><a name="add-description"> </a>Add descriptive information to a product</span></span>
<span data-ttu-id="f4add-142">A guia **Configurações** permite que você forneça informações detalhadas sobre o produto, como sua finalidade, as APIs a que fornece acesso, entre outras informações úteis.</span><span class="sxs-lookup"><span data-stu-id="f4add-142">The **Settings** tab allows you to provide detailed information about the product such as its purpose, the APIs it provides access to, and other useful information.</span></span> <span data-ttu-id="f4add-143">O conteúdo é voltado aos desenvolvedores que chamarão a API e pode ser escrito em texto sem formatação ou em marcação HTML.</span><span class="sxs-lookup"><span data-stu-id="f4add-143">The content is targeted at the developers that will be calling the API and can be written in plain text or HTML markup.</span></span>

![Configurações do produto][api-management-product-settings]

<span data-ttu-id="f4add-145">Marque **Exigir assinatura** para criar um produto protegido que requer uma assinatura ou desmarque a caixa de seleção para criar um produto livre que pode ser chamado sem uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="f4add-145">Check **Require subscription** to create a protected product that requires a subscription to be used, or clear the checkbox to create an open product that can be called without a subscription.</span></span>

<span data-ttu-id="f4add-146">Selecione **Requerer aprovação de assinatura** se desejar aprovar manualmente todas as solicitações de assinatura do produto.</span><span class="sxs-lookup"><span data-stu-id="f4add-146">Select **Require subscription approval** if you want to manually approve all product subscription requests.</span></span> <span data-ttu-id="f4add-147">Por padrão, todas as assinaturas de produto são aprovadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="f4add-147">By default all product subscriptions are granted automatically.</span></span>

<span data-ttu-id="f4add-148">Para permitir que contas de desenvolvedor assinem o produto várias vezes, marque a caixa de seleção **Permitir várias assinaturas** e, opcionalmente, especifique um limite.</span><span class="sxs-lookup"><span data-stu-id="f4add-148">To allow developer accounts to subscribe multiple times to the product, check the **Allow multiple subscriptions** check box and optionally specify a limit.</span></span> <span data-ttu-id="f4add-149">Se essa caixa não estiver marcada, cada conta de desenvolvedor poderá assinar o produto uma única vez.</span><span class="sxs-lookup"><span data-stu-id="f4add-149">If this box is not checked, each developer account can subscribe only a single time to the product.</span></span>

<span data-ttu-id="f4add-150">Outra opção é preencher o campo **Termos de uso** descrevendo os termos de uso do produto, que os assinantes deverão aceitar para usar o produto.</span><span class="sxs-lookup"><span data-stu-id="f4add-150">Optionally fill in the **Terms of use** field describing the terms of use for the product which subscribers must accept in order to use the product.</span></span>

## <span data-ttu-id="f4add-151"><a name="publish-product"> </a>Publicar um produto</span><span class="sxs-lookup"><span data-stu-id="f4add-151"><a name="publish-product"> </a>Publish a product</span></span>
<span data-ttu-id="f4add-152">Antes que as APIs de um produto possam ser chamadas, o produto precisa ser publicado.</span><span class="sxs-lookup"><span data-stu-id="f4add-152">Before the APIs in a product can be called, the product must be published.</span></span> <span data-ttu-id="f4add-153">Na guia **Resumo** do produto, clique em **Publicar** e depois clique em **Sim, publicar** para confirmar.</span><span class="sxs-lookup"><span data-stu-id="f4add-153">On the **Summary** tab for the product, click **Publish**, and then click **Yes, publish it** to confirm.</span></span> <span data-ttu-id="f4add-154">Para fazer com que um produto publicado volte a ser provado, clique em **Cancelar publicação**.</span><span class="sxs-lookup"><span data-stu-id="f4add-154">To make a previously published product private, click **Unpublish**.</span></span>

![Publicar produto][api-management-publish-product]

## <span data-ttu-id="f4add-156"><a name="make-visible"> </a>Tornar um produto visível para os desenvolvedores</span><span class="sxs-lookup"><span data-stu-id="f4add-156"><a name="make-visible"> </a>Make a product visible to developers</span></span>
<span data-ttu-id="f4add-157">A guia **Visibilidade** permite que você selecione quais funções deseja que possam ver o produto no portal do desenvolvedor e assinar o produto.</span><span class="sxs-lookup"><span data-stu-id="f4add-157">The **Visibility** tab allows you to choose which roles are able to see the product on the developer portal and subscribe to the product.</span></span>

![Visibilidade do produto][api-management-product-visiblity]

<span data-ttu-id="f4add-159">Para habilitar e desabilitar a visibilidade de um produto para os desenvolvedores de um grupo, marque ou desmarque a caixa de seleção ao lado do grupo e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="f4add-159">To enable or disable visibility of a product for the developers in a group, check or uncheck the check box beside the group and then click **Save**.</span></span>

> <span data-ttu-id="f4add-160">Para obter mais informações, consulte [Como criar e usar grupos para gerenciar contas de desenvolvedor no Gerenciamento de API do Azure][How to create and use groups to manage developer accounts in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="f4add-160">For more information, see [How to create and use groups to manage developer accounts in Azure API Management][How to create and use groups to manage developer accounts in Azure API Management].</span></span>
> 
> 

## <span data-ttu-id="f4add-161"><a name="view-subscribers"> </a>Ver os assinantes de um produto</span><span class="sxs-lookup"><span data-stu-id="f4add-161"><a name="view-subscribers"> </a>View subscribers to a product</span></span>
<span data-ttu-id="f4add-162">A guia **Desenvolvedores** lista os desenvolvedores que assinaram o produto.</span><span class="sxs-lookup"><span data-stu-id="f4add-162">The **Subscribers** tab lists the developers who have subscribed to the product.</span></span> <span data-ttu-id="f4add-163">Os detalhes e configurações de cada desenvolvedor podem ser vistos clicando em seus respectivos nomes.</span><span class="sxs-lookup"><span data-stu-id="f4add-163">The details and settings for each developer can be viewed by clicking on the developer's name.</span></span> <span data-ttu-id="f4add-164">Neste exemplo, nenhum desenvolvedor assinou o produto ainda.</span><span class="sxs-lookup"><span data-stu-id="f4add-164">In this example no developers have yet subscribed to the product.</span></span>

![Desenvolvedores][api-management-developer-list]

## <span data-ttu-id="f4add-166"><a name="next-steps"> </a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f4add-166"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="f4add-167">Após as APIs desejadas serem adicionadas e o produto publicado, os desenvolvedores podem assinar o produto e começar a chamar as APIs.</span><span class="sxs-lookup"><span data-stu-id="f4add-167">Once the desired APIs are added and the product published, developers can subscribe to the product and begin to call the APIs.</span></span> <span data-ttu-id="f4add-168">Para ver um tutorial que demonstra esses itens, bem como a configuração avançada do produto, consulte [Como criar e definir configurações avançadas no Gerenciamento de API do Azure][How create and configure advanced product settings in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="f4add-168">For a tutorial that demonstrates these items as well as advanced product configuration see [How create and configure advanced product settings in Azure API Management][How create and configure advanced product settings in Azure API Management].</span></span>

<span data-ttu-id="f4add-169">Para obter mais informações sobre como trabalhar com produtos, consulte o vídeo a seguir.</span><span class="sxs-lookup"><span data-stu-id="f4add-169">For more information about working with products, see the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

[Create a product]: #create-product
[Add APIs to a product]: #add-apis
[Add descriptive information to a product]: #add-description
[Publish a product]: #publish-product
[Make a product visible to developers]: #make-visible
[View subscribers to a product]: #view-subscribers
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


[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps
[How to create and use groups to manage developer accounts in Azure API Management]: api-management-howto-create-groups.md
[How create and configure advanced product settings in Azure API Management]: api-management-howto-product-with-rules.md 
