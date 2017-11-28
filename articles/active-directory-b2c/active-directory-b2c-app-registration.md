---
title: 'Azure Active Directory B2C: registro de aplicativos | Microsoft Docs'
description: Como tooregister seu aplicativo com o Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: PatAltimore
ms.assetid: 20e92275-b25d-45dd-9090-181a60c99f69
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/13/2017
ms.author: parakhj
ms.openlocfilehash: bd58e123751db387d6c8f16bd010291ba698b1a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-register-your-application"></a><span data-ttu-id="5807b-103">Azure Active Directory B2C: registrar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="5807b-103">Azure Active Directory B2C: Register your application</span></span>

<span data-ttu-id="5807b-104">Este Guia de início rápido ajuda você a registrar um aplicativo em um locatário do Microsoft Azure Active Directory (Azure AD) B2C em poucos minutos.</span><span class="sxs-lookup"><span data-stu-id="5807b-104">This Quickstart helps you register an application in a Microsoft Azure Active Directory (Azure AD) B2C tenant in a few minutes.</span></span> <span data-ttu-id="5807b-105">Quando você terminar, seu aplicativo está registrado para uso no locatário Olá B2C do Azure.</span><span class="sxs-lookup"><span data-stu-id="5807b-105">When you're finished, your application is registered for use in hello Azure B2C tenant.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5807b-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5807b-106">Prerequisites</span></span>

