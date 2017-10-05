---
title: Aplicativo Android v2.0 do Azure Active Directory | Microsoft Docs
description: "Como criar um aplicativo Android que conecte usuários com a conta pessoal e as contas corporativas ou de estudante da Microsoft e as chamadas à API do Graph usando bibliotecas de terceiros."
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
ms.openlocfilehash: c0a5a818c61f7af7ff04bf890b54e8364f3b21b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-android-app-using-a-third-party-library-with-graph-api-using-the-v20-endpoint"></a><span data-ttu-id="79978-103">Adicionar entrada a um aplicativo Android usando uma biblioteca de terceiros com a API do Graph usando o ponto de extremidade v2.0</span><span class="sxs-lookup"><span data-stu-id="79978-103">Add sign-in to an Android app using a third-party library with Graph API using the v2.0 endpoint</span></span>
<span data-ttu-id="79978-104">A plataforma de identidade da Microsoft usa padrões abertos, como OAuth2 e OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="79978-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="79978-105">Os desenvolvedores podem usar qualquer biblioteca desejada para integrar aos nossos serviços.</span><span class="sxs-lookup"><span data-stu-id="79978-105">Developers can use any library they want to integrate with our services.</span></span> <span data-ttu-id="79978-106">Para ajudar os desenvolvedores a usar nossa plataforma com outras bibliotecas, escrevemos alguns guias passo a passo como este para demonstrar como configurar bibliotecas de terceiros que se conectam à plataforma de identidade da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="79978-106">To help developers use our platform with other libraries, we've written a few walkthroughs like this one to demonstrate how to configure third-party libraries to connect to the Microsoft identity platform.</span></span> <span data-ttu-id="79978-107">A maioria das bibliotecas que implementa [a especificação RFC6749 do OAuth2](https://tools.ietf.org/html/rfc6749) pode se conectar à plataforma de identidade da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="79978-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect to the Microsoft identity platform.</span></span>

<span data-ttu-id="79978-108">Com o aplicativo que esse passo a passo cria, os usuários podem entrar na respectiva organização e pesquisar a si mesmos na organização usando a API do Graph.</span><span class="sxs-lookup"><span data-stu-id="79978-108">With the application that this walkthrough creates, users can sign in to their organization and then search for themselves in their organization by using the Graph API.</span></span>

