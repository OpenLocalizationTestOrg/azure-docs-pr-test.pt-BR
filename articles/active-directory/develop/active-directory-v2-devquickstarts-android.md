---
title: aplicativo do Android aaaAzure do Active Directory v 2.0 | Microsoft Docs
description: "Como um aplicativo do Android que conecta os usuários com pessoais conta da Microsoft e trabalho ou escolares e chamadas de toobuild Olá API do Graph usando bibliotecas de terceiros."
services: active-directory
documentationcenter: 
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: 16294c07-f27d-45c9-833f-7dbb12083794
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 1dd40bd3bcea28c629abce09abaed66b38774162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-android-app-using-a-third-party-library-with-graph-api-using-hello-v20-endpoint"></a><span data-ttu-id="bced9-103">Adicionar aplicativo do Android tooan entrar usando uma biblioteca de terceiros com a API do Graph usando o ponto de extremidade do hello v 2.0</span><span class="sxs-lookup"><span data-stu-id="bced9-103">Add sign-in tooan Android app using a third-party library with Graph API using hello v2.0 endpoint</span></span>
<span data-ttu-id="bced9-104">plataforma de identidade do Microsoft Hello usa padrões abertos como OAuth2 e OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="bced9-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="bced9-105">Os desenvolvedores podem usar qualquer biblioteca quiserem toointegrate com nossos serviços.</span><span class="sxs-lookup"><span data-stu-id="bced9-105">Developers can use any library they want toointegrate with our services.</span></span> <span data-ttu-id="bced9-106">os desenvolvedores de toohelp usar nossa plataforma com outras bibliotecas, escrevemos algumas instruções passo a passo como esse um toodemonstrate como plataforma de identidade da Microsoft tooconnect toohello tooconfigure bibliotecas de terceiros.</span><span class="sxs-lookup"><span data-stu-id="bced9-106">toohelp developers use our platform with other libraries, we've written a few walkthroughs like this one toodemonstrate how tooconfigure third-party libraries tooconnect toohello Microsoft identity platform.</span></span> <span data-ttu-id="bced9-107">A maioria das bibliotecas que implementam [especificação Olá RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) pode se conectar a plataforma de identidade do Microsoft toohello.</span><span class="sxs-lookup"><span data-stu-id="bced9-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect toohello Microsoft identity platform.</span></span>

<span data-ttu-id="bced9-108">Com o aplicativo hello que cria este passo a passo, os usuários podem entrar na organização tootheir e pesquisar por si mesmos em sua organização usando Olá API do Graph.</span><span class="sxs-lookup"><span data-stu-id="bced9-108">With hello application that this walkthrough creates, users can sign in tootheir organization and then search for themselves in their organization by using hello Graph API.</span></span>

