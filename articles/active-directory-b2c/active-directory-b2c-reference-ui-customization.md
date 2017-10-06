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
# <a name="azure-active-directory-b2c-customize-hello-azure-ad-b2c-user-interface-ui"></a>B2C de diretório ativo do Azure: Personalizar a interface do usuário de saudação do Azure AD B2C (IU)

A experiência do usuário é fundamental em um aplicativo voltado ao cliente.  Aumentar seu cliente base ao criar experiências de usuário com hello aparência de sua marca. O Azure AD B2C (Azure Active Directory B2C) permite personalizar as páginas de inscrição, entrada, edição de perfil e redefinição de senha com controle perfeito.

> [!NOTE]
> recurso de personalização do Hello página da interface do usuário descrito neste artigo não se aplica toohello única política, sua página de redefinição de senha que o acompanha e emails de verificação.  Esses recursos usam Olá [marca do recurso da empresa](../active-directory/active-directory-add-company-branding.md) em vez disso.
>

Este artigo aborda Olá seguintes tópicos:

* recurso de personalização da interface do usuário Olá página.
* Uma ferramenta para carregar tooAzure conteúdo HTML armazenamento de Blob para uso com o recurso de personalização do hello página da interface do usuário.
* Olá elementos de interface do usuário usados pelo Azure AD B2C que você pode personalizar usando folhas de estilo em cascata (CSS).
* Práticas recomendadas ao exercitar esse recurso.

## <a name="hello-page-ui-customization-feature"></a>recurso de personalização de interface do usuário de página Olá

Você pode personalizar Olá aparência de senha de inscrição, entrar, cliente redefinição e páginas de edição de perfil (configurando [políticas](active-directory-b2c-reference-policies.md)). Seus clientes terão uma experiência integrada ao navegar entre seu aplicativo e as páginas atendidas pelo Azure AD B2C.

Ao contrário de outros serviços em que opções de interface do usuário, B2C do Azure AD usa um simples e modernos abordagem tooUI personalização.

