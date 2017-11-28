---
title: aaaAzure B2C do Active Directory | Microsoft Docs
description: "Como o perfil toobuild um aplicativo web que tem inscrição-o/entrar, editar e redefinição de senha usando o Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: barbaraselden
ms.assetid: 30261336-d7a5-4a6d-8c1a-7943ad76ed25
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: 187f99a8dd50d212de4f0517f552cdbbe5a8edf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-web-app-with-azure-active-directory-b2c-sign-up-sign-in-profile-edit-and-password-reset"></a><span data-ttu-id="cb921-103">Criar um aplicativo Web ASP.NET com inscrição/entrada, edição de perfil e redefinição de senha do Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="cb921-103">Create an ASP.NET web app with Azure Active Directory B2C sign-up, sign-in, profile edit, and password reset</span></span>

<span data-ttu-id="cb921-104">Este tutorial mostra como:</span><span class="sxs-lookup"><span data-stu-id="cb921-104">This tutorial shows you how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cb921-105">Adicionar o aplicativo web do Azure AD B2C identidade recursos tooyour</span><span class="sxs-lookup"><span data-stu-id="cb921-105">Add Azure AD B2C identity features tooyour web app</span></span>
> * <span data-ttu-id="cb921-106">Registrar seu aplicativo Web em seu diretório do Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="cb921-106">Register your web app in your Azure AD B2C directory</span></span>
> * <span data-ttu-id="cb921-107">Criar inscrição/entrada, edição de perfil e política de redefinição de senha de usuário para o seu aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="cb921-107">Create a user sign-up/sign-in, profile edit, and password reset policy for your web app</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb921-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cb921-108">Prerequisites</span></span>

