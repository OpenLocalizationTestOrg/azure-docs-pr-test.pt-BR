---
title: modelos de aaaProduct no gerenciamento de API do Azure | Microsoft Docs
description: "Saiba como toocustomize conteúdo de saudação do produto Olá páginas no portal do desenvolvedor de gerenciamento de API do Azure hello."
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
ms.openlocfilehash: 60600299287aad87f9b621782ab5ceb866601d03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="product-templates-in-azure-api-management"></a><span data-ttu-id="1f3cf-103">Modelos de produto no Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="1f3cf-103">Product templates in Azure API Management</span></span>
<span data-ttu-id="1f3cf-104">Gerenciamento de API do Azure fornece que Olá conteúdo de saudação toocustomize capacidade de páginas de portal do desenvolvedor usando um conjunto de modelos que configurar seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="1f3cf-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="1f3cf-105">Usando [DotLiquid](http://dotliquidmarkup.org/) sintaxe e hello editor de sua escolha, como [DotLiquid para Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), e um conjunto fornecido de localizadas [recursos de cadeia de caracteres](api-management-template-resources.md#strings), [ Recursos de glifo](api-management-template-resources.md#glyphs), e [página controles](api-management-page-controls.md), você tiver um grande flexibilidade tooconfigure Olá conteúdo das páginas hello como desejar usar esses modelos.</span><span class="sxs-lookup"><span data-stu-id="1f3cf-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="1f3cf-106">Olá modelos nesta seção permitem toocustomize conteúdo de saudação de páginas de produto Olá no portal do desenvolvedor hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cf-106">hello templates in this section allow you toocustomize hello content of hello product pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="1f3cf-107">Lista de produtos</span><span class="sxs-lookup"><span data-stu-id="1f3cf-107">Product list</span></span>](#ProductList)  
  
