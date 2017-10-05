---
title: Integrar o Azure AD em um aplicativo iOS | Microsoft Docs
description: Como criar um aplicativo para iOS que se integre ao Azure AD para fazer entrar e que chame as APIs protegidas do Azure AD usando o OAuth.
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
ms.openlocfilehash: 57f465df99ac234466459b8031f61805d8334b59
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-azure-ad-into-an-ios-app"></a><span data-ttu-id="113c1-103">Integrar o Azure AD em um aplicativo iOS</span><span class="sxs-lookup"><span data-stu-id="113c1-103">Integrate Azure AD into an iOS app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> <span data-ttu-id="113c1-104">Experimente a demonstração do nosso novo [portal do desenvolvedor](https://identity.microsoft.com/Docs/iOS) que ajuda você a executar o Azure Active Directory em apenas alguns minutos!</span><span class="sxs-lookup"><span data-stu-id="113c1-104">Try the preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure Active Directory in just a few minutes!</span></span>  <span data-ttu-id="113c1-105">O portal do desenvolvedor orienta você pelo processo de registro de um aplicativo e integração do Azure AD em seu código.</span><span class="sxs-lookup"><span data-stu-id="113c1-105">The developer portal guides you through the process of registering an app and integrating Azure AD into your code.</span></span>  <span data-ttu-id="113c1-106">Quando terminar, você terá um aplicativo simples que pode autenticar os usuários em seu locatário e um back-end que pode aceitar tokens e executar a validação.</span><span class="sxs-lookup"><span data-stu-id="113c1-106">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a backend that can accept tokens and perform validation.</span></span> 
> 
> 

<span data-ttu-id="113c1-107">Para clientes iOS que precisam acessar recursos protegidos, o Azure AD (Azure Active Directory) fornece a biblioteca de autenticação do Active Directory ou ADAL.</span><span class="sxs-lookup"><span data-stu-id="113c1-107">Azure Active Directory (Azure AD) provides the Active Directory Authentication Library, or ADAL, for iOS clients that need to access protected resources.</span></span> <span data-ttu-id="113c1-108">O ADAL simplifica o processo que seu aplicativo usa para obter tokens de acesso.</span><span class="sxs-lookup"><span data-stu-id="113c1-108">ADAL simplifies the process that your app uses to obtain access tokens.</span></span> <span data-ttu-id="113c1-109">Para demonstrar como é fácil, criaremos neste guia um aplicativo de lista de tarefas pendentes Objective-C que:</span><span class="sxs-lookup"><span data-stu-id="113c1-109">To demonstrate how easy it is, in this article we build an Objective C To-Do List application that:</span></span>

