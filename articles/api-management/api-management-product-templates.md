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
# <a name="product-templates-in-azure-api-management"></a>Modelos de produto no Gerenciamento de API do Azure
Gerenciamento de API do Azure fornece que Olá conteúdo de saudação toocustomize capacidade de páginas de portal do desenvolvedor usando um conjunto de modelos que configurar seu conteúdo. Usando [DotLiquid](http://dotliquidmarkup.org/) sintaxe e hello editor de sua escolha, como [DotLiquid para Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), e um conjunto fornecido de localizadas [recursos de cadeia de caracteres](api-management-template-resources.md#strings), [ Recursos de glifo](api-management-template-resources.md#glyphs), e [página controles](api-management-page-controls.md), você tiver um grande flexibilidade tooconfigure Olá conteúdo das páginas hello como desejar usar esses modelos.  
  
 Olá modelos nesta seção permitem toocustomize conteúdo de saudação de páginas de produto Olá no portal do desenvolvedor hello.  
  
-   [Lista de produtos](#ProductList)  
  
-   [Produto](#Product)  
  
> [!NOTE]
>  Modelos de padrão de exemplo estão incluídos no hello documentação a seguir, mas são toochange assunto devido a melhorias toocontinuous. Você pode exibir modelos do saudação padrão em tempo real no portal do desenvolvedor Olá navegando modelos individuais toohello desejado. Para obter mais informações sobre como trabalhar com modelos, consulte [como toocustomize Olá portal do desenvolvedor do gerenciamento de API usando modelos](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).  
  
##  <a name="ProductList"></a> Lista de produtos  
 Olá **lista de produtos** modelo permite toocustomize corpo de Olá Olá lista da página de produtos no portal do desenvolvedor hello.  
  
 ![Lista de produtos](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")  
  
### <a name="default-template"></a>Modelo padrão  
  
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
  
### <a name="controls"></a>Controles  
 Olá `Product list` modelo pode usar a seguinte Olá [página controles](api-management-page-controls.md).  
  
-   [paging-control](api-management-page-controls.md#paging-control)  
  
-   [search-control](api-management-page-controls.md#search-control)  
  
### <a name="data-model"></a>Modelo de dados  
  
|Propriedade|Tipo|Descrição|  
|--------------|----------|-----------------|  
|Paginamento|Entidade de [paginação](api-management-template-data-model-reference.md#Paging).|Olá paginação as informações para a coleção de produtos de saudação.|  
|Filtragem|Entidade de [filtragem](api-management-template-data-model-reference.md#Filtering).|Olá informações de filtragem para página da lista de produtos de saudação.|  
|Produtos|Coleção de entidades de [produto](api-management-template-data-model-reference.md#Product).|usuário atual do Hello produtos toohello visível.|  
  
### <a name="sample-template-data"></a>Amostra de dados do modelo  
  
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
  
##  <a name="Product"></a> Produto  
 Olá **produto** modelo permite toocustomize corpo de Olá Olá da página de produtos no portal do desenvolvedor hello.  
  
 ![Página de produtos do portal do desenvolvedor](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")  
  
### <a name="default-template"></a>Modelo padrão  
  
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
  
### <a name="controls"></a>Controles  
 Olá `Product list` modelo pode usar a seguinte Olá [página controles](api-management-page-controls.md).  
  
-   [subscribe-button](api-management-page-controls.md#subscribe-button)  
  
### <a name="data-model"></a>Modelo de dados  
  
|Propriedade|Tipo|Descrição|  
|--------------|----------|-----------------|  
|Produto|[Produto](api-management-template-data-model-reference.md#Product)|produto do Hello especificado.|  
|IsDeveloperSubscribed|Booliano|Se o usuário atual Olá é produto toothis assinados.|  
|SubscriptionState|número|estado de saudação de assinatura de saudação. Os possíveis estados são:<br /><br /> -   `0 - suspended`– Olá assinatura está bloqueada e assinante Olá não é possível chamar quaisquer APIs do produto hello.<br />-   `1 - active`– Olá assinatura está ativa.<br />-   `2 - expired`– Olá atingiu sua data de expiração e foi desativada.<br />-   `3 - submitted`– solicitação de assinatura de saudação foi feita pelo desenvolvedor hello, mas ainda não foi aprovada ou rejeitada.<br />-   `4 - rejected`– solicitação de assinatura de saudação foi negada por um administrador.<br />-   `5 - cancelled`– Olá assinatura foi cancelada pelo administrador ou desenvolvedor de saudação.|  
|limites|array|Essa propriedade foi preterida e não deve ser usada.|  
|DelegatedSubscriptionEnabled|booleano|Se [delegação](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) está habilitada para essa assinatura.|  
|DelegatedSubscriptionUrl|string|Se a delegação estiver habilitada, Olá delegado URL de assinatura.|  
|IsAgreed|Booliano|Se o produto de saudação termos se Olá atual usuário concordou toohello termos.|  
|Assinaturas|Coleção de entidades de [Resumo da assinatura](api-management-template-data-model-reference.md#SubscriptionSummary).|produto de toohello de assinaturas de saudação.|  
|Apis|Coleção de entidades de [API](api-management-template-data-model-reference.md#API).|Olá APIs neste produto.|  
|CannotAddBecauseSubscriptionNumberLimitReached|Booliano|Se o usuário atual Olá é toosubscribe qualificados toothis produto com limite de assinatura de toohello de relação.|  
|CannotAddBecauseMultipleSubscriptionsNotAllowed|Booliano|Se o usuário atual Olá é toosubscribe qualificados toothis produto com assinaturas de toomultiple relação permitidas ou não.|  
  
### <a name="sample-template-data"></a>Amostra de dados do modelo  
  
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

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre como trabalhar com modelos, consulte [como toocustomize Olá portal do desenvolvedor do gerenciamento de API usando modelos](api-management-developer-portal-templates.md).
