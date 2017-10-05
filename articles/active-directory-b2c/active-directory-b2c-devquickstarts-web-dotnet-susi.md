---
title: Azure Active Directory B2C | Microsoft Docs
description: "Como criar um aplicativo Web com inscrição/entrada, edição de perfil e redefinição de senha usando o Azure Active Directory B2C."
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
ms.openlocfilehash: 3144ced01b524abb035dc1c6f0cdf764bec46804
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-aspnet-web-app-with-azure-active-directory-b2c-sign-up-sign-in-profile-edit-and-password-reset"></a><span data-ttu-id="d829d-103">Criar um aplicativo Web ASP.NET com inscrição/entrada, edição de perfil e redefinição de senha do Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="d829d-103">Create an ASP.NET web app with Azure Active Directory B2C sign-up, sign-in, profile edit, and password reset</span></span>

<span data-ttu-id="d829d-104">Este tutorial mostra como:</span><span class="sxs-lookup"><span data-stu-id="d829d-104">This tutorial shows you how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d829d-105">Adicionar recursos de identidade do Azure AD B2C ao seu aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="d829d-105">Add Azure AD B2C identity features to your web app</span></span>
> * <span data-ttu-id="d829d-106">Registrar seu aplicativo Web em seu diretório do Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="d829d-106">Register your web app in your Azure AD B2C directory</span></span>
> * <span data-ttu-id="d829d-107">Criar inscrição/entrada, edição de perfil e política de redefinição de senha de usuário para o seu aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="d829d-107">Create a user sign-up/sign-in, profile edit, and password reset policy for your web app</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d829d-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d829d-108">Prerequisites</span></span>

