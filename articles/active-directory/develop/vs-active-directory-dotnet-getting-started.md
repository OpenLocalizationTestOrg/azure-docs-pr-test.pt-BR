---
title: "Introdução ao Azure AD em projetos do Visual Studio MVC | Microsoft Docs"
description: "Como começar a usar o Active Directory do Azure em projetos do MVC após a conexão ou criação de um AD do Azure usando os serviços conectados do Visual Studio"
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1c8b6a58-5144-4965-a905-625b9ee7b22b
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: c4d49cfc9887e422b3eaed2b96348c99eca48881
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="getting-started-with-azure-active-directory-and-visual-studio-connected-services-mvc-projects"></a><span data-ttu-id="07284-103">Introdução ao Active Directory do Azure e aos serviços conectados do Visual Studio (Projetos do MVC)</span><span class="sxs-lookup"><span data-stu-id="07284-103">Getting Started with Azure Active Directory and Visual Studio connected services (MVC Projects)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="07284-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="07284-104">Getting Started</span></span>](vs-active-directory-dotnet-getting-started.md)
> * [<span data-ttu-id="07284-105">O que aconteceu</span><span class="sxs-lookup"><span data-stu-id="07284-105">What Happened</span></span>](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="requiring-authentication-to-access-controllers"></a><span data-ttu-id="07284-106">Exigir autenticação para acessar os controladores</span><span class="sxs-lookup"><span data-stu-id="07284-106">Requiring authentication to access controllers</span></span>
<span data-ttu-id="07284-107">Todos os controladores em seu projeto foram marcados com o atributo **Autorizar** .</span><span class="sxs-lookup"><span data-stu-id="07284-107">All controllers in your project were adorned with the **Authorize** attribute.</span></span> <span data-ttu-id="07284-108">Este atributo exige que o usuário seja autenticado antes de acessar esses controladores.</span><span class="sxs-lookup"><span data-stu-id="07284-108">This attribute requires the user to be authenticated before accessing these controllers.</span></span> <span data-ttu-id="07284-109">Para permitir que o controlador seja acessado anonimamente, remova este atributo do controlador.</span><span class="sxs-lookup"><span data-stu-id="07284-109">To allow the controller to be accessed anonymously, remove this attribute from the controller.</span></span> <span data-ttu-id="07284-110">Se desejar definir as permissões em um nível mais granular, aplique o atributo a cada método que necessita de autorização em vez de aplicá-lo à classe do controlador.</span><span class="sxs-lookup"><span data-stu-id="07284-110">If you want to set the permissions at a more granular level, apply the attribute to each method that requires authorization instead of applying it to the controller class.</span></span>

## <a name="adding-signin--signout-controls"></a><span data-ttu-id="07284-111">Adicionar controles de SignIn / SignOut</span><span class="sxs-lookup"><span data-stu-id="07284-111">Adding SignIn / SignOut Controls</span></span>
<span data-ttu-id="07284-112">Para adicionar controles SignIn/SignOut à exibição, é possível usar a exibição parcial **_LoginPartial.cshtml** para adicionar a funcionalidade a uma das exibições.</span><span class="sxs-lookup"><span data-stu-id="07284-112">To add the SignIn/SignOut controls to your view, you can use the **_LoginPartial.cshtml** partial view to add the functionality to one of your views.</span></span> <span data-ttu-id="07284-113">Veja um exemplo da funcionalidade adicionada à visualização standard**_Layout.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="07284-113">Here is an example of the functionality added to the standard **_Layout.cshtml** view.</span></span> <span data-ttu-id="07284-114">(Observe o último elemento no div com classe navbar-collapse):</span><span class="sxs-lookup"><span data-stu-id="07284-114">(Note the last element in the div with class navbar-collapse):</span></span>

<pre>
    &lt;!DOCTYPE html&gt; 
     &lt;html&gt; 
     &lt;head&gt; 
         &lt;meta charset="utf-8" /&gt; 
        &lt;meta name="viewport" content="width=device-width, initial-scale=1.0"&gt; 
        &lt;title&gt;@ViewBag.Title - My ASP.NET Application&lt;/title&gt; 
        @Styles.Render("~/Content/css") 
        @Scripts.Render("~/bundles/modernizr") 
    &lt;/head&gt; 
    &lt;body&gt; 
        &lt;div class="navbar navbar-inverse navbar-fixed-top"&gt; 
            &lt;div class="container"&gt; 
                &lt;div class="navbar-header"&gt; 
                    &lt;button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-collapse"&gt; 
                        &lt;span class="icon-bar"&gt;&lt;/span&gt; 
                        &lt;span class="icon-bar"&gt;&lt;/span&gt; 
                        &lt;span class="icon-bar"&gt;&lt;/span&gt; 
                    &lt;/button&gt; 
                    @Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" }) 
                &lt;/div&gt; 
                &lt;div class="navbar-collapse collapse"&gt; 
                    &lt;ul class="nav navbar-nav"&gt; 
                        &lt;li&gt;@Html.ActionLink("Home", "Index", "Home")&lt;/li&gt; 
                        &lt;li&gt;@Html.ActionLink("About", "About", "Home")&lt;/li&gt; 
                        &lt;li&gt;@Html.ActionLink("Contact", "Contact", "Home")&lt;/li&gt; 
                    &lt;/ul&gt; 
                    <span style="background-color:yellow">@Html.Partial("_LoginPartial")</span> 
                &lt;/div&gt; 
            &lt;/div&gt; 
        &lt;/div&gt; 
        &lt;div class="container body-content"&gt; 
            @RenderBody() 
            &lt;hr /&gt; 
            &lt;footer&gt; 
                &lt;p&gt;&amp;copy; @DateTime.Now.Year - My ASP.NET Application&lt;/p&gt; 
            &lt;/footer&gt; 
        &lt;/div&gt; 
        @Scripts.Render("~/bundles/jquery") 
        @Scripts.Render("~/bundles/bootstrap") 
        @RenderSection("scripts", required: false) 
    &lt;/body&gt; 
    &lt;/html&gt;
</pre>

## <a name="next-steps"></a><span data-ttu-id="07284-115">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="07284-115">Next steps</span></span>
- [<span data-ttu-id="07284-116">Saiba mais sobre o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="07284-116">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/) 

