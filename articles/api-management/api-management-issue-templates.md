---
title: modelos de aaaIssue no gerenciamento de API do Azure | Microsoft Docs
description: "Saiba como toocustomize Olá conteúdo das páginas de problema Olá no portal do desenvolvedor Olá no gerenciamento de API do Azure."
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
ms.openlocfilehash: e12902e52c164f73902a97f15ea550790dfecf1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="issue-templates-in-azure-api-management"></a><span data-ttu-id="ce54c-103">Modelos de problemas no Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="ce54c-103">Issue templates in Azure API Management</span></span>
<span data-ttu-id="ce54c-104">Gerenciamento de API do Azure fornece que Olá conteúdo de saudação toocustomize capacidade de páginas de portal do desenvolvedor usando um conjunto de modelos que configurar seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="ce54c-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="ce54c-105">Usando [DotLiquid](http://dotliquidmarkup.org/) sintaxe e hello editor de sua escolha, como [DotLiquid para Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), e um conjunto fornecido de localizadas [recursos de cadeia de caracteres](api-management-template-resources.md#strings), [ Recursos de glifo](api-management-template-resources.md#glyphs), e [página controles](api-management-page-controls.md), você tiver um grande flexibilidade tooconfigure Olá conteúdo das páginas hello como desejar usar esses modelos.</span><span class="sxs-lookup"><span data-stu-id="ce54c-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="ce54c-106">Olá modelos nesta seção permitem toocustomize conteúdo de saudação de páginas de problema Olá no portal do desenvolvedor hello.</span><span class="sxs-lookup"><span data-stu-id="ce54c-106">hello templates in this section allow you toocustomize hello content of hello Issue pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="ce54c-107">Lista de problemas</span><span class="sxs-lookup"><span data-stu-id="ce54c-107">Issue list</span></span>](#IssueList)  
  
> [!NOTE]
>  <span data-ttu-id="ce54c-108">Modelos de padrão de exemplo estão incluídos no hello documentação a seguir, mas são toochange assunto devido a melhorias toocontinuous.</span><span class="sxs-lookup"><span data-stu-id="ce54c-108">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="ce54c-109">Você pode exibir modelos do saudação padrão em tempo real no portal do desenvolvedor Olá navegando modelos individuais toohello desejado.</span><span class="sxs-lookup"><span data-stu-id="ce54c-109">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="ce54c-110">Para obter mais informações sobre como trabalhar com modelos, consulte [como toocustomize Olá portal do desenvolvedor do gerenciamento de API usando modelos](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ce54c-110">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>  
  
##  <span data-ttu-id="ce54c-111"><a name="IssueList"></a> Lista de problemas</span><span class="sxs-lookup"><span data-stu-id="ce54c-111"><a name="IssueList"></a> Issue list</span></span>  
 <span data-ttu-id="ce54c-112">Olá **lista problema** modelo permite toocustomize corpo de saudação da página de lista de problema Olá no portal do desenvolvedor hello.</span><span class="sxs-lookup"><span data-stu-id="ce54c-112">hello **Issue list** template allows you toocustomize hello body of hello issue list page in hello developer portal.</span></span>  
  
 <span data-ttu-id="ce54c-113">![Lista de problemas do portal do desenvolvedor](./media/api-management-issue-templates/APIM-Issue-List-Developer-Portal.png "Lista de problemas do portal do desenvolvedor do APIM")</span><span class="sxs-lookup"><span data-stu-id="ce54c-113">![Issue List Developer Portal](./media/api-management-issue-templates/APIM-Issue-List-Developer-Portal.png "APIM Issue List Developer Portal")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="ce54c-114">Modelo padrão</span><span class="sxs-lookup"><span data-stu-id="ce54c-114">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="ce54c-115">Controles</span><span class="sxs-lookup"><span data-stu-id="ce54c-115">Controls</span></span>  
 <span data-ttu-id="ce54c-116">Olá `Issue list` modelo pode usar a seguinte Olá [página controles](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="ce54c-116">hello `Issue list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="ce54c-117">paging-control</span><span class="sxs-lookup"><span data-stu-id="ce54c-117">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
### <a name="data-model"></a><span data-ttu-id="ce54c-118">Modelo de dados</span><span class="sxs-lookup"><span data-stu-id="ce54c-118">Data model</span></span>  
  
|<span data-ttu-id="ce54c-119">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ce54c-119">Property</span></span>|<span data-ttu-id="ce54c-120">Tipo</span><span class="sxs-lookup"><span data-stu-id="ce54c-120">Type</span></span>|<span data-ttu-id="ce54c-121">Descrição</span><span class="sxs-lookup"><span data-stu-id="ce54c-121">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="ce54c-122">Problemas</span><span class="sxs-lookup"><span data-stu-id="ce54c-122">Issues</span></span>|<span data-ttu-id="ce54c-123">Coleção de entidades de [problemas](api-management-template-data-model-reference.md#Issue).</span><span class="sxs-lookup"><span data-stu-id="ce54c-123">Collection of [Issue](api-management-template-data-model-reference.md#Issue) entities.</span></span>|<span data-ttu-id="ce54c-124">usuário atual do Hello problemas toohello visível.</span><span class="sxs-lookup"><span data-stu-id="ce54c-124">hello issues visible toohello current user.</span></span>|  
|<span data-ttu-id="ce54c-125">Paginamento</span><span class="sxs-lookup"><span data-stu-id="ce54c-125">Paging</span></span>|<span data-ttu-id="ce54c-126">Entidade de [paginação](api-management-template-data-model-reference.md#Paging).</span><span class="sxs-lookup"><span data-stu-id="ce54c-126">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="ce54c-127">Olá paginação as informações para a coleção de aplicativos de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce54c-127">hello paging information for hello applications collection.</span></span>|  
|<span data-ttu-id="ce54c-128">IsAuthenticated</span><span class="sxs-lookup"><span data-stu-id="ce54c-128">IsAuthenticated</span></span>|<span data-ttu-id="ce54c-129">Booliano</span><span class="sxs-lookup"><span data-stu-id="ce54c-129">boolean</span></span>|<span data-ttu-id="ce54c-130">Se o usuário atual Olá é toohello assinado no portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="ce54c-130">Whether hello current user is signed-in toohello developer portal.</span></span>|  
|<span data-ttu-id="ce54c-131">CanReportIssues</span><span class="sxs-lookup"><span data-stu-id="ce54c-131">CanReportIssues</span></span>|<span data-ttu-id="ce54c-132">Booliano</span><span class="sxs-lookup"><span data-stu-id="ce54c-132">boolean</span></span>|<span data-ttu-id="ce54c-133">Se o usuário atual Olá tem permissões toofile um problema.</span><span class="sxs-lookup"><span data-stu-id="ce54c-133">Whether hello current user has permissions toofile an issue.</span></span>|  
|<span data-ttu-id="ce54c-134">Pesquisar</span><span class="sxs-lookup"><span data-stu-id="ce54c-134">Search</span></span>|<span data-ttu-id="ce54c-135">string</span><span class="sxs-lookup"><span data-stu-id="ce54c-135">string</span></span>|<span data-ttu-id="ce54c-136">Essa propriedade foi preterida e não deve ser usada.</span><span class="sxs-lookup"><span data-stu-id="ce54c-136">This property is deprecated and should not be used.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="ce54c-137">Amostra de dados do modelo</span><span class="sxs-lookup"><span data-stu-id="ce54c-137">Sample template data</span></span>  
  
```json  
{  
    "Issues": [  
        {  
            "Id": "5702b68bb16653124c8f9ba7",  
            "ApiId": "570275f1b16653124c8f9ba3",  
            "Title": "I couldn't figure out how tooconnect my application toohello API",  
            "Description": "I'm having trouble connecting my application toohello backend API.",  
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

## <a name="next-steps"></a><span data-ttu-id="ce54c-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ce54c-138">Next steps</span></span>
<span data-ttu-id="ce54c-139">Para obter mais informações sobre como trabalhar com modelos, consulte [como toocustomize Olá portal do desenvolvedor do gerenciamento de API usando modelos](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ce54c-139">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
