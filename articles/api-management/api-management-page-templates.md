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
# <a name="page-templates-in-azure-api-management"></a>Modelos de página no Gerenciamento de API do Azure
Gerenciamento de API do Azure fornece que Olá conteúdo de saudação toocustomize capacidade de páginas de portal do desenvolvedor usando um conjunto de modelos que configurar seu conteúdo. Usando [DotLiquid](http://dotliquidmarkup.org/) sintaxe e hello editor de sua escolha, como [DotLiquid para Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), e um conjunto fornecido de localizadas [recursos de cadeia de caracteres](api-management-template-resources.md#strings), [ Recursos de glifo](api-management-template-resources.md#glyphs), e [página controles](api-management-page-controls.md), você tiver um grande flexibilidade tooconfigure Olá conteúdo das páginas hello como desejar usar esses modelos.  
  
 Olá modelos nesta seção permitem a você toocustomize conteúdo Olá Olá entrar, sinal de backup e página não encontrada páginas no portal do desenvolvedor hello.  
  
-   [Entrar](#SignIn)  
  
-   [Inscrever-se](#SignUp)  
  
-   [Página não encontrada](#PageNotFound)  
  
> [!NOTE]
>  Modelos de padrão de exemplo estão incluídos no hello documentação a seguir, mas são toochange assunto devido a melhorias toocontinuous. Você pode exibir modelos do saudação padrão em tempo real no portal do desenvolvedor Olá navegando modelos individuais toohello desejado. Para obter mais informações sobre como trabalhar com modelos, consulte [como toocustomize Olá portal do desenvolvedor do gerenciamento de API usando modelos](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).  
  
##  <a name="SignIn"></a> Entrar  
 Olá **entrar** modelo permite toocustomize Olá logon na página no portal do desenvolvedor hello.  
  
 ![Página de logon](./media/api-management-page-templates/APIM-Sign-In-Page-Developer-Portal-Templates.png "Modelos do portal do desenvolvedor para a página de entrada do APIM")  
  
### <a name="default-template"></a>Modelo padrão  
  
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
  
### <a name="controls"></a>Controles  
 Esse modelo pode usar a seguinte Olá [página controles](api-management-page-controls.md).  
  
-   [basic-signin](api-management-page-controls.md#basic-signin)  
  
-   [providers](api-management-page-controls.md#providers)  
  
### <a name="data-model"></a>Modelo de dados  
 Entidade [Entrada do usuário](api-management-template-data-model-reference.md#UseSignIn).  
  
### <a name="sample-template-data"></a>Amostra de dados do modelo  
  
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
  
##  <a name="SignUp"></a> Inscrever-se  
 Olá **inscrever** modelo permite toocustomize Olá página de inscrição no portal do desenvolvedor hello.  
  
 ![Página de inscrição](./media/api-management-page-templates/APIM-Sign-Up-Page-Developer-Portal-Templates.png "Modelos do portal do desenvolvedor para a página de inscrição do APIM")  
  
### <a name="default-template"></a>Modelo padrão  
  
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
  
### <a name="controls"></a>Controles  
 Esse modelo pode usar a seguinte Olá [página controles](api-management-page-controls.md).  
  
-   [sign-up](api-management-page-controls.md#sign-up)  
  
### <a name="data-model"></a>Modelo de dados  
 Entidade [Inscrição do usuário](api-management-template-data-model-reference.md#UserSignUp).  
  
### <a name="sample-template-data"></a>Amostra de dados do modelo  
  
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
  
##  <a name="PageNotFound"></a> Página não encontrada  
 Olá **página não encontrada** modelo permite que você toocustomize Olá página não encontrada página no portal do desenvolvedor hello.  
  
 ![Página não encontrada](./media/api-management-page-templates/APIM-Not-Found-Page-Developer-Portal-Templates.png "Modelos do portal do desenvolvedor para a página “não encontrada” do APIM")  
  
### <a name="default-template"></a>Modelo padrão  
  
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
  
### <a name="controls"></a>Controles  
 Este modelo pode não usar nenhum [controle de página](api-management-page-controls.md).  
  
### <a name="data-model"></a>Modelo de dados  
  
|Propriedade|Tipo|Descrição|  
|--------------|----------|-----------------|  
|referenceCode|string|Código gerado se esta página foi exibida como resultado de saudação de um erro interno.|  
|errorCode|string|Código gerado se esta página foi exibida como resultado de saudação de um erro interno.|  
|emailBody|string|Gerada se essa página foi exibida como resultado de saudação de um erro interno de corpo do email.|  
|requestedUrl|string|URL de saudação solicitada quando Olá página não foi encontrada.|  
|referrerUrl|string|Olá referenciador URL toohello URL solicitado.|  
  
### <a name="sample-template-data"></a>Amostra de dados do modelo  
  
```json  
{  
    "referenceCode": null,  
    "errorCode": null,  
    "emailBody": null,  
    "requestedUrl": "https://contoso5.portal.azure-api.net:443/NotFoundPage?startEditTemplate=NotFoundPage",  
    "referrerUrl": "https://contoso5.portal.azure-api.net/signup?startEditTemplate=SignUpTemplate"  
}  
```

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre como trabalhar com modelos, consulte [como toocustomize Olá portal do desenvolvedor do gerenciamento de API usando modelos](api-management-developer-portal-templates.md).