-   [<span data-ttu-id="1f3cf-108">Produto</span><span class="sxs-lookup"><span data-stu-id="1f3cf-108">Product</span></span>](#Product)  
  
> [!NOTE]
>  <span data-ttu-id="1f3cf-109">Modelos de padrão de exemplo estão incluídos no hello documentação a seguir, mas são toochange assunto devido a melhorias toocontinuous.</span><span class="sxs-lookup"><span data-stu-id="1f3cf-109">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="1f3cf-110">Você pode exibir modelos do saudação padrão em tempo real no portal do desenvolvedor Olá navegando modelos individuais toohello desejado.</span><span class="sxs-lookup"><span data-stu-id="1f3cf-110">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="1f3cf-111">Para obter mais informações sobre como trabalhar com modelos, consulte [como toocustomize Olá portal do desenvolvedor do gerenciamento de API usando modelos](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="1f3cf-111">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="1f3cf-112"><a name="ProductList"></a> Lista de produtos</span><span class="sxs-lookup"><span data-stu-id="1f3cf-112"><a name="ProductList"></a> Product list</span></span>  
 <span data-ttu-id="1f3cf-113">Olá **lista de produtos** modelo permite toocustomize corpo de Olá Olá lista da página de produtos no portal do desenvolvedor hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cf-113">hello **Product list** template allows you toocustomize hello body of hello product list page in hello developer portal.</span></span>  
  
 <span data-ttu-id="1f3cf-114">![Lista de produtos](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span><span class="sxs-lookup"><span data-stu-id="1f3cf-114">![Products list](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="1f3cf-115">Modelo padrão</span><span class="sxs-lookup"><span data-stu-id="1f3cf-115">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="1f3cf-116">Controles</span><span class="sxs-lookup"><span data-stu-id="1f3cf-116">Controls</span></span>  
 <span data-ttu-id="1f3cf-117">Olá `Product list` modelo pode usar a seguinte Olá [página controles](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="1f3cf-117">hello `Product list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="1f3cf-118">paging-control</span><span class="sxs-lookup"><span data-stu-id="1f3cf-118">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
-   [<span data-ttu-id="1f3cf-119">search-control</span><span class="sxs-lookup"><span data-stu-id="1f3cf-119">search-control</span></span>](api-management-page-controls.md#search-control)  
  
### <a name="data-model"></a><span data-ttu-id="1f3cf-120">Modelo de dados</span><span class="sxs-lookup"><span data-stu-id="1f3cf-120">Data model</span></span>  
  
|<span data-ttu-id="1f3cf-121">Propriedade</span><span class="sxs-lookup"><span data-stu-id="1f3cf-121">Property</span></span>|<span data-ttu-id="1f3cf-122">Tipo</span><span class="sxs-lookup"><span data-stu-id="1f3cf-122">Type</span></span>|<span data-ttu-id="1f3cf-123">Descrição</span><span class="sxs-lookup"><span data-stu-id="1f3cf-123">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="1f3cf-124">Paginamento</span><span class="sxs-lookup"><span data-stu-id="1f3cf-124">Paging</span></span>|<span data-ttu-id="1f3cf-125">Entidade de [paginação](api-management-template-data-model-reference.md#Paging).</span><span class="sxs-lookup"><span data-stu-id="1f3cf-125">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="1f3cf-126">Olá paginação as informações para a coleção de produtos de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f3cf-126">hello paging information for hello products collection.</span></span>|  
|<span data-ttu-id="1f3cf-127">Filtragem</span><span class="sxs-lookup"><span data-stu-id="1f3cf-127">Filtering</span></span>|<span data-ttu-id="1f3cf-128">Entidade de [filtragem](api-management-template-data-model-reference.md#Filtering).</span><span class="sxs-lookup"><span data-stu-id="1f3cf-128">[Filtering](api-management-template-data-model-reference.md#Filtering) entity.</span></span>|<span data-ttu-id="1f3cf-129">Olá informações de filtragem para página da lista de produtos de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f3cf-129">hello filtering information for hello products list page.</span></span>|  
|<span data-ttu-id="1f3cf-130">Produtos</span><span class="sxs-lookup"><span data-stu-id="1f3cf-130">Products</span></span>|<span data-ttu-id="1f3cf-131">Coleção de entidades de [produto](api-management-template-data-model-reference.md#Product).</span><span class="sxs-lookup"><span data-stu-id="1f3cf-131">Collection of [Product](api-management-template-data-model-reference.md#Product) entities.</span></span>|<span data-ttu-id="1f3cf-132">usuário atual do Hello produtos toohello visível.</span><span class="sxs-lookup"><span data-stu-id="1f3cf-132">hello products visible toohello current user.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="1f3cf-133">Amostra de dados do modelo</span><span class="sxs-lookup"><span data-stu-id="1f3cf-133">Sample template data</span></span>  
  
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
            "Description": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
            "Terms": "",  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        },  
        {  
            "Id": "56f9445ffaf7560049060002",  
            "Title": "Unlimited",  
            "Description": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",  
            "Terms": null,  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        }  
    ]  
}  
```  
  
##  <span data-ttu-id="1f3cf-134"><a name="Product"></a> Produto</span><span class="sxs-lookup"><span data-stu-id="1f3cf-134"><a name="Product"></a> Product</span></span>  
 <span data-ttu-id="1f3cf-135">Olá **produto** modelo permite toocustomize corpo de Olá Olá da página de produtos no portal do desenvolvedor hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cf-135">hello **Product** template allows you toocustomize hello body of hello product page in hello developer portal.</span></span>  
  
 <span data-ttu-id="1f3cf-136">![Página de produtos do portal do desenvolvedor](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span><span class="sxs-lookup"><span data-stu-id="1f3cf-136">![Developer portal product page](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="1f3cf-137">Modelo padrão</span><span class="sxs-lookup"><span data-stu-id="1f3cf-137">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="1f3cf-138">Controles</span><span class="sxs-lookup"><span data-stu-id="1f3cf-138">Controls</span></span>  
 <span data-ttu-id="1f3cf-139">Olá `Product list` modelo pode usar a seguinte Olá [página controles](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="1f3cf-139">hello `Product list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="1f3cf-140">subscribe-button</span><span class="sxs-lookup"><span data-stu-id="1f3cf-140">subscribe-button</span></span>](api-management-page-controls.md#subscribe-button)  
  
### <a name="data-model"></a><span data-ttu-id="1f3cf-141">Modelo de dados</span><span class="sxs-lookup"><span data-stu-id="1f3cf-141">Data model</span></span>  
  
|<span data-ttu-id="1f3cf-142">Propriedade</span><span class="sxs-lookup"><span data-stu-id="1f3cf-142">Property</span></span>|<span data-ttu-id="1f3cf-143">Tipo</span><span class="sxs-lookup"><span data-stu-id="1f3cf-143">Type</span></span>|<span data-ttu-id="1f3cf-144">Descrição</span><span class="sxs-lookup"><span data-stu-id="1f3cf-144">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="1f3cf-145">Produto</span><span class="sxs-lookup"><span data-stu-id="1f3cf-145">Product</span></span>|[<span data-ttu-id="1f3cf-146">Produto</span><span class="sxs-lookup"><span data-stu-id="1f3cf-146">Product</span></span>](api-management-template-data-model-reference.md#Product)|<span data-ttu-id="1f3cf-147">produto do Hello especificado.</span><span class="sxs-lookup"><span data-stu-id="1f3cf-147">hello specified product.</span></span>|  
|<span data-ttu-id="1f3cf-148">IsDeveloperSubscribed</span><span class="sxs-lookup"><span data-stu-id="1f3cf-148">IsDeveloperSubscribed</span></span>|<span data-ttu-id="1f3cf-149">Booliano</span><span class="sxs-lookup"><span data-stu-id="1f3cf-149">boolean</span></span>|<span data-ttu-id="1f3cf-150">Se o usuário atual Olá é produto toothis assinados.</span><span class="sxs-lookup"><span data-stu-id="1f3cf-150">Whether hello current user is subscribed toothis product.</span></span>|  
|<span data-ttu-id="1f3cf-151">SubscriptionState</span><span class="sxs-lookup"><span data-stu-id="1f3cf-151">SubscriptionState</span></span>|<span data-ttu-id="1f3cf-152">número</span><span class="sxs-lookup"><span data-stu-id="1f3cf-152">number</span></span>|<span data-ttu-id="1f3cf-153">estado de saudação de assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f3cf-153">hello state of hello subscription.</span></span> <span data-ttu-id="1f3cf-154">Os possíveis estados são:</span><span class="sxs-lookup"><span data-stu-id="1f3cf-154">Possible states are:</span></span><br /><br /> <span data-ttu-id="1f3cf-155">-   `0 - suspended`– Olá assinatura está bloqueada e assinante Olá não é possível chamar quaisquer APIs do produto hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cf-155">-   `0 - suspended` – hello subscription is blocked, and hello subscriber cannot call any APIs of hello product.</span></span><br /><span data-ttu-id="1f3cf-156">-   `1 - active`– Olá assinatura está ativa.</span><span class="sxs-lookup"><span data-stu-id="1f3cf-156">-   `1 - active` – hello subscription is active.</span></span><br /><span data-ttu-id="1f3cf-157">-   `2 - expired`– Olá atingiu sua data de expiração e foi desativada.</span><span class="sxs-lookup"><span data-stu-id="1f3cf-157">-   `2 - expired` – hello subscription reached its expiration date and was deactivated.</span></span><br /><span data-ttu-id="1f3cf-158">-   `3 - submitted`– solicitação de assinatura de saudação foi feita pelo desenvolvedor hello, mas ainda não foi aprovada ou rejeitada.</span><span class="sxs-lookup"><span data-stu-id="1f3cf-158">-   `3 - submitted` – hello subscription request has been made by hello developer, but has not yet been approved or rejected.</span></span><br /><span data-ttu-id="1f3cf-159">-   `4 - rejected`– solicitação de assinatura de saudação foi negada por um administrador.</span><span class="sxs-lookup"><span data-stu-id="1f3cf-159">-   `4 - rejected` – hello subscription request has been denied by an administrator.</span></span><br /><span data-ttu-id="1f3cf-160">-   `5 - cancelled`– Olá assinatura foi cancelada pelo administrador ou desenvolvedor de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f3cf-160">-   `5 - cancelled` – hello subscription has been cancelled by hello developer or administrator.</span></span>|  
|<span data-ttu-id="1f3cf-161">limites</span><span class="sxs-lookup"><span data-stu-id="1f3cf-161">Limits</span></span>|<span data-ttu-id="1f3cf-162">array</span><span class="sxs-lookup"><span data-stu-id="1f3cf-162">array</span></span>|<span data-ttu-id="1f3cf-163">Essa propriedade foi preterida e não deve ser usada.</span><span class="sxs-lookup"><span data-stu-id="1f3cf-163">This property is deprecated and should not be used.</span></span>|  
|<span data-ttu-id="1f3cf-164">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="1f3cf-164">DelegatedSubscriptionEnabled</span></span>|<span data-ttu-id="1f3cf-165">booleano</span><span class="sxs-lookup"><span data-stu-id="1f3cf-165">boolean</span></span>|<span data-ttu-id="1f3cf-166">Se [delegação](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) está habilitada para essa assinatura.</span><span class="sxs-lookup"><span data-stu-id="1f3cf-166">Whether [delegation](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) is enabled for this subscription.</span></span>|  
|<span data-ttu-id="1f3cf-167">DelegatedSubscriptionUrl</span><span class="sxs-lookup"><span data-stu-id="1f3cf-167">DelegatedSubscriptionUrl</span></span>|<span data-ttu-id="1f3cf-168">string</span><span class="sxs-lookup"><span data-stu-id="1f3cf-168">string</span></span>|<span data-ttu-id="1f3cf-169">Se a delegação estiver habilitada, Olá delegado URL de assinatura.</span><span class="sxs-lookup"><span data-stu-id="1f3cf-169">If delegation is enabled, hello delegated subscription URL.</span></span>|  
|<span data-ttu-id="1f3cf-170">IsAgreed</span><span class="sxs-lookup"><span data-stu-id="1f3cf-170">IsAgreed</span></span>|<span data-ttu-id="1f3cf-171">Booliano</span><span class="sxs-lookup"><span data-stu-id="1f3cf-171">boolean</span></span>|<span data-ttu-id="1f3cf-172">Se o produto de saudação termos se Olá atual usuário concordou toohello termos.</span><span class="sxs-lookup"><span data-stu-id="1f3cf-172">If hello product has terms, whether hello current user has agreed toohello terms.</span></span>|  
|<span data-ttu-id="1f3cf-173">Assinaturas</span><span class="sxs-lookup"><span data-stu-id="1f3cf-173">Subscriptions</span></span>|<span data-ttu-id="1f3cf-174">Coleção de entidades de [Resumo da assinatura](api-management-template-data-model-reference.md#SubscriptionSummary).</span><span class="sxs-lookup"><span data-stu-id="1f3cf-174">Collection of [Subscription summary](api-management-template-data-model-reference.md#SubscriptionSummary) entities.</span></span>|<span data-ttu-id="1f3cf-175">produto de toohello de assinaturas de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f3cf-175">hello subscriptions toohello product.</span></span>|  
|<span data-ttu-id="1f3cf-176">Apis</span><span class="sxs-lookup"><span data-stu-id="1f3cf-176">Apis</span></span>|<span data-ttu-id="1f3cf-177">Coleção de entidades de [API](api-management-template-data-model-reference.md#API).</span><span class="sxs-lookup"><span data-stu-id="1f3cf-177">Collection of [API](api-management-template-data-model-reference.md#API) entities.</span></span>|<span data-ttu-id="1f3cf-178">Olá APIs neste produto.</span><span class="sxs-lookup"><span data-stu-id="1f3cf-178">hello APIs in this product.</span></span>|  
|<span data-ttu-id="1f3cf-179">CannotAddBecauseSubscriptionNumberLimitReached</span><span class="sxs-lookup"><span data-stu-id="1f3cf-179">CannotAddBecauseSubscriptionNumberLimitReached</span></span>|<span data-ttu-id="1f3cf-180">Booliano</span><span class="sxs-lookup"><span data-stu-id="1f3cf-180">boolean</span></span>|<span data-ttu-id="1f3cf-181">Se o usuário atual Olá é toosubscribe qualificados toothis produto com limite de assinatura de toohello de relação.</span><span class="sxs-lookup"><span data-stu-id="1f3cf-181">Whether hello current user is eligible toosubscribe toothis product with regard toohello subscription limit.</span></span>|  
|<span data-ttu-id="1f3cf-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span><span class="sxs-lookup"><span data-stu-id="1f3cf-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span></span>|<span data-ttu-id="1f3cf-183">Booliano</span><span class="sxs-lookup"><span data-stu-id="1f3cf-183">boolean</span></span>|<span data-ttu-id="1f3cf-184">Se o usuário atual Olá é toosubscribe qualificados toothis produto com assinaturas de toomultiple relação permitidas ou não.</span><span class="sxs-lookup"><span data-stu-id="1f3cf-184">Whether hello current user is eligible toosubscribe toothis product with regard toomultiple subscriptions being allowed or not.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="1f3cf-185">Amostra de dados do modelo</span><span class="sxs-lookup"><span data-stu-id="1f3cf-185">Sample template data</span></span>  
  
```json  
{  
    "Product": {  
        "Id": "56f9445ffaf7560049060001",  
        "Title": "Starter",  
        "Description": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
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

## <a name="next-steps"></a><span data-ttu-id="1f3cf-186">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1f3cf-186">Next steps</span></span>
<span data-ttu-id="1f3cf-187">Para obter mais informações sobre como trabalhar com modelos, consulte [como toocustomize Olá portal do desenvolvedor do gerenciamento de API usando modelos](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="1f3cf-187">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
