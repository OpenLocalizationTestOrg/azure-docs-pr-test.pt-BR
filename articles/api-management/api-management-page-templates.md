---
title: modelos de aaaPage no gerenciamento de API do Azure | Microsoft Docs
description: "Saiba como toocustomize Olá conteúdo das páginas de portal do desenvolvedor usando um conjunto de modelos no gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: e57df269-1019-4b74-b74d-53155b809d59
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 84bd971ad4bcacfdd36c2ebbe05b16063f2a547b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="page-templates-in-azure-api-management"></a><span data-ttu-id="401be-103">Modelos de página no Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="401be-103">Page templates in Azure API Management</span></span>
<span data-ttu-id="401be-104">Gerenciamento de API do Azure fornece que Olá conteúdo de saudação toocustomize capacidade de páginas de portal do desenvolvedor usando um conjunto de modelos que configurar seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="401be-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="401be-105">Usando [DotLiquid](http://dotliquidmarkup.org/) sintaxe e hello editor de sua escolha, como [DotLiquid para Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), e um conjunto fornecido de localizadas [recursos de cadeia de caracteres](api-management-template-resources.md#strings), [ Recursos de glifo](api-management-template-resources.md#glyphs), e [página controles](api-management-page-controls.md), você tiver um grande flexibilidade tooconfigure Olá conteúdo das páginas hello como desejar usar esses modelos.</span><span class="sxs-lookup"><span data-stu-id="401be-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="401be-106">Olá modelos nesta seção permitem a você toocustomize conteúdo Olá Olá entrar, sinal de backup e página não encontrada páginas no portal do desenvolvedor hello.</span><span class="sxs-lookup"><span data-stu-id="401be-106">hello templates in this section allow you toocustomize hello content of hello sign in, sign up, and page not found pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="401be-107">Entrar</span><span class="sxs-lookup"><span data-stu-id="401be-107">Sign in</span></span>](#SignIn)  
  
-   [<span data-ttu-id="401be-108">Inscrever-se</span><span class="sxs-lookup"><span data-stu-id="401be-108">Sign up</span></span>](#SignUp)  
  
-   [<span data-ttu-id="401be-109">Página não encontrada</span><span class="sxs-lookup"><span data-stu-id="401be-109">Page not found</span></span>](#PageNotFound)  
  
> [!NOTE]
>  <span data-ttu-id="401be-110">Modelos de padrão de exemplo estão incluídos no hello documentação a seguir, mas são toochange assunto devido a melhorias toocontinuous.</span><span class="sxs-lookup"><span data-stu-id="401be-110">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="401be-111">Você pode exibir modelos do saudação padrão em tempo real no portal do desenvolvedor Olá navegando modelos individuais toohello desejado.</span><span class="sxs-lookup"><span data-stu-id="401be-111">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="401be-112">Para obter mais informações sobre como trabalhar com modelos, consulte [como toocustomize Olá portal do desenvolvedor do gerenciamento de API usando modelos](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="401be-112">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="401be-113"><a name="SignIn"></a> Entrar</span><span class="sxs-lookup"><span data-stu-id="401be-113"><a name="SignIn"></a> Sign in</span></span>  
 <span data-ttu-id="401be-114">Olá **entrar** modelo permite toocustomize Olá logon na página no portal do desenvolvedor hello.</span><span class="sxs-lookup"><span data-stu-id="401be-114">hello **sign in** template allows you toocustomize hello sign in page in hello developer portal.</span></span>  
  
 <span data-ttu-id="401be-115">![Página de logon](./media/api-management-page-templates/APIM-Sign-In-Page-Developer-Portal-Templates.png "Modelos do portal do desenvolvedor para a página de entrada do APIM")</span><span class="sxs-lookup"><span data-stu-id="401be-115">![Sign In Page](./media/api-management-page-templates/APIM-Sign-In-Page-Developer-Portal-Templates.png "APIM Sign In Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="401be-116">Modelo padrão</span><span class="sxs-lookup"><span data-stu-id="401be-116">Default template</span></span>  
  
```xml  
<h2 class="text-center">{% localized "SigninStrings|WebAuthenticationSigninTitle" %}</h2>  
{% if registrationEnabled == true %}  
<p class="text-center">{% localized "SigninStrings|WebAuthenticationNotAMember" %}</p>  
{% endif %}  
  
<div class="row center-block ap-idp-container">  
  <div class="col-md-6">  
    {% if registrationEnabled == true %}  
        <p>{% localized "SigninStrings|WebAuthenticationSigininWithPassword" %}</p>  
    <basic-SignIn></basic-SignIn>  
    {% endif %}  
  </div>  
  
    {% if registrationEnabled != true and providers.size == 0 %}  
        {% localized "ProviderInfoStrings|TextboxExternalIdentitiesDisabled" %}  
  {% else %}  
        {% if providers.size > 0 %}  
      <div class="col-md-6">  
            <div class="providers-list">  
                <p class="text-left">  
                {% if registrationEnabled == true %}  
                    {% localized "ProviderInfoStrings|TextboxExternalIdentitiesSigninInvitation" %}  
                {% else %}  
                    {% localized "ProviderInfoStrings|TextboxExternalIdentitiesSigninInvitationPrimary" %}  
                {% endif %}  
                </p>  
        <providers></providers>  
            </div>  
    </div>  
        {% endif %}  
    {% endif %}  
  
  {% if userRegistrationTermsEnabled == true %}  
    <div class="col-md-6">  
        <div id="terms" class="modal" role="dialog" tabindex="-1">  
            <div class="modal-dialog">  
                <div class="modal-content">  
                    <div class="modal-header">  
                        <h4 class="modal-title">{% localized "SigninResources|DialogHeadingTermsOfUse" %}</h4>  
                    </div>  
                    <div class="modal-body break-all">{{userRegistrationTerms}}</div>  
                    <div class="modal-footer">  
                        <button type="button" class="btn btn-default" data-dismiss="modal">{% localized "CommonStrings|ButtonLabelClose" %}</button>  
                    </div>  
                </div>  
            </div>  
        </div>  
        <p>{% localized "SigninResources|TextblockUserRegistrationTermsProvided" %}</p>  
    </div>  
    {% endif %}  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="401be-117">Controles</span><span class="sxs-lookup"><span data-stu-id="401be-117">Controls</span></span>  
 <span data-ttu-id="401be-118">Esse modelo pode usar a seguinte Olá [página controles](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="401be-118">This template may  use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="401be-119">basic-signin</span><span class="sxs-lookup"><span data-stu-id="401be-119">basic-signin</span></span>](api-management-page-controls.md#basic-signin)  
  
-   [<span data-ttu-id="401be-120">providers</span><span class="sxs-lookup"><span data-stu-id="401be-120">providers</span></span>](api-management-page-controls.md#providers)  
  
### <a name="data-model"></a><span data-ttu-id="401be-121">Modelo de dados</span><span class="sxs-lookup"><span data-stu-id="401be-121">Data model</span></span>  
 <span data-ttu-id="401be-122">Entidade [Entrada do usuário](api-management-template-data-model-reference.md#UseSignIn).</span><span class="sxs-lookup"><span data-stu-id="401be-122">[User sign in](api-management-template-data-model-reference.md#UseSignIn) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="401be-123">Amostra de dados do modelo</span><span class="sxs-lookup"><span data-stu-id="401be-123">Sample template data</span></span>  
  
```json  
{  
    "Email": null,  
    "Password": null,  
    "ReturnUrl": null,  
    "RememberMe": false,  
    "RegistrationEnabled": true,  
    "DelegationEnabled": false,  
    "DelegationUrl": null,  
    "SsoSignUpUrl": null,  
    "AuxServiceUrl": "https://manage.windowsazure.com/#Workspaces/ApiManagementExtension/service/contoso5/dashboard",  
    "Providers": [  
        {  
            "Properties": {  
                "AuthenticationType": "Aad",  
                "Caption": "Azure Active Directory"  
            },  
            "AuthenticationType": "Aad",  
            "Caption": "Azure Active Directory"  
        }  
    ],  
    "UserRegistrationTerms": null,  
    "UserRegistrationTermsEnabled": false  
}  
```  
  
##  <span data-ttu-id="401be-124"><a name="SignUp"></a> Inscrever-se</span><span class="sxs-lookup"><span data-stu-id="401be-124"><a name="SignUp"></a> Sign up</span></span>  
 <span data-ttu-id="401be-125">Olá **inscrever** modelo permite toocustomize Olá página de inscrição no portal do desenvolvedor hello.</span><span class="sxs-lookup"><span data-stu-id="401be-125">hello **sign up** template allows you toocustomize hello sign up page in hello developer portal.</span></span>  
  
 <span data-ttu-id="401be-126">![Página de inscrição](./media/api-management-page-templates/APIM-Sign-Up-Page-Developer-Portal-Templates.png "Modelos do portal do desenvolvedor para a página de inscrição do APIM")</span><span class="sxs-lookup"><span data-stu-id="401be-126">![Sign Up Page](./media/api-management-page-templates/APIM-Sign-Up-Page-Developer-Portal-Templates.png "APIM Sign Up Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="401be-127">Modelo padrão</span><span class="sxs-lookup"><span data-stu-id="401be-127">Default template</span></span>  
  
```xml  
<h2 class="text-center">{% localized "SignupStrings|PageTitleSignup" %}</h2>  
<p class="text-center">  
  {% localized "SignupStrings|WebAuthenticationAlreadyAMember" %} <a href="/signin">{% localized "SignupStrings|WebAuthenticationSigninNow" %}</a>  
</p>  
  
<div class="row center-block ap-idp-container">  
  <div class="col-md-6">  
    <p>{% localized "SignupStrings|WebAuthenticationCreateNewAccount" %}</p>  
    <sign-up></sign-up>  
  </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="401be-128">Controles</span><span class="sxs-lookup"><span data-stu-id="401be-128">Controls</span></span>  
 <span data-ttu-id="401be-129">Esse modelo pode usar a seguinte Olá [página controles](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="401be-129">This template may  use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="401be-130">sign-up</span><span class="sxs-lookup"><span data-stu-id="401be-130">sign-up</span></span>](api-management-page-controls.md#sign-up)  
  
### <a name="data-model"></a><span data-ttu-id="401be-131">Modelo de dados</span><span class="sxs-lookup"><span data-stu-id="401be-131">Data model</span></span>  
 <span data-ttu-id="401be-132">Entidade [Inscrição do usuário](api-management-template-data-model-reference.md#UserSignUp).</span><span class="sxs-lookup"><span data-stu-id="401be-132">[User sign up](api-management-template-data-model-reference.md#UserSignUp) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="401be-133">Amostra de dados do modelo</span><span class="sxs-lookup"><span data-stu-id="401be-133">Sample template data</span></span>  
  
```json  
{  
    "PasswordConfirm": null,  
    "Password": null,  
    "PasswordVerdictLevel": 0,  
    "UserRegistrationTerms": null,  
    "UserRegistrationTermsOptions": 0,  
    "ConsentAccepted": false,  
    "Email": null,  
    "FirstName": null,  
    "LastName": null,  
    "UserData": null,  
    "NameIdentifier": null,  
    "ProviderName": null  
}  
```  
  
##  <span data-ttu-id="401be-134"><a name="PageNotFound"></a> Página não encontrada</span><span class="sxs-lookup"><span data-stu-id="401be-134"><a name="PageNotFound"></a> Page not found</span></span>  
 <span data-ttu-id="401be-135">Olá **página não encontrada** modelo permite que você toocustomize Olá página não encontrada página no portal do desenvolvedor hello.</span><span class="sxs-lookup"><span data-stu-id="401be-135">hello **page not found** template allows you toocustomize hello page not found page in hello developer portal.</span></span>  
  
 <span data-ttu-id="401be-136">![Página não encontrada](./media/api-management-page-templates/APIM-Not-Found-Page-Developer-Portal-Templates.png "Modelos do portal do desenvolvedor para a página “não encontrada” do APIM")</span><span class="sxs-lookup"><span data-stu-id="401be-136">![Not Found Page](./media/api-management-page-templates/APIM-Not-Found-Page-Developer-Portal-Templates.png "APIM Not Found Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="401be-137">Modelo padrão</span><span class="sxs-lookup"><span data-stu-id="401be-137">Default template</span></span>  
  
```xml  
<h2>{% localized "NotFoundStrings|PageTitleNotFound" %}</h2>  
  
<h3>{% localized "NotFoundStrings|TitlePotentialCause" %}</h3>  
<ul>  
  <li>{% localized "NotFoundStrings|TextblockPotentialCauseOldLink" %}</li>  
  <li>{% localized "NotFoundStrings|TextblockPotentialCauseMisspelledUrl" %}</li>  
</ul>  
  
<h3>{% localized "NotFoundStrings|TitlePotentialSolution" %}</h3>  
<ul>  
  <li>{% localized "NotFoundStrings|TextblockPotentialSolutionRetype" %}</li>  
  <li>  
    {% capture textPotentialSolutionStartOver %}{% localized "NotFoundStrings|TextblockPotentialSolutionStartOver" %}{% endcapture %}  
    {% capture homeLink %}<a href="/">{% localized "NotFoundStrings|LinkLabelHomePage" %}</a>{% endcapture %}  
    {% assign replaceString = '{0}' %}  
  
    {{ textPotentialSolutionStartOver | replace : replaceString, homeLink }}  
  </li>  
</ul>  
  
<p>  
  {% capture textReportProblem %}{% localized "NotFoundStrings|TextReportProblem" %}{% endcapture %}  
  {% capture emailLink %}<a href="mailto:apimgmt@microsoft.com" target="_self" title="API Management Support">{% localized "NotFoundStrings|LinkLabelSendUsEmail" %}</a>{% endcapture %}  
  {% assign replaceString = '{0}' %}  
  
  {{ textReportProblem | replace : replaceString, emailLink }}  
</p>  
```  
  
### <a name="controls"></a><span data-ttu-id="401be-138">Controles</span><span class="sxs-lookup"><span data-stu-id="401be-138">Controls</span></span>  
 <span data-ttu-id="401be-139">Este modelo pode não usar nenhum [controle de página](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="401be-139">This template may  not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="401be-140">Modelo de dados</span><span class="sxs-lookup"><span data-stu-id="401be-140">Data model</span></span>  
  
|<span data-ttu-id="401be-141">Propriedade</span><span class="sxs-lookup"><span data-stu-id="401be-141">Property</span></span>|<span data-ttu-id="401be-142">Tipo</span><span class="sxs-lookup"><span data-stu-id="401be-142">Type</span></span>|<span data-ttu-id="401be-143">Descrição</span><span class="sxs-lookup"><span data-stu-id="401be-143">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="401be-144">referenceCode</span><span class="sxs-lookup"><span data-stu-id="401be-144">referenceCode</span></span>|<span data-ttu-id="401be-145">string</span><span class="sxs-lookup"><span data-stu-id="401be-145">string</span></span>|<span data-ttu-id="401be-146">Código gerado se esta página foi exibida como resultado de saudação de um erro interno.</span><span class="sxs-lookup"><span data-stu-id="401be-146">Code generated if this page was displayed as hello result of an internal error.</span></span>|  
|<span data-ttu-id="401be-147">errorCode</span><span class="sxs-lookup"><span data-stu-id="401be-147">errorCode</span></span>|<span data-ttu-id="401be-148">string</span><span class="sxs-lookup"><span data-stu-id="401be-148">string</span></span>|<span data-ttu-id="401be-149">Código gerado se esta página foi exibida como resultado de saudação de um erro interno.</span><span class="sxs-lookup"><span data-stu-id="401be-149">Code generated if this page was displayed as hello result of an internal error.</span></span>|  
|<span data-ttu-id="401be-150">emailBody</span><span class="sxs-lookup"><span data-stu-id="401be-150">emailBody</span></span>|<span data-ttu-id="401be-151">string</span><span class="sxs-lookup"><span data-stu-id="401be-151">string</span></span>|<span data-ttu-id="401be-152">Gerada se essa página foi exibida como resultado de saudação de um erro interno de corpo do email.</span><span class="sxs-lookup"><span data-stu-id="401be-152">Email body generated if this page was displayed as hello result of an internal error.</span></span>|  
|<span data-ttu-id="401be-153">requestedUrl</span><span class="sxs-lookup"><span data-stu-id="401be-153">requestedUrl</span></span>|<span data-ttu-id="401be-154">string</span><span class="sxs-lookup"><span data-stu-id="401be-154">string</span></span>|<span data-ttu-id="401be-155">URL de saudação solicitada quando Olá página não foi encontrada.</span><span class="sxs-lookup"><span data-stu-id="401be-155">hello URL requested when hello page was not found.</span></span>|  
|<span data-ttu-id="401be-156">referrerUrl</span><span class="sxs-lookup"><span data-stu-id="401be-156">referrerUrl</span></span>|<span data-ttu-id="401be-157">string</span><span class="sxs-lookup"><span data-stu-id="401be-157">string</span></span>|<span data-ttu-id="401be-158">Olá referenciador URL toohello URL solicitado.</span><span class="sxs-lookup"><span data-stu-id="401be-158">hello referrer URL toohello requested URL.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="401be-159">Amostra de dados do modelo</span><span class="sxs-lookup"><span data-stu-id="401be-159">Sample template data</span></span>  
  
```json  
{  
    "referenceCode": null,  
    "errorCode": null,  
    "emailBody": null,  
    "requestedUrl": "https://contoso5.portal.azure-api.net:443/NotFoundPage?startEditTemplate=NotFoundPage",  
    "referrerUrl": "https://contoso5.portal.azure-api.net/signup?startEditTemplate=SignUpTemplate"  
}  
```

## <a name="next-steps"></a><span data-ttu-id="401be-160">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="401be-160">Next steps</span></span>
<span data-ttu-id="401be-161">Para obter mais informações sobre como trabalhar com modelos, consulte [como toocustomize Olá portal do desenvolvedor do gerenciamento de API usando modelos](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="401be-161">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
