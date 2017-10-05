---
title: Modelos de produto no Gerenciamento de API do Azure | Microsoft Docs
description: "Saiba como personalizar o conteúdo das páginas de produto no portal do desenvolvedor do Gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 49f9254c-4c5f-4ed4-9c8d-798f44e805ee
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 9ddbb9860b437cb3e7334bdf5891f2fba1cffb76
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="product-templates-in-azure-api-management"></a><span data-ttu-id="03a2c-103">Modelos de produto no Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="03a2c-103">Product templates in Azure API Management</span></span>
<span data-ttu-id="03a2c-104">O Gerenciamento de API do Azure fornece a capacidade de personalizar o conteúdo das páginas do portal do desenvolvedor usando um conjunto de modelos que configura o respectivo conteúdo.</span><span class="sxs-lookup"><span data-stu-id="03a2c-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="03a2c-105">Usando a sintaxe [DotLiquid](http://dotliquidmarkup.org/) e o editor de sua escolha, como o [DotLiquid para Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), bem como um conjunto fornecido de [Recursos de cadeia de caracteres](api-management-template-resources.md#strings), [Recursos do Glyph](api-management-template-resources.md#glyphs) e [Controles de página](api-management-page-controls.md) localizados, você tem grande flexibilidade para configurar o conteúdo das páginas, conforme a necessidade, usando esses modelos.</span><span class="sxs-lookup"><span data-stu-id="03a2c-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="03a2c-106">Os modelos desta seção permitem personalizar o conteúdo das páginas de produto no portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="03a2c-106">The templates in this section allow you to customize the content of the product pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="03a2c-107">Lista de produtos</span><span class="sxs-lookup"><span data-stu-id="03a2c-107">Product list</span></span>](#ProductList)  
  
-   [<span data-ttu-id="03a2c-108">Produto</span><span class="sxs-lookup"><span data-stu-id="03a2c-108">Product</span></span>](#Product)  
  
> [!NOTE]
>  <span data-ttu-id="03a2c-109">Os modelos de amostra padrão estão incluídos na documentação a seguir, mas estão sujeitos à alteração devido a melhorias contínuas.</span><span class="sxs-lookup"><span data-stu-id="03a2c-109">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="03a2c-110">Você pode exibir os modelos padrão em tempo real no portal do desenvolvedor, navegando até os modelos individuais desejados.</span><span class="sxs-lookup"><span data-stu-id="03a2c-110">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="03a2c-111">Para saber mais sobre como trabalhar com modelos, confira [Como personalizar o portal de desenvolvedor de Gerenciamento de API do Azure usando modelos](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="03a2c-111">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="03a2c-112"><a name="ProductList"></a> Lista de produtos</span><span class="sxs-lookup"><span data-stu-id="03a2c-112"><a name="ProductList"></a> Product list</span></span>  
 <span data-ttu-id="03a2c-113">O modelo **Lista de produtos** permite personalizar o corpo da página de lista de produtos no portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="03a2c-113">The **Product list** template allows you to customize the body of the product list page in the developer portal.</span></span>  
  
 <span data-ttu-id="03a2c-114">![Lista de produtos](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span><span class="sxs-lookup"><span data-stu-id="03a2c-114">![Products list](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="03a2c-115">Modelo padrão</span><span class="sxs-lookup"><span data-stu-id="03a2c-115">Default template</span></span>  
  
```xml  
<search-control></search-control>  
<div class="row">  
    <div class="col-md-9">  
        <h2>{% localized "ProductsStrings|PageTitleProducts" %}</h2>  
    </div>  
</div>  
<div class="row">  
    <div class="col-md-12">  
    {% if products.size > 0 %}  
    <ul class="list-unstyled">  
    {% for product in products %}  
        <li>  
            <h3><a href="/products/{{product.id}}">{{product.title}}</a></h3>  
            {{product.description}}  
        </li>     
    {% endfor %}  
    </ul>  
    <paging-control></paging-control>  
    {% else %}  
    {% localized "CommonResources|NoItemsToDisplay" %}  
    {% endif %}  
    </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="03a2c-116">Controles</span><span class="sxs-lookup"><span data-stu-id="03a2c-116">Controls</span></span>  
 <span data-ttu-id="03a2c-117">O modelo `Product list` pode usar os seguintes [controles de página](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="03a2c-117">The `Product list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="03a2c-118">paging-control</span><span class="sxs-lookup"><span data-stu-id="03a2c-118">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
-   [<span data-ttu-id="03a2c-119">search-control</span><span class="sxs-lookup"><span data-stu-id="03a2c-119">search-control</span></span>](api-management-page-controls.md#search-control)  
  
### <a name="data-model"></a><span data-ttu-id="03a2c-120">Modelo de dados</span><span class="sxs-lookup"><span data-stu-id="03a2c-120">Data model</span></span>  
  
|<span data-ttu-id="03a2c-121">Propriedade</span><span class="sxs-lookup"><span data-stu-id="03a2c-121">Property</span></span>|<span data-ttu-id="03a2c-122">Tipo</span><span class="sxs-lookup"><span data-stu-id="03a2c-122">Type</span></span>|<span data-ttu-id="03a2c-123">Descrição</span><span class="sxs-lookup"><span data-stu-id="03a2c-123">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="03a2c-124">Paginamento</span><span class="sxs-lookup"><span data-stu-id="03a2c-124">Paging</span></span>|<span data-ttu-id="03a2c-125">Entidade de [paginação](api-management-template-data-model-reference.md#Paging).</span><span class="sxs-lookup"><span data-stu-id="03a2c-125">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="03a2c-126">As informações de paginação da coleção de produtos.</span><span class="sxs-lookup"><span data-stu-id="03a2c-126">The paging information for the products collection.</span></span>|  
|<span data-ttu-id="03a2c-127">Filtragem</span><span class="sxs-lookup"><span data-stu-id="03a2c-127">Filtering</span></span>|<span data-ttu-id="03a2c-128">Entidade de [filtragem](api-management-template-data-model-reference.md#Filtering).</span><span class="sxs-lookup"><span data-stu-id="03a2c-128">[Filtering](api-management-template-data-model-reference.md#Filtering) entity.</span></span>|<span data-ttu-id="03a2c-129">As informações de filtragem da página de lista de produtos.</span><span class="sxs-lookup"><span data-stu-id="03a2c-129">The filtering information for the products list page.</span></span>|  
|<span data-ttu-id="03a2c-130">Produtos</span><span class="sxs-lookup"><span data-stu-id="03a2c-130">Products</span></span>|<span data-ttu-id="03a2c-131">Coleção de entidades de [produto](api-management-template-data-model-reference.md#Product).</span><span class="sxs-lookup"><span data-stu-id="03a2c-131">Collection of [Product](api-management-template-data-model-reference.md#Product) entities.</span></span>|<span data-ttu-id="03a2c-132">Os produtos visíveis para o usuário atual.</span><span class="sxs-lookup"><span data-stu-id="03a2c-132">The products visible to the current user.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="03a2c-133">Amostra de dados do modelo</span><span class="sxs-lookup"><span data-stu-id="03a2c-133">Sample template data</span></span>  
  
```json  
{  
    "Paging": {  
        "Page": 1,  
        "PageSize": 10,  
        "TotalItemCount": 2,  
        "ShowAll": false,  
        "PageCount": 1  
    },  
    "Filtering": {  
        "Pattern": null,  
        "Placeholder": "Search products"  
    },  
    "Products": [  
        {  
            "Id": "56f9445ffaf7560049060001",  
            "Title": "Starter",  
            "Description": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
            "Terms": "",  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        },  
        {  
            "Id": "56f9445ffaf7560049060002",  
            "Title": "Unlimited",  
            "Description": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
            "Terms": null,  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        }  
    ]  
}  
```  
  
##  <span data-ttu-id="03a2c-134"><a name="Product"></a> Produto</span><span class="sxs-lookup"><span data-stu-id="03a2c-134"><a name="Product"></a> Product</span></span>  
 <span data-ttu-id="03a2c-135">O modelo **Produto** permite personalizar o corpo da página de produtos no portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="03a2c-135">The **Product** template allows you to customize the body of the product page in the developer portal.</span></span>  
  
 <span data-ttu-id="03a2c-136">![Página de produtos do portal do desenvolvedor](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span><span class="sxs-lookup"><span data-stu-id="03a2c-136">![Developer portal product page](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="03a2c-137">Modelo padrão</span><span class="sxs-lookup"><span data-stu-id="03a2c-137">Default template</span></span>  
  
```xml  
<h2>{{Product.Title}}</h2>  
<p>{{Product.Description}}</p>  
  
{% assign replaceString0 = '{0}' %}  
  
{% if Limits and Limits.size > 0 %}  
<h3>{% localized "ProductDetailsStrings|WebProductsUsageLimitsHeader"%}</h3>  
<ul>  
  {% for limit in Limits %}  
  <li>{{limit.DisplayName}}</li>  
  {% endfor %}  
</ul>  
{% endif %}  
  
{% if apis.size > 0 %}  
<p>  
  <b>  
    {% if apis.size == 1 %}  
    {% capture apisCountText %}{% localized "ProductDetailsStrings|TextblockSingleApisCount" %}{% endcapture %}  
    {% else %}  
    {% capture apisCountText %}{% localized "ProductDetailsStrings|TextblockMultipleApisCount" %}{% endcapture %}  
    {% endif %}  
  
    {% capture apisCount %}{{apis.size}}{% endcapture %}  
    {{ apisCountText | replace : replaceString0, apisCount }}  
  </b>  
</p>  
  
<ul>  
  {% for api in Apis %}  
  <li>  
    <a href="/docs/services/{{api.Id}}">{{api.Name}}</a>  
  </li>  
  {% endfor %}  
</ul>  
{% endif %}  
  
{% if subscriptions.size > 0 %}  
<p>  
  <b>  
    {% if subscriptions.size == 1 %}  
    {% capture subscriptionsCountText %}{% localized "ProductDetailsStrings|TextblockSingleSubscriptionsCount" %}{% endcapture %}  
    {% else %}  
    {% capture subscriptionsCountText %}{% localized "ProductDetailsStrings|TextblockMultipleSubscriptionsCount" %}{% endcapture %}  
    {% endif %}  
  
    {% capture subscriptionsCount %}{{subscriptions.size}}{% endcapture %}  
    {{ subscriptionsCountText | replace : replaceString0, subscriptionsCount }}  
  </b>  
</p>  
  
<ul>  
  {% for subscription in subscriptions %}  
  <li>  
    <a href="/developer#{{subscription.Id}}">{{subscription.DisplayName}}</a>  
  </li>  
  {% endfor %}  
</ul>  
{% endif %}  
{% if CannotAddBecauseSubscriptionNumberLimitReached %}  
<b>{% localized "ProductDetailsStrings|TextblockSubscriptionLimitReached" %}</b>  
{% elsif CannotAddBecauseMultipleSubscriptionsNotAllowed == false %}  
<subscribe-button></subscribe-button>  
{% endif %}  
```  
  
### <a name="controls"></a><span data-ttu-id="03a2c-138">Controles</span><span class="sxs-lookup"><span data-stu-id="03a2c-138">Controls</span></span>  
 <span data-ttu-id="03a2c-139">O modelo `Product list` pode usar os seguintes [controles de página](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="03a2c-139">The `Product list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="03a2c-140">subscribe-button</span><span class="sxs-lookup"><span data-stu-id="03a2c-140">subscribe-button</span></span>](api-management-page-controls.md#subscribe-button)  
  
### <a name="data-model"></a><span data-ttu-id="03a2c-141">Modelo de dados</span><span class="sxs-lookup"><span data-stu-id="03a2c-141">Data model</span></span>  
  
|<span data-ttu-id="03a2c-142">Propriedade</span><span class="sxs-lookup"><span data-stu-id="03a2c-142">Property</span></span>|<span data-ttu-id="03a2c-143">Tipo</span><span class="sxs-lookup"><span data-stu-id="03a2c-143">Type</span></span>|<span data-ttu-id="03a2c-144">Descrição</span><span class="sxs-lookup"><span data-stu-id="03a2c-144">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="03a2c-145">Produto</span><span class="sxs-lookup"><span data-stu-id="03a2c-145">Product</span></span>|[<span data-ttu-id="03a2c-146">Produto</span><span class="sxs-lookup"><span data-stu-id="03a2c-146">Product</span></span>](api-management-template-data-model-reference.md#Product)|<span data-ttu-id="03a2c-147">O produto especificado.</span><span class="sxs-lookup"><span data-stu-id="03a2c-147">The specified product.</span></span>|  
|<span data-ttu-id="03a2c-148">IsDeveloperSubscribed</span><span class="sxs-lookup"><span data-stu-id="03a2c-148">IsDeveloperSubscribed</span></span>|<span data-ttu-id="03a2c-149">booleano</span><span class="sxs-lookup"><span data-stu-id="03a2c-149">boolean</span></span>|<span data-ttu-id="03a2c-150">Se o usuário atual assinou esse produto.</span><span class="sxs-lookup"><span data-stu-id="03a2c-150">Whether the current user is subscribed to this product.</span></span>|  
|<span data-ttu-id="03a2c-151">SubscriptionState</span><span class="sxs-lookup"><span data-stu-id="03a2c-151">SubscriptionState</span></span>|<span data-ttu-id="03a2c-152">número</span><span class="sxs-lookup"><span data-stu-id="03a2c-152">number</span></span>|<span data-ttu-id="03a2c-153">O estado da assinatura.</span><span class="sxs-lookup"><span data-stu-id="03a2c-153">The state of the subscription.</span></span> <span data-ttu-id="03a2c-154">Os possíveis estados são:</span><span class="sxs-lookup"><span data-stu-id="03a2c-154">Possible states are:</span></span><br /><br /> <span data-ttu-id="03a2c-155">-   `0 - suspended` – a assinatura está bloqueada e o assinante não pode chamar APIs do produto.</span><span class="sxs-lookup"><span data-stu-id="03a2c-155">-   `0 - suspended` – the subscription is blocked, and the subscriber cannot call any APIs of the product.</span></span><br /><span data-ttu-id="03a2c-156">-   `1 - active` – a assinatura está ativa.</span><span class="sxs-lookup"><span data-stu-id="03a2c-156">-   `1 - active` – the subscription is active.</span></span><br /><span data-ttu-id="03a2c-157">-   `2 - expired` – a assinatura atingiu sua data de validade e foi desativada.</span><span class="sxs-lookup"><span data-stu-id="03a2c-157">-   `2 - expired` – the subscription reached its expiration date and was deactivated.</span></span><br /><span data-ttu-id="03a2c-158">-   `3 - submitted` – a solicitação de assinatura foi feita pelo desenvolvedor, mas ainda não foi aprovada ou rejeitada.</span><span class="sxs-lookup"><span data-stu-id="03a2c-158">-   `3 - submitted` – the subscription request has been made by the developer, but has not yet been approved or rejected.</span></span><br /><span data-ttu-id="03a2c-159">-   `4 - rejected` – a solicitação de assinatura foi negada por um administrador.</span><span class="sxs-lookup"><span data-stu-id="03a2c-159">-   `4 - rejected` – the subscription request has been denied by an administrator.</span></span><br /><span data-ttu-id="03a2c-160">-   `5 - cancelled` – a assinatura foi cancelada pelo desenvolvedor ou administrador.</span><span class="sxs-lookup"><span data-stu-id="03a2c-160">-   `5 - cancelled` – the subscription has been cancelled by the developer or administrator.</span></span>|  
|<span data-ttu-id="03a2c-161">limites</span><span class="sxs-lookup"><span data-stu-id="03a2c-161">Limits</span></span>|<span data-ttu-id="03a2c-162">array</span><span class="sxs-lookup"><span data-stu-id="03a2c-162">array</span></span>|<span data-ttu-id="03a2c-163">Essa propriedade foi preterida e não deve ser usada.</span><span class="sxs-lookup"><span data-stu-id="03a2c-163">This property is deprecated and should not be used.</span></span>|  
|<span data-ttu-id="03a2c-164">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="03a2c-164">DelegatedSubscriptionEnabled</span></span>|<span data-ttu-id="03a2c-165">booleano</span><span class="sxs-lookup"><span data-stu-id="03a2c-165">boolean</span></span>|<span data-ttu-id="03a2c-166">Se [delegação](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) está habilitada para essa assinatura.</span><span class="sxs-lookup"><span data-stu-id="03a2c-166">Whether [delegation](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) is enabled for this subscription.</span></span>|  
|<span data-ttu-id="03a2c-167">DelegatedSubscriptionUrl</span><span class="sxs-lookup"><span data-stu-id="03a2c-167">DelegatedSubscriptionUrl</span></span>|<span data-ttu-id="03a2c-168">string</span><span class="sxs-lookup"><span data-stu-id="03a2c-168">string</span></span>|<span data-ttu-id="03a2c-169">Se delegação estiver habilitada, a URL da assinatura delegada.</span><span class="sxs-lookup"><span data-stu-id="03a2c-169">If delegation is enabled, the delegated subscription URL.</span></span>|  
|<span data-ttu-id="03a2c-170">IsAgreed</span><span class="sxs-lookup"><span data-stu-id="03a2c-170">IsAgreed</span></span>|<span data-ttu-id="03a2c-171">booleano</span><span class="sxs-lookup"><span data-stu-id="03a2c-171">boolean</span></span>|<span data-ttu-id="03a2c-172">Se o produto tiver termos, se o atual usuário concordou com os termos.</span><span class="sxs-lookup"><span data-stu-id="03a2c-172">If the product has terms, whether the current user has agreed to the terms.</span></span>|  
|<span data-ttu-id="03a2c-173">Assinaturas</span><span class="sxs-lookup"><span data-stu-id="03a2c-173">Subscriptions</span></span>|<span data-ttu-id="03a2c-174">Coleção de entidades de [Resumo da assinatura](api-management-template-data-model-reference.md#SubscriptionSummary).</span><span class="sxs-lookup"><span data-stu-id="03a2c-174">Collection of [Subscription summary](api-management-template-data-model-reference.md#SubscriptionSummary) entities.</span></span>|<span data-ttu-id="03a2c-175">As assinaturas para o produto.</span><span class="sxs-lookup"><span data-stu-id="03a2c-175">The subscriptions to the product.</span></span>|  
|<span data-ttu-id="03a2c-176">Apis</span><span class="sxs-lookup"><span data-stu-id="03a2c-176">Apis</span></span>|<span data-ttu-id="03a2c-177">Coleção de entidades de [API](api-management-template-data-model-reference.md#API).</span><span class="sxs-lookup"><span data-stu-id="03a2c-177">Collection of [API](api-management-template-data-model-reference.md#API) entities.</span></span>|<span data-ttu-id="03a2c-178">As APIs nesse produto.</span><span class="sxs-lookup"><span data-stu-id="03a2c-178">The APIs in this product.</span></span>|  
|<span data-ttu-id="03a2c-179">CannotAddBecauseSubscriptionNumberLimitReached</span><span class="sxs-lookup"><span data-stu-id="03a2c-179">CannotAddBecauseSubscriptionNumberLimitReached</span></span>|<span data-ttu-id="03a2c-180">booleano</span><span class="sxs-lookup"><span data-stu-id="03a2c-180">boolean</span></span>|<span data-ttu-id="03a2c-181">Se o usuário atual está qualificado para assinar esse produto com relação ao limite de assinatura.</span><span class="sxs-lookup"><span data-stu-id="03a2c-181">Whether the current user is eligible to subscribe to this product with regard to the subscription limit.</span></span>|  
|<span data-ttu-id="03a2c-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span><span class="sxs-lookup"><span data-stu-id="03a2c-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span></span>|<span data-ttu-id="03a2c-183">booleano</span><span class="sxs-lookup"><span data-stu-id="03a2c-183">boolean</span></span>|<span data-ttu-id="03a2c-184">Se o usuário atual está qualificado para assinar esse produto com relação à permissão ou não de várias assinaturas.</span><span class="sxs-lookup"><span data-stu-id="03a2c-184">Whether the current user is eligible to subscribe to this product with regard to multiple subscriptions being allowed or not.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="03a2c-185">Amostra de dados do modelo</span><span class="sxs-lookup"><span data-stu-id="03a2c-185">Sample template data</span></span>  
  
```json  
{  
    "Product": {  
        "Id": "56f9445ffaf7560049060001",  
        "Title": "Starter",  
        "Description": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
        "Terms": "",  
        "ProductState": 1,  
        "AllowMultipleSubscriptions": false,  
        "MultipleSubscriptionsCount": 1  
    },  
    "IsDeveloperSubscribed": true,  
    "SubscriptionState": 1,  
    "Limits": [],  
    "DelegatedSubscriptionEnabled": false,  
    "DelegatedSubscriptionUrl": null,  
    "IsAgreed": false,  
    "Subscriptions": [  
        {  
            "Id": "56f9445ffaf7560049070001",  
            "DisplayName": "Starter  (default)"  
        }  
    ],  
    "Apis": [  
        {  
            "id": "56f9445ffaf7560049040001",  
            "name": "Echo API",  
            "description": null,  
            "serviceUrl": "http://echoapi.cloudapp.net/api",  
            "path": "echo",  
            "protocols": [  
                2  
            ],  
            "authenticationSettings": null,  
            "subscriptionKeyParameterNames": null  
        }  
    ],  
    "CannotAddBecauseSubscriptionNumberLimitReached": false,  
    "CannotAddBecauseMultipleSubscriptionsNotAllowed": true  
}  
```

## <a name="next-steps"></a><span data-ttu-id="03a2c-186">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="03a2c-186">Next steps</span></span>
<span data-ttu-id="03a2c-187">Para saber mais sobre como trabalhar com modelos, confira [Como personalizar o portal de desenvolvedor de Gerenciamento de API do Azure usando modelos](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="03a2c-187">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>