- <span data-ttu-id="cb921-109">Você deve conectar o tooan B2C locatário conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb921-109">You must connect your B2C Tenant tooan Azure account.</span></span> <span data-ttu-id="cb921-110">Você pode criar uma conta gratuita do Azure [aqui](https://azure.microsoft.com/en-us/).</span><span class="sxs-lookup"><span data-stu-id="cb921-110">You can create a free Azure account [here](https://azure.microsoft.com/en-us/).</span></span>
- <span data-ttu-id="cb921-111">Você precisa [Microsoft Visual Studio](https://www.visualstudio.com/) ou semelhantes tooview de programa e modificar o código de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="cb921-111">You need [Microsoft Visual Studio](https://www.visualstudio.com/) or a similar program tooview and modify hello sample code.</span></span>

## <a name="create-an-azure-ad-b2c-directory"></a><span data-ttu-id="cb921-112">Criar um diretório do AD B2C do Azure</span><span class="sxs-lookup"><span data-stu-id="cb921-112">Create an Azure AD B2C directory</span></span>

<span data-ttu-id="cb921-113">Antes de usar AD B2C do Azure, você deve criar um diretório ou locatário.</span><span class="sxs-lookup"><span data-stu-id="cb921-113">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="cb921-114">Um diretório é um contêiner para todos os seus usuários, aplicativos, grupos e muito mais.</span><span class="sxs-lookup"><span data-stu-id="cb921-114">A directory is a container for all your users, apps, groups, and more.</span></span> <span data-ttu-id="cb921-115">Se você ainda não tiver um, crie um diretório B2C antes de prosseguir neste guia.</span><span class="sxs-lookup"><span data-stu-id="cb921-115">If you don't have one already, create a B2C directory before you continue in this guide.</span></span>

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

> [!NOTE]
> 
> <span data-ttu-id="cb921-116">É necessário tooconnect Olá B2C locatário tooyour assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb921-116">You need tooconnect hello B2C Tenant tooyour Azure subscription.</span></span> <span data-ttu-id="cb921-117">Depois de selecionar **criar**, selecione Olá **toomy Link um existente B2C de AD do Azure locatário assinatura do Azure** opção e, em seguida, em Olá **locatário Azure AD B2C** lista suspensa, selecione locatário Olá tooassociate desejado.</span><span class="sxs-lookup"><span data-stu-id="cb921-117">After selecting **Create**, select hello **Link an existing Azure AD B2C Tenant toomy Azure subscription** option, and then in hello **Azure AD B2C Tenant** drop down, select hello tenant you want tooassociate.</span></span>

## <a name="create-and-register-an-application"></a><span data-ttu-id="cb921-118">Criar e registrar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="cb921-118">Create and register an application</span></span>

<span data-ttu-id="cb921-119">Em seguida, você precisa toocreate e registrar o aplicativo hello em seu diretório do B2C.</span><span class="sxs-lookup"><span data-stu-id="cb921-119">Next, you need toocreate and register hello app in your B2C directory.</span></span> <span data-ttu-id="cb921-120">Isso fornece informações que o Azure AD B2C precisa toosecurely se comunicar com seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cb921-120">This provides information that Azure AD B2C needs toosecurely communicate with your app.</span></span> 

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

<span data-ttu-id="cb921-121">Quando você terminar, você terá uma API e um aplicativo nativo nas suas configurações de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cb921-121">When you are done, you will have both an API and a native application in your application settings.</span></span>

## <a name="create-policies-on-your-b2c-tenant"></a><span data-ttu-id="cb921-122">Criar políticas em seu locatário B2C</span><span class="sxs-lookup"><span data-stu-id="cb921-122">Create policies on your B2C tenant</span></span>

<span data-ttu-id="cb921-123">No AD B2C do Azure, cada experiência do usuário é definida por uma [política](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="cb921-123">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="cb921-124">Este exemplo de código contém três experiências de identidade: **inscrição e entrada**, **edição de perfil** e **redefinição de senha**.</span><span class="sxs-lookup"><span data-stu-id="cb921-124">This code sample contains three identity experiences: **sign-up & sign-in**, **profile edit**, and **password reset**.</span></span>  <span data-ttu-id="cb921-125">Você precisa de uma política de toocreate de cada tipo, conforme descrito em Olá [artigo de referência de política](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="cb921-125">You need toocreate one policy of each type, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="cb921-126">Para cada política, ser-se de atributo de nome de exibição tooselect hello ou declaração e toocopy nome hello da política para uso posterior.</span><span class="sxs-lookup"><span data-stu-id="cb921-126">For each policy, be sure tooselect hello Display name attribute or claim, and toocopy down hello name of your policy for later use.</span></span>

### <a name="add-your-identity-providers"></a><span data-ttu-id="cb921-127">Adicionar seus provedores de identidade</span><span class="sxs-lookup"><span data-stu-id="cb921-127">Add your identity providers</span></span>

<span data-ttu-id="cb921-128">Nas configurações, selecione **Provedores de Identidade** e escolha Inscrição do nome de usuário ou Inscrição de email.</span><span class="sxs-lookup"><span data-stu-id="cb921-128">From your settings, select **Identity Providers** and choose Username signup or Email signup.</span></span>

### <a name="create-a-sign-up-and-sign-in-policy"></a><span data-ttu-id="cb921-129">Criar uma política de inscrição e entrada</span><span class="sxs-lookup"><span data-stu-id="cb921-129">Create a sign-up and sign-in policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

### <a name="create-a-profile-editing-policy"></a><span data-ttu-id="cb921-130">Criar uma política de edição de perfil</span><span class="sxs-lookup"><span data-stu-id="cb921-130">Create a profile editing policy</span></span>

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

### <a name="create-a-password-reset-policy"></a><span data-ttu-id="cb921-131">Criar uma política de redefinição de senha</span><span class="sxs-lookup"><span data-stu-id="cb921-131">Create a password reset policy</span></span>

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

<span data-ttu-id="cb921-132">Depois de criar as políticas, você está pronto toobuild seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cb921-132">After you create your policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-sample-code"></a><span data-ttu-id="cb921-133">Baixar o código de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="cb921-133">Download hello sample code</span></span>

<span data-ttu-id="cb921-134">código de saudação para este tutorial é mantido em [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="cb921-134">hello code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="cb921-135">Você pode clonar o exemplo hello executando:</span><span class="sxs-lookup"><span data-stu-id="cb921-135">You can clone hello sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="cb921-136">Depois de baixar o código de exemplo hello, Olá abra o Visual Studio. sln arquivo tooget é iniciado.</span><span class="sxs-lookup"><span data-stu-id="cb921-136">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="cb921-137">o arquivo de solução Olá contém dois projetos: `TaskWebApp` e `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="cb921-137">hello solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="cb921-138">`TaskWebApp`é Olá aplicativo web MVC que Olá usuário interage com.</span><span class="sxs-lookup"><span data-stu-id="cb921-138">`TaskWebApp` is hello MVC web application that hello user interacts with.</span></span> <span data-ttu-id="cb921-139">`TaskService`é a API de web de back-end do aplicativo hello que armazena a lista de tarefas de cada usuário.</span><span class="sxs-lookup"><span data-stu-id="cb921-139">`TaskService` is hello app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="cb921-140">Este artigo discutirá somente Olá `TaskWebApp` aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cb921-140">This article will only discuss hello `TaskWebApp` application.</span></span> <span data-ttu-id="cb921-141">toolearn como toobuild `TaskService` usando o Azure AD B2C, consulte [nosso tutorial de api da web .NET](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="cb921-141">toolearn how toobuild `TaskService` using Azure AD B2C, see [our .NET web api tutorial](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

## <a name="update-code-toouse-your-tenant-and-policies"></a><span data-ttu-id="cb921-142">Atualizar código toouse as políticas e seu locatário</span><span class="sxs-lookup"><span data-stu-id="cb921-142">Update code toouse your tenant and policies</span></span>

<span data-ttu-id="cb921-143">Nosso exemplo é a ID de cliente e as políticas de Olá de toouse configurado do nosso locatário de demonstração.</span><span class="sxs-lookup"><span data-stu-id="cb921-143">Our sample is configured toouse hello policies and client ID of our demo tenant.</span></span> <span data-ttu-id="cb921-144">tooconnect-locatário da própria tooyour, você precisa tooopen `web.config` em Olá `TaskWebApp` do projeto e substituir Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="cb921-144">tooconnect it tooyour own tenant, you need tooopen `web.config` in hello `TaskWebApp` project and replace hello following values:</span></span>

* <span data-ttu-id="cb921-145">`ida:Tenant` pelo nome do locatário</span><span class="sxs-lookup"><span data-stu-id="cb921-145">`ida:Tenant` with your tenant name</span></span>
* <span data-ttu-id="cb921-146">`ida:ClientId` pela ID de aplicativo do aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="cb921-146">`ida:ClientId` with your web app application ID</span></span>
* <span data-ttu-id="cb921-147">`ida:ClientSecret` pela chave de segredo do aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="cb921-147">`ida:ClientSecret` with your web app secret key</span></span>
* <span data-ttu-id="cb921-148">`ida:SignUpSignInPolicyId` pelo nome da política "Inscrever-se ou Entrar"</span><span class="sxs-lookup"><span data-stu-id="cb921-148">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
* <span data-ttu-id="cb921-149">`ida:EditProfilePolicyId` pelo nome de política "Editar Perfil"</span><span class="sxs-lookup"><span data-stu-id="cb921-149">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
* <span data-ttu-id="cb921-150">`ida:ResetPasswordPolicyId` pelo nome de política "Redefinir Senha"</span><span class="sxs-lookup"><span data-stu-id="cb921-150">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>

## <a name="launch-hello-app"></a><span data-ttu-id="cb921-151">Inicie o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="cb921-151">Launch hello app</span></span>
<span data-ttu-id="cb921-152">De dentro do Visual Studio, inicie o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="cb921-152">From within Visual Studio, launch hello app.</span></span> <span data-ttu-id="cb921-153">Navegue toohello guia de lista de tarefas e Olá Observação URl é: https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*& client_id = *YourclientID*...</span><span class="sxs-lookup"><span data-stu-id="cb921-153">Navigate toohello To-Do List tab, and note hello URl is: https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*&client_id=*YourclientID*.....</span></span>

<span data-ttu-id="cb921-154">Inscreva-se para o aplicativo hello usando seu nome de usuário ou endereço de email.</span><span class="sxs-lookup"><span data-stu-id="cb921-154">Sign up for hello app by using your email address or user name.</span></span> <span data-ttu-id="cb921-155">Sair, e entrar novamente e editar o perfil de saudação ou redefinir a senha de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb921-155">Sign out, then sign in again and edit hello profile or reset hello password.</span></span> <span data-ttu-id="cb921-156">Saia e entre como outro usuário.</span><span class="sxs-lookup"><span data-stu-id="cb921-156">Sign out and sign in as a different user.</span></span> 

## <a name="add-social-idps"></a><span data-ttu-id="cb921-157">Adicionar IDPs sociais</span><span class="sxs-lookup"><span data-stu-id="cb921-157">Add social IDPs</span></span>

<span data-ttu-id="cb921-158">Atualmente, o aplicativo hello suporta apenas o usuário se inscrever e entrar usando **contas locais**; contas armazenadas no seu diretório do B2C que usam um nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="cb921-158">Currently, hello app supports only user sign-up and sign-in by using **local accounts**; accounts stored in your B2C directory that use a user name and password.</span></span> <span data-ttu-id="cb921-159">Com o Azure AD B2C, você pode adicionar suporte a outros **provedores de identidade** (IDPs), sem alterar qualquer código.</span><span class="sxs-lookup"><span data-stu-id="cb921-159">By using Azure AD B2C, you can add support for other **identity providers** (IDPs) without changing any of your code.</span></span>

<span data-ttu-id="cb921-160">tooadd social IDPs tooyour aplicativo, comece seguindo Olá detalhadas as instruções neste artigo.</span><span class="sxs-lookup"><span data-stu-id="cb921-160">tooadd social IDPs tooyour app, begin by following hello detailed instructions in these articles.</span></span> <span data-ttu-id="cb921-161">Para cada IDP toosupport desejado, você precisa tooregister um aplicativo no sistema e obter uma ID de cliente.</span><span class="sxs-lookup"><span data-stu-id="cb921-161">For each IDP you want toosupport, you need tooregister an application in that system and obtain a client ID.</span></span>

* [<span data-ttu-id="cb921-162">Configurar o Facebook como um IDP</span><span class="sxs-lookup"><span data-stu-id="cb921-162">Set up Facebook as an IDP</span></span>](active-directory-b2c-setup-fb-app.md)
* [<span data-ttu-id="cb921-163">Configurar o Google como um IDP</span><span class="sxs-lookup"><span data-stu-id="cb921-163">Set up Google as an IDP</span></span>](active-directory-b2c-setup-goog-app.md)
* [<span data-ttu-id="cb921-164">Configurar o Amazon como um IDP</span><span class="sxs-lookup"><span data-stu-id="cb921-164">Set up Amazon as an IDP</span></span>](active-directory-b2c-setup-amzn-app.md)
* [<span data-ttu-id="cb921-165">Configurar o LinkedIn como um IDP</span><span class="sxs-lookup"><span data-stu-id="cb921-165">Set up LinkedIn as an IDP</span></span>](active-directory-b2c-setup-li-app.md)

<span data-ttu-id="cb921-166">Depois de adicionar tooyour de provedores de identidade Olá directory B2C, edite seu tooinclude três políticas Olá IDPs novo, conforme descrito em Olá [artigo de referência de política](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="cb921-166">After you add hello identity providers tooyour B2C directory, edit each of your three policies tooinclude hello new IDPs, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="cb921-167">Depois de salvar suas políticas, execute novamente o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="cb921-167">After you save your policies, run hello app again.</span></span>  <span data-ttu-id="cb921-168">Você deve ver Olá que idps novo são adicionados como opções de entrada e inscreva-se em cada uma das suas experiências de identidade.</span><span class="sxs-lookup"><span data-stu-id="cb921-168">You should see hello new IDPs added as sign-in and sign-up options in each of your identity experiences.</span></span>

<span data-ttu-id="cb921-169">Você pode fazer experiências com suas políticas e observar o efeito de saudação em seu aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="cb921-169">You can experiment with your policies and observe hello effect on your sample app.</span></span> <span data-ttu-id="cb921-170">Adicione ou remova IDPs, manipule declarações de aplicativo ou altere os atributos de inscrição.</span><span class="sxs-lookup"><span data-stu-id="cb921-170">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span></span> <span data-ttu-id="cb921-171">Experimente até começar a entender como as políticas, solicitações de autenticação e OWIN funcionam juntos.</span><span class="sxs-lookup"><span data-stu-id="cb921-171">Experiment until you can see how policies, authentication requests, and OWIN tie together.</span></span>

## <a name="sample-code-walkthrough"></a><span data-ttu-id="cb921-172">Passo a passo do código de exemplo</span><span class="sxs-lookup"><span data-stu-id="cb921-172">Sample code walkthrough</span></span>
<span data-ttu-id="cb921-173">Olá seções a seguir mostra como o código do aplicativo de exemplo hello está configurado.</span><span class="sxs-lookup"><span data-stu-id="cb921-173">hello following sections show you how hello sample application code is configured.</span></span> <span data-ttu-id="cb921-174">Você pode usar isso como um guia no desenvolvimento do seu futuro aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cb921-174">You may use this as a guide in your future app development.</span></span>

### <a name="add-authentication-support"></a><span data-ttu-id="cb921-175">Adicionar suporte a autenticação</span><span class="sxs-lookup"><span data-stu-id="cb921-175">Add authentication support</span></span>

<span data-ttu-id="cb921-176">Agora você pode configurar seu toouse de aplicativo do Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="cb921-176">You can now configure your app toouse Azure AD B2C.</span></span> <span data-ttu-id="cb921-177">Seu aplicativo se comunica com o Azure AD B2C ao enviar solicitações de autenticação OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="cb921-177">Your app communicates with Azure AD B2C by sending OpenID Connect authentication requests.</span></span> <span data-ttu-id="cb921-178">solicitações Hello ditam experiência do usuário Olá seu aplicativo deseja tooexecute especificando a diretiva de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb921-178">hello requests dictate hello user experience your app wants tooexecute by specifying hello policy.</span></span> <span data-ttu-id="cb921-179">Você pode usar toosend de biblioteca do Microsoft OWIN essas solicitações, executar políticas, gerenciar sessões de usuário e muito mais.</span><span class="sxs-lookup"><span data-stu-id="cb921-179">You can use Microsoft's OWIN library toosend these requests, execute policies, manage user sessions, and more.</span></span>

#### <a name="install-owin"></a><span data-ttu-id="cb921-180">Instalar a OWIN</span><span class="sxs-lookup"><span data-stu-id="cb921-180">Install OWIN</span></span>

<span data-ttu-id="cb921-181">toobegin, Adicionar projeto de toohello Olá OWIN middleware NuGet pacotes usando Olá Visual Studio Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="cb921-181">toobegin, add hello OWIN middleware NuGet packages toohello project by using hello Visual Studio Package Manager Console.</span></span>

```Console
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
PM> Install-Package Microsoft.Owin.Security.Cookies
PM> Install-Package Microsoft.Owin.Host.SystemWeb
```

#### <a name="add-an-owin-startup-class"></a><span data-ttu-id="cb921-182">Adicionar uma classe de inicialização da OWIN</span><span class="sxs-lookup"><span data-stu-id="cb921-182">Add an OWIN startup class</span></span>

<span data-ttu-id="cb921-183">Adicionar uma toohello de classe de inicialização OWIN API chamado `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="cb921-183">Add an OWIN startup class toohello API called `Startup.cs`.</span></span>  <span data-ttu-id="cb921-184">Clique com botão direito no projeto hello, selecione **adicionar** e **Novo Item**e, em seguida, procure a OWIN.</span><span class="sxs-lookup"><span data-stu-id="cb921-184">Right-click on hello project, select **Add** and **New Item**, and then search for OWIN.</span></span> <span data-ttu-id="cb921-185">Olá OWIN middleware invocará Olá `Configuration(…)` método quando seu aplicativo é iniciado.</span><span class="sxs-lookup"><span data-stu-id="cb921-185">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>

<span data-ttu-id="cb921-186">Em nosso exemplo, alteramos declaração de classe Olá muito`public partial class Startup` e implementado Olá outra parte da classe Olá no `App_Start\Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="cb921-186">In our sample, we changed hello class declaration too`public partial class Startup` and implemented hello other part of hello class in `App_Start\Startup.Auth.cs`.</span></span> <span data-ttu-id="cb921-187">Olá interna `Configuration` método, adicionamos uma chamada muito`ConfigureAuth`, que é definido em `Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="cb921-187">Inside hello `Configuration` method, we added a call too`ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span></span> <span data-ttu-id="cb921-188">Depois de modificações de saudação `Startup.cs` parece com hello seguinte:</span><span class="sxs-lookup"><span data-stu-id="cb921-188">After hello modifications, `Startup.cs` looks like hello following:</span></span>

```CSharp
// Startup.cs

public partial class Startup
{
    // hello OWIN middleware will invoke this method when hello app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of hello class
        ConfigureAuth(app);
    }
}
```

#### <a name="configure-hello-authentication-middleware"></a><span data-ttu-id="cb921-189">Configurar o middleware de autenticação Olá</span><span class="sxs-lookup"><span data-stu-id="cb921-189">Configure hello authentication middleware</span></span>

<span data-ttu-id="cb921-190">Arquivo hello abrir `App_Start\Startup.Auth.cs` e implementar Olá `ConfigureAuth(...)` método.</span><span class="sxs-lookup"><span data-stu-id="cb921-190">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(...)` method.</span></span> <span data-ttu-id="cb921-191">Olá parâmetros que você fornece em `OpenIdConnectAuthenticationOptions` servem como coordenadas para toocommunicate seu aplicativo com o Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="cb921-191">hello parameters you provide in `OpenIdConnectAuthenticationOptions` serve as coordinates for your app toocommunicate with Azure AD B2C.</span></span> <span data-ttu-id="cb921-192">Se você não especificar certos parâmetros, ele usará o valor padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb921-192">If you do not specify certain parameters, it will use hello default value.</span></span> <span data-ttu-id="cb921-193">Por exemplo, não especificamos Olá `ResponseType` no exemplo hello, Olá assim o valor padrão `code id_token` serão usados em cada tooAzure de solicitação de saída AD B2C.</span><span class="sxs-lookup"><span data-stu-id="cb921-193">For example, we do not specify hello `ResponseType` in hello sample, so hello default value `code id_token` will be used in each outgoing request tooAzure AD B2C.</span></span>

<span data-ttu-id="cb921-194">Você também precisa tooset a autenticação de cookie.</span><span class="sxs-lookup"><span data-stu-id="cb921-194">You also need tooset up cookie authentication.</span></span> <span data-ttu-id="cb921-195">Olá OpenID Connect middleware usa sessões do usuário toomaintain cookies, entre outras coisas.</span><span class="sxs-lookup"><span data-stu-id="cb921-195">hello OpenID Connect middleware uses cookies toomaintain user sessions, among other things.</span></span>

```CSharp
// App_Start\Startup.Auth.cs

public partial class Startup
{
    // Initialize variables ...

    // Configure hello OWIN middleware
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseCookieAuthentication(new CookieAuthenticationOptions());
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Generate hello metadata address using hello tenant and policy information
                MetadataAddress = String.Format(AadInstance, Tenant, DefaultPolicy),

                // These are standard OpenID Connect parameters, with values pulled from web.config
                ClientId = ClientId,
                RedirectUri = RedirectUri,
                PostLogoutRedirectUri = RedirectUri,

                // Specify hello callbacks for each type of notifications
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    RedirectToIdentityProvider = OnRedirectToIdentityProvider,
                    AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    AuthenticationFailed = OnAuthenticationFailed,
                },

                // Specify hello claims toovalidate
                TokenValidationParameters = new TokenValidationParameters
                {
                    NameClaimType = "name"
                },

                // Specify hello scope by appending all of hello scopes requested into one string (seperated by a blank space)
                Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
            }
        );
    }

    // Implement hello "Notification" methods...
}
```

<span data-ttu-id="cb921-196">Em `OpenIdConnectAuthenticationOptions` acima, definimos um conjunto de funções de retorno de chamada para notificações específicas que são recebidas pelo middleware de OpenID Connect hello.</span><span class="sxs-lookup"><span data-stu-id="cb921-196">In `OpenIdConnectAuthenticationOptions` above, we define a set of callback functions for specific notifications that are received by hello OpenID Connect middleware.</span></span> <span data-ttu-id="cb921-197">Esses comportamentos são definidos usando um `OpenIdConnectAuthenticationNotifications` de objeto e armazenados em Olá `Notifications` variável.</span><span class="sxs-lookup"><span data-stu-id="cb921-197">These behaviors are defined using a `OpenIdConnectAuthenticationNotifications` object and stored into hello `Notifications` variable.</span></span> <span data-ttu-id="cb921-198">Em nosso exemplo, podemos definir três retornos de chamada diferentes dependendo do evento hello.</span><span class="sxs-lookup"><span data-stu-id="cb921-198">In our sample, we define three different callbacks depending on hello event.</span></span>

### <a name="using-different-policies"></a><span data-ttu-id="cb921-199">Usando políticas diferentes</span><span class="sxs-lookup"><span data-stu-id="cb921-199">Using different policies</span></span>

<span data-ttu-id="cb921-200">Olá `RedirectToIdentityProvider` notificação é acionada sempre que uma solicitação é feita tooAzure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="cb921-200">hello `RedirectToIdentityProvider` notification is triggered whenever a request is made tooAzure AD B2C.</span></span> <span data-ttu-id="cb921-201">Na função de retorno de chamada hello `OnRedirectToIdentityProvider`, verificamos em Olá chamada de saída se quisermos toouse uma regra diferente.</span><span class="sxs-lookup"><span data-stu-id="cb921-201">In hello callback function `OnRedirectToIdentityProvider`, we check in hello outgoing call if we want toouse a different policy.</span></span> <span data-ttu-id="cb921-202">Em ordem toodo uma senha redefinida ou editar um perfil, você precisa política correspondente do toouse hello como política em vez da saudação "Inscrever ou entrar" diretiva de redefinição de senha de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb921-202">In order toodo a password reset or edit a profile, you need toouse hello corresponding policy such as hello password reset policy instead of hello default "Sign-up or Sign-in" policy.</span></span>

<span data-ttu-id="cb921-203">Em nosso exemplo, quando um usuário deseja senha de saudação tooreset ou editar o perfil de hello, adicionamos política Olá que preferir toouse no contexto do OWIN hello.</span><span class="sxs-lookup"><span data-stu-id="cb921-203">In our sample, when a user wants tooreset hello password or edit hello profile, we add hello policy we prefer toouse into hello OWIN context.</span></span> <span data-ttu-id="cb921-204">Isso pode ser feito fazendo Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="cb921-204">That can be done by doing hello following:</span></span>

```CSharp
    // Let hello middleware know you are trying toouse hello edit profile policy
    HttpContext.GetOwinContext().Set("Policy", EditProfilePolicyId);
```

<span data-ttu-id="cb921-205">E você pode implementar uma função de retorno de chamada hello `OnRedirectToIdentityProvider` fazendo Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="cb921-205">And you can implement hello callback function `OnRedirectToIdentityProvider` by doing hello following:</span></span>

```CSharp
/*
*  On each call tooAzure AD B2C, check if a policy (e.g. hello profile edit or password reset policy) has been specified in hello OWIN context.
*  If so, use that policy when making hello call. Also, don't request a code (since it won't be needed).
*/
private Task OnRedirectToIdentityProvider(RedirectToIdentityProviderNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    var policy = notification.OwinContext.Get<string>("Policy");

    if (!string.IsNullOrEmpty(policy) && !policy.Equals(DefaultPolicy))
    {
        notification.ProtocolMessage.Scope = OpenIdConnectScopes.OpenId;
        notification.ProtocolMessage.ResponseType = OpenIdConnectResponseTypes.IdToken;
        notification.ProtocolMessage.IssuerAddress = notification.ProtocolMessage.IssuerAddress.Replace(DefaultPolicy, policy);
    }

    return Task.FromResult(0);
}
```

### <a name="handling-authorization-codes"></a><span data-ttu-id="cb921-206">Manipulando códigos de autorização</span><span class="sxs-lookup"><span data-stu-id="cb921-206">Handling authorization codes</span></span>

<span data-ttu-id="cb921-207">Olá `AuthorizationCodeReceived` notificação é acionada quando um código de autorização é recebido.</span><span class="sxs-lookup"><span data-stu-id="cb921-207">hello `AuthorizationCodeReceived` notification is triggered when an authorization code is received.</span></span> <span data-ttu-id="cb921-208">Olá OpenID Connect middleware não dá suporte a códigos de troca para tokens de acesso.</span><span class="sxs-lookup"><span data-stu-id="cb921-208">hello OpenID Connect middleware does not support exchanging codes for access tokens.</span></span> <span data-ttu-id="cb921-209">Você pode trocar manualmente código Olá para o token de saudação em uma função de retorno de chamada.</span><span class="sxs-lookup"><span data-stu-id="cb921-209">You can manually exchange hello code for hello token in a callback function.</span></span> <span data-ttu-id="cb921-210">Para obter mais informações, examine a saudação [documentação](active-directory-b2c-devquickstarts-web-api-dotnet.md) que explica como.</span><span class="sxs-lookup"><span data-stu-id="cb921-210">For more information, please look at hello [documentation](active-directory-b2c-devquickstarts-web-api-dotnet.md) that explains how.</span></span>

### <a name="handling-errors"></a><span data-ttu-id="cb921-211">Tratamento de erros</span><span class="sxs-lookup"><span data-stu-id="cb921-211">Handling errors</span></span>

<span data-ttu-id="cb921-212">Olá `AuthenticationFailed` notificação é disparada quando a autenticação falhará.</span><span class="sxs-lookup"><span data-stu-id="cb921-212">hello `AuthenticationFailed` notification is triggered when authentication fails.</span></span> <span data-ttu-id="cb921-213">Em seu método de retorno de chamada, você pode manipular erros hello como desejar.</span><span class="sxs-lookup"><span data-stu-id="cb921-213">In its callback method, you can handle hello errors as you wish.</span></span> <span data-ttu-id="cb921-214">No entanto, você deve adicionar uma verificação de código de erro Olá `AADB2C90118`.</span><span class="sxs-lookup"><span data-stu-id="cb921-214">You should however add a check for hello error code `AADB2C90118`.</span></span> <span data-ttu-id="cb921-215">Durante a execução Olá Olá política "Inscrever ou entrar", o usuário de saudação tem Olá oportunidade tooselect um **esqueceu sua senha?** link.</span><span class="sxs-lookup"><span data-stu-id="cb921-215">During hello execution of hello "Sign-up or Sign-in" policy, hello user has hello opportunity tooselect a **Forgot your password?** link.</span></span> <span data-ttu-id="cb921-216">Nesse caso, o Azure AD B2C envia seu aplicativo esse código de erro indicando que o aplicativo deve fazer uma solicitação usando a política de redefinição de senha Olá em vez disso.</span><span class="sxs-lookup"><span data-stu-id="cb921-216">In this event, Azure AD B2C sends your app that error code indicating that your app should make a request using hello password reset policy instead.</span></span>

```CSharp
/*
* Catch any failures received by hello authentication middleware and handle appropriately
*/
private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    notification.HandleResponse();

    // Handle hello error code that Azure AD B2C throws when trying tooreset a password from hello login page
    // because password reset is not supported by a "sign-up or sign-in policy"
    if (notification.ProtocolMessage.ErrorDescription != null && notification.ProtocolMessage.ErrorDescription.Contains("AADB2C90118"))
    {
        // If hello user clicked hello reset password link, redirect toohello reset password route
        notification.Response.Redirect("/Account/ResetPassword");
    }
    else if (notification.Exception.Message == "access_denied")
    {
        notification.Response.Redirect("/");
    }
    else
    {
        notification.Response.Redirect("/Home/Error?message=" + notification.Exception.Message);
    }

    return Task.FromResult(0);
}
```

### <a name="send-authentication-requests-tooazure-ad"></a><span data-ttu-id="cb921-217">Enviar solicitações de autenticação tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="cb921-217">Send authentication requests tooAzure AD</span></span>

<span data-ttu-id="cb921-218">Seu aplicativo agora está toocommunicate corretamente configurado com o Azure AD B2C usando o protocolo de autenticação OpenID Connect hello.</span><span class="sxs-lookup"><span data-stu-id="cb921-218">Your app is now properly configured toocommunicate with Azure AD B2C by using hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="cb921-219">OWIN gerencia os detalhes de saudação de criação de mensagens de autenticação, validando tokens do Azure AD B2C e manter a sessão de usuário.</span><span class="sxs-lookup"><span data-stu-id="cb921-219">OWIN manages hello details of crafting authentication messages, validating tokens from Azure AD B2C, and maintaining user session.</span></span> <span data-ttu-id="cb921-220">Tudo o que permanece é tooinitiate fluxo de cada usuário.</span><span class="sxs-lookup"><span data-stu-id="cb921-220">All that remains is tooinitiate each user's flow.</span></span>

<span data-ttu-id="cb921-221">Quando um usuário seleciona **Sign up/entrar**, **Editar perfil**, ou **Redefinir senha** no Olá web app, ação Olá associado é invocada em `Controllers\AccountController.cs`:</span><span class="sxs-lookup"><span data-stu-id="cb921-221">When a user selects **Sign up/Sign in**, **Edit profile**, or **Reset password** in hello web app, hello associated action is invoked in `Controllers\AccountController.cs`:</span></span>

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting toosign up or sign in
*/
public void SignUpSignIn()
{
    // Use hello default policy tooprocess hello sign up / sign in flow
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge();
        return;
    }

    Response.Redirect("/");
}

/*
*  Called when requesting tooedit a profile
*/
public void EditProfile()
{
    if (Request.IsAuthenticated)
    {
        // Let hello middleware know you are trying toouse hello edit profile policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
        HttpContext.GetOwinContext().Set("Policy", Startup.EditProfilePolicyId);

        // Set hello page tooredirect tooafter editing hello profile
        var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
        HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

        return;
    }

    Response.Redirect("/");

}

/*
*  Called when requesting tooreset a password
*/
public void ResetPassword()
{
    // Let hello middleware know you are trying toouse hello reset password policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
    HttpContext.GetOwinContext().Set("Policy", Startup.ResetPasswordPolicyId);

    // Set hello page tooredirect tooafter changing passwords
    var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
    HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

    return;
}
```

<span data-ttu-id="cb921-222">Você também pode usar toosign OWIN usuário saudação do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="cb921-222">You can also use OWIN toosign out hello user from hello app.</span></span> <span data-ttu-id="cb921-223">Em `Controllers\AccountController.cs`, temos:</span><span class="sxs-lookup"><span data-stu-id="cb921-223">In `Controllers\AccountController.cs` we have:</span></span>

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting toosign out
*/
public void SignOut()
{
    // toosign out hello user, you should issue an OpenIDConnect sign out request.
    if (Request.IsAuthenticated)
    {
        IEnumerable<AuthenticationDescription> authTypes = HttpContext.GetOwinContext().Authentication.GetAuthenticationTypes();
        HttpContext.GetOwinContext().Authentication.SignOut(authTypes.Select(t => t.AuthenticationType).ToArray());
        Request.GetOwinContext().Authentication.GetAuthenticationTypes();
    }
}
```

<span data-ttu-id="cb921-224">Em adição tooexplicitly de invocar uma política, você pode usar um `[Authorize]` marca em seus controladores que executa uma política, se o usuário Olá não está conectado.</span><span class="sxs-lookup"><span data-stu-id="cb921-224">In addition tooexplicitly invoking a policy, you can use a `[Authorize]` tag in your controllers that executes a policy if hello user is not signed in.</span></span> <span data-ttu-id="cb921-225">Abra `Controllers\HomeController.cs` e adicione Olá `[Authorize]` marca toohello declarações controlador.</span><span class="sxs-lookup"><span data-stu-id="cb921-225">Open `Controllers\HomeController.cs` and add hello `[Authorize]` tag toohello claims controller.</span></span>  <span data-ttu-id="cb921-226">OWIN seleciona a última política de saudação configurada quando hello `[Authorize]` marca for atingida.</span><span class="sxs-lookup"><span data-stu-id="cb921-226">OWIN selects hello last policy configured when hello `[Authorize]` tag is hit.</span></span>

```CSharp
// Controllers\HomeController.cs

// You can use hello Authorize decorator tooexecute a certain policy if hello user is not already signed into hello app.
[Authorize]
public ActionResult Claims()
{
  ...
```

### <a name="display-user-information"></a><span data-ttu-id="cb921-227">Exibir informações do usuário</span><span class="sxs-lookup"><span data-stu-id="cb921-227">Display user information</span></span>

<span data-ttu-id="cb921-228">Quando você autenticar usuários usando o OpenID Connect, o Azure AD B2C retorna um aplicativo de toohello token de ID que contém **declarações**.</span><span class="sxs-lookup"><span data-stu-id="cb921-228">When you authenticate users by using OpenID Connect, Azure AD B2C returns an ID token toohello app that contains **claims**.</span></span> <span data-ttu-id="cb921-229">Esses são afirmações sobre usuário hello.</span><span class="sxs-lookup"><span data-stu-id="cb921-229">These are assertions about hello user.</span></span> <span data-ttu-id="cb921-230">Você pode usar declarações toopersonalize seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cb921-230">You can use claims toopersonalize your app.</span></span>

<span data-ttu-id="cb921-231">Olá abrir `Controllers\HomeController.cs` arquivo.</span><span class="sxs-lookup"><span data-stu-id="cb921-231">Open hello `Controllers\HomeController.cs` file.</span></span> <span data-ttu-id="cb921-232">Você pode acessar as declarações de usuário em seus controladores via Olá `ClaimsPrincipal.Current` objeto de segurança.</span><span class="sxs-lookup"><span data-stu-id="cb921-232">You can access user claims in your controllers via hello `ClaimsPrincipal.Current` security principal object.</span></span>

```CSharp
// Controllers\HomeController.cs

[Authorize]
public ActionResult Claims()
{
    Claim displayName = ClaimsPrincipal.Current.FindFirst(ClaimsPrincipal.Current.Identities.First().NameClaimType);
    ViewBag.DisplayName = displayName != null ? displayName.Value : string.Empty;
    return View();
}
```

<span data-ttu-id="cb921-233">Você pode acessar qualquer declaração que seu aplicativo recebe em Olá mesmo modo.</span><span class="sxs-lookup"><span data-stu-id="cb921-233">You can access any claim that your application receives in hello same way.</span></span>  <span data-ttu-id="cb921-234">Uma lista de todas as declarações de Olá Olá aplicativo recebe está disponível para você no hello **declarações** página.</span><span class="sxs-lookup"><span data-stu-id="cb921-234">A list of all hello claims hello app receives is available for you on hello **Claims** page.</span></span>