<span data-ttu-id="79978-109">Se ainda não conhece o OAuth2 ou o OpenID Connect, grande parte desta configuração de exemplo pode não fazer muito sentido para você.</span><span class="sxs-lookup"><span data-stu-id="79978-109">If you're new to OAuth2 or OpenID Connect, much of this sample configuration may not make sense to you.</span></span> <span data-ttu-id="79978-110">É recomendável ler o artigo [Protocolos 2.0 – Fluxo de código de autorização do OAuth 2.0](active-directory-v2-protocols-oauth-code.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="79978-110">We recommend that you read [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="79978-111">Alguns recursos da nossa plataforma que possuem uma expressão nos padrões OAuth2 ou OpenID Connect, como o Acesso Condicional e o gerenciamento de políticas do Intune, exigem que você use nossas Bibliotecas de Identidade do Microsoft Azure de software livre.</span><span class="sxs-lookup"><span data-stu-id="79978-111">Some features of our platform that do have an expression in the OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you to use our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="79978-112">O ponto de extremidade v2.0 não dá suporte a todos os cenários e recursos do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="79978-112">The v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="79978-113">Para determinar se você deve usar o ponto de extremidade v2.0, leia sobre as [limitações da v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="79978-113">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-the-code-from-github"></a><span data-ttu-id="79978-114">Baixar o código do GitHub</span><span class="sxs-lookup"><span data-stu-id="79978-114">Download the code from GitHub</span></span>
<span data-ttu-id="79978-115">O código para este tutorial é mantido [no GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).</span><span class="sxs-lookup"><span data-stu-id="79978-115">The code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).</span></span>  <span data-ttu-id="79978-116">Para acompanhar, você pode [baixar o esqueleto do aplicativo como um .zip](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) ou clonar o esqueleto:</span><span class="sxs-lookup"><span data-stu-id="79978-116">To follow along, you can  [download the app's skeleton as a .zip](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) or clone the skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

<span data-ttu-id="79978-117">Você também pode apenas baixar o exemplo e começar imediatamente:</span><span class="sxs-lookup"><span data-stu-id="79978-117">You can also just download the sample and get started right away:</span></span>

```
git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="79978-118">Registrar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="79978-118">Register an app</span></span>
<span data-ttu-id="79978-119">Crie um novo aplicativo no [Portal de registro de aplicativos](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) ou siga as etapas detalhadas em [Como registrar um aplicativo com o ponto de extremidade v 2.0](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="79978-119">Create a new app at the [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow the detailed steps at [How to register an app with the v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="79978-120">Não se esqueça de:</span><span class="sxs-lookup"><span data-stu-id="79978-120">Make sure to:</span></span>

* <span data-ttu-id="79978-121">Copiar a **ID do Aplicativo** atribuída ao seu aplicativo, pois você precisará dela em breve.</span><span class="sxs-lookup"><span data-stu-id="79978-121">Copy the **Application Id** that's assigned to your app because you'll need it soon.</span></span>
* <span data-ttu-id="79978-122">Adicione a plataforma **Móvel** de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="79978-122">Add the **Mobile** platform for your app.</span></span>

> <span data-ttu-id="79978-123">Observação: o portal de registro de aplicativo fornece um valor de **URI de redirecionamento** .</span><span class="sxs-lookup"><span data-stu-id="79978-123">Note: The Application registration portal provides a **Redirect URI** value.</span></span> <span data-ttu-id="79978-124">No entanto, neste exemplo, você deve usar o valor padrão de `https://login.microsoftonline.com/common/oauth2/nativeclient`.</span><span class="sxs-lookup"><span data-stu-id="79978-124">However, in this example you must use the default value of `https://login.microsoftonline.com/common/oauth2/nativeclient`.</span></span>
> 
> 

## <a name="download-the-nxoauth2-third-party-library-and-create-a-workspace"></a><span data-ttu-id="79978-125">Baixar a biblioteca de terceiros NXOAuth2 e criar um espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="79978-125">Download the NXOAuth2 third-party library and create a workspace</span></span>
<span data-ttu-id="79978-126">Para este passo a passo, você usará a OIDCAndroidLib do GitHub, que é uma biblioteca OAuth2 com base no código do OpenID Connect do Google.</span><span class="sxs-lookup"><span data-stu-id="79978-126">For this walkthrough, you will use the OIDCAndroidLib from GitHub, which is an OAuth2 library based on the OpenID Connect code of Google.</span></span> <span data-ttu-id="79978-127">Ela implementa o perfil de aplicativo nativo e dá suporte ao ponto de extremidade de autorização do usuário.</span><span class="sxs-lookup"><span data-stu-id="79978-127">It implements the native application profile and supports the authorization endpoint of the user.</span></span> <span data-ttu-id="79978-128">Isso é tudo de que você precisa para a integração à plataforma de identidade da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="79978-128">These are all the things that you'll need to integrate with the Microsoft identity platform.</span></span>

<span data-ttu-id="79978-129">Clone o repositório OIDCAndroidLib em seu computador.</span><span class="sxs-lookup"><span data-stu-id="79978-129">Clone the OIDCAndroidLib repo to your computer.</span></span>

```
git@github.com:kalemontes/OIDCAndroidLib.git
```

![androidStudio](../media/active-directory-android-native-oidcandroidlib-v2/emotes-url.png)

## <a name="set-up-your-android-studio-environment"></a><span data-ttu-id="79978-131">Configurar o ambiente do Android Studio</span><span class="sxs-lookup"><span data-stu-id="79978-131">Set up your Android Studio environment</span></span>
1. <span data-ttu-id="79978-132">Crie um novo projeto do Android Studio e aceite os padrões do assistente.</span><span class="sxs-lookup"><span data-stu-id="79978-132">Create a new Android Studio project and accept the defaults in the wizard.</span></span>
   
    ![Criar novo projeto no Android Studio](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample1.PNG)
   
    ![Dispositivos Android de destino](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample2.PNG)
   
    ![Adicionar uma atividade ao celular](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample3.PNG)
2. <span data-ttu-id="79978-136">Para configurar os módulos de projeto, mova o repositório clonado para o local do projeto.</span><span class="sxs-lookup"><span data-stu-id="79978-136">To set up your project modules, move the cloned repo to the project location.</span></span> <span data-ttu-id="79978-137">Você também pode criar o projeto e cloná-lo diretamente no local do projeto.</span><span class="sxs-lookup"><span data-stu-id="79978-137">You can also create the project and then clone it directly to the project location.</span></span>
   
    ![Módulos do projeto](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4_1.PNG)
3. <span data-ttu-id="79978-139">Abra as configurações de módulos do projeto usando o menu de contexto ou usando o atalho Ctrl+Alt+Maj+S.</span><span class="sxs-lookup"><span data-stu-id="79978-139">Open the project modules settings by using the context menu or by using the Ctrl+Alt+Maj+S shortcut.</span></span>
   
    ![Configurações dos módulos do projeto](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4.PNG)
4. <span data-ttu-id="79978-141">Remova o módulo de aplicativo padrão, pois você quer apenas as configurações de contêiner do projeto.</span><span class="sxs-lookup"><span data-stu-id="79978-141">Remove the default app module because you only want the project container settings.</span></span>
   
    ![O módulo de aplicativo padrão](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample5.PNG)
5. <span data-ttu-id="79978-143">Importe os módulos do repositório clonado para o projeto atual.</span><span class="sxs-lookup"><span data-stu-id="79978-143">Import modules from the cloned repo to the current project.</span></span>
   
    <span data-ttu-id="79978-144">![Importar o projeto de gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![criar a nova página de módulo](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span><span class="sxs-lookup"><span data-stu-id="79978-144">![Import gradle project](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![Create new module page](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span></span>
6. <span data-ttu-id="79978-145">Repita essas etapas para o módulo `oidlib-sample` .</span><span class="sxs-lookup"><span data-stu-id="79978-145">Repeat these steps for the `oidlib-sample` module.</span></span>
7. <span data-ttu-id="79978-146">Verifique as dependências de oidclib no módulo `oidlib-sample` .</span><span class="sxs-lookup"><span data-stu-id="79978-146">Check the oidclib dependencies on the `oidlib-sample` module.</span></span>
   
    ![dependências de oidclib no módulo de exemplo oidlib](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8.PNG)
8. <span data-ttu-id="79978-148">Clique em **OK** e aguarde a sincronização do gradle.</span><span class="sxs-lookup"><span data-stu-id="79978-148">Click **OK** and wait for gradle sync.</span></span>
   
    <span data-ttu-id="79978-149">O settings.gradle deve se parecer com este:</span><span class="sxs-lookup"><span data-stu-id="79978-149">Your settings.gradle should look like:</span></span>
   
    ![Captura de tela de settings.gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8_1.PNG)
9. <span data-ttu-id="79978-151">Crie o aplicativo de exemplo para garantir que o exemplo seja executado corretamente.</span><span class="sxs-lookup"><span data-stu-id="79978-151">Build the sample app to make sure that the sample running correctly.</span></span>
   
    <span data-ttu-id="79978-152">Você ainda não poderá usá-lo com o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="79978-152">You won't be able to use this with Azure Active Directory yet.</span></span> <span data-ttu-id="79978-153">Você precisará configurar alguns pontos de extremidade primeiro.</span><span class="sxs-lookup"><span data-stu-id="79978-153">We'll need to configure some endpoints first.</span></span> <span data-ttu-id="79978-154">Isso é para garantir que você não tenha problemas no Android Studio antes de começar a personalizar o aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="79978-154">This is to ensure you don't have an Android Studio issues before we start customizing the sample app.</span></span>
10. <span data-ttu-id="79978-155">Compile e execute `oidlib-sample` como o destino no Android Studio.</span><span class="sxs-lookup"><span data-stu-id="79978-155">Build and run `oidlib-sample` as the target in Android Studio.</span></span>
    
    ![Progresso da criação do exemplo oidlib](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample9.png)
11. <span data-ttu-id="79978-157">Exclua o diretório `app ` que foi deixado durante a remoção do módulo do projeto, já que o Android Studio não o exclui por segurança.</span><span class="sxs-lookup"><span data-stu-id="79978-157">Delete the `app ` directory that was left when you removed the module from the project because Android Studio doesn't delete it for safety.</span></span>
    
    ![Estrutura do arquivo que inclui o diretório de aplicativo](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample12.PNG)
12. <span data-ttu-id="79978-159">Abra o menu **Editar Configurações** para remover a configuração de execução que também foi deixada quando você removeu o módulo do projeto.</span><span class="sxs-lookup"><span data-stu-id="79978-159">Open the **Edit Configurations** menu to remove the run configuration that was also left when you removed the module from the project.</span></span>
    
    <span data-ttu-id="79978-160">![Menu Editar configurações](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
    ![Executar configuração do aplicativo](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span><span class="sxs-lookup"><span data-stu-id="79978-160">![Edit configurations menu](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
![Run configuration of app](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span></span>

## <a name="configure-the-endpoints-of-the-sample"></a><span data-ttu-id="79978-161">Configurar os pontos de extremidade do exemplo</span><span class="sxs-lookup"><span data-stu-id="79978-161">Configure the endpoints of the sample</span></span>
<span data-ttu-id="79978-162">Agora que `oidlib-sample` está em execução com êxito, vamos editar alguns pontos de extremidade para que isso funcione com o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="79978-162">Now that you have the `oidlib-sample` running successfully, let's edit some endpoints to get this working with Azure Active Directory.</span></span>

### <a name="configure-your-client-by-editing-the-oidcclientconfxml-file"></a><span data-ttu-id="79978-163">Configurar o cliente editando o arquivo oidc_clientconf.xml</span><span class="sxs-lookup"><span data-stu-id="79978-163">Configure your client by editing the oidc_clientconf.xml file</span></span>
1. <span data-ttu-id="79978-164">Já que você está usando somente fluxos do OAuth2 para obter um token e chamar a API do Graph, defina o cliente somente para OAuth2.</span><span class="sxs-lookup"><span data-stu-id="79978-164">Because you are using OAuth2 flows only to get a token and call the Graph API, set the client to do OAuth2 only.</span></span> <span data-ttu-id="79978-165">O OIDC aparecerá em um exemplo mais adiante.</span><span class="sxs-lookup"><span data-stu-id="79978-165">OIDC will come in a later example.</span></span>
   
    ```xml
        <bool name="oidc_oauth2only">true</bool>
    ```
2. <span data-ttu-id="79978-166">Configure a ID de cliente que você recebeu do portal de registro.</span><span class="sxs-lookup"><span data-stu-id="79978-166">Configure your client ID that you received from the registration portal.</span></span>
   
    ```xml
        <string name="oidc_clientId">86172f9d-a1ae-4348-aafa-7b3e5d1b36f5</string>
        <string name="oidc_clientSecret"></string>
    ```
3. <span data-ttu-id="79978-167">Configure o URI de redirecionamento com o exemplo abaixo.</span><span class="sxs-lookup"><span data-stu-id="79978-167">Configure your redirect URI with the one below.</span></span>
   
    ```xml
        <string name="oidc_redirectUrl">https://login.microsoftonline.com/common/oauth2/nativeclient</string>
    ```
4. <span data-ttu-id="79978-168">Configure os escopos de que você precisa para acessar a API do Graph.</span><span class="sxs-lookup"><span data-stu-id="79978-168">Configure your scopes that you need in order to access the Graph API.</span></span>
   
    ```xml
        <string-array name="oidc_scopes">
            <item>openid</item>
            <item>https://graph.microsoft.com/User.Read</item>
            <item>offline_access</item>
        </string-array>
    ```

<span data-ttu-id="79978-169">O valor `User.Read` em `oidc_scopes` permite que você leia o perfil básico do usuário conectado.</span><span class="sxs-lookup"><span data-stu-id="79978-169">The `User.Read` value in `oidc_scopes` allows you to read the basic profile the signed in user.</span></span>
<span data-ttu-id="79978-170">É possível saber mais sobre todos os escopos disponíveis em [Escopos de permissão do Microsoft Graph](https://graph.microsoft.io/docs/authorization/permission_scopes).</span><span class="sxs-lookup"><span data-stu-id="79978-170">You can learn more about all the available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="79978-171">Se você quiser explicações sobre `openid` ou `offline_access` como escopos no OpenID Connect, confira [Protocolos v2.0 – Fluxo de código de autorização do OAuth 2.0](active-directory-v2-protocols-oauth-code.md).</span><span class="sxs-lookup"><span data-stu-id="79978-171">If you'd like explanations about `openid` or `offline_access` as scopes in OpenID Connect, see [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md).</span></span>

### <a name="configure-your-client-endpoints-by-editing-the-oidcendpointsxml-file"></a><span data-ttu-id="79978-172">Configurar pontos de extremidade do cliente editando o oidc_endpoints.xml</span><span class="sxs-lookup"><span data-stu-id="79978-172">Configure your client endpoints by editing the oidc_endpoints.xml file</span></span>
* <span data-ttu-id="79978-173">Abra o arquivo `oidc_endpoints.xml` e faça estas alterações:</span><span class="sxs-lookup"><span data-stu-id="79978-173">Open the `oidc_endpoints.xml` file and make the following changes:</span></span>
  
    ```xml
    <!-- Stores OpenID Connect provider endpoints. -->
    <resources>
        <string name="op_authorizationEnpoint">https://login.microsoftonline.com/common/oauth2/v2.0/authorize</string>
        <string name="op_tokenEndpoint">https://login.microsoftonline.com/common/oauth2/v2.0/token</string>
        <string name="op_userInfoEndpoint">https://www.example.com/oauth2/userinfo</string>
        <string name="op_revocationEndpoint">https://www.example.com/oauth2/revoketoken</string>
    </resources>
    ```

<span data-ttu-id="79978-174">Esses pontos de extremidade nunca deverão ser alterados se você estiver usando o OAuth2 como seu protocolo.</span><span class="sxs-lookup"><span data-stu-id="79978-174">These endpoints should never change if you are using OAuth2 as your protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="79978-175">Os pontos de extremidade de `userInfoEndpoint` e `revocationEndpoint` atualmente não têm suporte do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="79978-175">The endpoints for `userInfoEndpoint` and `revocationEndpoint` are currently not supported by Azure Active Directory.</span></span> <span data-ttu-id="79978-176">Se deixá-los com o valor padrão de example.com, você será lembrado que eles não estão disponíveis no exemplo :-)</span><span class="sxs-lookup"><span data-stu-id="79978-176">If you leave these with the default example.com value, you will be reminded that they are not available in the sample :-)</span></span>
> 
> 

## <a name="configure-a-graph-api-call"></a><span data-ttu-id="79978-177">Configurar uma chamada à API do Graph</span><span class="sxs-lookup"><span data-stu-id="79978-177">Configure a Graph API call</span></span>
* <span data-ttu-id="79978-178">Abra o arquivo `HomeActivity.java` e faça estas alterações:</span><span class="sxs-lookup"><span data-stu-id="79978-178">Open the `HomeActivity.java` file and make the following changes:</span></span>
  
    ```Java
       //TODO: set your protected resource url
        private static final String protectedResUrl = "https://graph.microsoft.com/v1.0/me/";
    ```

<span data-ttu-id="79978-179">Aqui, uma chamada simples à API do Graph retorna nossas informações.</span><span class="sxs-lookup"><span data-stu-id="79978-179">Here a simple Graph API call returns our information.</span></span>

<span data-ttu-id="79978-180">Essas são todas as alterações que você precisa fazer.</span><span class="sxs-lookup"><span data-stu-id="79978-180">Those are all the changes that you need to do.</span></span> <span data-ttu-id="79978-181">Execute o aplicativo `oidlib-sample` e clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="79978-181">Run the `oidlib-sample` application, and click **Sign in**.</span></span>

<span data-ttu-id="79978-182">Depois da autenticação bem-sucedida, escolha o botão **Solicitar Recurso Protegido** para testar sua chamada à API do Graph.</span><span class="sxs-lookup"><span data-stu-id="79978-182">After you've successfully authenticated, select the **Request Protected Resource** button to test your call to the Graph API.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="79978-183">Obter atualizações de segurança para nosso produto</span><span class="sxs-lookup"><span data-stu-id="79978-183">Get security updates for our product</span></span>
<span data-ttu-id="79978-184">É recomendável obter notificações sobre incidentes de segurança visitando a página [Segurança TechCenter](https://technet.microsoft.com/security/dd252948) e assinando os alertas do Security Advisory.</span><span class="sxs-lookup"><span data-stu-id="79978-184">We encourage you to get notifications about security incidents by visiting the [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

