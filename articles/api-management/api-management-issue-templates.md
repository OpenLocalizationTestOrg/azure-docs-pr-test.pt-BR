---
title: Modelos de problemas no Gerenciamento de API do Azure | Microsoft Docs
description: "Saiba como personalizar o conteúdo das páginas de Problemas no portal do desenvolvedor do Gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 47da4bb2-426e-4e53-8fa7-214ee2e3ab37
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: e13344df198bca4f73c75fa58221436b94e2f258
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="issue-templates-in-azure-api-management"></a><span data-ttu-id="6c16b-103">Modelos de problemas no Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="6c16b-103">Issue templates in Azure API Management</span></span>
<span data-ttu-id="6c16b-104">O Gerenciamento de API do Azure fornece a capacidade de personalizar o conteúdo das páginas do portal do desenvolvedor usando um conjunto de modelos que configura o respectivo conteúdo.</span><span class="sxs-lookup"><span data-stu-id="6c16b-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="6c16b-105">Usando a sintaxe [DotLiquid](http://dotliquidmarkup.org/) e o editor de sua escolha, como o [DotLiquid para Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), bem como um conjunto fornecido de [Recursos de cadeia de caracteres](api-management-template-resources.md#strings), [Recursos do Glyph](api-management-template-resources.md#glyphs) e [Controles de página](api-management-page-controls.md) localizados, você tem grande flexibilidade para configurar o conteúdo das páginas, conforme a necessidade, usando esses modelos.</span><span class="sxs-lookup"><span data-stu-id="6c16b-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="6c16b-106">Os modelos desta seção permitem personalizar o conteúdo das páginas de problemas no portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="6c16b-106">The templates in this section allow you to customize the content of the Issue pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="6c16b-107">Lista de problemas</span><span class="sxs-lookup"><span data-stu-id="6c16b-107">Issue list</span></span>](#IssueList)  
  
> [!NOTE]
>  <span data-ttu-id="6c16b-108">Os modelos de amostra padrão estão incluídos na documentação a seguir, mas estão sujeitos à alteração devido a melhorias contínuas.</span><span class="sxs-lookup"><span data-stu-id="6c16b-108">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="6c16b-109">Você pode exibir os modelos padrão em tempo real no portal do desenvolvedor, navegando até os modelos individuais desejados.</span><span class="sxs-lookup"><span data-stu-id="6c16b-109">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="6c16b-110">Para saber mais sobre como trabalhar com modelos, confira [Como personalizar o portal de desenvolvedor de Gerenciamento de API do Azure usando modelos](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="6c16b-110">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>  
  
##  <span data-ttu-id="6c16b-111"><a name="IssueList"></a> Lista de problemas</span><span class="sxs-lookup"><span data-stu-id="6c16b-111"><a name="IssueList"></a> Issue list</span></span>  
 <span data-ttu-id="6c16b-112">O modelo **Lista de problemas** possibilita personalizar o corpo da página de lista de problemas no portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="6c16b-112">The **Issue list** template allows you to customize the body of the issue list page in the developer portal.</span></span>  
  
 <span data-ttu-id="6c16b-113">![Lista de problemas do portal do desenvolvedor](./media/api-management-issue-templates/APIM-Issue-List-Developer-Portal.png "Lista de problemas do portal do desenvolvedor do APIM")</span><span class="sxs-lookup"><span data-stu-id="6c16b-113">![Issue List Developer Portal](./media/api-management-issue-templates/APIM-Issue-List-Developer-Portal.png "APIM Issue List Developer Portal")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="6c16b-114">Modelo padrão</span><span class="sxs-lookup"><span data-stu-id="6c16b-114">Default template</span></span>  
  
```xml  
<div class="row">  
  <div class="col-md-9">  
    <h2>{% localized "IssuesStrings|WebIssuesIndexTitle" %}</h2>  
  </div>  
</div>  
<div class="row">  
  <div class="col-md-12">  
    {% if issues.size > 0 %}  
    <ul class="list-unstyled">  
      {% capture reportedBy %}{% localized "IssuesStrings|WebIssuesStatusReportedBy" %}{% endcapture %}  
      {% assign replaceString0 = '{0}' %}  
      {% assign replaceString1 = '{1}' %}  
      {% for issue in issues %}  
      <li>  
        <h3>  
          <a href="/issues/{{issue.id}}">{{issue.title}}</a>  
        </h3>  
        <p>{{issue.description}}</p>  
        <em>  
          {% capture state %}{{issue.issueState}}{% endcapture %}  
          {% capture devName %}{{issue.subscriptionDeveloperName}}{% endcapture %}  
          {% capture str1 %}{{ reportedBy | replace : replaceString0, state }}{% endcapture %}  
          {{ str1 | replace : replaceString1, devName }}  
          <span class="UtcDateElement">{{ issue.reportedOn | date: "r" }}</span>  
        </em>  
      </li>  
      {% endfor %}  
    </ul>  
    <paging-control></paging-control>  
    {% else %}  
    {% localized "CommonResources|NoItemsToDisplay" %}  
    {% endif %}  
    {% if canReportIssue %}  
    <a class="btn btn-primary" id="createIssue" href="/Issues/Create">{% localized "IssuesStrings|WebIssuesReportIssueButton" %}</a>  
    {% elsif isAuthenticated %}  
    <hr />  
    <p>{% localized "IssuesStrings|WebIssuesNoActiveSubscriptions" %}</p>  
    {% else %}  
    <hr />  
    <p>  
      {% capture signIntext %}{% localized "IssuesStrings|WebIssuesNotSignin" %}{% endcapture %}  
      {% capture link %}<a href="/signin">{% localized "IssuesStrings|WebIssuesSignIn" %}</a>{% endcapture %}  
      {{ signIntext | replace : replaceString0, link }}  
    </p>  
    {% endif %}  
  </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="6c16b-115">Controles</span><span class="sxs-lookup"><span data-stu-id="6c16b-115">Controls</span></span>  
 <span data-ttu-id="6c16b-116">O modelo `Issue list` pode usar os seguintes [controles de página](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="6c16b-116">The `Issue list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="6c16b-117">paging-control</span><span class="sxs-lookup"><span data-stu-id="6c16b-117">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
### <a name="data-model"></a><span data-ttu-id="6c16b-118">Modelo de dados</span><span class="sxs-lookup"><span data-stu-id="6c16b-118">Data model</span></span>  
  
|<span data-ttu-id="6c16b-119">Propriedade</span><span class="sxs-lookup"><span data-stu-id="6c16b-119">Property</span></span>|<span data-ttu-id="6c16b-120">Tipo</span><span class="sxs-lookup"><span data-stu-id="6c16b-120">Type</span></span>|<span data-ttu-id="6c16b-121">Descrição</span><span class="sxs-lookup"><span data-stu-id="6c16b-121">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="6c16b-122">Problemas</span><span class="sxs-lookup"><span data-stu-id="6c16b-122">Issues</span></span>|<span data-ttu-id="6c16b-123">Coleção de entidades de [problemas](api-management-template-data-model-reference.md#Issue).</span><span class="sxs-lookup"><span data-stu-id="6c16b-123">Collection of [Issue](api-management-template-data-model-reference.md#Issue) entities.</span></span>|<span data-ttu-id="6c16b-124">Os problemas visíveis para o usuário atual.</span><span class="sxs-lookup"><span data-stu-id="6c16b-124">The issues visible to the current user.</span></span>|  
|<span data-ttu-id="6c16b-125">Paginamento</span><span class="sxs-lookup"><span data-stu-id="6c16b-125">Paging</span></span>|<span data-ttu-id="6c16b-126">Entidade de [paginação](api-management-template-data-model-reference.md#Paging).</span><span class="sxs-lookup"><span data-stu-id="6c16b-126">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="6c16b-127">As informações de paginação da coleção de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="6c16b-127">The paging information for the applications collection.</span></span>|  
|<span data-ttu-id="6c16b-128">IsAuthenticated</span><span class="sxs-lookup"><span data-stu-id="6c16b-128">IsAuthenticated</span></span>|<span data-ttu-id="6c16b-129">booleano</span><span class="sxs-lookup"><span data-stu-id="6c16b-129">boolean</span></span>|<span data-ttu-id="6c16b-130">Se o usuário atual está conectado ao portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="6c16b-130">Whether the current user is signed-in to the developer portal.</span></span>|  
|<span data-ttu-id="6c16b-131">CanReportIssues</span><span class="sxs-lookup"><span data-stu-id="6c16b-131">CanReportIssues</span></span>|<span data-ttu-id="6c16b-132">booleano</span><span class="sxs-lookup"><span data-stu-id="6c16b-132">boolean</span></span>|<span data-ttu-id="6c16b-133">Se o usuário atual tem permissões para arquivar um problema.</span><span class="sxs-lookup"><span data-stu-id="6c16b-133">Whether the current user has permissions to file an issue.</span></span>|  
|<span data-ttu-id="6c16b-134">Pesquisar</span><span class="sxs-lookup"><span data-stu-id="6c16b-134">Search</span></span>|<span data-ttu-id="6c16b-135">string</span><span class="sxs-lookup"><span data-stu-id="6c16b-135">string</span></span>|<span data-ttu-id="6c16b-136">Essa propriedade foi preterida e não deve ser usada.</span><span class="sxs-lookup"><span data-stu-id="6c16b-136">This property is deprecated and should not be used.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="6c16b-137">Amostra de dados do modelo</span><span class="sxs-lookup"><span data-stu-id="6c16b-137">Sample template data</span></span>  
  
```json  
{  
    "Issues": [  
        {  
            "Id": "5702b68bb16653124c8f9ba7",  
            "ApiId": "570275f1b16653124c8f9ba3",  
            "Title": "I couldn't figure out how to connect my application to the API",  
            "Description": "I'm having trouble connecting my application to the backend API.",  
            "SubscriptionDeveloperName": "Clayton",  
            "IssueState": "Proposed",  
            "ReportedOn": "2016-04-04T18:46:35.64",  
            "Comments": null,  
            "Attachments": null,  
            "Services": null  
        }  
    ],  
    "Paging": {  
        "Page": 1,  
        "PageSize": 10,  
        "TotalItemCount": 1,  
        "ShowAll": false,  
        "PageCount": 1  
    },  
    "IsAuthenticated": true,  
    "CanReportIssue": true,  
    "Search": null  
}  
```

## <a name="next-steps"></a><span data-ttu-id="6c16b-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6c16b-138">Next steps</span></span>
<span data-ttu-id="6c16b-139">Para saber mais sobre como trabalhar com modelos, confira [Como personalizar o portal de desenvolvedor de Gerenciamento de API do Azure usando modelos](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="6c16b-139">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>