---
title: aaaIntegrate AD do Azure em um aplicativo do iOS | Microsoft Docs
description: Como toobuild um aplicativo iOS que se integra ao AD do Azure para entrar e chamadas de AD do Azure APIs protegidas usando OAuth.
services: active-directory
documentationcenter: ios
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: 42303177-9566-48ed-8abb-279fcf1e6ddb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 01/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: 6e05745b2b2b122995dcba896ab0f2ed32509e3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-an-ios-app"></a><span data-ttu-id="b6df9-103">Integrar o Azure AD em um aplicativo iOS</span><span class="sxs-lookup"><span data-stu-id="b6df9-103">Integrate Azure AD into an iOS app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> <span data-ttu-id="b6df9-104">Experimentar a visualização de saudação do nosso novo [portal do desenvolvedor](https://identity.microsoft.com/Docs/iOS) que ajuda a colocar em funcionamento com o Azure Active Directory em apenas alguns minutos!</span><span class="sxs-lookup"><span data-stu-id="b6df9-104">Try hello preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure Active Directory in just a few minutes!</span></span>  <span data-ttu-id="b6df9-105">portal do desenvolvedor Olá o guiará pelo processo de saudação do registro de um aplicativo e a integração do AD do Azure em seu código.</span><span class="sxs-lookup"><span data-stu-id="b6df9-105">hello developer portal guides you through hello process of registering an app and integrating Azure AD into your code.</span></span>  <span data-ttu-id="b6df9-106">Quando terminar, você terá um aplicativo simples que pode autenticar os usuários em seu locatário e um back-end que pode aceitar tokens e executar a validação.</span><span class="sxs-lookup"><span data-stu-id="b6df9-106">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a backend that can accept tokens and perform validation.</span></span> 
> 
> 

<span data-ttu-id="b6df9-107">Azure Active Directory (AD do Azure) fornece Olá biblioteca de autenticação do Active Directory ou ADAL, para os clientes do iOS que precisam tooaccess protegido recursos.</span><span class="sxs-lookup"><span data-stu-id="b6df9-107">Azure Active Directory (Azure AD) provides hello Active Directory Authentication Library, or ADAL, for iOS clients that need tooaccess protected resources.</span></span> <span data-ttu-id="b6df9-108">ADAL simplifica o processo de saudação que seu aplicativo usa tooobtain tokens de acesso.</span><span class="sxs-lookup"><span data-stu-id="b6df9-108">ADAL simplifies hello process that your app uses tooobtain access tokens.</span></span> <span data-ttu-id="b6df9-109">toodemonstrate fácil é, este artigo é criar um aplicativo de lista de tarefas do objetivo C que:</span><span class="sxs-lookup"><span data-stu-id="b6df9-109">toodemonstrate how easy it is, in this article we build an Objective C To-Do List application that:</span></span>