<span data-ttu-id="bced9-109">Se você for novo tooOAuth2 ou OpenID Connect, muito dessa configuração de exemplo pode não fazer sentido tooyou.</span><span class="sxs-lookup"><span data-stu-id="bced9-109">If you're new tooOAuth2 or OpenID Connect, much of this sample configuration may not make sense tooyou.</span></span> <span data-ttu-id="bced9-110">É recomendável ler o artigo [Protocolos 2.0 – Fluxo de código de autorização do OAuth 2.0](active-directory-v2-protocols-oauth-code.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="bced9-110">We recommend that you read [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="bced9-111">Alguns recursos de nossa plataforma que têm uma expressão em Olá OAuth2 ou padrões de OpenID Connect, como acesso condicional e gerenciamento de política do Intune, exigem você toouse nosso código-fonte aberto bibliotecas de identidade do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="bced9-111">Some features of our platform that do have an expression in hello OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you toouse our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="bced9-112">o ponto de extremidade do Hello v 2.0 não oferece suporte a todos os recursos e cenários de Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="bced9-112">hello v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="bced9-113">toodetermine se você deve usar o ponto de extremidade de v 2.0 hello, leia sobre [limitações v 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="bced9-113">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-hello-code-from-github"></a><span data-ttu-id="bced9-114">Baixar o código de saudação do GitHub</span><span class="sxs-lookup"><span data-stu-id="bced9-114">Download hello code from GitHub</span></span>
<span data-ttu-id="bced9-115">código de saudação para este tutorial é mantido [no GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).</span><span class="sxs-lookup"><span data-stu-id="bced9-115">hello code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).</span></span>  <span data-ttu-id="bced9-116">toofollow ao longo, você pode [baixar o esqueleto do aplicativo hello como. zip](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) ou esqueleto de saudação do clone:</span><span class="sxs-lookup"><span data-stu-id="bced9-116">toofollow along, you can  [download hello app's skeleton as a .zip](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) or clone hello skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

<span data-ttu-id="bced9-117">Você também pode baixar o exemplo hello e começar imediatamente:</span><span class="sxs-lookup"><span data-stu-id="bced9-117">You can also just download hello sample and get started right away:</span></span>

```
git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="bced9-118">Registrar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="bced9-118">Register an app</span></span>
<span data-ttu-id="bced9-119">Criar um novo aplicativo no hello [portal de registro de aplicativo](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou siga Olá etapas detalhadas em [como tooregister um aplicativo com o ponto de extremidade do hello v 2.0](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="bced9-119">Create a new app at hello [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow hello detailed steps at [How tooregister an app with hello v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="bced9-120">Não se esqueça de:</span><span class="sxs-lookup"><span data-stu-id="bced9-120">Make sure to:</span></span>

* <span data-ttu-id="bced9-121">Saudação de cópia **Id do aplicativo** que é atribuído tooyour aplicativo porque você precisará dele em breve.</span><span class="sxs-lookup"><span data-stu-id="bced9-121">Copy hello **Application Id** that's assigned tooyour app because you'll need it soon.</span></span>
* <span data-ttu-id="bced9-122">Adicionar Olá **Mobile** plataforma para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bced9-122">Add hello **Mobile** platform for your app.</span></span>

> <span data-ttu-id="bced9-123">Observação: o portal de registro de aplicativo hello fornece um **URI de redirecionamento** valor.</span><span class="sxs-lookup"><span data-stu-id="bced9-123">Note: hello Application registration portal provides a **Redirect URI** value.</span></span> <span data-ttu-id="bced9-124">No entanto, neste exemplo você deve usar o valor padrão Olá `https://login.microsoftonline.com/common/oauth2/nativeclient`.</span><span class="sxs-lookup"><span data-stu-id="bced9-124">However, in this example you must use hello default value of `https://login.microsoftonline.com/common/oauth2/nativeclient`.</span></span>
> 
> 

## <a name="download-hello-nxoauth2-third-party-library-and-create-a-workspace"></a><span data-ttu-id="bced9-125">Baixar a biblioteca de terceiros NXOAuth2 hello e criar um espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="bced9-125">Download hello NXOAuth2 third-party library and create a workspace</span></span>
<span data-ttu-id="bced9-126">Para este passo a passo, você usará Olá OIDCAndroidLib do GitHub, que é uma biblioteca de OAuth2 com base em Olá código OpenID Connect do Google.</span><span class="sxs-lookup"><span data-stu-id="bced9-126">For this walkthrough, you will use hello OIDCAndroidLib from GitHub, which is an OAuth2 library based on hello OpenID Connect code of Google.</span></span> <span data-ttu-id="bced9-127">Ele implementa um perfil de aplicativo nativo hello e dá suporte ao ponto de extremidade de autorização de saudação do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="bced9-127">It implements hello native application profile and supports hello authorization endpoint of hello user.</span></span> <span data-ttu-id="bced9-128">Essas são todas as coisas hello, você precisará toointegrate com a plataforma de identidade Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="bced9-128">These are all hello things that you'll need toointegrate with hello Microsoft identity platform.</span></span>

<span data-ttu-id="bced9-129">Clone um computador de tooyour Olá OIDCAndroidLib repositório.</span><span class="sxs-lookup"><span data-stu-id="bced9-129">Clone hello OIDCAndroidLib repo tooyour computer.</span></span>

```
git@github.com:kalemontes/OIDCAndroidLib.git
```

![androidStudio](../media/active-directory-android-native-oidcandroidlib-v2/emotes-url.png)

## <a name="set-up-your-android-studio-environment"></a><span data-ttu-id="bced9-131">Configurar o ambiente do Android Studio</span><span class="sxs-lookup"><span data-stu-id="bced9-131">Set up your Android Studio environment</span></span>
1. <span data-ttu-id="bced9-132">Criar um novo projeto do Android Studio e aceite os padrões de saudação no Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="bced9-132">Create a new Android Studio project and accept hello defaults in hello wizard.</span></span>
   
    ![Criar novo projeto no Android Studio](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample1.PNG)
   
    ![Dispositivos Android de destino](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample2.PNG)
   
    ![Adicionar uma atividade toomobile](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample3.PNG)
2. <span data-ttu-id="bced9-136">tooset seus módulos de projeto, mover Olá clonado repositório toohello projeto local.</span><span class="sxs-lookup"><span data-stu-id="bced9-136">tooset up your project modules, move hello cloned repo toohello project location.</span></span> <span data-ttu-id="bced9-137">Você também pode criar projeto hello e, em seguida, clone-a diretamente toohello local do projeto.</span><span class="sxs-lookup"><span data-stu-id="bced9-137">You can also create hello project and then clone it directly toohello project location.</span></span>
   
    ![Módulos do projeto](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4_1.PNG)
3. <span data-ttu-id="bced9-139">Abra as configurações de módulos de projeto de saudação usando o menu de contexto de saudação ou usando o atalho do hello Ctrl + Alt + lin + S.</span><span class="sxs-lookup"><span data-stu-id="bced9-139">Open hello project modules settings by using hello context menu or by using hello Ctrl+Alt+Maj+S shortcut.</span></span>
   
    ![Configurações dos módulos do projeto](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4.PNG)
4. <span data-ttu-id="bced9-141">Remova o módulo de aplicativo padrão Olá porque desejar somente as configurações de contêiner de projeto hello.</span><span class="sxs-lookup"><span data-stu-id="bced9-141">Remove hello default app module because you only want hello project container settings.</span></span>
   
    ![módulo de aplicativo Hello padrão](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample5.PNG)
5. <span data-ttu-id="bced9-143">Importar os módulos de projeto atual do toohello Olá repositório clonado.</span><span class="sxs-lookup"><span data-stu-id="bced9-143">Import modules from hello cloned repo toohello current project.</span></span>
   
    <span data-ttu-id="bced9-144">![Importar o projeto de gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![criar a nova página de módulo](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span><span class="sxs-lookup"><span data-stu-id="bced9-144">![Import gradle project](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![Create new module page](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span></span>
6. <span data-ttu-id="bced9-145">Repita essas etapas para Olá `oidlib-sample` módulo.</span><span class="sxs-lookup"><span data-stu-id="bced9-145">Repeat these steps for hello `oidlib-sample` module.</span></span>
7. <span data-ttu-id="bced9-146">Verificar dependências oidclib Olá Olá `oidlib-sample` módulo.</span><span class="sxs-lookup"><span data-stu-id="bced9-146">Check hello oidclib dependencies on hello `oidlib-sample` module.</span></span>
   
    ![dependências de oidclib no módulo de oidlib exemplo hello](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8.PNG)
8. <span data-ttu-id="bced9-148">Clique em **OK** e aguarde a sincronização do gradle.</span><span class="sxs-lookup"><span data-stu-id="bced9-148">Click **OK** and wait for gradle sync.</span></span>
   
    <span data-ttu-id="bced9-149">O settings.gradle deve se parecer com este:</span><span class="sxs-lookup"><span data-stu-id="bced9-149">Your settings.gradle should look like:</span></span>
   
    ![Captura de tela de settings.gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8_1.PNG)
9. <span data-ttu-id="bced9-151">Criar toomake de aplicativo de exemplo de hello-se de que esse exemplo hello sendo executado corretamente.</span><span class="sxs-lookup"><span data-stu-id="bced9-151">Build hello sample app toomake sure that hello sample running correctly.</span></span>
   
    <span data-ttu-id="bced9-152">Você não será capaz de toouse isso com o Azure Active Directory ainda.</span><span class="sxs-lookup"><span data-stu-id="bced9-152">You won't be able toouse this with Azure Active Directory yet.</span></span> <span data-ttu-id="bced9-153">Vamos precisar tooconfigure alguns pontos de extremidade primeiro.</span><span class="sxs-lookup"><span data-stu-id="bced9-153">We'll need tooconfigure some endpoints first.</span></span> <span data-ttu-id="bced9-154">Isso é tooensure você não tiver um problemas de Android Studio antes de começar a personalizar o aplicativo de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="bced9-154">This is tooensure you don't have an Android Studio issues before we start customizing hello sample app.</span></span>
10. <span data-ttu-id="bced9-155">Compilar e executar `oidlib-sample` como destino Olá no Android Studio.</span><span class="sxs-lookup"><span data-stu-id="bced9-155">Build and run `oidlib-sample` as hello target in Android Studio.</span></span>
    
    ![Progresso da criação do exemplo oidlib](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample9.png)
11. <span data-ttu-id="bced9-157">Excluir Olá `app ` diretório que foi deixado quando módulo Olá é removido do projeto Olá porque Android Studio não excluí-la para segurança.</span><span class="sxs-lookup"><span data-stu-id="bced9-157">Delete hello `app ` directory that was left when you removed hello module from hello project because Android Studio doesn't delete it for safety.</span></span>
    
    ![Estrutura do arquivo que contém o diretório de aplicativo hello](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample12.PNG)
12. <span data-ttu-id="bced9-159">Olá abrir **editar configurações** configuração Olá executado do menu tooremove que também foi deixada quando removido o módulo de saudação do projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="bced9-159">Open hello **Edit Configurations** menu tooremove hello run configuration that was also left when you removed hello module from hello project.</span></span>
    
    <span data-ttu-id="bced9-160">![Menu Editar configurações](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
    ![Executar configuração do aplicativo](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span><span class="sxs-lookup"><span data-stu-id="bced9-160">![Edit configurations menu](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
![Run configuration of app](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span></span>

## <a name="configure-hello-endpoints-of-hello-sample"></a><span data-ttu-id="bced9-161">Configurar pontos de extremidade de saudação do exemplo hello</span><span class="sxs-lookup"><span data-stu-id="bced9-161">Configure hello endpoints of hello sample</span></span>
<span data-ttu-id="bced9-162">Agora que você tem Olá `oidlib-sample` em execução com êxito, vamos Editar tooget alguns pontos de extremidade isso funcionar com o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="bced9-162">Now that you have hello `oidlib-sample` running successfully, let's edit some endpoints tooget this working with Azure Active Directory.</span></span>

### <a name="configure-your-client-by-editing-hello-oidcclientconfxml-file"></a><span data-ttu-id="bced9-163">Configurar o cliente editando o arquivo de oidc_clientconf.xml Olá</span><span class="sxs-lookup"><span data-stu-id="bced9-163">Configure your client by editing hello oidc_clientconf.xml file</span></span>
1. <span data-ttu-id="bced9-164">Porque você está usando OAuth2 de fluxos apenas tooget um token e chamar hello API do Graph, defina Olá cliente toodo OAuth2 somente.</span><span class="sxs-lookup"><span data-stu-id="bced9-164">Because you are using OAuth2 flows only tooget a token and call hello Graph API, set hello client toodo OAuth2 only.</span></span> <span data-ttu-id="bced9-165">O OIDC aparecerá em um exemplo mais adiante.</span><span class="sxs-lookup"><span data-stu-id="bced9-165">OIDC will come in a later example.</span></span>
   
    ```xml
        <bool name="oidc_oauth2only">true</bool>
    ```
2. <span data-ttu-id="bced9-166">Configure sua ID de cliente que você recebeu do portal de registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="bced9-166">Configure your client ID that you received from hello registration portal.</span></span>
   
    ```xml
        <string name="oidc_clientId">86172f9d-a1ae-4348-aafa-7b3e5d1b36f5</string>
        <string name="oidc_clientSecret"></string>
    ```
3. <span data-ttu-id="bced9-167">Configure o URI de redirecionamento com hello um abaixo.</span><span class="sxs-lookup"><span data-stu-id="bced9-167">Configure your redirect URI with hello one below.</span></span>
   
    ```xml
        <string name="oidc_redirectUrl">https://login.microsoftonline.com/common/oauth2/nativeclient</string>
    ```
4. <span data-ttu-id="bced9-168">Configure os escopos que você precisa em ordem tooaccess Olá API do Graph.</span><span class="sxs-lookup"><span data-stu-id="bced9-168">Configure your scopes that you need in order tooaccess hello Graph API.</span></span>
   
    ```xml
        <string-array name="oidc_scopes">
            <item>openid</item>
            <item>https://graph.microsoft.com/User.Read</item>
            <item>offline_access</item>
        </string-array>
    ```

<span data-ttu-id="bced9-169">Olá `User.Read` valor em `oidc_scopes` permite que você tooread Olá perfil básico Olá usuário conectado.</span><span class="sxs-lookup"><span data-stu-id="bced9-169">hello `User.Read` value in `oidc_scopes` allows you tooread hello basic profile hello signed in user.</span></span>
<span data-ttu-id="bced9-170">Você pode aprender mais sobre todos os escopos disponíveis de saudação em [escopos de permissão do Microsoft Graph](https://graph.microsoft.io/docs/authorization/permission_scopes).</span><span class="sxs-lookup"><span data-stu-id="bced9-170">You can learn more about all hello available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="bced9-171">Se você quiser explicações sobre `openid` ou `offline_access` como escopos no OpenID Connect, confira [Protocolos v2.0 – Fluxo de código de autorização do OAuth 2.0](active-directory-v2-protocols-oauth-code.md).</span><span class="sxs-lookup"><span data-stu-id="bced9-171">If you'd like explanations about `openid` or `offline_access` as scopes in OpenID Connect, see [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md).</span></span>

### <a name="configure-your-client-endpoints-by-editing-hello-oidcendpointsxml-file"></a><span data-ttu-id="bced9-172">Configurar seus pontos de extremidade do cliente, editando o arquivo de oidc_endpoints.xml Olá</span><span class="sxs-lookup"><span data-stu-id="bced9-172">Configure your client endpoints by editing hello oidc_endpoints.xml file</span></span>
* <span data-ttu-id="bced9-173">Olá abrir `oidc_endpoints.xml` de arquivo e fazer Olá as seguintes alterações:</span><span class="sxs-lookup"><span data-stu-id="bced9-173">Open hello `oidc_endpoints.xml` file and make hello following changes:</span></span>
  
    ```xml
    <!-- Stores OpenID Connect provider endpoints. -->
    <resources>
        <string name="op_authorizationEnpoint">https://login.microsoftonline.com/common/oauth2/v2.0/authorize</string>
        <string name="op_tokenEndpoint">https://login.microsoftonline.com/common/oauth2/v2.0/token</string>
        <string name="op_userInfoEndpoint">https://www.example.com/oauth2/userinfo</string>
        <string name="op_revocationEndpoint">https://www.example.com/oauth2/revoketoken</string>
    </resources>
    ```

<span data-ttu-id="bced9-174">Esses pontos de extremidade nunca deverão ser alterados se você estiver usando o OAuth2 como seu protocolo.</span><span class="sxs-lookup"><span data-stu-id="bced9-174">These endpoints should never change if you are using OAuth2 as your protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="bced9-175">Olá pontos de extremidade para `userInfoEndpoint` e `revocationEndpoint` atualmente não são suportados pelo Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="bced9-175">hello endpoints for `userInfoEndpoint` and `revocationEndpoint` are currently not supported by Azure Active Directory.</span></span> <span data-ttu-id="bced9-176">Se você deixar esses recursos com valor de example.com saudação padrão, você será lembrado que eles não estão disponíveis no exemplo hello :-)</span><span class="sxs-lookup"><span data-stu-id="bced9-176">If you leave these with hello default example.com value, you will be reminded that they are not available in hello sample :-)</span></span>
> 
> 

## <a name="configure-a-graph-api-call"></a><span data-ttu-id="bced9-177">Configurar uma chamada à API do Graph</span><span class="sxs-lookup"><span data-stu-id="bced9-177">Configure a Graph API call</span></span>
* <span data-ttu-id="bced9-178">Olá abrir `HomeActivity.java` de arquivo e fazer Olá as seguintes alterações:</span><span class="sxs-lookup"><span data-stu-id="bced9-178">Open hello `HomeActivity.java` file and make hello following changes:</span></span>
  
    ```Java
       //TODO: set your protected resource url
        private static final String protectedResUrl = "https://graph.microsoft.com/v1.0/me/";
    ```

<span data-ttu-id="bced9-179">Aqui, uma chamada simples à API do Graph retorna nossas informações.</span><span class="sxs-lookup"><span data-stu-id="bced9-179">Here a simple Graph API call returns our information.</span></span>

<span data-ttu-id="bced9-180">Essas são todas as alterações de saudação que você precisa toodo.</span><span class="sxs-lookup"><span data-stu-id="bced9-180">Those are all hello changes that you need toodo.</span></span> <span data-ttu-id="bced9-181">Executar Olá `oidlib-sample` aplicativo e clique em **entrar**.</span><span class="sxs-lookup"><span data-stu-id="bced9-181">Run hello `oidlib-sample` application, and click **Sign in**.</span></span>

<span data-ttu-id="bced9-182">Depois que você foi autenticado com êxito, selecione Olá **solicitar o recurso protegido** botão tootest toohello sua chamada de API do Graph.</span><span class="sxs-lookup"><span data-stu-id="bced9-182">After you've successfully authenticated, select hello **Request Protected Resource** button tootest your call toohello Graph API.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="bced9-183">Obter atualizações de segurança para nosso produto</span><span class="sxs-lookup"><span data-stu-id="bced9-183">Get security updates for our product</span></span>
<span data-ttu-id="bced9-184">Recomendamos que você tooget notificações sobre incidentes de segurança visitando Olá [TechCenter de segurança](https://technet.microsoft.com/security/dd252948) e assinando tooSecurity alertas de aviso.</span><span class="sxs-lookup"><span data-stu-id="bced9-184">We encourage you tooget notifications about security incidents by visiting hello [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