<span data-ttu-id="5807b-107">toobuild um aplicativo que aceita o consumidor Inscreva-se e entrar, você precisa primeiro aplicativo de hello tooregister com um locatário do Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="5807b-107">toobuild an application that accepts consumer sign-up and sign-in, you first need tooregister hello application with an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="5807b-108">Obter seu próprio locatário usando Olá etapas descritas em [criar um locatário Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5807b-108">Get your own tenant by using hello steps outlined in [Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

<span data-ttu-id="5807b-109">Os aplicativos criados na folha de saudação do Azure AD B2C em Olá portal do Azure devem ser gerenciados da saudação mesmo local.</span><span class="sxs-lookup"><span data-stu-id="5807b-109">Applications created from hello Azure AD B2C blade in hello Azure portal must be managed from hello same location.</span></span> <span data-ttu-id="5807b-110">Se você editar aplicativos de B2C hello usando o PowerShell ou outro portal, eles se tornam sem suporte e não funcionam com o Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="5807b-110">If you edit hello B2C applications using PowerShell or another portal, they become unsupported and do not work with Azure AD B2C.</span></span> <span data-ttu-id="5807b-111">Consulte os detalhes em Olá [falha aplicativos](#faulted-apps) seção.</span><span class="sxs-lookup"><span data-stu-id="5807b-111">See details in hello [faulted apps](#faulted-apps) section.</span></span> 

## <a name="navigate-toob2c-settings"></a><span data-ttu-id="5807b-112">Navegue tooB2C configurações</span><span class="sxs-lookup"><span data-stu-id="5807b-112">Navigate tooB2C settings</span></span>

<span data-ttu-id="5807b-113">Faça logon no toohello [portal do Azure](https://portal.azure.com/) como Olá Administrador Global do locatário Olá B2C.</span><span class="sxs-lookup"><span data-stu-id="5807b-113">Log in toohello [Azure portal](https://portal.azure.com/) as hello Global Administrator of hello B2C tenant.</span></span> 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../../includes/active-directory-b2c-switch-b2c-tenant.md)]

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](../../includes/active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="5807b-114">Escolha as próximas etapas com base no tipo de aplicativo hello que está sendo registrado:</span><span class="sxs-lookup"><span data-stu-id="5807b-114">Choose next steps based on hello application type you are registering:</span></span>

* [<span data-ttu-id="5807b-115">Registrar um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="5807b-115">Register a web application</span></span>](#register-a-web-app)
* [<span data-ttu-id="5807b-116">Registrar uma API Web</span><span class="sxs-lookup"><span data-stu-id="5807b-116">Register a web API</span></span>](#register-a-web-api)
* [<span data-ttu-id="5807b-117">Registrar um aplicativo móvel ou nativo</span><span class="sxs-lookup"><span data-stu-id="5807b-117">Register a mobile or native application</span></span>](#register-a-mobile-or-native-app)
 
## <a name="register-a-web-app"></a><span data-ttu-id="5807b-118">Registrar um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="5807b-118">Register a web app</span></span>

[!INCLUDE [active-directory-b2c-register-web-app](../../includes/active-directory-b2c-register-web-app.md)]

<span data-ttu-id="5807b-119">Se o aplicativo Web chamar uma API da Web protegida pelo Azure AD B2C, execute estas etapas:</span><span class="sxs-lookup"><span data-stu-id="5807b-119">If your web application calls a web API secured by Azure AD B2C, perform these steps:</span></span>
   1. <span data-ttu-id="5807b-120">Criar um segredo do aplicativo, vai toohello **chaves** folha e clicando em Olá **gerar chave** botão.</span><span class="sxs-lookup"><span data-stu-id="5807b-120">Create an application secret by going toohello **Keys** blade and clicking hello **Generate Key** button.</span></span> <span data-ttu-id="5807b-121">Anote Olá **chave do aplicativo** valor.</span><span class="sxs-lookup"><span data-stu-id="5807b-121">Make note of hello **App key** value.</span></span> <span data-ttu-id="5807b-122">Valor de saudação é usado como o segredo do aplicativo hello no código do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5807b-122">You use hello value as hello application secret in your application's code.</span></span>
   2. <span data-ttu-id="5807b-123">Clique em **Acesso à API**, clique em **Adicionar** e selecione sua API da Web e escopos (permissões).</span><span class="sxs-lookup"><span data-stu-id="5807b-123">Click **API Access**, click **Add**, and select your web API and scopes (permissions).</span></span>

> [!NOTE]
> <span data-ttu-id="5807b-124">Um **Segredo de Aplicativo** é uma credencial de segurança importante e deve ser protegido adequadamente.</span><span class="sxs-lookup"><span data-stu-id="5807b-124">An **Application Secret** is an important security credential, and should be secured appropriately.</span></span>
> 

[<span data-ttu-id="5807b-125">Saltar muito**próximas etapas**</span><span class="sxs-lookup"><span data-stu-id="5807b-125">Jump too**next steps**</span></span>](#next-steps)

## <a name="register-a-web-api"></a><span data-ttu-id="5807b-126">Registrar uma API Web</span><span class="sxs-lookup"><span data-stu-id="5807b-126">Register a web API</span></span>

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

<span data-ttu-id="5807b-127">Clique em **publicado escopos** tooadd mais escopos conforme o necessário.</span><span class="sxs-lookup"><span data-stu-id="5807b-127">Click **Published scopes** tooadd more scopes as necessary.</span></span> <span data-ttu-id="5807b-128">Por padrão, o escopo de "user_impersonation" hello é definido.</span><span class="sxs-lookup"><span data-stu-id="5807b-128">By default, hello "user_impersonation" scope is defined.</span></span> <span data-ttu-id="5807b-129">o escopo user_impersonation Olá fornece tooaccess de capacidade de saudação outros aplicativos essa api em nome do usuário conectado do hello.</span><span class="sxs-lookup"><span data-stu-id="5807b-129">hello user_impersonation scope gives other applications hello ability tooaccess this api on behalf of hello signed-in user.</span></span> <span data-ttu-id="5807b-130">Se desejar, o escopo user_impersonation Olá pode ser removido.</span><span class="sxs-lookup"><span data-stu-id="5807b-130">If you wish, hello user_impersonation scope can be removed.</span></span>

[<span data-ttu-id="5807b-131">Saltar muito**próximas etapas**</span><span class="sxs-lookup"><span data-stu-id="5807b-131">Jump too**next steps**</span></span>](#next-steps)

## <a name="register-a-mobile-or-native-app"></a><span data-ttu-id="5807b-132">Registrar um aplicativo móvel ou nativo</span><span class="sxs-lookup"><span data-stu-id="5807b-132">Register a mobile or native app</span></span>

[!INCLUDE [active-directory-b2c-register-mobile-native-app](../../includes/active-directory-b2c-register-mobile-native-app.md)]

[<span data-ttu-id="5807b-133">Saltar muito**próximas etapas**</span><span class="sxs-lookup"><span data-stu-id="5807b-133">Jump too**next steps**</span></span>](#next-steps)

## <a name="limitations"></a><span data-ttu-id="5807b-134">Limitações</span><span class="sxs-lookup"><span data-stu-id="5807b-134">Limitations</span></span>

### <a name="choosing-a-web-app-or-api-reply-url"></a><span data-ttu-id="5807b-135">Escolher aplicativo Web ou URL de resposta da API</span><span class="sxs-lookup"><span data-stu-id="5807b-135">Choosing a web app or api reply URL</span></span>

<span data-ttu-id="5807b-136">Atualmente, os aplicativos que são registrados com o Azure AD B2C são conjunto restrito tooa limitado de valores da URL de resposta.</span><span class="sxs-lookup"><span data-stu-id="5807b-136">Currently, apps that are registered with Azure AD B2C are restricted tooa limited set of reply URL values.</span></span> <span data-ttu-id="5807b-137">Olá resposta URL para serviços e aplicativos web deve começar com o esquema de saudação `https`, e respondam a todos os valores da URL devem compartilhar um único domínio DNS.</span><span class="sxs-lookup"><span data-stu-id="5807b-137">hello reply URL for web apps and services must begin with hello scheme `https`, and all reply URL values must share a single DNS domain.</span></span> <span data-ttu-id="5807b-138">Por exemplo, você não pode registrar um aplicativo Web que tenha uma destas URLs de resposta:</span><span class="sxs-lookup"><span data-stu-id="5807b-138">For example, you cannot register a web app that has one of these reply URLs:</span></span>

`https://login-east.contoso.com`

`https://login-west.contoso.com`

<span data-ttu-id="5807b-139">sistema de registro de saudação compara Olá todo DNS nome de saudação existente resposta URL toohello DNS Olá da URL de resposta que você está adicionando.</span><span class="sxs-lookup"><span data-stu-id="5807b-139">hello registration system compares hello whole DNS name of hello existing reply URL toohello DNS name of hello reply URL that you are adding.</span></span> <span data-ttu-id="5807b-140">Olá tooadd da solicitação Olá nome DNS falhará se uma saudação seguintes condições for verdadeira:</span><span class="sxs-lookup"><span data-stu-id="5807b-140">hello request tooadd hello DNS name fails if either of hello following conditions is true:</span></span>

* <span data-ttu-id="5807b-141">nome DNS todo Olá Olá novo da URL de resposta não coincide com nome DNS Olá Olá existente da URL de resposta.</span><span class="sxs-lookup"><span data-stu-id="5807b-141">hello whole DNS name of hello new reply URL does not match hello DNS name of hello existing reply URL.</span></span>
* <span data-ttu-id="5807b-142">nome DNS todo Olá Olá novo da URL de resposta não é um subdomínio Olá existente da URL de resposta.</span><span class="sxs-lookup"><span data-stu-id="5807b-142">hello whole DNS name of hello new reply URL is not a subdomain of hello existing reply URL.</span></span>

<span data-ttu-id="5807b-143">Por exemplo, se hello aplicativo tem essa URL de resposta:</span><span class="sxs-lookup"><span data-stu-id="5807b-143">For example, if hello app has this reply URL:</span></span>

`https://login.contoso.com`

<span data-ttu-id="5807b-144">Você pode adicionar tooit, como este:</span><span class="sxs-lookup"><span data-stu-id="5807b-144">You can add tooit, like this:</span></span>

`https://login.contoso.com/new`

<span data-ttu-id="5807b-145">Nesse caso, o nome DNS de saudação corresponder exatamente.</span><span class="sxs-lookup"><span data-stu-id="5807b-145">In this case, hello DNS name matches exactly.</span></span> <span data-ttu-id="5807b-146">Ou você pode fazer isto:</span><span class="sxs-lookup"><span data-stu-id="5807b-146">Or, you can do this:</span></span>

`https://new.login.contoso.com`

<span data-ttu-id="5807b-147">Nesse caso, você está fazendo referência tooa subdomínio DNS de login.contoso.com. Se você quiser toohave um aplicativo que tenha o logon east.contoso.com e west.contoso.com logon como responder a URLs, você deve adicionar as URLs de resposta nesta ordem:</span><span class="sxs-lookup"><span data-stu-id="5807b-147">In this case, you're referring tooa DNS subdomain of login.contoso.com. If you want toohave an app that has login-east.contoso.com and login-west.contoso.com as reply URLs, you must add those reply URLs in this order:</span></span>

`https://contoso.com`

`https://login-east.contoso.com`

`https://login-west.contoso.com`

<span data-ttu-id="5807b-148">Você pode adicionar Olá dois últimos porque eles são subdomínios Olá primeiro da URL de resposta, contoso.com.</span><span class="sxs-lookup"><span data-stu-id="5807b-148">You can add hello latter two because they are subdomains of hello first reply URL, contoso.com.</span></span>

### <a name="choosing-a-native-app-redirect-uri"></a><span data-ttu-id="5807b-149">Escolher um URI de redirecionamento do aplicativo nativo</span><span class="sxs-lookup"><span data-stu-id="5807b-149">Choosing a native app redirect URI</span></span>

<span data-ttu-id="5807b-150">Há duas considerações importantes ao escolher um URI de redirecionamento para aplicativos móveis/nativo:</span><span class="sxs-lookup"><span data-stu-id="5807b-150">There are two important considerations when choosing a redirect URI for mobile/native applications:</span></span>

* <span data-ttu-id="5807b-151">**Exclusivo**: esquema de saudação do URI de redirecionamento Olá deve ser exclusiva para cada aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5807b-151">**Unique**: hello scheme of hello redirect URI should be unique for every application.</span></span> <span data-ttu-id="5807b-152">Em nosso exemplo (com.onmicrosoft.contoso.appname://redirect/path), usamos com.onmicrosoft.contoso.appname como esquema de saudação.</span><span class="sxs-lookup"><span data-stu-id="5807b-152">In our example (com.onmicrosoft.contoso.appname://redirect/path), we use com.onmicrosoft.contoso.appname as hello scheme.</span></span> <span data-ttu-id="5807b-153">É recomendável seguir esse padrão.</span><span class="sxs-lookup"><span data-stu-id="5807b-153">We recommend following this pattern.</span></span> <span data-ttu-id="5807b-154">Se dois aplicativos compartilharem Olá mesmo esquema, hello usuário vê uma caixa de diálogo "Escolha o aplicativo".</span><span class="sxs-lookup"><span data-stu-id="5807b-154">If two applications share hello same scheme, hello user sees a "choose app" dialog.</span></span> <span data-ttu-id="5807b-155">Se o usuário Olá faz uma escolha incorreta, falha de logon de saudação.</span><span class="sxs-lookup"><span data-stu-id="5807b-155">If hello user makes an incorrect choice, hello login fails.</span></span>
* <span data-ttu-id="5807b-156">**Completo**: o URI de redirecionamento deve ter um esquema e um caminho.</span><span class="sxs-lookup"><span data-stu-id="5807b-156">**Complete**: Redirect URI must have a scheme and a path.</span></span> <span data-ttu-id="5807b-157">caminho de saudação deve conter pelo menos uma barra invertida após domínio hello (por exemplo, //contoso/ funciona e //contoso falhar).</span><span class="sxs-lookup"><span data-stu-id="5807b-157">hello path must contain at least one forward slash after hello domain (for example, //contoso/ works and //contoso fails).</span></span>

<span data-ttu-id="5807b-158">Verifique se que há sem caracteres especiais, como o uri de redirecionamento sublinhados em hello.</span><span class="sxs-lookup"><span data-stu-id="5807b-158">Ensure there are no special characters like underscores in hello redirect uri.</span></span>

### <a name="faulted-apps"></a><span data-ttu-id="5807b-159">Aplicativos com falha</span><span class="sxs-lookup"><span data-stu-id="5807b-159">Faulted apps</span></span>

<span data-ttu-id="5807b-160">Os aplicativos B2C NÃO devem ser editados:</span><span class="sxs-lookup"><span data-stu-id="5807b-160">B2C applications should NOT be edited:</span></span>

* <span data-ttu-id="5807b-161">Em outros portais de gerenciamento de aplicativo, como o [portal clássico do Azure](https://manage.windowsazure.com/) e o [Portal de Registro de Aplicativo](https://apps.dev.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="5807b-161">On other application management portals such as the [Azure classic portal](https://manage.windowsazure.com/) & the [Application Registration Portal](https://apps.dev.microsoft.com/).</span></span>
* <span data-ttu-id="5807b-162">Uso da API do Graph ou do PowerShell</span><span class="sxs-lookup"><span data-stu-id="5807b-162">Using Graph API or PowerShell</span></span>

<span data-ttu-id="5807b-163">Se você editar o aplicativo hello B2C conforme descrito acima e tente tooedit-la novamente na folha de recursos de saudação do Azure AD B2C em Olá portal do Azure, torna-se um aplicativo com falha e o aplicativo não será mais utilizável com o Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="5807b-163">If you edit hello B2C application as described above and try tooedit it again in hello Azure AD B2C features blade on hello Azure portal, it becomes a faulted app, and your application is no longer usable with Azure AD B2C.</span></span> <span data-ttu-id="5807b-164">Você tem o aplicativo hello de toodelete e criá-la novamente.</span><span class="sxs-lookup"><span data-stu-id="5807b-164">You have toodelete hello application and create it again.</span></span>

<span data-ttu-id="5807b-165">toodelete Olá aplicativo, vá toohello [Portal de registro de aplicativo](https://apps.dev.microsoft.com/) e excluir o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="5807b-165">toodelete hello app, go toohello [Application Registration Portal](https://apps.dev.microsoft.com/) and delete hello application there.</span></span> <span data-ttu-id="5807b-166">Para toobe de aplicativo hello visível, é necessário toobe proprietário de saudação do aplicativo hello (e não apenas um administrador de locatário Olá).</span><span class="sxs-lookup"><span data-stu-id="5807b-166">In order for hello application toobe visible, you need toobe hello owner of hello application (and not just an admin of hello tenant).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5807b-167">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5807b-167">Next steps</span></span>

<span data-ttu-id="5807b-168">Agora que você tem um aplicativo registrado com o Azure AD B2C, você pode executar uma das [nossos tutoriais de início rápido](active-directory-b2c-overview.md#get-started) tooget em funcionamento.</span><span class="sxs-lookup"><span data-stu-id="5807b-168">Now that you have an application registered with Azure AD B2C, you can complete one of [our quick-start tutorials](active-directory-b2c-overview.md#get-started) tooget up and running.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5807b-169">Criar um aplicativo Web ASP.NET com inscrição, entrada e redefinição de senha</span><span class="sxs-lookup"><span data-stu-id="5807b-169">Create an ASP.NET web app with sign-up, sign-in, and password reset</span></span>](active-directory-b2c-devquickstarts-web-dotnet-susi.md)