* <span data-ttu-id="b6df9-110">Obtém acesso tokens para chamar a API do Azure AD Graph Olá usando Olá [protocolo de autenticação OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="b6df9-110">Gets access tokens for calling hello Azure AD Graph API by using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="b6df9-111">Pesquisa um diretório para usuários com um determinado alias.</span><span class="sxs-lookup"><span data-stu-id="b6df9-111">Searches a directory for users with a given alias.</span></span>

<span data-ttu-id="b6df9-112">aplicativo de trabalho concluída hello de toobuild, você precisa:</span><span class="sxs-lookup"><span data-stu-id="b6df9-112">toobuild hello complete working application, you need to:</span></span>

1. <span data-ttu-id="b6df9-113">Registrar seu aplicativo no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b6df9-113">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="b6df9-114">Instalar e configurar a ADAL.</span><span class="sxs-lookup"><span data-stu-id="b6df9-114">Install and configure ADAL.</span></span>
3. <span data-ttu-id="b6df9-115">Use ADAL tooget tokens do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="b6df9-115">Use ADAL tooget tokens from Azure AD.</span></span>

<span data-ttu-id="b6df9-116">tooget iniciado, [baixar o esqueleto do aplicativo hello](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) ou [baixar exemplo hello concluída](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="b6df9-116">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span> <span data-ttu-id="b6df9-117">Você também precisará de um locatário do Azure AD no qual possa criar usuários e registrar um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b6df9-117">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="b6df9-118">Se você ainda não tiver um locatário, [Saiba como tooget uma](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="b6df9-118">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>


> [!TIP]
> <span data-ttu-id="b6df9-119">Experimentar a visualização de saudação do nosso novo [portal do desenvolvedor](https://identity.microsoft.com/Docs/iOS) que ajuda a colocar em funcionamento com o Azure AD em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="b6df9-119">Try hello preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="b6df9-120">portal do desenvolvedor Olá o guiará pelo processo de saudação do registro de um aplicativo e a integração do AD do Azure em seu código.</span><span class="sxs-lookup"><span data-stu-id="b6df9-120">hello developer portal guides you through hello process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="b6df9-121">Quando terminar, você terá um aplicativo simples que pode autenticar os usuários em seu locatário e um back-end que pode aceitar tokens e executar a validação.</span><span class="sxs-lookup"><span data-stu-id="b6df9-121">When you’re finished, you'll have a simple application that can authenticate users in your tenant, and a back end that can accept tokens and perform validation.</span></span> 
> 
> 

## <a name="1-determine-what-your-redirect-uri-is-for-ios"></a><span data-ttu-id="b6df9-122">1. Determine qual é seu URI de redirecionamento para iOS</span><span class="sxs-lookup"><span data-stu-id="b6df9-122">1. Determine what your redirect URI is for iOS</span></span>
<span data-ttu-id="b6df9-123">toosecurely iniciar seus aplicativos em determinados cenários SSO, você deve criar um *URI de redirecionamento* em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="b6df9-123">toosecurely start your applications in certain SSO scenarios, you must create a *redirect URI* in a particular format.</span></span> <span data-ttu-id="b6df9-124">Um redirecionamento de URI é usado tooensure que Olá tokens retorno toohello aplicativo correto que solicitado para eles.</span><span class="sxs-lookup"><span data-stu-id="b6df9-124">A redirect URI is used tooensure that hello tokens return toohello correct application that asked for them.</span></span>


<span data-ttu-id="b6df9-125">Olá iOS formato um redirecionamento de URI é:</span><span class="sxs-lookup"><span data-stu-id="b6df9-125">hello iOS format for a redirect URI is:</span></span>

```
<app-scheme>://<bundle-id>
```

* <span data-ttu-id="b6df9-126">**app-scheme** – isso é registrado no projeto XCode.</span><span class="sxs-lookup"><span data-stu-id="b6df9-126">**app-scheme** - This is registered in your XCode project.</span></span> <span data-ttu-id="b6df9-127">É como os outros aplicativos podem chamar você.</span><span class="sxs-lookup"><span data-stu-id="b6df9-127">It is how other applications can call you.</span></span> <span data-ttu-id="b6df9-128">Você pode encontrar isso em Info.plist -> tipos de URL -> identificador de URL.</span><span class="sxs-lookup"><span data-stu-id="b6df9-128">You can find this under Info.plist -> URL types -> URL Identifier.</span></span> <span data-ttu-id="b6df9-129">Você deve criar um se você ainda não tiver um ou mais configurados.</span><span class="sxs-lookup"><span data-stu-id="b6df9-129">You should create one if you don't already have one or more configured.</span></span>
* <span data-ttu-id="b6df9-130">**id do pacote** -isso é hello identificador de pacote encontrado em "identity" cancelar suas configurações de projeto no XCode.</span><span class="sxs-lookup"><span data-stu-id="b6df9-130">**bundle-id** - This is hello Bundle Identifier found under "identity" un your project settings in XCode.</span></span>

<span data-ttu-id="b6df9-131">Um exemplo para este código de Início Rápido é: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***</span><span class="sxs-lookup"><span data-stu-id="b6df9-131">An example for this QuickStart code: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***</span></span>

## <a name="2-register-hello-directorysearcher-application"></a><span data-ttu-id="b6df9-132">2. Registrar o aplicativo de DirectorySearcher hello</span><span class="sxs-lookup"><span data-stu-id="b6df9-132">2. Register hello DirectorySearcher application</span></span>
<span data-ttu-id="b6df9-133">tooset backup de seus tokens de tooget do aplicativo, primeiro é necessário tooregistê-lo no AD do Azure locatário e conceda a ela Olá tooaccess de permissão do Azure AD Graph API:</span><span class="sxs-lookup"><span data-stu-id="b6df9-133">tooset up your app tooget tokens, you first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="b6df9-134">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b6df9-134">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b6df9-135">Na barra superior do hello, clique em sua conta.</span><span class="sxs-lookup"><span data-stu-id="b6df9-135">On hello top bar, click your account.</span></span> <span data-ttu-id="b6df9-136">Em Olá **diretório** , escolha o locatário do Active Directory Olá onde você deseja tooregister seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b6df9-136">Under hello **Directory** list, choose hello Active Directory tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="b6df9-137">Clique em **mais serviços** Olá painel de navegação esquerda e, em seguida, selecione **Active Directory do Azure**.</span><span class="sxs-lookup"><span data-stu-id="b6df9-137">Click **More Services** in hello leftmost navigation pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="b6df9-138">Clique em **Registros do aplicativo** e, em seguida, selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="b6df9-138">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="b6df9-139">Siga Olá solicita toocreate um novo **aplicativo cliente nativo**.</span><span class="sxs-lookup"><span data-stu-id="b6df9-139">Follow hello prompts toocreate a new **Native Client Application**.</span></span>
  * <span data-ttu-id="b6df9-140">Olá **nome** da saudação aplicativo descreve os usuários de tooend do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b6df9-140">hello **Name** of hello application describes your application tooend users.</span></span>
  * <span data-ttu-id="b6df9-141">Olá **Uri de redirecionamento** é uma combinação de esquema e a cadeia de caracteres que o AD do Azure usa tooreturn respostas de token.</span><span class="sxs-lookup"><span data-stu-id="b6df9-141">hello **Redirect Uri** is a scheme and string combination that Azure AD uses tooreturn token responses.</span></span>  <span data-ttu-id="b6df9-142">Insira um valor que é tooyour específico de aplicativo e se baseia em informações de URI de redirecionamento anteriores hello.</span><span class="sxs-lookup"><span data-stu-id="b6df9-142">Enter a value that is specific tooyour application and is based on hello previous redirect URI information.</span></span>
6. <span data-ttu-id="b6df9-143">Depois de concluir o registro de hello, Azure AD atribui seu aplicativo a uma ID exclusiva do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b6df9-143">After you've completed hello registration, Azure AD assigns your app a unique application ID.</span></span>  <span data-ttu-id="b6df9-144">Você precisará desse valor nas seções de Avançar hello, portanto copiá-lo do guia do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="b6df9-144">You'll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="b6df9-145">De saudação **configurações** página, selecione **permissões necessárias** e, em seguida, selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="b6df9-145">From hello **Settings** page, select **Required Permissions** and then select **Add**.</span></span> <span data-ttu-id="b6df9-146">Selecione **Microsoft Graph** como Olá API e, em seguida, adicione Olá **ler dados do diretório** permissão em **permissões delegadas**.</span><span class="sxs-lookup"><span data-stu-id="b6df9-146">Select **Microsoft Graph** as hello API, and then add hello **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="b6df9-147">Isso configura a saudação de tooquery seu aplicativo do Azure AD Graph API para os usuários.</span><span class="sxs-lookup"><span data-stu-id="b6df9-147">This sets up your application tooquery hello Azure AD Graph API for users.</span></span>

## <a name="3-install-and-configure-adal"></a><span data-ttu-id="b6df9-148">3. Instalar e configurar a ADAL</span><span class="sxs-lookup"><span data-stu-id="b6df9-148">3. Install and configure ADAL</span></span>
<span data-ttu-id="b6df9-149">Agora que você tem um aplicativo no AD do Azure, você pode instalar a ADAL e escrever seu código relacionado à identidade.</span><span class="sxs-lookup"><span data-stu-id="b6df9-149">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="b6df9-150">Para obter toocommunicate ADAL com o AD do Azure, você precisa tooprovide-lo com algumas informações sobre o registro do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b6df9-150">For ADAL toocommunicate with Azure AD, you need tooprovide it with some information about your app registration.</span></span>

1. <span data-ttu-id="b6df9-151">Comece adicionando toohello ADAL DirectorySearcher projeto usando CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="b6df9-151">Begin by adding ADAL toohello DirectorySearcher project by using CocoaPods.</span></span>

    ```
    $ vi Podfile
    ```
2. <span data-ttu-id="b6df9-152">Adicione Olá toothis podfile a seguir:</span><span class="sxs-lookup"><span data-stu-id="b6df9-152">Add hello following toothis podfile:</span></span>

    ```
    source 'https://github.com/CocoaPods/Specs.git'
    link_with ['QuickStart']
    xcodeproj 'QuickStart'

    pod 'ADALiOS'
    ```

3. <span data-ttu-id="b6df9-153">Carregar agora Olá podfile usando CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="b6df9-153">Now load hello podfile by using CocoaPods.</span></span> <span data-ttu-id="b6df9-154">Esta etapa cria um novo espaço de trabalho do XCode que você carrega.</span><span class="sxs-lookup"><span data-stu-id="b6df9-154">This step creates a new XCode workspace that you load.</span></span>

    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

4. <span data-ttu-id="b6df9-155">No projeto de início rápido do hello, abrir o arquivo de plist Olá `settings.plist`.</span><span class="sxs-lookup"><span data-stu-id="b6df9-155">In hello QuickStart project, open hello plist file `settings.plist`.</span></span>  <span data-ttu-id="b6df9-156">Substitua valores de saudação de elementos Olá Olá seção tooreflect Olá os valores que você inseriu na Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b6df9-156">Replace hello values of hello elements in hello section tooreflect hello values that you entered in hello Azure portal.</span></span> <span data-ttu-id="b6df9-157">Seu código faz referência a esses valores sempre que ele usar a ADAL.</span><span class="sxs-lookup"><span data-stu-id="b6df9-157">Your code references these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="b6df9-158">Olá `tenant` é o domínio de saudação do seu locatário do AD do Azure, por exemplo, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="b6df9-158">hello `tenant` is hello domain of your Azure AD tenant, for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="b6df9-159">Olá `clientId` é Olá ID do cliente do aplicativo que você copiou do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="b6df9-159">hello `clientId` is hello client ID of your application that you copied from hello portal.</span></span>
  * <span data-ttu-id="b6df9-160">Olá `redirectUri` é a URL de redirecionamento de saudação registrado no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="b6df9-160">hello `redirectUri` is hello redirect URL that you registered in hello portal.</span></span>

## <a name="4----use-adal-tooget-tokens-from-azure-ad"></a><span data-ttu-id="b6df9-161">4.    Usar o ADAL tooget tokens do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b6df9-161">4.    Use ADAL tooget tokens from Azure AD</span></span>
<span data-ttu-id="b6df9-162">Olá princípio básico de ADAL é que sempre que seu aplicativo precisa de um token de acesso, ele simplesmente chama um completionBlock `+(void) getToken : `, e ADAL Olá rest.</span><span class="sxs-lookup"><span data-stu-id="b6df9-162">hello basic principle behind ADAL is that whenever your app needs an access token, it simply calls a completionBlock `+(void) getToken : `, and ADAL does hello rest.</span></span>  

1. <span data-ttu-id="b6df9-163">Em Olá `QuickStart` projeto, abra `GraphAPICaller.m` e localize Olá `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` comentário superior hello.</span><span class="sxs-lookup"><span data-stu-id="b6df9-163">In hello `QuickStart` project, open `GraphAPICaller.m` and locate hello `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` comment near hello top.</span></span>  <span data-ttu-id="b6df9-164">Isso é onde você pode passa Olá ADAL coordenadas por meio de um CompletionBlock, toocommunicate com o AD do Azure e informe como toocache tokens.</span><span class="sxs-lookup"><span data-stu-id="b6df9-164">This is where you pass ADAL hello coordinates through a CompletionBlock, toocommunicate with Azure AD, and tell it how toocache tokens.</span></span>

    ```ObjC
    +(void) getToken : (BOOL) clearCache
               parent:(UIViewController*) parent
    completionHandler:(void (^) (NSString*, NSError*))completionBlock;
    {
        AppData* data = [AppData getInstance];
        if(data.userItem){
            completionBlock(data.userItem.accessToken, nil);
            return;
        }

        ADAuthenticationError *error;
        authContext = [ADAuthenticationContext authenticationContextWithAuthority:data.authority error:&error];
        authContext.parentController = parent;
        NSURL *redirectUri = [[NSURL alloc]initWithString:data.redirectUriString];

        [ADAuthenticationSettings sharedInstance].enableFullScreen = YES;
        [authContext acquireTokenWithResource:data.resourceId
                                     clientId:data.clientId
                                  redirectUri:redirectUri
                               promptBehavior:AD_PROMPT_AUTO
                                       userId:data.userItem.userInformation.userId
                        extraQueryParameters: @"nux=1" // if this strikes you as strange it was legacy toodisplay hello correct mobile UX. You most likely won't need it in your code.
                             completionBlock:^(ADAuthenticationResult *result) {

                                  if (result.status != AD_SUCCEEDED)
                                  {
                                     completionBlock(nil, result.error);
                                  }
                                  else
                                  {
                                      data.userItem = result.tokenCacheStoreItem;
                                      completionBlock(result.tokenCacheStoreItem.accessToken, nil);
                                  }
                             }];
    }

    ```

2. <span data-ttu-id="b6df9-165">Agora precisamos toouse toosearch esse token para usuários no gráfico de saudação.</span><span class="sxs-lookup"><span data-stu-id="b6df9-165">Now we need toouse this token toosearch for users in hello graph.</span></span> <span data-ttu-id="b6df9-166">Localize Olá `// TODO: implement SearchUsersList` comentário.</span><span class="sxs-lookup"><span data-stu-id="b6df9-166">Find hello `// TODO: implement SearchUsersList` comment.</span></span> <span data-ttu-id="b6df9-167">Esse método torna um tooquery de toohello do Azure AD Graph API de solicitação GET para usuários cujo UPN começa com hello dado o termo de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="b6df9-167">This method makes a GET request toohello Azure AD Graph API tooquery for users whose UPN begins with hello given search term.</span></span>  <span data-ttu-id="b6df9-168">tooquery hello Azure AD Graph API, você precisa tooinclude um access_token no hello `Authorization` cabeçalho de solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="b6df9-168">tooquery hello Azure AD Graph API, you need tooinclude an access_token in hello `Authorization` header of hello request.</span></span> <span data-ttu-id="b6df9-169">É aí que a ADAL entra em cena.</span><span class="sxs-lookup"><span data-stu-id="b6df9-169">This is where ADAL comes in.</span></span>

    ```ObjC
    +(void) searchUserList:(NSString*)searchString
                    parent:(UIViewController*) parent
          completionBlock:(void (^) (NSMutableArray* Users, NSError* error)) completionBlock
    {
        if (!loadedApplicationSettings)
       {
            [self readApplicationSettings];
        }
        
        AppData* data = [AppData getInstance];

        NSString *graphURL = [NSString stringWithFormat:@"%@%@/users?api-version=%@&$filter=startswith(userPrincipalName, '%@')", data.taskWebApiUrlString, data.tenant, data.apiversion, searchString];

        [self craftRequest:[self.class trimString:graphURL]
                    parent:parent
         completionHandler:^(NSMutableURLRequest *request, NSError *error) {

             if (error != nil)
             {
                 completionBlock(nil, error);
             }
             else
             {

                 NSOperationQueue *queue = [[NSOperationQueue alloc]init];

                 [NSURLConnection sendAsynchronousRequest:request queue:queue completionHandler:^(NSURLResponse *response, NSData *data, NSError *error) {

                     if (error == nil && data != nil){

                         NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:data options:0 error:nil];

                         // We can grab hello JSON node at hello top tooget our graph data.
                         NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                         // Don't be thrown off by hello key name being "value". It really is hello name of the
                         // first node. :-)

                         // Each object is a key value pair
                         NSDictionary *keyValuePairs;
                         NSMutableArray* Users = [[NSMutableArray alloc]init];

                         for(int i =0; i < graphDataArray.count; i++)
                         {
                             keyValuePairs = [graphDataArray objectAtIndex:i];

                             User *s = [[User alloc]init];
                             s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                             s.name =[keyValuePairs valueForKey:@"givenName"];

                             [Users addObject:s];
                         }

                         completionBlock(Users, nil);
                     }
                     else
                     {
                         completionBlock(nil, error);
                     }

                }];
             }
         }];

    }

    ```


3. <span data-ttu-id="b6df9-170">Quando o aplicativo solicita um token chamando `getToken(...)`, ADAL tentativas tooreturn um token sem solicitar credenciais de usuário hello.</span><span class="sxs-lookup"><span data-stu-id="b6df9-170">When your app requests a token by calling `getToken(...)`, ADAL attempts tooreturn a token without asking hello user for credentials.</span></span>  <span data-ttu-id="b6df9-171">Se ADAL determina que o usuário Olá precisa toosign em tooget um token, ele será exibir uma caixa de diálogo para entrar, coletar credenciais de saudação do usuário e, em seguida, retorna um token após a autenticação bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="b6df9-171">If ADAL determines that hello user needs toosign in tooget a token, it will display a dialog box for sign-in, collect hello user's credentials, and then return a token after successful authentication.</span></span>  <span data-ttu-id="b6df9-172">Se a ADAL não é capaz de tooreturn um token por qualquer motivo, ele gerará um `AdalException`.</span><span class="sxs-lookup"><span data-stu-id="b6df9-172">If ADAL is not able tooreturn a token for any reason, it throws an `AdalException`.</span></span>

> [!Note] 
> <span data-ttu-id="b6df9-173">Olá `AuthenticationResult` objeto contém um `tokenCacheStoreItem` objeto que pode ser usado toocollect Olá informações que seu aplicativo pode precisar.</span><span class="sxs-lookup"><span data-stu-id="b6df9-173">hello `AuthenticationResult` object contains a `tokenCacheStoreItem` object that can be used toocollect hello information that your app may need.</span></span> <span data-ttu-id="b6df9-174">Em Olá QuickStart, `tokenCacheStoreItem` é toodetermine usado se a autenticação já foi concluída.</span><span class="sxs-lookup"><span data-stu-id="b6df9-174">In hello QuickStart, `tokenCacheStoreItem` is used toodetermine if authentication is already done.</span></span>
>
>

## <a name="5-build-and-run-hello-application"></a><span data-ttu-id="b6df9-175">5. Compilar e executar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="b6df9-175">5. Build and run hello application</span></span>
<span data-ttu-id="b6df9-176">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="b6df9-176">Congratulations!</span></span> <span data-ttu-id="b6df9-177">Agora você tem um aplicativo do iOS funcional que pode autenticar os usuários, com segurança chamar APIs da Web usando o OAuth 2.0 e obter informações básicas sobre o usuário hello.</span><span class="sxs-lookup"><span data-stu-id="b6df9-177">You now have a working iOS application that can authenticate users, securely call Web APIs by using OAuth 2.0, and get basic information about hello user.</span></span>  <span data-ttu-id="b6df9-178">Se você ainda não fez isso, agora é Olá tempo toopopulate seu locatário com alguns usuários.</span><span class="sxs-lookup"><span data-stu-id="b6df9-178">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span>  <span data-ttu-id="b6df9-179">Inicie o aplicativo do Guia de início rápido e entre com um desses usuários.</span><span class="sxs-lookup"><span data-stu-id="b6df9-179">Start your QuickStart app, and then sign in with one of those users.</span></span>  <span data-ttu-id="b6df9-180">Procure por outros usuários com base em seus UPNs.</span><span class="sxs-lookup"><span data-stu-id="b6df9-180">Search for other users based on their UPN.</span></span>  <span data-ttu-id="b6df9-181">Feche o aplicativo hello e, em seguida, inicie-o novamente.</span><span class="sxs-lookup"><span data-stu-id="b6df9-181">Close hello app, and then start it again.</span></span>  <span data-ttu-id="b6df9-182">Observe que a sessão do usuário Olá permanece intacta.</span><span class="sxs-lookup"><span data-stu-id="b6df9-182">Notice that hello user's session remains intact.</span></span>

<span data-ttu-id="b6df9-183">ADAL torna fácil tooincorporate todos esses recursos comuns de identidade em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b6df9-183">ADAL makes it easy tooincorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="b6df9-184">Cuida de todo o trabalho sujo Olá para você, como gerenciamento de cache, suporte de protocolo OAuth, apresentar Olá usuário toosign uma interface do usuário no e atualizar tokens expirados.</span><span class="sxs-lookup"><span data-stu-id="b6df9-184">It takes care of all hello dirty work for you, like cache management, OAuth protocol support, presenting hello user with a UI toosign in, and refreshing expired tokens.</span></span>  <span data-ttu-id="b6df9-185">Tudo o que você realmente precisa de tooknow é uma única chamada de API, `getToken`.</span><span class="sxs-lookup"><span data-stu-id="b6df9-185">All you really need tooknow is a single API call, `getToken`.</span></span>

<span data-ttu-id="b6df9-186">Para referência, o exemplo hello concluída (sem os valores de configuração) é fornecido em [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="b6df9-186">For reference, hello completed sample (without your configuration values) is provided on [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="b6df9-187">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b6df9-187">Next steps</span></span>
<span data-ttu-id="b6df9-188">Agora você pode mover tooadditional cenários.</span><span class="sxs-lookup"><span data-stu-id="b6df9-188">You can now move on tooadditional scenarios.</span></span>  <span data-ttu-id="b6df9-189">Você pode desejar tootry:</span><span class="sxs-lookup"><span data-stu-id="b6df9-189">You may want tootry:</span></span>

* [<span data-ttu-id="b6df9-190">Proteger uma API Web Node.js com o Azure AD</span><span class="sxs-lookup"><span data-stu-id="b6df9-190">Secure a Node.JS Web API with Azure AD</span></span>](active-directory-devquickstarts-webapi-nodejs.md)
* <span data-ttu-id="b6df9-191">Saiba [como tooenable SSO entre aplicativos no iOS usando o ADAL](active-directory-sso-ios.md)</span><span class="sxs-lookup"><span data-stu-id="b6df9-191">Learn [how tooenable cross-app SSO on iOS using ADAL](active-directory-sso-ios.md)</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