É assim que ela funciona: o Azure AD B2C executa o código no navegador do cliente e usa uma abordagem moderna chamada [CORS (Compartilhamento de Recursos entre Origens)](http://www.w3.org/TR/cors/).  Em tempo de execução, o conteúdo é carregado de uma URL que você especifica em uma política. Você pode especificar URLs diferentes para diferentes páginas. Depois de carregado do seu URL de conteúdo é mesclado com um fragmento HTML inserido a partir do Azure AD B2C, página Olá é exibida tooyour cliente. Você só precisa toodo é:

1. Criar conteúdo com vazio do HTML5 bem formado `<div id="api"></div>` elemento localizado em algum lugar no hello `<body>`. Este marcas de elemento onde hello Azure AD B2C conteúdo é inserido.
1. Hospede seu conteúdo em um ponto de extremidade HTTPS (com CORS permitido). Observe que os métodos de solicitação GET e OPTIONS precisam ser habilitados configurar o CORS.
1. Use CSS toostyle Olá elementos da IU que insere B2C do Azure AD.

### <a name="a-basic-example-of-customized-html"></a>Um exemplo básico de HTML personalizado

saudação de exemplo a seguir é conteúdo HTML mais básico Olá que você pode usar tootest esse recurso. Saudação de uso [ferramenta auxiliar](active-directory-b2c-reference-ui-customization-helper-tool.md) tooupload e configurar esse conteúdo em seu armazenamento de BLOBs do Azure. Em seguida, você pode verificar Olá básica não estilizado botões e campos de formulário em cada página são exibidos e funcional.

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

## <a name="test-out-hello-ui-customization-feature"></a>Testar o recurso de personalização da interface do usuário Olá

Deseja tootry recurso de personalização da interface do usuário hello usando nosso conteúdo HTML e CSS do exemplo?  Fornecemos uma [ferramenta auxiliar](active-directory-b2c-reference-ui-customization-helper-tool.md) que carrega e configura o conteúdo de exemplo em seu armazenamento de Blobs do Azure.

> [!NOTE]
> Você pode hospedar o conteúdo da interface do usuário em qualquer lugar: em servidores Web, CDNs, AWS S3, sistemas de compartilhamento de arquivos etc. Desde que o conteúdo de saudação está hospedado em um ponto de extremidade HTTPS disponível publicamente com CORS habilitado, você está toogo BOM. Estamos usando o armazenamento de Blobs do Azure somente para fins ilustrativos.
>

## <a name="hello-ui-fragments-embedded-by-azure-ad-b2c"></a>Olá fragmentos de interface do usuário inseridos pelo Azure AD B2C

Olá, seções a seguir listam os fragmentos de saudação HTML5 do Azure AD B2C mescla Olá `<div id="api"></div>` elemento localizado no seu conteúdo. **Não insira esses fragmentos em seu conteúdo HTML 5.** Olá serviço do Azure AD B2C insere em tempo de execução. Use esses fragmentos como referência ao criar seu próprio CSS (folhas de estilos em cascata).

### <a name="fragment-inserted-into-hello-identity-provider-selection-page"></a>Fragmento inserido hello "Página de seleção de provedor de identidade"

Esta página contém uma lista de provedores que Olá usuário podem escolher durante a inscrição ou entrada de identidade. Esses botões incluem provedores de identidade social como Facebook e Google+ ou então contas locais (baseadas em endereço de email ou nome de usuário).

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

### <a name="fragment-inserted-into-hello-local-account-sign-up-page"></a>Fragmento inserido hello "página de inscrição de conta Local"

Esta página contém um formulário para inscrições com conta local baseada em endereço de email ou nome de usuário. formulário de saudação pode conter controles de entrada diferentes, como a caixa de entrada de texto, caixa de entrada de senha, botão de opção, caixas de lista suspensa de seleção única e selecionar várias caixas de seleção.

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

### <a name="fragment-inserted-into-hello-social-account-sign-up-page"></a>Fragmento inseridos hello "" Social conta página de inscrição"

Esta página pode aparecer ao se inscrever usando uma conta existente de um provedor de identidade social, como o Facebook ou Google+.  Ele é usado quando informações adicionais devem ser coletadas do usuário final de saudação usando um formulário de inscrição. Esta página é semelhante toohello conta local inscrição página (mostrada na seção anterior Olá) com exceção de saudação de campos de entrada de senha hello.

### <a name="fragment-inserted-into-hello-unified-sign-up-or-sign-in-page"></a>Fragmento inseridos hello "Página de inscrição ou entrar unificada"

Esta página controla tanto a inscrição quanto a entrada de clientes, que podem usar provedores de identidade social como Facebook ou Google+ ou contas locais.

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

### <a name="fragment-inserted-into-hello-multi-factor-authentication-page"></a>Fragmento inserido hello "página de autenticação multifator"

Nesta página, os usuários pode verificar seus números de telefone (usando mensagem de texto ou por voz) durante a inscrição ou entrada.

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

### <a name="fragment-inserted-into-hello-error-page"></a>Fragmento inserido hello "[NULL]"Página de erro

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

## <a name="localizing-your-html-content"></a>Localização do conteúdo HTML

Localize o conteúdo HTML ativando a [“Personalização de idioma”](active-directory-b2c-reference-language-customization.md).  Habilitar esse recurso permite o Azure AD B2C tooforward abrir conexão de ID parâmetro hello, `ui-locales`, tooyour de ponto de extremidade.  O servidor de conteúdo pode usar este páginas HTML tooprovide personalizado de parâmetro que são específicos do idioma.

## <a name="things-tooremember-when-building-your-own-content"></a>Coisas tooremember ao criar seu próprio conteúdo

Se você estiver planejando o recurso de personalização de interface do usuário do toouse Olá página, examine Olá práticas recomendadas a seguir:

* Não copiar o conteúdo de padrão da saudação do Azure AD B2C e tente toomodify-la. Ele é melhor toobuild seu conteúdo HTML5 do conteúdo de padrão de zero e toouse como referência.
* Por motivos de segurança, não permitimos tooinclude qualquer JavaScript no seu conteúdo. Mais do que você precisa devem estar disponível sem necessidade de saudação. Se não, use [User Voice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c) toorequest nova funcionalidade.
* Versões do navegador para as quais há suporte:
  * Internet Explorer 11, 10, Edge
  * Suporte limitado para o Internet Explorer 9, 8
  * Google Chrome 42.0 e superior
  * Mozilla Firefox 38.0 e superior
