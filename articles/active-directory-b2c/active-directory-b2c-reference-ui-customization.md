---
title: "Personalização da UI (interface do usuário) – Azure AD B2C | Microsoft Docs"
description: "Um tópico sobre os recursos de personalização de interface do usuário Olá usuário no Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 99f5a391-5328-471d-a15c-a2fafafe233d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 04f8c5f1277f8d4409cd10971d22a0ebd2024785
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-customize-hello-azure-ad-b2c-user-interface-ui"></a><span data-ttu-id="cf860-103">B2C de diretório ativo do Azure: Personalizar a interface do usuário de saudação do Azure AD B2C (IU)</span><span class="sxs-lookup"><span data-stu-id="cf860-103">Azure Active Directory B2C: Customize hello Azure AD B2C user interface (UI)</span></span>

<span data-ttu-id="cf860-104">A experiência do usuário é fundamental em um aplicativo voltado ao cliente.</span><span class="sxs-lookup"><span data-stu-id="cf860-104">User experience is paramount in a customer facing application.</span></span>  <span data-ttu-id="cf860-105">Aumentar seu cliente base ao criar experiências de usuário com hello aparência de sua marca.</span><span class="sxs-lookup"><span data-stu-id="cf860-105">Grow your customer base by crafting user experiences with hello look and feel of your brand.</span></span> <span data-ttu-id="cf860-106">O Azure AD B2C (Azure Active Directory B2C) permite personalizar as páginas de inscrição, entrada, edição de perfil e redefinição de senha com controle perfeito.</span><span class="sxs-lookup"><span data-stu-id="cf860-106">Azure Active Directory B2C (Azure AD B2C) lets you customize sign-up, sign-in, profile editing, and password reset pages with pixel-perfect control.</span></span>

> [!NOTE]
> <span data-ttu-id="cf860-107">recurso de personalização do Hello página da interface do usuário descrito neste artigo não se aplica toohello única política, sua página de redefinição de senha que o acompanha e emails de verificação.</span><span class="sxs-lookup"><span data-stu-id="cf860-107">hello page UI customization feature described in this article does not apply toohello sign-in only policy, its accompanying password reset page, and verification emails.</span></span>  <span data-ttu-id="cf860-108">Esses recursos usam Olá [marca do recurso da empresa](../active-directory/active-directory-add-company-branding.md) em vez disso.</span><span class="sxs-lookup"><span data-stu-id="cf860-108">These features use hello [company branding feature](../active-directory/active-directory-add-company-branding.md) instead.</span></span>
>

<span data-ttu-id="cf860-109">Este artigo aborda Olá seguintes tópicos:</span><span class="sxs-lookup"><span data-stu-id="cf860-109">This article covers hello following topics:</span></span>

* <span data-ttu-id="cf860-110">recurso de personalização da interface do usuário Olá página.</span><span class="sxs-lookup"><span data-stu-id="cf860-110">hello page UI customization feature.</span></span>
* <span data-ttu-id="cf860-111">Uma ferramenta para carregar tooAzure conteúdo HTML armazenamento de Blob para uso com o recurso de personalização do hello página da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="cf860-111">A tool for uploading HTML content tooAzure Blob Storage for use with hello page UI customization feature.</span></span>
* <span data-ttu-id="cf860-112">Olá elementos de interface do usuário usados pelo Azure AD B2C que você pode personalizar usando folhas de estilo em cascata (CSS).</span><span class="sxs-lookup"><span data-stu-id="cf860-112">hello UI elements used by Azure AD B2C that you can customize using Cascading Style Sheets (CSS).</span></span>
* <span data-ttu-id="cf860-113">Práticas recomendadas ao exercitar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="cf860-113">Best practices when exercising this feature.</span></span>

## <a name="hello-page-ui-customization-feature"></a><span data-ttu-id="cf860-114">recurso de personalização de interface do usuário de página Olá</span><span class="sxs-lookup"><span data-stu-id="cf860-114">hello page UI customization feature</span></span>