* <span data-ttu-id="113c1-110">Obtém tokens de acesso para chamar a API do Graph do Azure AD usando o [protocolo de autenticação OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="113c1-110">Gets access tokens for calling the Azure AD Graph API by using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="113c1-111">Pesquisa um diretório para usuários com um determinado alias.</span><span class="sxs-lookup"><span data-stu-id="113c1-111">Searches a directory for users with a given alias.</span></span>

<span data-ttu-id="113c1-112">Para criar o aplicativo em funcionamento completo, será necessário:</span><span class="sxs-lookup"><span data-stu-id="113c1-112">To build the complete working application, you need to:</span></span>

1. <span data-ttu-id="113c1-113">Registrar seu aplicativo no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="113c1-113">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="113c1-114">Instalar e configurar a ADAL.</span><span class="sxs-lookup"><span data-stu-id="113c1-114">Install and configure ADAL.</span></span>
3. <span data-ttu-id="113c1-115">Usar a ADAL para obter tokens do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="113c1-115">Use ADAL to get tokens from Azure AD.</span></span>

<span data-ttu-id="113c1-116">Para começar, [baixe o esqueleto do aplicativo](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) ou [baixe o exemplo concluído](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="113c1-116">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span> <span data-ttu-id="113c1-117">Você também precisará de um locatário do Azure AD no qual possa criar usuários e registrar um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="113c1-117">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="113c1-118">Se você ainda não tiver um locatário [saiba como obter um](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="113c1-118">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>


> [!TIP]
> <span data-ttu-id="113c1-119">Experimente a versão de visualização de nosso novo [portal do desenvolvedor](https://identity.microsoft.com/Docs/iOS), que ajudará você a executar o Azure AD em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="113c1-119">Try the preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="113c1-120">O portal do desenvolvedor orienta você pelo processo de registro de um aplicativo e integração do Azure AD em seu código.</span><span class="sxs-lookup"><span data-stu-id="113c1-120">The developer portal guides you through the process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="113c1-121">Quando terminar, você terá um aplicativo simples que pode autenticar os usuários em seu locatário e um back-end que pode aceitar tokens e executar a validação.</span><span class="sxs-lookup"><span data-stu-id="113c1-121">When you’re finished, you'll have a simple application that can authenticate users in your tenant, and a back end that can accept tokens and perform validation.</span></span> 
> 
> 

## <a name="1-determine-what-your-redirect-uri-is-for-ios"></a><span data-ttu-id="113c1-122">1. Determine qual é seu URI de redirecionamento para iOS</span><span class="sxs-lookup"><span data-stu-id="113c1-122">1. Determine what your redirect URI is for iOS</span></span>
<span data-ttu-id="113c1-123">Para iniciar com segurança os aplicativos em determinados cenários SSO, você deve criar um *URI de redirecionamento* em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="113c1-123">To securely start your applications in certain SSO scenarios, you must create a *redirect URI* in a particular format.</span></span> <span data-ttu-id="113c1-124">Um URI de redirecionamento é usado para garantir que os tokens retornem para o aplicativo correto que os solicitam.</span><span class="sxs-lookup"><span data-stu-id="113c1-124">A redirect URI is used to ensure that the tokens return to the correct application that asked for them.</span></span>


<span data-ttu-id="113c1-125">O formato do iOS para um URI de redirecionamento é:</span><span class="sxs-lookup"><span data-stu-id="113c1-125">The iOS format for a redirect URI is:</span></span>

```
<app-scheme>://<bundle-id>
```

* <span data-ttu-id="113c1-126">**app-scheme** – isso é registrado no projeto XCode.</span><span class="sxs-lookup"><span data-stu-id="113c1-126">**app-scheme** - This is registered in your XCode project.</span></span> <span data-ttu-id="113c1-127">É como os outros aplicativos podem chamar você.</span><span class="sxs-lookup"><span data-stu-id="113c1-127">It is how other applications can call you.</span></span> <span data-ttu-id="113c1-128">Você pode encontrar isso em Info.plist -> tipos de URL -> identificador de URL.</span><span class="sxs-lookup"><span data-stu-id="113c1-128">You can find this under Info.plist -> URL types -> URL Identifier.</span></span> <span data-ttu-id="113c1-129">Você deve criar um se você ainda não tiver um ou mais configurados.</span><span class="sxs-lookup"><span data-stu-id="113c1-129">You should create one if you don't already have one or more configured.</span></span>
* <span data-ttu-id="113c1-130">**bundle-id** - esse é o identificador de pacote localizado em "identidade" nas configurações do seu projeto no XCode.</span><span class="sxs-lookup"><span data-stu-id="113c1-130">**bundle-id** - This is the Bundle Identifier found under "identity" un your project settings in XCode.</span></span>

<span data-ttu-id="113c1-131">Um exemplo para este código de Início Rápido é: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***</span><span class="sxs-lookup"><span data-stu-id="113c1-131">An example for this QuickStart code: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***</span></span>

## <a name="2-register-the-directorysearcher-application"></a><span data-ttu-id="113c1-132">2. Registrar o aplicativo DirectorySearcher</span><span class="sxs-lookup"><span data-stu-id="113c1-132">2. Register the DirectorySearcher application</span></span>
<span data-ttu-id="113c1-133">Para configurar o aplicativo para obter tokens, primeiro será necessário registrá-lo no seu locatário do Azure AD e conceder permissão para acessar a API do Graph do Azure AD:</span><span class="sxs-lookup"><span data-stu-id="113c1-133">To set up your app to get tokens, you first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API:</span></span>

1. <span data-ttu-id="113c1-134">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="113c1-134">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="113c1-135">Na barra superior, clique em sua conta.</span><span class="sxs-lookup"><span data-stu-id="113c1-135">On the top bar, click your account.</span></span> <span data-ttu-id="113c1-136">Sob o **diretório** , escolha onde você deseja registrar seu aplicativo de locatário do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="113c1-136">Under the **Directory** list, choose the Active Directory tenant where you want to register your application.</span></span>
3. <span data-ttu-id="113c1-137">Clique em **Mais Serviços** no painel de navegação mais à esquerda e selecione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="113c1-137">Click **More Services** in the leftmost navigation pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="113c1-138">Clique em **Registros do aplicativo**e, em seguida, selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="113c1-138">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="113c1-139">Siga os prompts para criar um novo **Aplicativo Cliente Nativo**.</span><span class="sxs-lookup"><span data-stu-id="113c1-139">Follow the prompts to create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="113c1-140">O **Nome** do aplicativo descreve o seu aplicativo aos usuários finais.</span><span class="sxs-lookup"><span data-stu-id="113c1-140">The **Name** of the application describes your application to end users.</span></span>
  * <span data-ttu-id="113c1-141">O **URI de redirecionamento** é uma combinação de esquema e de cadeia de caracteres que o Azure AD usa para retornar respostas de tokens.</span><span class="sxs-lookup"><span data-stu-id="113c1-141">The **Redirect Uri** is a scheme and string combination that Azure AD uses to return token responses.</span></span>  <span data-ttu-id="113c1-142">Insira um valor específico para seu aplicativo e baseado nas informações de URI de redirecionamento anteriores.</span><span class="sxs-lookup"><span data-stu-id="113c1-142">Enter a value that is specific to your application and is based on the previous redirect URI information.</span></span>
6. <span data-ttu-id="113c1-143">Depois de você concluir o registro, o Azure AD atribui uma ID do aplicativo exclusiva ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="113c1-143">After you've completed the registration, Azure AD assigns your app a unique application ID.</span></span>  <span data-ttu-id="113c1-144">Você precisará desse valor nas próximas seções, portanto, copie-o da guia do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="113c1-144">You'll need this value in the next sections, so copy it from the application tab.</span></span>
7. <span data-ttu-id="113c1-145">Na página **Configurações**, selecione **Permissões Necessárias** e escolha **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="113c1-145">From the **Settings** page, select **Required Permissions** and then select **Add**.</span></span> <span data-ttu-id="113c1-146">Escolha o **Microsoft Graph** como a API e adicione a permissão **Ler Dados do Diretório** em **Permissões Delegadas**.</span><span class="sxs-lookup"><span data-stu-id="113c1-146">Select **Microsoft Graph** as the API, and then add the **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="113c1-147">Isso permitirá que o aplicativo consulte a API do Graph do Azure AD para os usuários.</span><span class="sxs-lookup"><span data-stu-id="113c1-147">This sets up your application to query the Azure AD Graph API for users.</span></span>

## <a name="3-install-and-configure-adal"></a><span data-ttu-id="113c1-148">3. Instalar e configurar a ADAL</span><span class="sxs-lookup"><span data-stu-id="113c1-148">3. Install and configure ADAL</span></span>
<span data-ttu-id="113c1-149">Agora que você tem um aplicativo no AD do Azure, você pode instalar a ADAL e escrever seu código relacionado à identidade.</span><span class="sxs-lookup"><span data-stu-id="113c1-149">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="113c1-150">Para que a ADAL possa se comunicar com o Azure AD, é necessário fornecer a ela algumas informações sobre o registro do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="113c1-150">For ADAL to communicate with Azure AD, you need to provide it with some information about your app registration.</span></span>

1. <span data-ttu-id="113c1-151">Inicie adicionando a ADAL ao projeto DirectorySearcher usando o CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="113c1-151">Begin by adding ADAL to the DirectorySearcher project by using CocoaPods.</span></span>

    ```
    $ vi Podfile
    ```
2. <span data-ttu-id="113c1-152">Adicione o seguinte a esse podfile:</span><span class="sxs-lookup"><span data-stu-id="113c1-152">Add the following to this podfile:</span></span>

    ```
    source 'https://github.com/CocoaPods/Specs.git'
    link_with ['QuickStart']
    xcodeproj 'QuickStart'

    pod 'ADALiOS'
    ```

3. <span data-ttu-id="113c1-153">Carregue o podfile usando o CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="113c1-153">Now load the podfile by using CocoaPods.</span></span> <span data-ttu-id="113c1-154">Esta etapa cria um novo espaço de trabalho do XCode que você carrega.</span><span class="sxs-lookup"><span data-stu-id="113c1-154">This step creates a new XCode workspace that you load.</span></span>

    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

4. <span data-ttu-id="113c1-155">No projeto do Guia de início rápido, abra o arquivo plist `settings.plist`.</span><span class="sxs-lookup"><span data-stu-id="113c1-155">In the QuickStart project, open the plist file `settings.plist`.</span></span>  <span data-ttu-id="113c1-156">Substitua os valores dos elementos na seção para refletir os valores que você inseriu no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="113c1-156">Replace the values of the elements in the section to reflect the values that you entered in the Azure portal.</span></span> <span data-ttu-id="113c1-157">Seu código faz referência a esses valores sempre que ele usar a ADAL.</span><span class="sxs-lookup"><span data-stu-id="113c1-157">Your code references these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="113c1-158">O `tenant` é o domínio do seu locatário do Azure AD, por exemplo, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="113c1-158">The `tenant` is the domain of your Azure AD tenant, for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="113c1-159">O `clientId` é a ID do cliente do seu aplicativo que você copiou do portal.</span><span class="sxs-lookup"><span data-stu-id="113c1-159">The `clientId` is the client ID of your application that you copied from the portal.</span></span>
  * <span data-ttu-id="113c1-160">O `redirectUri` é a URL de redirecionamento que você registrou no portal.</span><span class="sxs-lookup"><span data-stu-id="113c1-160">The `redirectUri` is the redirect URL that you registered in the portal.</span></span>

## <a name="4----use-adal-to-get-tokens-from-azure-ad"></a><span data-ttu-id="113c1-161">4.    Usar a ADAL para obter tokens do Azure AD</span><span class="sxs-lookup"><span data-stu-id="113c1-161">4.    Use ADAL to get tokens from Azure AD</span></span>
<span data-ttu-id="113c1-162">O princípio básico da ADAL é que sempre que seu aplicativo precisar de um token de acesso, ele simplesmente chama um completionBlock `+(void) getToken : `, e a ADAL faz o resto.</span><span class="sxs-lookup"><span data-stu-id="113c1-162">The basic principle behind ADAL is that whenever your app needs an access token, it simply calls a completionBlock `+(void) getToken : `, and ADAL does the rest.</span></span>  

1. <span data-ttu-id="113c1-163">No projeto `QuickStart`, abra `GraphAPICaller.m` e localize o comentário `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` perto da parte de cima.</span><span class="sxs-lookup"><span data-stu-id="113c1-163">In the `QuickStart` project, open `GraphAPICaller.m` and locate the `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` comment near the top.</span></span>  <span data-ttu-id="113c1-164">É aqui que você passa à ADAL as coordenadas necessárias, por um CompletionBlock, para se comunicar com o Azure AD e informar a ele como armazenar tokens em cache.</span><span class="sxs-lookup"><span data-stu-id="113c1-164">This is where you pass ADAL the coordinates through a CompletionBlock, to communicate with Azure AD, and tell it how to cache tokens.</span></span>

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
                        extraQueryParameters: @"nux=1" // if this strikes you as strange it was legacy to display the correct mobile UX. You most likely won't need it in your code.
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

2. <span data-ttu-id="113c1-165">Agora, precisamos usar esse token para pesquisar usuários no gráfico.</span><span class="sxs-lookup"><span data-stu-id="113c1-165">Now we need to use this token to search for users in the graph.</span></span> <span data-ttu-id="113c1-166">Encontre o comentário `// TODO: implement SearchUsersList`.</span><span class="sxs-lookup"><span data-stu-id="113c1-166">Find the `// TODO: implement SearchUsersList` comment.</span></span> <span data-ttu-id="113c1-167">Esse método faz uma solicitação GET para que a Graph API do AD do Azure procure por usuários cujo UPN começa com o termo de pesquisa fornecido.</span><span class="sxs-lookup"><span data-stu-id="113c1-167">This method makes a GET request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span>  <span data-ttu-id="113c1-168">Para consultar a API do Graph do Azure AD, você precisa incluir um access_token no cabeçalho `Authorization` da solicitação.</span><span class="sxs-lookup"><span data-stu-id="113c1-168">To query the Azure AD Graph API, you need to include an access_token in the `Authorization` header of the request.</span></span> <span data-ttu-id="113c1-169">É aí que a ADAL entra em cena.</span><span class="sxs-lookup"><span data-stu-id="113c1-169">This is where ADAL comes in.</span></span>

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

                         // We can grab the JSON node at the top to get our graph data.
                         NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                         // Don't be thrown off by the key name being "value". It really is the name of the
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


3. <span data-ttu-id="113c1-170">Quando o aplicativo solicita um token chamando `getToken(...)`, a ADAL tenta retornar um token sem pedir as credenciais ao usuário.</span><span class="sxs-lookup"><span data-stu-id="113c1-170">When your app requests a token by calling `getToken(...)`, ADAL attempts to return a token without asking the user for credentials.</span></span>  <span data-ttu-id="113c1-171">Se a ADAL determina que o usuário precisa entrar para obter um token, ela exibirá uma caixa de diálogo para entrada, coletará as credenciais do usuário e retornará um token após uma autenticação bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="113c1-171">If ADAL determines that the user needs to sign in to get a token, it will display a dialog box for sign-in, collect the user's credentials, and then return a token after successful authentication.</span></span>  <span data-ttu-id="113c1-172">Se a ADAL não puder retornar um token por qualquer motivo, ela lançará um `AdalException`.</span><span class="sxs-lookup"><span data-stu-id="113c1-172">If ADAL is not able to return a token for any reason, it throws an `AdalException`.</span></span>

> [!Note] 
> <span data-ttu-id="113c1-173">O objeto `AuthenticationResult` contém um objeto `tokenCacheStoreItem` que pode ser usado para coletar as informações de que seu aplicativo pode precisar.</span><span class="sxs-lookup"><span data-stu-id="113c1-173">The `AuthenticationResult` object contains a `tokenCacheStoreItem` object that can be used to collect the information that your app may need.</span></span> <span data-ttu-id="113c1-174">No Guia de Início Rápido, `tokenCacheStoreItem` é usado para determinar se a autenticação já ocorreu.</span><span class="sxs-lookup"><span data-stu-id="113c1-174">In the QuickStart, `tokenCacheStoreItem` is used to determine if authentication is already done.</span></span>
>
>

## <a name="5-build-and-run-the-application"></a><span data-ttu-id="113c1-175">5. Compile e execute o aplicativo</span><span class="sxs-lookup"><span data-stu-id="113c1-175">5. Build and run the application</span></span>
<span data-ttu-id="113c1-176">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="113c1-176">Congratulations!</span></span> <span data-ttu-id="113c1-177">Agora você tem um aplicativo iOS que tem a capacidade de autenticar usuários, chamar APIs Web com segurança usando OAuth 2.0 e obter informações básicas sobre o usuário.</span><span class="sxs-lookup"><span data-stu-id="113c1-177">You now have a working iOS application that can authenticate users, securely call Web APIs by using OAuth 2.0, and get basic information about the user.</span></span>  <span data-ttu-id="113c1-178">Se você ainda não fez isso, agora é o momento de preencher seu locatário com alguns usuários.</span><span class="sxs-lookup"><span data-stu-id="113c1-178">If you haven't already, now is the time to populate your tenant with some users.</span></span>  <span data-ttu-id="113c1-179">Inicie o aplicativo do Guia de início rápido e entre com um desses usuários.</span><span class="sxs-lookup"><span data-stu-id="113c1-179">Start your QuickStart app, and then sign in with one of those users.</span></span>  <span data-ttu-id="113c1-180">Procure por outros usuários com base em seus UPNs.</span><span class="sxs-lookup"><span data-stu-id="113c1-180">Search for other users based on their UPN.</span></span>  <span data-ttu-id="113c1-181">Feche o aplicativo e, em seguida, inicie-o novamente.</span><span class="sxs-lookup"><span data-stu-id="113c1-181">Close the app, and then start it again.</span></span>  <span data-ttu-id="113c1-182">Observe que a sessão do usuário permanece intacta.</span><span class="sxs-lookup"><span data-stu-id="113c1-182">Notice that the user's session remains intact.</span></span>

<span data-ttu-id="113c1-183">A ADAL facilita a incorporar todos esses recursos comuns de identidade em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="113c1-183">ADAL makes it easy to incorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="113c1-184">Ele se encarrega de todo o trabalho difícil para você, por exemplo, gerenciamento de cache, suporte a protocolo OAuth, apresentação de uma interface do usuário de entrada ao usuário e atualização de tokens expirados.</span><span class="sxs-lookup"><span data-stu-id="113c1-184">It takes care of all the dirty work for you, like cache management, OAuth protocol support, presenting the user with a UI to sign in, and refreshing expired tokens.</span></span>  <span data-ttu-id="113c1-185">Tudo o que você realmente precisa saber é uma única chamada à API, `getToken`.</span><span class="sxs-lookup"><span data-stu-id="113c1-185">All you really need to know is a single API call, `getToken`.</span></span>

<span data-ttu-id="113c1-186">Para referência, o exemplo concluído (sem seus valores de configuração) é fornecido no [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="113c1-186">For reference, the completed sample (without your configuration values) is provided on [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="113c1-187">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="113c1-187">Next steps</span></span>
<span data-ttu-id="113c1-188">Agora você pode passar para cenários de adicionais.</span><span class="sxs-lookup"><span data-stu-id="113c1-188">You can now move on to additional scenarios.</span></span>  <span data-ttu-id="113c1-189">Você pode desejar experimentar:</span><span class="sxs-lookup"><span data-stu-id="113c1-189">You may want to try:</span></span>

* [<span data-ttu-id="113c1-190">Proteger uma API Web Node.js com o Azure AD</span><span class="sxs-lookup"><span data-stu-id="113c1-190">Secure a Node.JS Web API with Azure AD</span></span>](active-directory-devquickstarts-webapi-nodejs.md)
* <span data-ttu-id="113c1-191">Saiba [como habilitar o SSO entre aplicativos no iOS usando a ADAL](active-directory-sso-ios.md)</span><span class="sxs-lookup"><span data-stu-id="113c1-191">Learn [how to enable cross-app SSO on iOS using ADAL](active-directory-sso-ios.md)</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

