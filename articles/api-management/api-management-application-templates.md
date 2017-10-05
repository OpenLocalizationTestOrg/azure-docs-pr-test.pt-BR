---
title: Modelos de aplicativo no Gerenciamento de API do Azure | Microsoft Docs
description: "Saiba como personalizar o conteúdo das páginas de aplicativo no portal do desenvolvedor do Gerenciamento de API do Azure."
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
ms.openlocfilehash: 6d2d44465800219f16866a621d4822614ac9e1dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="application-templates-in-azure-api-management"></a><span data-ttu-id="40b27-103">Modelos de aplicativo no Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="40b27-103">Application templates in Azure API Management</span></span>
<span data-ttu-id="40b27-104">O Gerenciamento de API do Azure fornece a capacidade de personalizar o conteúdo das páginas do portal do desenvolvedor usando um conjunto de modelos que configura o respectivo conteúdo.</span><span class="sxs-lookup"><span data-stu-id="40b27-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="40b27-105">Usando a sintaxe [DotLiquid](http://dotliquidmarkup.org/) e o editor de sua escolha, como o [DotLiquid para Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), bem como um conjunto fornecido de [Recursos de cadeia de caracteres](api-management-template-resources.md#strings), [Recursos do Glyph](api-management-template-resources.md#glyphs) e [Controles de página](api-management-page-controls.md) localizados, você tem grande flexibilidade para configurar o conteúdo das páginas, conforme a necessidade, usando esses modelos.</span><span class="sxs-lookup"><span data-stu-id="40b27-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="40b27-106">Os modelos desta seção permitem personalizar o conteúdo das páginas de aplicativo no portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="40b27-106">The templates in this section allow you to customize the content of the Application pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="40b27-107">Lista de aplicativos</span><span class="sxs-lookup"><span data-stu-id="40b27-107">Application list</span></span>](#ProductList)  
  
-   [<span data-ttu-id="40b27-108">Aplicativo</span><span class="sxs-lookup"><span data-stu-id="40b27-108">Application</span></span>](#Application)  
  
> [!NOTE]
>  <span data-ttu-id="40b27-109">Os modelos de amostra padrão estão incluídos na documentação a seguir, mas estão sujeitos à alteração devido a melhorias contínuas.</span><span class="sxs-lookup"><span data-stu-id="40b27-109">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="40b27-110">Você pode exibir os modelos padrão em tempo real no portal do desenvolvedor, navegando até os modelos individuais desejados.</span><span class="sxs-lookup"><span data-stu-id="40b27-110">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="40b27-111">Para saber mais sobre como trabalhar com modelos, confira [Como personalizar o portal de desenvolvedor de Gerenciamento de API do Azure usando modelos](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="40b27-111">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="40b27-112"><a name="ProductList"></a> Lista de aplicativos</span><span class="sxs-lookup"><span data-stu-id="40b27-112"><a name="ProductList"></a> Application list</span></span>  
 <span data-ttu-id="40b27-113">O modelo **Lista de aplicativos** permite personalizar o corpo da página de lista de aplicativos no portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="40b27-113">The **Application list** template allows you to customize the body of the application list page in the developer portal.</span></span>  
  
 <span data-ttu-id="40b27-114">![Modelos do portal do desenvolvedor da página de lista de aplicativos](./media/api-management-application-templates/APIM-Application-List-Page-Developer-Portal-Templates.png "Modelos do portal do desenvolvedor da página de lista de aplicativos do APIM")</span><span class="sxs-lookup"><span data-stu-id="40b27-114">![Application List Page Developer Portal Templates](./media/api-management-application-templates/APIM-Application-List-Page-Developer-Portal-Templates.png "APIM Application List Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="40b27-115">Modelo padrão</span><span class="sxs-lookup"><span data-stu-id="40b27-115">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="40b27-116">Controles</span><span class="sxs-lookup"><span data-stu-id="40b27-116">Controls</span></span>  
 <span data-ttu-id="40b27-117">O modelo `Product list` pode usar os seguintes [controles de página](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="40b27-117">The `Product list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="40b27-118">paging-control</span><span class="sxs-lookup"><span data-stu-id="40b27-118">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
### <a name="data-model"></a><span data-ttu-id="40b27-119">Modelo de dados</span><span class="sxs-lookup"><span data-stu-id="40b27-119">Data model</span></span>  
  
|<span data-ttu-id="40b27-120">Propriedade</span><span class="sxs-lookup"><span data-stu-id="40b27-120">Property</span></span>|<span data-ttu-id="40b27-121">Tipo</span><span class="sxs-lookup"><span data-stu-id="40b27-121">Type</span></span>|<span data-ttu-id="40b27-122">Descrição</span><span class="sxs-lookup"><span data-stu-id="40b27-122">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="40b27-123">Paginamento</span><span class="sxs-lookup"><span data-stu-id="40b27-123">Paging</span></span>|<span data-ttu-id="40b27-124">Entidade de [paginação](api-management-template-data-model-reference.md#Paging).</span><span class="sxs-lookup"><span data-stu-id="40b27-124">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="40b27-125">As informações de paginação da coleção de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="40b27-125">The paging information for the applications collection.</span></span>|  
|<span data-ttu-id="40b27-126">Aplicativos</span><span class="sxs-lookup"><span data-stu-id="40b27-126">Applications</span></span>|<span data-ttu-id="40b27-127">Coleção de entidades de [Aplicativo](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="40b27-127">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="40b27-128">Os aplicativos visíveis para o usuário atual.</span><span class="sxs-lookup"><span data-stu-id="40b27-128">The applications visible to the current user.</span></span>|  
|<span data-ttu-id="40b27-129">CategoryName</span><span class="sxs-lookup"><span data-stu-id="40b27-129">CategoryName</span></span>|<span data-ttu-id="40b27-130">string</span><span class="sxs-lookup"><span data-stu-id="40b27-130">string</span></span>|<span data-ttu-id="40b27-131">A categoria do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="40b27-131">The category of application.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="40b27-132">Amostra de dados do modelo</span><span class="sxs-lookup"><span data-stu-id="40b27-132">Sample template data</span></span>  
  
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
  
##  <span data-ttu-id="40b27-133"><a name="Application"></a> Aplicativo</span><span class="sxs-lookup"><span data-stu-id="40b27-133"><a name="Application"></a> Application</span></span>  
 <span data-ttu-id="40b27-134">O modelo **Aplicativos** permite personalizar o corpo da página de aplicativos no portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="40b27-134">The **Application** template allows you to customize the body of the application page in the developer portal.</span></span>  
  
 <span data-ttu-id="40b27-135">![Modelos do portal do desenvolvedor da página de aplicativos](./media/api-management-application-templates/APIM-Application-Page-Developer-Portal-Templates.png "Modelos do portal do desenvolvedor da página de aplicativos do APIM")</span><span class="sxs-lookup"><span data-stu-id="40b27-135">![Application Page Developer Portal Templates](./media/api-management-application-templates/APIM-Application-Page-Developer-Portal-Templates.png "APIM Application Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="40b27-136">Modelo padrão</span><span class="sxs-lookup"><span data-stu-id="40b27-136">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="40b27-137">Controles</span><span class="sxs-lookup"><span data-stu-id="40b27-137">Controls</span></span>  
 <span data-ttu-id="40b27-138">O modelo `Application` não permite o uso de quaisquer [controles de página](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="40b27-138">The `Application` template does not allow the use of any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="40b27-139">Modelo de dados</span><span class="sxs-lookup"><span data-stu-id="40b27-139">Data model</span></span>  
 <span data-ttu-id="40b27-140">Entidade de [aplicativo](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="40b27-140">[Application](api-management-template-data-model-reference.md#Application) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="40b27-141">Amostra de dados do modelo</span><span class="sxs-lookup"><span data-stu-id="40b27-141">Sample template data</span></span>  
  
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

## <a name="next-steps"></a><span data-ttu-id="40b27-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="40b27-142">Next steps</span></span>
<span data-ttu-id="40b27-143">Para saber mais sobre como trabalhar com modelos, confira [Como personalizar o portal de desenvolvedor de Gerenciamento de API do Azure usando modelos](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="40b27-143">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>