---
title: modelos de aaaApplication no gerenciamento de API do Azure | Microsoft Docs
description: "Saiba como toocustomize Olá conteúdo das páginas de aplicativo hello no portal do desenvolvedor Olá no gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: f3122c4d-e10e-4cdf-977b-36e8f4133fc8
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: f4dc078be7163b047ca2e640a9065ba9e5ba709e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="application-templates-in-azure-api-management"></a><span data-ttu-id="2b1ff-103">Modelos de aplicativo no Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="2b1ff-103">Application templates in Azure API Management</span></span>
<span data-ttu-id="2b1ff-104">Gerenciamento de API do Azure fornece que Olá conteúdo de saudação toocustomize capacidade de páginas de portal do desenvolvedor usando um conjunto de modelos que configurar seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="2b1ff-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="2b1ff-105">Usando [DotLiquid](http://dotliquidmarkup.org/) sintaxe e hello editor de sua escolha, como [DotLiquid para Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), e um conjunto fornecido de localizadas [recursos de cadeia de caracteres](api-management-template-resources.md#strings), [ Recursos de glifo](api-management-template-resources.md#glyphs), e [página controles](api-management-page-controls.md), você tiver um grande flexibilidade tooconfigure Olá conteúdo das páginas hello como desejar usar esses modelos.</span><span class="sxs-lookup"><span data-stu-id="2b1ff-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="2b1ff-106">Olá modelos nesta seção permitem toocustomize conteúdo de saudação de páginas de aplicativo hello no portal do desenvolvedor hello.</span><span class="sxs-lookup"><span data-stu-id="2b1ff-106">hello templates in this section allow you toocustomize hello content of hello Application pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="2b1ff-107">Lista de aplicativos</span><span class="sxs-lookup"><span data-stu-id="2b1ff-107">Application list</span></span>](#ProductList)  
  
-   [<span data-ttu-id="2b1ff-108">Aplicativo</span><span class="sxs-lookup"><span data-stu-id="2b1ff-108">Application</span></span>](#Application)  
  
> [!NOTE]
>  <span data-ttu-id="2b1ff-109">Modelos de padrão de exemplo estão incluídos no hello documentação a seguir, mas são toochange assunto devido a melhorias toocontinuous.</span><span class="sxs-lookup"><span data-stu-id="2b1ff-109">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="2b1ff-110">Você pode exibir modelos do saudação padrão em tempo real no portal do desenvolvedor Olá navegando modelos individuais toohello desejado.</span><span class="sxs-lookup"><span data-stu-id="2b1ff-110">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="2b1ff-111">Para obter mais informações sobre como trabalhar com modelos, consulte [como toocustomize Olá portal do desenvolvedor do gerenciamento de API usando modelos](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="2b1ff-111">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="2b1ff-112"><a name="ProductList"></a> Lista de aplicativos</span><span class="sxs-lookup"><span data-stu-id="2b1ff-112"><a name="ProductList"></a> Application list</span></span>  
 <span data-ttu-id="2b1ff-113">Olá **lista de aplicativos** modelo permite toocustomize corpo de saudação da página de lista do aplicativo hello no portal do desenvolvedor hello.</span><span class="sxs-lookup"><span data-stu-id="2b1ff-113">hello **Application list** template allows you toocustomize hello body of hello application list page in hello developer portal.</span></span>  
  
 <span data-ttu-id="2b1ff-114">![Modelos do portal do desenvolvedor da página de lista de aplicativos](./media/api-management-application-templates/APIM-Application-List-Page-Developer-Portal-Templates.png "Modelos do portal do desenvolvedor da página de lista de aplicativos do APIM")</span><span class="sxs-lookup"><span data-stu-id="2b1ff-114">![Application List Page Developer Portal Templates](./media/api-management-application-templates/APIM-Application-List-Page-Developer-Portal-Templates.png "APIM Application List Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="2b1ff-115">Modelo padrão</span><span class="sxs-lookup"><span data-stu-id="2b1ff-115">Default template</span></span>  
  
```xml  
<div class="row">  
    <div class="col-md-9">  
        <h2>{% localized "AppStrings|WebApplicationsHeader" %}</h2>  
    </div>  
</div>  
<div class="row">  
    <div class="col-md-12">  
    {% if applications.size > 0 %}  
        <ul class="list-unstyled">  
        {% for app in applications %}  
            <li>  
            {% if app.application.icon.url != "" %}  
                <aside>  
                    <a href="/applications/details/{{app.application.id}}"><img src="{{app.application.icon.url}}" alt="App Icon" /></a>  
                </aside>  
            {% endif %}  
                <h3><a href="/applications/details/{{app.application.id}}">{{app.application.title}}</a></h3>  
                {{app.application.description}}  
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
  
### <a name="controls"></a><span data-ttu-id="2b1ff-116">Controles</span><span class="sxs-lookup"><span data-stu-id="2b1ff-116">Controls</span></span>  
 <span data-ttu-id="2b1ff-117">Olá `Product list` modelo pode usar a seguinte Olá [página controles](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="2b1ff-117">hello `Product list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="2b1ff-118">paging-control</span><span class="sxs-lookup"><span data-stu-id="2b1ff-118">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
### <a name="data-model"></a><span data-ttu-id="2b1ff-119">Modelo de dados</span><span class="sxs-lookup"><span data-stu-id="2b1ff-119">Data model</span></span>  
  
|<span data-ttu-id="2b1ff-120">Propriedade</span><span class="sxs-lookup"><span data-stu-id="2b1ff-120">Property</span></span>|<span data-ttu-id="2b1ff-121">Tipo</span><span class="sxs-lookup"><span data-stu-id="2b1ff-121">Type</span></span>|<span data-ttu-id="2b1ff-122">Descrição</span><span class="sxs-lookup"><span data-stu-id="2b1ff-122">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="2b1ff-123">Paginamento</span><span class="sxs-lookup"><span data-stu-id="2b1ff-123">Paging</span></span>|<span data-ttu-id="2b1ff-124">Entidade de [paginação](api-management-template-data-model-reference.md#Paging).</span><span class="sxs-lookup"><span data-stu-id="2b1ff-124">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="2b1ff-125">Olá paginação as informações para a coleção de aplicativos de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b1ff-125">hello paging information for hello applications collection.</span></span>|  
|<span data-ttu-id="2b1ff-126">Aplicativos</span><span class="sxs-lookup"><span data-stu-id="2b1ff-126">Applications</span></span>|<span data-ttu-id="2b1ff-127">Coleção de entidades de [Aplicativo](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="2b1ff-127">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="2b1ff-128">usuário atual do Hello aplicativos toohello visível.</span><span class="sxs-lookup"><span data-stu-id="2b1ff-128">hello applications visible toohello current user.</span></span>|  
|<span data-ttu-id="2b1ff-129">CategoryName</span><span class="sxs-lookup"><span data-stu-id="2b1ff-129">CategoryName</span></span>|<span data-ttu-id="2b1ff-130">string</span><span class="sxs-lookup"><span data-stu-id="2b1ff-130">string</span></span>|<span data-ttu-id="2b1ff-131">categoria de saudação do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2b1ff-131">hello category of application.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="2b1ff-132">Amostra de dados do modelo</span><span class="sxs-lookup"><span data-stu-id="2b1ff-132">Sample template data</span></span>  
  
```json  
{  
    "Paging": {  
        "Page": 1,  
        "PageSize": 10,  
        "TotalItemCount": 1,  
        "ShowAll": false,  
        "PageCount": 1  
    },  
    "Applications": [  
        {  
            "Application": {  
                "Id": "5702b96fb16653124c8f9ba8",  
                "Title": "Contoso Calculator",  
                "Description": "A simple online calculator.",  
                "Url": null,  
                "Version": null,  
                "Requirements": "Free application with no requirements.",  
                "State": 2,  
                "RegistrationDate": "2016-04-04T18:59:00",  
                "CategoryId": 5,  
                "DeveloperId": "5702b5b0b16653124c8f9ba4",  
                "Attachments": [  
                    {  
                        "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
                        "Url": "https://apimgmtst65gdjvjrgdbfhr4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
                        "Type": "Icon",  
                        "ContentType": "image/png"  
                    },  
                    {  
                        "UniqueId": "2b4fa5dd-00ff-4a8f-b1b7-51e715849ede",  
                        "Url": "https://apimgmtst65gdjvjrgdbfhr4.blob.core.windows.net/content/applications/2b4fa5dd-00ff-4a8f-b1b7-51e715849ede.png",  
                        "Type": "Screenshot",  
                        "ContentType": "image/png"  
                    }  
                ],  
                "Icon": {  
                    "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
                    "Url": "https://apimgmtst65gdjvjrgdbfhr4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
                    "Type": "Icon",  
                    "ContentType": "image/png"  
                }  
            },  
            "CategoryName": "Finance"  
        }  
    ]  
}  
```  
  
##  <span data-ttu-id="2b1ff-133"><a name="Application"></a> Aplicativo</span><span class="sxs-lookup"><span data-stu-id="2b1ff-133"><a name="Application"></a> Application</span></span>  
 <span data-ttu-id="2b1ff-134">Olá **aplicativo** modelo permite toocustomize corpo de saudação da página de aplicativo hello no portal do desenvolvedor hello.</span><span class="sxs-lookup"><span data-stu-id="2b1ff-134">hello **Application** template allows you toocustomize hello body of hello application page in hello developer portal.</span></span>  
  
 <span data-ttu-id="2b1ff-135">![Modelos do portal do desenvolvedor da página de aplicativos](./media/api-management-application-templates/APIM-Application-Page-Developer-Portal-Templates.png "Modelos do portal do desenvolvedor da página de aplicativos do APIM")</span><span class="sxs-lookup"><span data-stu-id="2b1ff-135">![Application Page Developer Portal Templates](./media/api-management-application-templates/APIM-Application-Page-Developer-Portal-Templates.png "APIM Application Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="2b1ff-136">Modelo padrão</span><span class="sxs-lookup"><span data-stu-id="2b1ff-136">Default template</span></span>  
  
```xml  
<h2>{{title}}</h2>  
{% if icon.url != "" %}  
<aside class="applications_aside">  
  <div class="image-placeholder">  
    <img src="{{icon.url}}" alt="Application Icon" />  
  </div>  
</aside>  
{% endif %}  
  
<article>  
  {% if url != "" %}  
    <a target="_blank" href="{{url}}">{{url}}</a>  
  {% endif %}  
  
  <p>{{description}}</p>  
  
  {% if requirements != null %}  
  <h3>{% localized "AppDetailsStrings|WebApplicationsRequirementsHeader" %}</h3>  
  <p>{{requirements}}</p>  
  {% endif %}  
  
  {% if attachments.size > 0 %}  
  <h3>{% localized "AppDetailsStrings|WebApplicationsScreenshotsHeader" %}</h3>  
    {% for screenshot in attachments %}  
      {% if screenshot.type != "Icon" %}  
      <a href="{{screenshot.url}}" data-lightbox="example-set">  
          <img src="/Developer/Applications/Thumbnail?url={{screenshot.url}}" alt='{% localized "AppDetailsStrings|WebApplicationsScreenshotAlt" %}' />  
      </a>  
      {% endif %}  
    {% endfor %}  
  {% endif %}  
</article>  
  
```  
  
### <a name="controls"></a><span data-ttu-id="2b1ff-137">Controles</span><span class="sxs-lookup"><span data-stu-id="2b1ff-137">Controls</span></span>  
 <span data-ttu-id="2b1ff-138">Olá `Application` modelo não permite o uso de saudação de qualquer [página controles](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="2b1ff-138">hello `Application` template does not allow hello use of any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="2b1ff-139">Modelo de dados</span><span class="sxs-lookup"><span data-stu-id="2b1ff-139">Data model</span></span>  
 <span data-ttu-id="2b1ff-140">Entidade de [aplicativo](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="2b1ff-140">[Application](api-management-template-data-model-reference.md#Application) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="2b1ff-141">Amostra de dados do modelo</span><span class="sxs-lookup"><span data-stu-id="2b1ff-141">Sample template data</span></span>  
  
```json  
{  
    "Id": "5702b96fb16653124c8f9ba8",  
    "Title": "Contoso Calculator",  
    "Description": "A simple online calculator.",  
    "Url": null,  
    "Version": null,  
    "Requirements": "Free application with no requirements.",  
    "State": 2,  
    "RegistrationDate": "2016-04-04T18:59:00",  
    "CategoryId": 5,  
    "DeveloperId": "5702b5b0b16653124c8f9ba4",  
    "Attachments": [  
        {  
            "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
            "Url": "https://apimgmtst3aybshdqqcqrle4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
            "Type": "Icon",  
            "ContentType": "image/png"  
        },  
        {  
            "UniqueId": "2b4fa5dd-00ff-4a8f-b1b7-51e715849ede",  
            "Url": "https://apimgmtst3aybshdqqcqrle4.blob.core.windows.net/content/applications/2b4fa5dd-00ff-4a8f-b1b7-51e715849ede.png",  
            "Type": "Screenshot",  
            "ContentType": "image/png"  
        }  
    ],  
    "Icon": {  
        "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
        "Url": "https://apimgmtst3aybshdqqcqrle4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
        "Type": "Icon",  
        "ContentType": "image/png"  
    }  
}  
```

## <a name="next-steps"></a><span data-ttu-id="2b1ff-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2b1ff-142">Next steps</span></span>
<span data-ttu-id="2b1ff-143">Para obter mais informações sobre como trabalhar com modelos, consulte [como toocustomize Olá portal do desenvolvedor do gerenciamento de API usando modelos](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="2b1ff-143">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