- <span data-ttu-id="d829d-109">Você deve conectar seu Locatário B2C a uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="d829d-109">You must connect your B2C Tenant to an Azure account.</span></span> <span data-ttu-id="d829d-110">Você pode criar uma conta gratuita do Azure [aqui](https://azure.microsoft.com/en-us/).</span><span class="sxs-lookup"><span data-stu-id="d829d-110">You can create a free Azure account [here](https://azure.microsoft.com/en-us/).</span></span>
- <span data-ttu-id="d829d-111">Você precisa do [Microsoft Visual Studio](https://www.visualstudio.com/) ou um programa semelhante para exibir e modificar o código de exemplo.</span><span class="sxs-lookup"><span data-stu-id="d829d-111">You need [Microsoft Visual Studio](https://www.visualstudio.com/) or a similar program to view and modify the sample code.</span></span>

## <a name="create-an-azure-ad-b2c-directory"></a><span data-ttu-id="d829d-112">Criar um diretório do AD B2C do Azure</span><span class="sxs-lookup"><span data-stu-id="d829d-112">Create an Azure AD B2C directory</span></span>

<span data-ttu-id="d829d-113">Antes de usar AD B2C do Azure, você deve criar um diretório ou locatário.</span><span class="sxs-lookup"><span data-stu-id="d829d-113">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="d829d-114">Um diretório é um contêiner para todos os seus usuários, aplicativos, grupos e muito mais.</span><span class="sxs-lookup"><span data-stu-id="d829d-114">A directory is a container for all your users, apps, groups, and more.</span></span> <span data-ttu-id="d829d-115">Se você ainda não tiver um, crie um diretório B2C antes de prosseguir neste guia.</span><span class="sxs-lookup"><span data-stu-id="d829d-115">If you don't have one already, create a B2C directory before you continue in this guide.</span></span>

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

> [!NOTE]
> 
> <span data-ttu-id="d829d-116">Você precisa se conectar ao Locatário B2C para sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="d829d-116">You need to connect the B2C Tenant to your Azure subscription.</span></span> <span data-ttu-id="d829d-117">Depois de selecionar **Criar**, selecione a opção **Associar um Locatário do Azure AD B2C existente à minha assinatura do Azure** e, em seguida, na lista suspensa de **Locatário do Azure AD B2C**, selecione o locatário que você deseja associar.</span><span class="sxs-lookup"><span data-stu-id="d829d-117">After selecting **Create**, select the **Link an existing Azure AD B2C Tenant to my Azure subscription** option, and then in the **Azure AD B2C Tenant** drop down, select the tenant you want to associate.</span></span>

## <a name="create-and-register-an-application"></a><span data-ttu-id="d829d-118">Criar e registrar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="d829d-118">Create and register an application</span></span>

<span data-ttu-id="d829d-119">Em seguida, você precisa criar e registrar um aplicativo em seu diretório B2C.</span><span class="sxs-lookup"><span data-stu-id="d829d-119">Next, you need to create and register the app in your B2C directory.</span></span> <span data-ttu-id="d829d-120">Isso fornece ao Azure AD B2C as informações de que ele precisa para se comunicar de forma segura com seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d829d-120">This provides information that Azure AD B2C needs to securely communicate with your app.</span></span> 

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

<span data-ttu-id="d829d-121">Quando você terminar, você terá uma API e um aplicativo nativo nas suas configurações de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d829d-121">When you are done, you will have both an API and a native application in your application settings.</span></span>

## <a name="create-policies-on-your-b2c-tenant"></a><span data-ttu-id="d829d-122">Criar políticas em seu locatário B2C</span><span class="sxs-lookup"><span data-stu-id="d829d-122">Create policies on your B2C tenant</span></span>

<span data-ttu-id="d829d-123">No AD B2C do Azure, cada experiência do usuário é definida por uma [política](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="d829d-123">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="d829d-124">Este exemplo de código contém três experiências de identidade: **inscrição e entrada**, **edição de perfil** e **redefinição de senha**.</span><span class="sxs-lookup"><span data-stu-id="d829d-124">This code sample contains three identity experiences: **sign-up & sign-in**, **profile edit**, and **password reset**.</span></span>  <span data-ttu-id="d829d-125">Você precisa criar uma política de cada tipo, conforme descrito no [artigo de referência de política](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="d829d-125">You need to create one policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="d829d-126">Para cada política, certifique-se de selecionar a declaração ou atributo de Nome de exibição e copiar o nome da sua política para uso posterior.</span><span class="sxs-lookup"><span data-stu-id="d829d-126">For each policy, be sure to select the Display name attribute or claim, and to copy down the name of your policy for later use.</span></span>

### <a name="add-your-identity-providers"></a><span data-ttu-id="d829d-127">Adicionar seus provedores de identidade</span><span class="sxs-lookup"><span data-stu-id="d829d-127">Add your identity providers</span></span>

<span data-ttu-id="d829d-128">Nas configurações, selecione **Provedores de Identidade** e escolha Inscrição do nome de usuário ou Inscrição de email.</span><span class="sxs-lookup"><span data-stu-id="d829d-128">From your settings, select **Identity Providers** and choose Username signup or Email signup.</span></span>

### <a name="create-a-sign-up-and-sign-in-policy"></a><span data-ttu-id="d829d-129">Criar uma política de inscrição e entrada</span><span class="sxs-lookup"><span data-stu-id="d829d-129">Create a sign-up and sign-in policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

### <a name="create-a-profile-editing-policy"></a><span data-ttu-id="d829d-130">Criar uma política de edição de perfil</span><span class="sxs-lookup"><span data-stu-id="d829d-130">Create a profile editing policy</span></span>

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

### <a name="create-a-password-reset-policy"></a><span data-ttu-id="d829d-131">Criar uma política de redefinição de senha</span><span class="sxs-lookup"><span data-stu-id="d829d-131">Create a password reset policy</span></span>

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

<span data-ttu-id="d829d-132">Depois de criar as políticas, você estará pronto para compilar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d829d-132">After you create your policies, you're ready to build your app.</span></span>

## <a name="download-the-sample-code"></a><span data-ttu-id="d829d-133">Baixe o código de exemplo</span><span class="sxs-lookup"><span data-stu-id="d829d-133">Download the sample code</span></span>

<span data-ttu-id="d829d-134">O código para este tutorial é mantido no [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="d829d-134">The code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="d829d-135">Você pode clonar a amostra executando:</span><span class="sxs-lookup"><span data-stu-id="d829d-135">You can clone the sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="d829d-136">Depois de baixar o código de exemplo, abra o arquivo .sln do Visual Studio para começar.</span><span class="sxs-lookup"><span data-stu-id="d829d-136">After you download the sample code, open the Visual Studio .sln file to get started.</span></span> <span data-ttu-id="d829d-137">Agora, sua solução contém dois projetos: `TaskWebApp` e `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="d829d-137">The solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="d829d-138">`TaskWebApp` é o aplicativo Web MVC com o qual o usuário interage.</span><span class="sxs-lookup"><span data-stu-id="d829d-138">`TaskWebApp` is the MVC web application that the user interacts with.</span></span> <span data-ttu-id="d829d-139">`TaskService` é API Web back-end do aplicativo que armazena a lista de tarefas de cada usuário.</span><span class="sxs-lookup"><span data-stu-id="d829d-139">`TaskService` is the app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="d829d-140">Este artigo discutirá apenas o aplicativo `TaskWebApp`.</span><span class="sxs-lookup"><span data-stu-id="d829d-140">This article will only discuss the `TaskWebApp` application.</span></span> <span data-ttu-id="d829d-141">Para saber como criar `TaskService` usando o Azure AD B2C, confira [nosso tutorial da API Web .NET](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="d829d-141">To learn how to build `TaskService` using Azure AD B2C, see [our .NET web api tutorial](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

## <a name="update-code-to-use-your-tenant-and-policies"></a><span data-ttu-id="d829d-142">Atualizar o código para usar as suas políticas e locatário</span><span class="sxs-lookup"><span data-stu-id="d829d-142">Update code to use your tenant and policies</span></span>

<span data-ttu-id="d829d-143">Nossa amostra é configurada para usar as políticas e a ID do cliente de nosso locatário de demonstração.</span><span class="sxs-lookup"><span data-stu-id="d829d-143">Our sample is configured to use the policies and client ID of our demo tenant.</span></span> <span data-ttu-id="d829d-144">Para conectar-se ao seu próprio locatário, você precisa abrir `web.config` no projeto `TaskWebApp` e substituir os valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="d829d-144">To connect it to your own tenant, you need to open `web.config` in the `TaskWebApp` project and replace the following values:</span></span>

* <span data-ttu-id="d829d-145">`ida:Tenant` pelo nome do locatário</span><span class="sxs-lookup"><span data-stu-id="d829d-145">`ida:Tenant` with your tenant name</span></span>
* <span data-ttu-id="d829d-146">`ida:ClientId` pela ID de aplicativo do aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="d829d-146">`ida:ClientId` with your web app application ID</span></span>
* <span data-ttu-id="d829d-147">`ida:ClientSecret` pela chave de segredo do aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="d829d-147">`ida:ClientSecret` with your web app secret key</span></span>
* <span data-ttu-id="d829d-148">`ida:SignUpSignInPolicyId` pelo nome da política "Inscrever-se ou Entrar"</span><span class="sxs-lookup"><span data-stu-id="d829d-148">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
* <span data-ttu-id="d829d-149">`ida:EditProfilePolicyId` pelo nome de política "Editar Perfil"</span><span class="sxs-lookup"><span data-stu-id="d829d-149">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
* <span data-ttu-id="d829d-150">`ida:ResetPasswordPolicyId` pelo nome de política "Redefinir Senha"</span><span class="sxs-lookup"><span data-stu-id="d829d-150">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>

## <a name="launch-the-app"></a><span data-ttu-id="d829d-151">Iniciar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="d829d-151">Launch the app</span></span>
<span data-ttu-id="d829d-152">No Visual Studio, inicie o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d829d-152">From within Visual Studio, launch the app.</span></span> <span data-ttu-id="d829d-153">Navegue até a guia Lista de tarefas e observe que o URl é: https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*&client_id=*YourclientID*.....</span><span class="sxs-lookup"><span data-stu-id="d829d-153">Navigate to the To-Do List tab, and note the URl is: https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*&client_id=*YourclientID*.....</span></span>

<span data-ttu-id="d829d-154">Inscreva-se no aplicativo usando o seu endereço de email ou nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="d829d-154">Sign up for the app by using your email address or user name.</span></span> <span data-ttu-id="d829d-155">Saia, em seguida, entre novamente e edite o perfil ou redefina a senha.</span><span class="sxs-lookup"><span data-stu-id="d829d-155">Sign out, then sign in again and edit the profile or reset the password.</span></span> <span data-ttu-id="d829d-156">Saia e entre como outro usuário.</span><span class="sxs-lookup"><span data-stu-id="d829d-156">Sign out and sign in as a different user.</span></span> 

## <a name="add-social-idps"></a><span data-ttu-id="d829d-157">Adicionar IDPs sociais</span><span class="sxs-lookup"><span data-stu-id="d829d-157">Add social IDPs</span></span>

<span data-ttu-id="d829d-158">Atualmente, o aplicativo suporta inscrição e entrada usando apenas **contas locais**; contas armazenadas no seu diretório do B2C que usam um nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="d829d-158">Currently, the app supports only user sign-up and sign-in by using **local accounts**; accounts stored in your B2C directory that use a user name and password.</span></span> <span data-ttu-id="d829d-159">Com o Azure AD B2C, você pode adicionar suporte a outros **provedores de identidade** (IDPs), sem alterar qualquer código.</span><span class="sxs-lookup"><span data-stu-id="d829d-159">By using Azure AD B2C, you can add support for other **identity providers** (IDPs) without changing any of your code.</span></span>

<span data-ttu-id="d829d-160">Para adicionar IDPs sociais ao seu aplicativo, comece seguindo as instruções detalhadas nestes artigos.</span><span class="sxs-lookup"><span data-stu-id="d829d-160">To add social IDPs to your app, begin by following the detailed instructions in these articles.</span></span> <span data-ttu-id="d829d-161">Para cada IDP ao qual deseja oferecer suporte, você precisa registrar um aplicativo no sistema e obter uma ID de cliente.</span><span class="sxs-lookup"><span data-stu-id="d829d-161">For each IDP you want to support, you need to register an application in that system and obtain a client ID.</span></span>

* [<span data-ttu-id="d829d-162">Configurar o Facebook como um IDP</span><span class="sxs-lookup"><span data-stu-id="d829d-162">Set up Facebook as an IDP</span></span>](active-directory-b2c-setup-fb-app.md)
* [<span data-ttu-id="d829d-163">Configurar o Google como um IDP</span><span class="sxs-lookup"><span data-stu-id="d829d-163">Set up Google as an IDP</span></span>](active-directory-b2c-setup-goog-app.md)
* [<span data-ttu-id="d829d-164">Configurar o Amazon como um IDP</span><span class="sxs-lookup"><span data-stu-id="d829d-164">Set up Amazon as an IDP</span></span>](active-directory-b2c-setup-amzn-app.md)
* [<span data-ttu-id="d829d-165">Configurar o LinkedIn como um IDP</span><span class="sxs-lookup"><span data-stu-id="d829d-165">Set up LinkedIn as an IDP</span></span>](active-directory-b2c-setup-li-app.md)

<span data-ttu-id="d829d-166">Após adicionar provedores de identidade ao seu diretório de B2C, edite cada uma das suas três políticas para incluir os novos IDPs, como descrito no [artigo de referência de política](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="d829d-166">After you add the identity providers to your B2C directory, edit each of your three policies to include the new IDPs, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="d829d-167">Depois de salvar as políticas, execute o aplicativo novamente.</span><span class="sxs-lookup"><span data-stu-id="d829d-167">After you save your policies, run the app again.</span></span>  <span data-ttu-id="d829d-168">Você deve ver os novos IDPs adicionados como opções de entrada e de inscrição em cada experiência de identidade.</span><span class="sxs-lookup"><span data-stu-id="d829d-168">You should see the new IDPs added as sign-in and sign-up options in each of your identity experiences.</span></span>

<span data-ttu-id="d829d-169">Você pode fazer experiências com suas políticas e observar o efeito no exemplo de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d829d-169">You can experiment with your policies and observe the effect on your sample app.</span></span> <span data-ttu-id="d829d-170">Adicione ou remova IDPs, manipule declarações de aplicativo ou altere os atributos de inscrição.</span><span class="sxs-lookup"><span data-stu-id="d829d-170">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span></span> <span data-ttu-id="d829d-171">Experimente até começar a entender como as políticas, solicitações de autenticação e OWIN funcionam juntos.</span><span class="sxs-lookup"><span data-stu-id="d829d-171">Experiment until you can see how policies, authentication requests, and OWIN tie together.</span></span>

## <a name="sample-code-walkthrough"></a><span data-ttu-id="d829d-172">Passo a passo do código de exemplo</span><span class="sxs-lookup"><span data-stu-id="d829d-172">Sample code walkthrough</span></span>
<span data-ttu-id="d829d-173">As seções a seguir mostram como o código do aplicativo de exemplo está configurado.</span><span class="sxs-lookup"><span data-stu-id="d829d-173">The following sections show you how the sample application code is configured.</span></span> <span data-ttu-id="d829d-174">Você pode usar isso como um guia no desenvolvimento do seu futuro aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d829d-174">You may use this as a guide in your future app development.</span></span>

### <a name="add-authentication-support"></a><span data-ttu-id="d829d-175">Adicionar suporte a autenticação</span><span class="sxs-lookup"><span data-stu-id="d829d-175">Add authentication support</span></span>

<span data-ttu-id="d829d-176">Agora você pode configurar seu aplicativo para usar o Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="d829d-176">You can now configure your app to use Azure AD B2C.</span></span> <span data-ttu-id="d829d-177">Seu aplicativo se comunica com o Azure AD B2C ao enviar solicitações de autenticação OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="d829d-177">Your app communicates with Azure AD B2C by sending OpenID Connect authentication requests.</span></span> <span data-ttu-id="d829d-178">As solicitações determinam a experiência do usuário que o aplicativo deseja executar especificando a política.</span><span class="sxs-lookup"><span data-stu-id="d829d-178">The requests dictate the user experience your app wants to execute by specifying the policy.</span></span> <span data-ttu-id="d829d-179">Você pode usar a biblioteca OWIN da Microsoft para enviar essas solicitações, executar políticas, gerenciar sessões do usuário e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="d829d-179">You can use Microsoft's OWIN library to send these requests, execute policies, manage user sessions, and more.</span></span>

#### <a name="install-owin"></a><span data-ttu-id="d829d-180">Instalar a OWIN</span><span class="sxs-lookup"><span data-stu-id="d829d-180">Install OWIN</span></span>

<span data-ttu-id="d829d-181">Para começar, adicione os pacotes do NuGet de middleware do OWIN ao projeto usando o Console do Gerenciador de Pacotes do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d829d-181">To begin, add the OWIN middleware NuGet packages to the project by using the Visual Studio Package Manager Console.</span></span>

```Console
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
PM> Install-Package Microsoft.Owin.Security.Cookies
PM> Install-Package Microsoft.Owin.Host.SystemWeb
```

#### <a name="add-an-owin-startup-class"></a><span data-ttu-id="d829d-182">Adicionar uma classe de inicialização da OWIN</span><span class="sxs-lookup"><span data-stu-id="d829d-182">Add an OWIN startup class</span></span>

<span data-ttu-id="d829d-183">Adicione uma classe de inicialização OWIN para a API chamada `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="d829d-183">Add an OWIN startup class to the API called `Startup.cs`.</span></span>  <span data-ttu-id="d829d-184">Clique com o botão direito do mouse no projeto, selecione **Adicionar** e **Novo Item** e pesquise OWIN.</span><span class="sxs-lookup"><span data-stu-id="d829d-184">Right-click on the project, select **Add** and **New Item**, and then search for OWIN.</span></span> <span data-ttu-id="d829d-185">O middleware OWIN invocará o método `Configuration(…)` quando seu aplicativo for iniciado.</span><span class="sxs-lookup"><span data-stu-id="d829d-185">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span></span>

<span data-ttu-id="d829d-186">Em nossa amostra, alteramos a declaração de classe para `public partial class Startup` e implementamos a outra parte da classe em `App_Start\Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="d829d-186">In our sample, we changed the class declaration to `public partial class Startup` and implemented the other part of the class in `App_Start\Startup.Auth.cs`.</span></span> <span data-ttu-id="d829d-187">No método `Configuration`, adicionamos uma chamada para `ConfigureAuth`, que é definida em `Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="d829d-187">Inside the `Configuration` method, we added a call to `ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span></span> <span data-ttu-id="d829d-188">Após as modificações, `Startup.cs` é semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="d829d-188">After the modifications, `Startup.cs` looks like the following:</span></span>

```CSharp
// Startup.cs

public partial class Startup
{
    // The OWIN middleware will invoke this method when the app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of the class
        ConfigureAuth(app);
    }
}
```

#### <a name="configure-the-authentication-middleware"></a><span data-ttu-id="d829d-189">Configurar do middleware de autenticação</span><span class="sxs-lookup"><span data-stu-id="d829d-189">Configure the authentication middleware</span></span>

<span data-ttu-id="d829d-190">Abra o arquivo `App_Start\Startup.Auth.cs` e implemente o método `ConfigureAuth(...)`.</span><span class="sxs-lookup"><span data-stu-id="d829d-190">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(...)` method.</span></span> <span data-ttu-id="d829d-191">Os parâmetros que você fornece em `OpenIdConnectAuthenticationOptions` servem como coordenadas para seu aplicativo se comunicar com o Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="d829d-191">The parameters you provide in `OpenIdConnectAuthenticationOptions` serve as coordinates for your app to communicate with Azure AD B2C.</span></span> <span data-ttu-id="d829d-192">Se você não especificar certos parâmetros, ele usará o valor padrão.</span><span class="sxs-lookup"><span data-stu-id="d829d-192">If you do not specify certain parameters, it will use the default value.</span></span> <span data-ttu-id="d829d-193">Por exemplo, não especificamos o `ResponseType` na amostra, então o valor padrão `code id_token` será usado em cada solicitação de saída para o Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="d829d-193">For example, we do not specify the `ResponseType` in the sample, so the default value `code id_token` will be used in each outgoing request to Azure AD B2C.</span></span>

<span data-ttu-id="d829d-194">Você também precisa configurar a autenticação de cookie.</span><span class="sxs-lookup"><span data-stu-id="d829d-194">You also need to set up cookie authentication.</span></span> <span data-ttu-id="d829d-195">O middleware OpenID Connect usa cookies para manter as sessões de usuário, entre outras coisas.</span><span class="sxs-lookup"><span data-stu-id="d829d-195">The OpenID Connect middleware uses cookies to maintain user sessions, among other things.</span></span>

```CSharp
// App_Start\Startup.Auth.cs

public partial class Startup
{
    // Initialize variables ...

    // Configure the OWIN middleware
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseCookieAuthentication(new CookieAuthenticationOptions());
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Generate the metadata address using the tenant and policy information
                MetadataAddress = String.Format(AadInstance, Tenant, DefaultPolicy),

                // These are standard OpenID Connect parameters, with values pulled from web.config
                ClientId = ClientId,
                RedirectUri = RedirectUri,
                PostLogoutRedirectUri = RedirectUri,

                // Specify the callbacks for each type of notifications
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    RedirectToIdentityProvider = OnRedirectToIdentityProvider,
                    AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    AuthenticationFailed = OnAuthenticationFailed,
                },

                // Specify the claims to validate
                TokenValidationParameters = new TokenValidationParameters
                {
                    NameClaimType = "name"
                },

                // Specify the scope by appending all of the scopes requested into one string (seperated by a blank space)
                Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
            }
        );
    }

    // Implement the "Notification" methods...
}
```

<span data-ttu-id="d829d-196">Em `OpenIdConnectAuthenticationOptions` acima, definimos um conjunto de funções de retorno de chamada para notificações específicas que são recebidas pelo middleware OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="d829d-196">In `OpenIdConnectAuthenticationOptions` above, we define a set of callback functions for specific notifications that are received by the OpenID Connect middleware.</span></span> <span data-ttu-id="d829d-197">Esses comportamentos são definidos usando um objeto `OpenIdConnectAuthenticationNotifications` e armazenados na variável `Notifications`.</span><span class="sxs-lookup"><span data-stu-id="d829d-197">These behaviors are defined using a `OpenIdConnectAuthenticationNotifications` object and stored into the `Notifications` variable.</span></span> <span data-ttu-id="d829d-198">Em nossa amostra, podemos definir três retornos de chamada diferentes dependendo do evento.</span><span class="sxs-lookup"><span data-stu-id="d829d-198">In our sample, we define three different callbacks depending on the event.</span></span>

### <a name="using-different-policies"></a><span data-ttu-id="d829d-199">Usando políticas diferentes</span><span class="sxs-lookup"><span data-stu-id="d829d-199">Using different policies</span></span>

<span data-ttu-id="d829d-200">A notificação `RedirectToIdentityProvider` é disparada sempre que uma solicitação é feita ao Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="d829d-200">The `RedirectToIdentityProvider` notification is triggered whenever a request is made to Azure AD B2C.</span></span> <span data-ttu-id="d829d-201">Na função de retorno de chamada `OnRedirectToIdentityProvider`, verificamos na chamada de saída se desejamos usar uma política diferente.</span><span class="sxs-lookup"><span data-stu-id="d829d-201">In the callback function `OnRedirectToIdentityProvider`, we check in the outgoing call if we want to use a different policy.</span></span> <span data-ttu-id="d829d-202">Para fazer uma redefinição de senha ou editar um perfil, você precisa usar a política correspondente, assim como a política de redefinição de senha, em vez da política padrão de "Inscrever-se ou Entrar".</span><span class="sxs-lookup"><span data-stu-id="d829d-202">In order to do a password reset or edit a profile, you need to use the corresponding policy such as the password reset policy instead of the default "Sign-up or Sign-in" policy.</span></span>

<span data-ttu-id="d829d-203">Em nossa amostra, quando um usuário deseja redefinir a senha ou editar o perfil, adicionamos a política que preferimos usar no contexto do OWIN.</span><span class="sxs-lookup"><span data-stu-id="d829d-203">In our sample, when a user wants to reset the password or edit the profile, we add the policy we prefer to use into the OWIN context.</span></span> <span data-ttu-id="d829d-204">Isso pode ser feito fazendo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="d829d-204">That can be done by doing the following:</span></span>

```CSharp
    // Let the middleware know you are trying to use the edit profile policy
    HttpContext.GetOwinContext().Set("Policy", EditProfilePolicyId);
```

<span data-ttu-id="d829d-205">Você também pode implementar a função de retorno de chamada `OnRedirectToIdentityProvider` fazendo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="d829d-205">And you can implement the callback function `OnRedirectToIdentityProvider` by doing the following:</span></span>

```CSharp
/*
*  On each call to Azure AD B2C, check if a policy (e.g. the profile edit or password reset policy) has been specified in the OWIN context.
*  If so, use that policy when making the call. Also, don't request a code (since it won't be needed).
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

### <a name="handling-authorization-codes"></a><span data-ttu-id="d829d-206">Manipulando códigos de autorização</span><span class="sxs-lookup"><span data-stu-id="d829d-206">Handling authorization codes</span></span>

<span data-ttu-id="d829d-207">A notificação `AuthorizationCodeReceived` é disparada quando um código de autorização é recebido.</span><span class="sxs-lookup"><span data-stu-id="d829d-207">The `AuthorizationCodeReceived` notification is triggered when an authorization code is received.</span></span> <span data-ttu-id="d829d-208">O middleware OpenID Connect não dá suporte à permutação de códigos por tokens de acesso.</span><span class="sxs-lookup"><span data-stu-id="d829d-208">The OpenID Connect middleware does not support exchanging codes for access tokens.</span></span> <span data-ttu-id="d829d-209">Você pode permutar manualmente o código pelo token em uma função de retorno de chamada.</span><span class="sxs-lookup"><span data-stu-id="d829d-209">You can manually exchange the code for the token in a callback function.</span></span> <span data-ttu-id="d829d-210">Para obter mais informações, examine a [documentação](active-directory-b2c-devquickstarts-web-api-dotnet.md) que explica como fazê-lo.</span><span class="sxs-lookup"><span data-stu-id="d829d-210">For more information, please look at the [documentation](active-directory-b2c-devquickstarts-web-api-dotnet.md) that explains how.</span></span>

### <a name="handling-errors"></a><span data-ttu-id="d829d-211">Tratamento de erros</span><span class="sxs-lookup"><span data-stu-id="d829d-211">Handling errors</span></span>

<span data-ttu-id="d829d-212">A notificação `AuthenticationFailed` é disparada quando a autenticação falha.</span><span class="sxs-lookup"><span data-stu-id="d829d-212">The `AuthenticationFailed` notification is triggered when authentication fails.</span></span> <span data-ttu-id="d829d-213">Em seu método de retorno de chamada, você pode tratar os erros como desejar.</span><span class="sxs-lookup"><span data-stu-id="d829d-213">In its callback method, you can handle the errors as you wish.</span></span> <span data-ttu-id="d829d-214">No entanto, você deve adicionar uma verificação para o código de erro `AADB2C90118`.</span><span class="sxs-lookup"><span data-stu-id="d829d-214">You should however add a check for the error code `AADB2C90118`.</span></span> <span data-ttu-id="d829d-215">Durante a execução da política "Inscrever-se ou Entrar", o usuário tem a oportunidade de selecionar o link **Esqueceu sua senha?**.</span><span class="sxs-lookup"><span data-stu-id="d829d-215">During the execution of the "Sign-up or Sign-in" policy, the user has the opportunity to select a **Forgot your password?** link.</span></span> <span data-ttu-id="d829d-216">Nesse caso, o Azure AD B2C envia esse código de erro para o seu aplicativo indicando que seu aplicativo faça uma solicitação usando a política de redefinição de senha em vez disso.</span><span class="sxs-lookup"><span data-stu-id="d829d-216">In this event, Azure AD B2C sends your app that error code indicating that your app should make a request using the password reset policy instead.</span></span>

```CSharp
/*
* Catch any failures received by the authentication middleware and handle appropriately
*/
private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    notification.HandleResponse();

    // Handle the error code that Azure AD B2C throws when trying to reset a password from the login page
    // because password reset is not supported by a "sign-up or sign-in policy"
    if (notification.ProtocolMessage.ErrorDescription != null && notification.ProtocolMessage.ErrorDescription.Contains("AADB2C90118"))
    {
        // If the user clicked the reset password link, redirect to the reset password route
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

### <a name="send-authentication-requests-to-azure-ad"></a><span data-ttu-id="d829d-217">Enviar solicitações de autenticação ao AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d829d-217">Send authentication requests to Azure AD</span></span>

<span data-ttu-id="d829d-218">Seu aplicativo agora está configurado corretamente para se comunicar com o AD B2C do Azure usando o protocolo de autenticação OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="d829d-218">Your app is now properly configured to communicate with Azure AD B2C by using the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="d829d-219">O OWIN gerencia todos os detalhes da criação de mensagens de autenticação, validação de tokens do Azure AD B2C e manutenção da sessão do usuário.</span><span class="sxs-lookup"><span data-stu-id="d829d-219">OWIN manages the details of crafting authentication messages, validating tokens from Azure AD B2C, and maintaining user session.</span></span> <span data-ttu-id="d829d-220">Tudo o que resta é iniciar o fluxo de cada usuário.</span><span class="sxs-lookup"><span data-stu-id="d829d-220">All that remains is to initiate each user's flow.</span></span>

<span data-ttu-id="d829d-221">Quando um usuário escolhe **Inscrever-se/Entrar**, **Editar perfil** ou **Redefinir senha** no aplicativo Web, a ação associada é invocada em `Controllers\AccountController.cs`:</span><span class="sxs-lookup"><span data-stu-id="d829d-221">When a user selects **Sign up/Sign in**, **Edit profile**, or **Reset password** in the web app, the associated action is invoked in `Controllers\AccountController.cs`:</span></span>

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting to sign up or sign in
*/
public void SignUpSignIn()
{
    // Use the default policy to process the sign up / sign in flow
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge();
        return;
    }

    Response.Redirect("/");
}

/*
*  Called when requesting to edit a profile
*/
public void EditProfile()
{
    if (Request.IsAuthenticated)
    {
        // Let the middleware know you are trying to use the edit profile policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
        HttpContext.GetOwinContext().Set("Policy", Startup.EditProfilePolicyId);

        // Set the page to redirect to after editing the profile
        var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
        HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

        return;
    }

    Response.Redirect("/");

}

/*
*  Called when requesting to reset a password
*/
public void ResetPassword()
{
    // Let the middleware know you are trying to use the reset password policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
    HttpContext.GetOwinContext().Set("Policy", Startup.ResetPasswordPolicyId);

    // Set the page to redirect to after changing passwords
    var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
    HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

    return;
}
```

<span data-ttu-id="d829d-222">Você também pode usar OWIN para desconectar o usuário do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d829d-222">You can also use OWIN to sign out the user from the app.</span></span> <span data-ttu-id="d829d-223">Em `Controllers\AccountController.cs`, temos:</span><span class="sxs-lookup"><span data-stu-id="d829d-223">In `Controllers\AccountController.cs` we have:</span></span>

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting to sign out
*/
public void SignOut()
{
    // To sign out the user, you should issue an OpenIDConnect sign out request.
    if (Request.IsAuthenticated)
    {
        IEnumerable<AuthenticationDescription> authTypes = HttpContext.GetOwinContext().Authentication.GetAuthenticationTypes();
        HttpContext.GetOwinContext().Authentication.SignOut(authTypes.Select(t => t.AuthenticationType).ToArray());
        Request.GetOwinContext().Authentication.GetAuthenticationTypes();
    }
}
```

<span data-ttu-id="d829d-224">Além de chamar explicitamente uma política, você pode usar uma marca `[Authorize]` em seus controladores que executa uma política se o usuário não estiver conectado.</span><span class="sxs-lookup"><span data-stu-id="d829d-224">In addition to explicitly invoking a policy, you can use a `[Authorize]` tag in your controllers that executes a policy if the user is not signed in.</span></span> <span data-ttu-id="d829d-225">Abra `Controllers\HomeController.cs` e adicione a marca `[Authorize]` ao controlador de declarações.</span><span class="sxs-lookup"><span data-stu-id="d829d-225">Open `Controllers\HomeController.cs` and add the `[Authorize]` tag to the claims controller.</span></span>  <span data-ttu-id="d829d-226">O OWIN seleciona a última política configurada quando a marca `[Authorize]` for atingida.</span><span class="sxs-lookup"><span data-stu-id="d829d-226">OWIN selects the last policy configured when the `[Authorize]` tag is hit.</span></span>

```CSharp
// Controllers\HomeController.cs

// You can use the Authorize decorator to execute a certain policy if the user is not already signed into the app.
[Authorize]
public ActionResult Claims()
{
  ...
```

### <a name="display-user-information"></a><span data-ttu-id="d829d-227">Exibir informações do usuário</span><span class="sxs-lookup"><span data-stu-id="d829d-227">Display user information</span></span>

<span data-ttu-id="d829d-228">Ao autenticar usuários com o OpenID Connect, o Azure AD B2C retorna um token de ID para o aplicativo que contém **declarações**.</span><span class="sxs-lookup"><span data-stu-id="d829d-228">When you authenticate users by using OpenID Connect, Azure AD B2C returns an ID token to the app that contains **claims**.</span></span> <span data-ttu-id="d829d-229">Esses são declarações sobre o usuário.</span><span class="sxs-lookup"><span data-stu-id="d829d-229">These are assertions about the user.</span></span> <span data-ttu-id="d829d-230">Você pode usar as declarações para personalizar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d829d-230">You can use claims to personalize your app.</span></span>

<span data-ttu-id="d829d-231">Abra o arquivo `Controllers\HomeController.cs` .</span><span class="sxs-lookup"><span data-stu-id="d829d-231">Open the `Controllers\HomeController.cs` file.</span></span> <span data-ttu-id="d829d-232">Você pode acessar as declarações do usuário em seus controladores por meio do objeto principal de segurança `ClaimsPrincipal.Current` .</span><span class="sxs-lookup"><span data-stu-id="d829d-232">You can access user claims in your controllers via the `ClaimsPrincipal.Current` security principal object.</span></span>

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

<span data-ttu-id="d829d-233">Você pode acessar qualquer declaração de que seu aplicativo recebe da mesma maneira.</span><span class="sxs-lookup"><span data-stu-id="d829d-233">You can access any claim that your application receives in the same way.</span></span>  <span data-ttu-id="d829d-234">Confira na página **Declarações** uma lista de todas as declarações recebidas pelo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d829d-234">A list of all the claims the app receives is available for you on the **Claims** page.</span></span>