<span data-ttu-id="cf860-115">Você pode personalizar Olá aparência de senha de inscrição, entrar, cliente redefinição e páginas de edição de perfil (configurando [políticas](active-directory-b2c-reference-policies.md)).</span><span class="sxs-lookup"><span data-stu-id="cf860-115">You can customize hello look and feel of customer sign-up, sign-in, password reset, and profile-editing pages (by configuring [policies](active-directory-b2c-reference-policies.md)).</span></span> <span data-ttu-id="cf860-116">Seus clientes terão uma experiência integrada ao navegar entre seu aplicativo e as páginas atendidas pelo Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="cf860-116">Your customers get a seamless experience when navigating between your application and pages served by Azure AD B2C.</span></span>

<span data-ttu-id="cf860-117">Ao contrário de outros serviços em que opções de interface do usuário, B2C do Azure AD usa um simples e modernos abordagem tooUI personalização.</span><span class="sxs-lookup"><span data-stu-id="cf860-117">Unlike other services where UI options, Azure AD B2C uses a simple and modern approach tooUI customization.</span></span>

<span data-ttu-id="cf860-118">É assim que ela funciona: o Azure AD B2C executa o código no navegador do cliente e usa uma abordagem moderna chamada [CORS (Compartilhamento de Recursos entre Origens)](http://www.w3.org/TR/cors/).</span><span class="sxs-lookup"><span data-stu-id="cf860-118">Here's how it works: Azure AD B2C runs code in your customer's browser and uses a modern approach called [Cross-Origin Resource Sharing (CORS)](http://www.w3.org/TR/cors/).</span></span>  <span data-ttu-id="cf860-119">Em tempo de execução, o conteúdo é carregado de uma URL que você especifica em uma política.</span><span class="sxs-lookup"><span data-stu-id="cf860-119">At run-time, content is loaded from a URL that you specify in a policy.</span></span> <span data-ttu-id="cf860-120">Você pode especificar URLs diferentes para diferentes páginas.</span><span class="sxs-lookup"><span data-stu-id="cf860-120">You can specify different URLs for different pages.</span></span> <span data-ttu-id="cf860-121">Depois de carregado do seu URL de conteúdo é mesclado com um fragmento HTML inserido a partir do Azure AD B2C, página Olá é exibida tooyour cliente.</span><span class="sxs-lookup"><span data-stu-id="cf860-121">After content loaded from your URL is merged with an HTML fragment inserted from Azure AD B2C, hello page is displayed tooyour customer.</span></span> <span data-ttu-id="cf860-122">Você só precisa toodo é:</span><span class="sxs-lookup"><span data-stu-id="cf860-122">All you need toodo is:</span></span>

1. <span data-ttu-id="cf860-123">Criar conteúdo com vazio do HTML5 bem formado `<div id="api"></div>` elemento localizado em algum lugar no hello `<body>`.</span><span class="sxs-lookup"><span data-stu-id="cf860-123">Create well-formed HTML5 content with an empty `<div id="api"></div>` element located somewhere in hello `<body>`.</span></span> <span data-ttu-id="cf860-124">Este marcas de elemento onde hello Azure AD B2C conteúdo é inserido.</span><span class="sxs-lookup"><span data-stu-id="cf860-124">This element marks where hello Azure AD B2C content is inserted.</span></span>
1. <span data-ttu-id="cf860-125">Hospede seu conteúdo em um ponto de extremidade HTTPS (com CORS permitido).</span><span class="sxs-lookup"><span data-stu-id="cf860-125">Host your content on an HTTPS endpoint (with CORS allowed).</span></span> <span data-ttu-id="cf860-126">Observe que os métodos de solicitação GET e OPTIONS precisam ser habilitados configurar o CORS.</span><span class="sxs-lookup"><span data-stu-id="cf860-126">Note both GET and OPTIONS request methods must be enabled when configuring CORS.</span></span>
1. <span data-ttu-id="cf860-127">Use CSS toostyle Olá elementos da IU que insere B2C do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cf860-127">Use CSS toostyle hello UI elements that Azure AD B2C inserts.</span></span>

### <a name="a-basic-example-of-customized-html"></a><span data-ttu-id="cf860-128">Um exemplo básico de HTML personalizado</span><span class="sxs-lookup"><span data-stu-id="cf860-128">A basic example of customized HTML</span></span>

<span data-ttu-id="cf860-129">saudação de exemplo a seguir é conteúdo HTML mais básico Olá que você pode usar tootest esse recurso.</span><span class="sxs-lookup"><span data-stu-id="cf860-129">hello following example is hello most basic HTML content that you can use tootest this capability.</span></span> <span data-ttu-id="cf860-130">Saudação de uso [ferramenta auxiliar](active-directory-b2c-reference-ui-customization-helper-tool.md) tooupload e configurar esse conteúdo em seu armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="cf860-130">Use hello [helper tool](active-directory-b2c-reference-ui-customization-helper-tool.md) tooupload and configure this content on your Azure Blob storage.</span></span> <span data-ttu-id="cf860-131">Em seguida, você pode verificar Olá básica não estilizado botões e campos de formulário em cada página são exibidos e funcional.</span><span class="sxs-lookup"><span data-stu-id="cf860-131">You can then verify that hello basic, non-stylized buttons & form fields on each page are displayed and functional.</span></span>

```HTML
<!DOCTYPE html>
<html>
    <head>
        <title>!Add your title here!</title>
    </head>
    <body>
        <div id="api"></div>   <!-- Leave this element empty because Azure AD B2C will insert content here. -->
    </body>
</html>
```

## <a name="test-out-hello-ui-customization-feature"></a><span data-ttu-id="cf860-132">Testar o recurso de personalização da interface do usuário Olá</span><span class="sxs-lookup"><span data-stu-id="cf860-132">Test out hello UI customization feature</span></span>

<span data-ttu-id="cf860-133">Deseja tootry recurso de personalização da interface do usuário hello usando nosso conteúdo HTML e CSS do exemplo?</span><span class="sxs-lookup"><span data-stu-id="cf860-133">Want tootry out hello UI customization feature by using our sample HTML and CSS content?</span></span>  <span data-ttu-id="cf860-134">Fornecemos uma [ferramenta auxiliar](active-directory-b2c-reference-ui-customization-helper-tool.md) que carrega e configura o conteúdo de exemplo em seu armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="cf860-134">We've provided you [a helper tool](active-directory-b2c-reference-ui-customization-helper-tool.md) that uploads and configures sample content on your Azure Blob storage.</span></span>

> [!NOTE]
> <span data-ttu-id="cf860-135">Você pode hospedar o conteúdo da interface do usuário em qualquer lugar: em servidores Web, CDNs, AWS S3, sistemas de compartilhamento de arquivos etc. Desde que o conteúdo de saudação está hospedado em um ponto de extremidade HTTPS disponível publicamente com CORS habilitado, você está toogo BOM.</span><span class="sxs-lookup"><span data-stu-id="cf860-135">You can host your UI content anywhere: on web servers, CDNs, AWS S3, file sharing systems, etc. As long as hello content is hosted on a publicly available HTTPS endpoint with CORS enabled, you are good toogo.</span></span> <span data-ttu-id="cf860-136">Estamos usando o armazenamento de Blobs do Azure somente para fins ilustrativos.</span><span class="sxs-lookup"><span data-stu-id="cf860-136">We are using Azure Blob storage for illustrative purposes only.</span></span>
>

## <a name="hello-ui-fragments-embedded-by-azure-ad-b2c"></a><span data-ttu-id="cf860-137">Olá fragmentos de interface do usuário inseridos pelo Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="cf860-137">hello UI fragments embedded by Azure AD B2C</span></span>

<span data-ttu-id="cf860-138">Olá, seções a seguir listam os fragmentos de saudação HTML5 do Azure AD B2C mescla Olá `<div id="api"></div>` elemento localizado no seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="cf860-138">hello following sections list hello HTML5 fragments that Azure AD B2C merges into hello `<div id="api"></div>` element located in your content.</span></span> <span data-ttu-id="cf860-139">**Não insira esses fragmentos em seu conteúdo HTML 5.**</span><span class="sxs-lookup"><span data-stu-id="cf860-139">**Do not insert these fragments in your HTML 5 content.**</span></span> <span data-ttu-id="cf860-140">Olá serviço do Azure AD B2C insere em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="cf860-140">hello Azure AD B2C service inserts them in at run-time.</span></span> <span data-ttu-id="cf860-141">Use esses fragmentos como referência ao criar seu próprio CSS (folhas de estilos em cascata).</span><span class="sxs-lookup"><span data-stu-id="cf860-141">Use these fragments as a reference when designing your own Cascading Style Sheets (CSS).</span></span>

### <a name="fragment-inserted-into-hello-identity-provider-selection-page"></a><span data-ttu-id="cf860-142">Fragmento inserido hello "Página de seleção de provedor de identidade"</span><span class="sxs-lookup"><span data-stu-id="cf860-142">Fragment inserted into hello "Identity provider selection page"</span></span>

<span data-ttu-id="cf860-143">Esta página contém uma lista de provedores que Olá usuário podem escolher durante a inscrição ou entrada de identidade.</span><span class="sxs-lookup"><span data-stu-id="cf860-143">This page contains a list of identity providers that hello user can choose from during sign-up or sign-in.</span></span> <span data-ttu-id="cf860-144">Esses botões incluem provedores de identidade social como Facebook e Google+ ou então contas locais (baseadas em endereço de email ou nome de usuário).</span><span class="sxs-lookup"><span data-stu-id="cf860-144">These buttons include social identity providers such as Facebook and Google+, or local accounts (based on email address or user name).</span></span>

```HTML
<div id="api" data-name="IdpSelections">
    <div class="intro">
         <p>Sign up</p>
    </div>

    <div>
        <ul>
            <li>
                <button class="accountButton" id="FacebookExchange">Facebook</button>
            </li>
            <li>
                <button class="accountButton" id="GoogleExchange">Google+</button>
            </li>
            <li>
                <button class="accountButton" id="SignUpWithLogonEmailExchange">Email</button>
            </li>
        </ul>
    </div>
</div>
```

### <a name="fragment-inserted-into-hello-local-account-sign-up-page"></a><span data-ttu-id="cf860-145">Fragmento inserido hello "página de inscrição de conta Local"</span><span class="sxs-lookup"><span data-stu-id="cf860-145">Fragment inserted into hello "Local account sign-up page"</span></span>

<span data-ttu-id="cf860-146">Esta página contém um formulário para inscrições com conta local baseada em endereço de email ou nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="cf860-146">This page contains a form for local account sign-up based on an email address or a user name.</span></span> <span data-ttu-id="cf860-147">formulário de saudação pode conter controles de entrada diferentes, como a caixa de entrada de texto, caixa de entrada de senha, botão de opção, caixas de lista suspensa de seleção única e selecionar várias caixas de seleção.</span><span class="sxs-lookup"><span data-stu-id="cf860-147">hello form can contain different input controls such as text input box, password entry box, radio button, single-select drop-down boxes, and multi-select check boxes.</span></span>

```HTML
<div id="api" data-name="SelfAsserted">
    <div class="intro">
        <p>Create your account by providing hello following details</p>
    </div>

    <div id="attributeVerification">
        <div class="errorText" id="passwordEntryMismatch" style="display: none;">hello password entry fields do not match. Please enter hello same password in both fields and try again.</div>
        <div class="errorText" id="requiredFieldMissing" style="display: none;">A required field is missing. Please fill out all required fields and try again.</div>
        <div class="errorText" id="fieldIncorrect" style="display: none;">One or more fields are filled out incorrectly. Please check your entries and try again.</div>
        <div class="errorText" id="claimVerificationServerError" style="display: none;"></div>
        <div class="attr" id="attributeList">
            <ul>
                <li>
                    <div class="attrEntry validate">
                        <div>
                            <div class="verificationInfoText" id="email_intro" style="display: inline;">Verification is necessary. Please click Send button.</div>
                            <div class="verificationInfoText" id="email_info" style="display:none">Verification code has been sent tooyour inbox. Please copy it toohello input box below.</div>
                            <div class="verificationSuccessText" id="email_success" style="display:none">E-mail address verified. You can now continue.</div>
                            <div class="verificationErrorText" id="email_fail_retry" style="display:none">Incorrect code, try again.</div>
                            <div class="verificationErrorText" id="email_fail_no_retry" style="display:none">Exceeded number of retries you need toosend new code.</div>
                            <div class="verificationErrorText" id="email_fail_server" style="display:none">Server error, please try again</div>
                            <div class="verificationErrorText" id="email_incorrect_format" style="display:none">Incorect format.</div>
                        </div>

                    <div class="helpText show">This information is required</div>
                        <label>Email</label>
                        <input id="email" class="textInput" type="text" placeholder="Email" required="" autofocus=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Email address that can be used toocontact you.');" class="tiny">What is this?</a>

                    <div class="buttons verify" claim_id="email">
                        <div id="email_ver_wait" class="working" style="display: none;"></div>
                            <label id="email_ver_input_label" for="email_ver_input" style="display: none;">Verification code</label>
                            <input id="email_ver_input" type="text" placeholder="Verification code" style="display:none">
                            <button id="email_ver_but_send" class="sendButton" type="button" style="display: inline;">Send verification code</button>
                            <button id="email_ver_but_verify" class="verifyButton" type="button" style="display:none">Verify code</button>
                            <button id="email_ver_but_resend" class="sendButton" type="button" style="display:none">Send new code</button>
                            <button id="email_ver_but_edit" class="editButton" type="button" style="display:none">Change e-mail</button>
                            <button id="email_ver_but_default" class="defaultButton" type="button" style="display:none">Default</button>
                        </div>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText">8-16 characters, containing 3 out of 4 of hello following: Lowercase characters, uppercase characters, digits (0-9), and one or more of hello following symbols: @ # $ % ^ &amp; * - _ + = [ ] { } | \ : ' , ? / ` ~ " ( ) ; .This information is required</div>
                        <label>Enter password</label>
                        <input id="password" class="textInput" type="password" placeholder="Enter password" pattern="^((?=.*[a-z])(?=.*[A-Z])(?=.*\d)|(?=.*[a-z])(?=.*[A-Z])(?=.*[^A-Za-z0-9])|(?=.*[a-z])(?=.*\d)(?=.*[^A-Za-z0-9])|(?=.*[A-Z])(?=.*\d)(?=.*[^A-Za-z0-9]))([A-Za-z\d@#$%^&amp;*\-_+=[\]{}|\\:',?/`~&quot;();!]|\.(?!@)){8,16}$" title="8-16 characters, containing 3 out of 4 of hello following: Lowercase characters, uppercase characters, digits (0-9), and one or more of hello following symbols: @ # $ % ^ &amp; * - _ + = [ ] { } | \ : ' , ? / ` ~ &quot; ( ) ; ." required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Enter password');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"> This information is required</div>
                        <label>Reenter password</label>
                        <input id="reenterPassword" class="textInput" type="password" placeholder="Reenter password" pattern="^((?=.*[a-z])(?=.*[A-Z])(?=.*\d)|(?=.*[a-z])(?=.*[A-Z])(?=.*[^A-Za-z0-9])|(?=.*[a-z])(?=.*\d)(?=.*[^A-Za-z0-9])|(?=.*[A-Z])(?=.*\d)(?=.*[^A-Za-z0-9]))([A-Za-z\d@#$%^&amp;*\-_+=[\]{}|\\:',?/`~&quot;();!]|\.(?!@)){8,16}$" title=" " required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Reenter password');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText">This information is required</div>
                        <label>Name</label>
                        <input id="displayName" class="textInput" type="text" placeholder="Name" required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Your display name.');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"></div>
                        <label>Gender</label>
                        <input id="extension_Gender_F" name="extension_Gender" type="radio" value="F" autofocus="">
                        <label for="extension_Gender_F">Female</label>
                        <input id="extension_Gender_M" name="extension_Gender" type="radio" value="M">
                        <label for="extension_Gender_M">Male</label>
                        <a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"></div>
                        <label>Loyalty number</label>
                        <input id="extension_MemNum" class="textInput" type="text" placeholder="Loyalty number"><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Membership number');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"></div>
                        <label>State</label>
                        <select class="dropdown_single" id="state">
                            <option style="display:none" disabled="disabled" value="placeholder" selected="">State</option>
                            <option value="WA">Washington</option>
                            <option value="NY">New York</option>
                            <option value="CA">California</option>
                        </select>
                        <a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Your residential state or province.');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText">This information is required</div>
                        <label>Zip code</label>
                        <input id="postalCode" class="textInput" type="text" placeholder="Zip code" required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('hello postal code of your address.');" class="tiny">What is this?</a>
                    </div>
                </li>
            </ul>
        </div>
        <div class="buttons"> <button id="continue" disabled="">Create</button> <button id="cancel">Cancel</button></div>
    </div>
    <div class="verifying-modal">
        <div class="preloader"> <img src="https://login.microsoftonline.com/static/img/win8loader.gif" alt="Please wait"></div>
        <div id="verifying_blurb"></div>
    </div>
</div>
```

### <a name="fragment-inserted-into-hello-social-account-sign-up-page"></a><span data-ttu-id="cf860-148">Fragmento inseridos hello "" Social conta página de inscrição"</span><span class="sxs-lookup"><span data-stu-id="cf860-148">Fragment inserted into hello ""Social account sign-up page"</span></span>

<span data-ttu-id="cf860-149">Esta página pode aparecer ao se inscrever usando uma conta existente de um provedor de identidade social, como o Facebook ou Google+.</span><span class="sxs-lookup"><span data-stu-id="cf860-149">This page may appear when signing up using an existing account from a social identity provider such as Facebook or Google+.</span></span>  <span data-ttu-id="cf860-150">Ele é usado quando informações adicionais devem ser coletadas do usuário final de saudação usando um formulário de inscrição.</span><span class="sxs-lookup"><span data-stu-id="cf860-150">It is used when additional information must be collected from hello end user using a sign-up form.</span></span> <span data-ttu-id="cf860-151">Esta página é semelhante toohello conta local inscrição página (mostrada na seção anterior Olá) com exceção de saudação de campos de entrada de senha hello.</span><span class="sxs-lookup"><span data-stu-id="cf860-151">This page is similar toohello local account sign-up page (shown in hello previous section) with hello exception of hello password entry fields.</span></span>

### <a name="fragment-inserted-into-hello-unified-sign-up-or-sign-in-page"></a><span data-ttu-id="cf860-152">Fragmento inseridos hello "Página de inscrição ou entrar unificada"</span><span class="sxs-lookup"><span data-stu-id="cf860-152">Fragment inserted into hello "Unified sign-up or sign-in page"</span></span>

<span data-ttu-id="cf860-153">Esta página controla tanto a inscrição quanto a entrada de clientes, que podem usar provedores de identidade social como Facebook ou Google+ ou contas locais.</span><span class="sxs-lookup"><span data-stu-id="cf860-153">This page handles both sign-up & sign-in of customers, who can use social identity providers such as Facebook or Google+, or local accounts.</span></span>

```HTML
<div id="api" data-name="Unified">
        <div class="social" role="form">
               <div class="intro">
                       <h2>Sign in with your social account</h2>
               </div>
               <div class="options">
                       <div><button class="accountButton firstButton" id="MicrosoftAccountExchange" tabindex="1">msa</button></div>
                       <div><button class="accountButton" id="FacebookExchange" tabindex="1">fb</button></div>
               </div>
        </div>
        <div class="divider">
               <h2>OR</h2>
        </div>
        <div class="localAccount" role="form">
               <div class="intro">
                       <h2>Sign in with your existing account</h2>
               </div>
               <div class="error pageLevel" aria-hidden="true" style="display: none;">
                       <p role="alert"></p>
               </div>
               <div class="entry">
                       <div class="entry-item">
                               <label for="logonIdentifier">Email Address</label> 
                               <div class="error itemLevel" aria-hidden="true" style="display: none;">
                                      <p role="alert"></p>
                               </div>
                               <input type="email" id="logonIdentifier" name="LogonIdentifier" pattern="^[a-zA-Z0-9.!#$%&amp;’*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$" placeholder="LogonIdentifier" value="" tabindex="1">
                       </div>
                       <div class="entry-item">
                               <div class="password-label"> <label for="password">Password</label><a id="forgotPassword" tabindex="2">Forgot your password?</a></div>
                               <div class="error itemLevel" aria-hidden="true" style="display: none;">
                                      <p role="alert"></p>
                               </div>
                               <input type="password" id="password" name="Password" placeholder="Password" tabindex="1">
                       </div>
                       <div class="working"></div>
                       <div class="buttons"> <button id="next" tabindex="1">Sign in</button> </div>
               </div>
               <div class="divider">
                       <h2>OR</h2>
               </div>
               <div class="create">
                       <p>Don't have an account?<a id="createAccount" tabindex="1">Sign up now</a> </p>
               </div>
        </div>
</div>
```

### <a name="fragment-inserted-into-hello-multi-factor-authentication-page"></a><span data-ttu-id="cf860-154">Fragmento inserido hello "página de autenticação multifator"</span><span class="sxs-lookup"><span data-stu-id="cf860-154">Fragment inserted into hello "Multi-factor authentication page"</span></span>

<span data-ttu-id="cf860-155">Nesta página, os usuários pode verificar seus números de telefone (usando mensagem de texto ou por voz) durante a inscrição ou entrada.</span><span class="sxs-lookup"><span data-stu-id="cf860-155">On this page, users can verify their phone numbers (using text or voice) during sign-up or sign-in.</span></span>

```HTML
<div id="api" data-name="Phonefactor">
    <div id="phonefactor_initial">
        <div class="intro">
            <p>Enter a number below that we can send a code via SMS or phone tooauthenticate you.</p>
        </div>
        <div class="errorText" id="errorMessage" style="display:none"></div>
        <div class="phoneEntry" id="phoneEntry">
            <div class="phoneNumber">
                <select id="countryCode" style="display:inline-block">
                    <option value="+93">Afghanistan (+93)</option>
                    <!-- Not all country codes listed -->
                    <option value="+44">United Kingdom (+44)</option>
                    <option value="+1" selected="">United States (+1)</option>
                    <!-- Not all country codes listed -->
                </select>
            </div>
            <div class="phoneNumber">
                <input type="text" id="localNumber" style="display:inline-block" placeholder="Phone number">
            </div>
        </div>
        <div id="codeVerification" style="display:none">
            <div>
                <p>Enter your verification code below, or <button id="retryCode" class="textButton">send a new code</button></p>
                <input type="text" id="verificationCode" placeholder="Verification code">
            </div>
        </div>
        <div class="buttons">
            <button id="verifyCode" class="sendInitialCodeButton">Send Code</button>
            <button id="verifyPhone" style="display:inline-block">Call Me</button>
            <button id="cancel" style="display:inline-block">Cancel</button>
        </div>
    </div>
    <div class="dialing-modal">
        <div class="preloader"> <img src="https://login.microsoftonline.com/static/img/win8loader.gif" alt="Please wait"></div>
        <div id="dialing_blurb"></div><div id="dialing_number"></div>
    </div>
</div>
```

### <a name="fragment-inserted-into-hello-error-page"></a><span data-ttu-id="cf860-156">Fragmento inserido hello "[NULL]"Página de erro</span><span class="sxs-lookup"><span data-stu-id="cf860-156">Fragment inserted into hello ""Error page"</span></span>

```HTML
<div id="api" class="error-page-content" data-name="GlobalException">
    <h2>Sorry, but we're having trouble signing you in.</h2>
    <div class="error-page-help">We track these errors automatically, but if hello problem persists feel free toocontact us. In hello meantime, please try again.</div>
    <div class="error-page-messagedetails">Your administrator hasn't provided any contact details.</div>
    <div class="error-page-messagedetails">
        <div class="error-page-correlationid">Correlation ID:1c4f0397-c6e4-4afe-bf74-42f488f2f15f</div>
        <div>Timestamp:2015-09-14 23:22:35Z</div>
        <div class="error-page-detail">AADB2C90065: A B2C client-side error 'Access is denied.' has occurred requesting hello remote resource.</div>
    </div>
</div>
```

## <a name="localizing-your-html-content"></a><span data-ttu-id="cf860-157">Localização do conteúdo HTML</span><span class="sxs-lookup"><span data-stu-id="cf860-157">Localizing your HTML content</span></span>

<span data-ttu-id="cf860-158">Localize o conteúdo HTML ativando a [“Personalização de idioma”](active-directory-b2c-reference-language-customization.md).</span><span class="sxs-lookup"><span data-stu-id="cf860-158">You can localize your HTML content by turning on ['Language customization'](active-directory-b2c-reference-language-customization.md).</span></span>  <span data-ttu-id="cf860-159">Habilitar esse recurso permite o Azure AD B2C tooforward abrir conexão de ID parâmetro hello, `ui-locales`, tooyour de ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="cf860-159">Enabling this feature allows Azure AD B2C tooforward hello Open ID Connect parameter, `ui-locales`, tooyour endpoint.</span></span>  <span data-ttu-id="cf860-160">O servidor de conteúdo pode usar este páginas HTML tooprovide personalizado de parâmetro que são específicos do idioma.</span><span class="sxs-lookup"><span data-stu-id="cf860-160">Your content server can use this parameter tooprovide customized HTML pages that are language-specific.</span></span>

## <a name="things-tooremember-when-building-your-own-content"></a><span data-ttu-id="cf860-161">Coisas tooremember ao criar seu próprio conteúdo</span><span class="sxs-lookup"><span data-stu-id="cf860-161">Things tooremember when building your own content</span></span>

<span data-ttu-id="cf860-162">Se você estiver planejando o recurso de personalização de interface do usuário do toouse Olá página, examine Olá práticas recomendadas a seguir:</span><span class="sxs-lookup"><span data-stu-id="cf860-162">If you are planning toouse hello page UI customization feature, review hello following best practices:</span></span>

* <span data-ttu-id="cf860-163">Não copiar o conteúdo de padrão da saudação do Azure AD B2C e tente toomodify-la.</span><span class="sxs-lookup"><span data-stu-id="cf860-163">Don't copy hello Azure AD B2C's default content and attempt toomodify it.</span></span> <span data-ttu-id="cf860-164">Ele é melhor toobuild seu conteúdo HTML5 do conteúdo de padrão de zero e toouse como referência.</span><span class="sxs-lookup"><span data-stu-id="cf860-164">It is best toobuild your HTML5 content from scratch and toouse default content as reference.</span></span>
* <span data-ttu-id="cf860-165">Por motivos de segurança, não permitimos tooinclude qualquer JavaScript no seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="cf860-165">For security reasons, we don't allow you tooinclude any JavaScript in your content.</span></span> <span data-ttu-id="cf860-166">Mais do que você precisa devem estar disponível sem necessidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="cf860-166">Most of what you need should be available out of hello box.</span></span> <span data-ttu-id="cf860-167">Se não, use [User Voice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c) toorequest nova funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="cf860-167">If not, use [User Voice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c) toorequest new functionality.</span></span>
* <span data-ttu-id="cf860-168">Versões do navegador para as quais há suporte:</span><span class="sxs-lookup"><span data-stu-id="cf860-168">Supported browser versions:</span></span>
  * <span data-ttu-id="cf860-169">Internet Explorer 11, 10, Edge</span><span class="sxs-lookup"><span data-stu-id="cf860-169">Internet Explorer 11, 10, Edge</span></span>
  * <span data-ttu-id="cf860-170">Suporte limitado para o Internet Explorer 9, 8</span><span class="sxs-lookup"><span data-stu-id="cf860-170">Limited support for Internet Explorer 9, 8</span></span>
  * <span data-ttu-id="cf860-171">Google Chrome 42.0 e superior</span><span class="sxs-lookup"><span data-stu-id="cf860-171">Google Chrome 42.0 and above</span></span>
  * <span data-ttu-id="cf860-172">Mozilla Firefox 38.0 e superior</span><span class="sxs-lookup"><span data-stu-id="cf860-172">Mozilla Firefox 38.0 and above</span></span>
