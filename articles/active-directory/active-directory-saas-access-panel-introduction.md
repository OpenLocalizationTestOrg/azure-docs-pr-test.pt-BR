---
title: "O que é o painel de acesso no Azure Active Directory? | Microsoft Docs"
description: "Saiba como usar variações do painel de acesso (navegador da Web, aplicativo Android, iPhone e iPad) para acessar os aplicativos SaaS."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: c0252d01-7e6e-4f79-a70e-600479577dfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bd9066c251188c0f18fe1a9403baa2beaeeb987c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="what-is-the-access-panel"></a><span data-ttu-id="e0bff-104">O que é o painel de acesso?</span><span class="sxs-lookup"><span data-stu-id="e0bff-104">What is the access panel?</span></span>

<span data-ttu-id="e0bff-105">O painel de acesso é um portal baseado na Web.</span><span class="sxs-lookup"><span data-stu-id="e0bff-105">The access panel is a web-based portal.</span></span> <span data-ttu-id="e0bff-106">Ele permite que um usuário com uma conta corporativa ou de estudante no Azure Active Directory exiba e inicie aplicativos baseados em nuvem que um administrador do Azure AD concedeu acesso.</span><span class="sxs-lookup"><span data-stu-id="e0bff-106">It enables a user with a work or school account in Azure Active Directory to view and start cloud-based applications an Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="e0bff-107">Você também pode usar os recursos de gerenciamento de grupo de autoatendimento e aplicativo por meio do painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="e0bff-107">You can also use self-service group and app management capabilities through the access panel.</span></span>

<span data-ttu-id="e0bff-108">O painel de acesso é separado do Portal do Azure e você não tem uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="e0bff-108">The access panel is separate from the Azure portal and does not you to have an Azure subscription.</span></span>

![Painel de acesso][1]

<span data-ttu-id="e0bff-110">O painel de acesso permite que você edite algumas de suas configurações de perfil, incluindo a capacidade de:</span><span class="sxs-lookup"><span data-stu-id="e0bff-110">The access panel enables you to edit some of your profile settings, including the ability to:</span></span>

- <span data-ttu-id="e0bff-111">Alterar a senha associada a uma conta corporativa ou de estudante</span><span class="sxs-lookup"><span data-stu-id="e0bff-111">Change the password associated with a work or school account</span></span>

- <span data-ttu-id="e0bff-112">Editar configurações de redefinição de senha</span><span class="sxs-lookup"><span data-stu-id="e0bff-112">Edit password reset settings</span></span>

- <span data-ttu-id="e0bff-113">Editar configurações de preferências e contato relacionadas a autenticação multifator (para contas cujo administrador solicitou o uso desse recurso)</span><span class="sxs-lookup"><span data-stu-id="e0bff-113">Edit contact and preference settings related to multi-factor authentication (for accounts that have been required to use it by an administrator)</span></span>

- <span data-ttu-id="e0bff-114">Exibir detalhes da conta, como ID de usuário, email alternativo, números de celular e do escritório e dispositivos</span><span class="sxs-lookup"><span data-stu-id="e0bff-114">View account details, such as user ID, alternate email, and mobile and office phone numbers, and devices</span></span>

- <span data-ttu-id="e0bff-115">Exibir e iniciar aplicativos baseados em nuvem aos quais o administrador do Azure AD concedeu acesso.</span><span class="sxs-lookup"><span data-stu-id="e0bff-115">View and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="e0bff-116">Para saber mais sobre o painel de acesso da perspectiva dos usuários, veja Usando o painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="e0bff-116">For more information about the access panel from the users’ perspective, see Using the access panel.</span></span> 

- <span data-ttu-id="e0bff-117">Autogerenciar grupos.</span><span class="sxs-lookup"><span data-stu-id="e0bff-117">Self-manage groups.</span></span> <span data-ttu-id="e0bff-118">Mais especificamente, o administrador pode criar e gerenciar grupos de segurança e solicitar associações ao grupo de segurança no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e0bff-118">More specifically, the administrator can create and manage security groups and request security group memberships in Azure AD.</span></span> <span data-ttu-id="e0bff-119">Para saber mais, confira [Gerenciamento de grupo de autoatendimento para usuários no Azure AD](active-directory-accessmanagement-self-service-group-management.md) e [Gerenciar seus grupos](active-directory-manage-groups.md).</span><span class="sxs-lookup"><span data-stu-id="e0bff-119">For more information, see [Self-service group management for users in Azure AD](active-directory-accessmanagement-self-service-group-management.md) and [Manage your groups](active-directory-manage-groups.md).</span></span>




## <a name="accessing-the-access-panel"></a><span data-ttu-id="e0bff-120">Acessando o painel de acesso</span><span class="sxs-lookup"><span data-stu-id="e0bff-120">Accessing the access panel</span></span>

<span data-ttu-id="e0bff-121">Você pode acessar o painel de acesso visitando a seguinte URL em um navegador da Web: `http://myapps.microsoft.com`</span><span class="sxs-lookup"><span data-stu-id="e0bff-121">You can access the access panel by visiting the following URL in a web browser: `http://myapps.microsoft.com`</span></span>

<span data-ttu-id="e0bff-122">Se tiver a identidade visual personalizada configurada para sua página de entrada, você poderá carregar essa identidade visual, anexando o domínio da sua organização ao final da URL: `http://myapps.microsoft.com/<your domain>.com`</span><span class="sxs-lookup"><span data-stu-id="e0bff-122">If you have custom branding configured for your sign-in page, you can load this branding by appending your organization’s domain to the end of the URL: `http://myapps.microsoft.com/<your domain>.com`</span></span>

<span data-ttu-id="e0bff-123">Nesse caso, você pode usar qualquer nome de domínio ativo ou verificado que foi configurado no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e0bff-123">In this case, you can use any active or verified domain name that has been configured in your Azure portal.</span></span>

![Nome de domínio Wingtip Toys][2]  

<span data-ttu-id="e0bff-125">Você precisa distribuir a URL a todos os usuários que entrarão nos aplicativos integrados ao Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e0bff-125">You need to distribute the URL to all users who will sign in to applications that are integrated with Azure AD.</span></span>

## <a name="authentication"></a><span data-ttu-id="e0bff-126">Autenticação</span><span class="sxs-lookup"><span data-stu-id="e0bff-126">Authentication</span></span>

<span data-ttu-id="e0bff-127">Para acessar o painel de acesso, você deve ser autenticado usando uma conta corporativa ou de estudante no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e0bff-127">To reach the access panel, you must be authenticated through a work or school account in Azure AD.</span></span> <span data-ttu-id="e0bff-128">Você pode ser autenticado no Azure AD diretamente.</span><span class="sxs-lookup"><span data-stu-id="e0bff-128">You can be authenticated to Azure AD directly.</span></span> <span data-ttu-id="e0bff-129">Como alternativa, se uma organização tiver configurado a federação usando o AD FS (Serviços de Federação do Active Directory) ou outras tecnologias, você pode ser autenticado pelo Windows Server Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e0bff-129">Alternatively, if an organization has configured federation by using Active Directory Federation Services (AD FS) or other technologies, you can be authenticated by Windows Server Active Directory.</span></span>

<span data-ttu-id="e0bff-130">Se você tiver uma assinatura do Azure ou Office 365 e estiver usando o Portal do Azure ou um aplicativo do Office 365, você verá a lista de aplicativos sem entrar novamente.</span><span class="sxs-lookup"><span data-stu-id="e0bff-130">If you have a subscription for Azure or Office 365 and you have been using the Azure portal or an Office 365 application, you can see the list of applications without signing-in again.</span></span> <span data-ttu-id="e0bff-131">Se você não está autenticado receberá uma solicitação para entrar usando o nome de usuário e a senha de sua conta no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e0bff-131">If you are are not authenticated you are prompted to sign in by using the username and password for your account in Azure AD.</span></span> <span data-ttu-id="e0bff-132">Se sua organização tiver configurado a federação, digitar o nome do usuário será suficiente.</span><span class="sxs-lookup"><span data-stu-id="e0bff-132">If your organization has configured federation, typing the username is sufficient.</span></span>

<span data-ttu-id="e0bff-133">Quando está autenticado, você pode interagir com os aplicativos integrados ao diretório pelo administrador.</span><span class="sxs-lookup"><span data-stu-id="e0bff-133">When you are authenticated, you can interact with the applications that your administrator has integrated with the directory.</span></span> <span data-ttu-id="e0bff-134">Para saber como integrar aplicativos ao Azure AD, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e0bff-134">To learn how to integrate applications with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="web-browser-requirements"></a><span data-ttu-id="e0bff-135">Requisitos de navegador da Web</span><span class="sxs-lookup"><span data-stu-id="e0bff-135">Web browser requirements</span></span>

<span data-ttu-id="e0bff-136">O painel de acesso exige, pelo menos, um navegador com suporte para JavaScript e CSS habilitado.</span><span class="sxs-lookup"><span data-stu-id="e0bff-136">At a minimum, the access panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="e0bff-137">Para que o usuário possa acessar os aplicativos usando SSO (logon único) baseado em senha, a extensão do painel de acesso deve estar instalada no seu navegador.</span><span class="sxs-lookup"><span data-stu-id="e0bff-137">For the user to be signed in to applications through password-based single sign-on (SSO), the access panel extension must be installed in your browser.</span></span> <span data-ttu-id="e0bff-138">A extensão é baixada automaticamente quando você seleciona um aplicativo configurado para SSO baseado em senha.</span><span class="sxs-lookup"><span data-stu-id="e0bff-138">The extension is downloaded automatically when you select an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="e0bff-139">No momento, a extensão do painel de acesso está disponível para os navegadores Internet Explorer 8 e superior, Edge, Chrome e Firefox.</span><span class="sxs-lookup"><span data-stu-id="e0bff-139">The access panel extension is currently available for Internet Explorer 8 and later, Edge, Chrome, and Firefox browsers.</span></span>

## <a name="mobile-app-support"></a><span data-ttu-id="e0bff-140">Suporte a aplicativos móveis</span><span class="sxs-lookup"><span data-stu-id="e0bff-140">Mobile app support</span></span>

<span data-ttu-id="e0bff-141">A equipe do Azure Active Directory publica o aplicativo móvel Meus Aplicativos.</span><span class="sxs-lookup"><span data-stu-id="e0bff-141">The Azure Active Directory team publishes the my apps mobile app.</span></span> <span data-ttu-id="e0bff-142">Quando você instala esse aplicativo, você pode entrar em aplicativos de SSO baseado em senha em dispositivos iOS e Android.</span><span class="sxs-lookup"><span data-stu-id="e0bff-142">When you install the app, you can sign in to password-based SSO applications on iOS and Android devices.</span></span>

> [!NOTE]
> <span data-ttu-id="e0bff-143">Você pode entrar em aplicativos que dão suporte à federação com o Azure AD (incluindo Salesforce, Google Apps, Dropbox, Box, Concur, Workday, Office 365 e mais de 70 outros) em praticamente qualquer navegador da Web em qualquer dispositivo, sem a necessidade de um plug-in ou aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="e0bff-143">You can sign in to applications that support federation with Azure AD (including Salesforce, Google Apps, Dropbox, Box, Concur, Workday, Office 365, and more than 70 others) on virtually any web browser, on any device, without needing a plug-in or mobile app.</span></span> <span data-ttu-id="e0bff-144">O restante da [experiência do Painel de Acesso](https://myapps.microsoft.com/) também não exige que o aplicativo móvel Meus Aplicativos seja usado em um dispositivo móvel.</span><span class="sxs-lookup"><span data-stu-id="e0bff-144">All other [access panel experiences](https://myapps.microsoft.com/) do also not require the my apps mobile app to be used on a mobile device.</span></span>
>
>

### <a name="my-apps-for-android"></a><span data-ttu-id="e0bff-145">Meus aplicativos para Android</span><span class="sxs-lookup"><span data-stu-id="e0bff-145">My apps for Android</span></span>

<span data-ttu-id="e0bff-146">Meus aplicativos para Android tem suporte em qualquer dispositivo Android que esteja executando o Android versão 4.1 e posteriores.</span><span class="sxs-lookup"><span data-stu-id="e0bff-146">My apps for Android is supported on any Android device that is running Android version 4.1 and later.</span></span>  
<span data-ttu-id="e0bff-147">Ele está disponível na [Google Play Store](https://play.google.com/store/apps/details?id=com.microsoft.myapps).</span><span class="sxs-lookup"><span data-stu-id="e0bff-147">It is available in the [Google Play store](https://play.google.com/store/apps/details?id=com.microsoft.myapps).</span></span>

![Meus aplicativos para Android][3]   

### <a name="my-apps-for-iphone-and-ipad"></a><span data-ttu-id="e0bff-149">Meus aplicativos para iPhone e iPad</span><span class="sxs-lookup"><span data-stu-id="e0bff-149">My apps for iPhone and iPad</span></span>

<span data-ttu-id="e0bff-150">Meus aplicativos para iOS tem suporte em qualquer iPhone ou iPad que esteja executando a versão do iOS 7 e posterior.</span><span class="sxs-lookup"><span data-stu-id="e0bff-150">My apps for iOS is supported on any iPhone or iPad that is running iOS version 7 and later.</span></span>  
<span data-ttu-id="e0bff-151">Ele está disponível na [Apple App Store](https://itunes.apple.com/us/app/my-apps-azure-active-directory/id824048653?mt=8).</span><span class="sxs-lookup"><span data-stu-id="e0bff-151">It is available in the [Apple App Store](https://itunes.apple.com/us/app/my-apps-azure-active-directory/id824048653?mt=8).</span></span>

![Meus aplicativos para iOS][4]    



## <a name="managed-browser-for-my-apps"></a><span data-ttu-id="e0bff-153">Navegador gerenciado para Meus aplicativos</span><span class="sxs-lookup"><span data-stu-id="e0bff-153">Managed browser for my apps</span></span>

<span data-ttu-id="e0bff-154">Meus aplicativos também é integrado no Intune Managed Browser.</span><span class="sxs-lookup"><span data-stu-id="e0bff-154">My apps is also integrated in the Intune Managed Browser.</span></span> <span data-ttu-id="e0bff-155">O Intune Managed Browser para dispositivos iOS e Android desempenha uma função fundamental em assegurar que os dados em dispositivos móveis permaneçam seguros.</span><span class="sxs-lookup"><span data-stu-id="e0bff-155">The Intune Managed Browser for iOS and Android devices plays a key role in ensuring that data on mobile devices stays secure.</span></span> <span data-ttu-id="e0bff-156">Ele permite exibir e navegar por páginas da web que podem conter informações da empresa e fornece uma experiência de navegação na web segura.</span><span class="sxs-lookup"><span data-stu-id="e0bff-156">It lets you safely view and navigate web pages that might contain company information, and provides a secure web-browsing experience.</span></span>  
<span data-ttu-id="e0bff-157">Você encontrar acesso rápido aos meus aplicativos em sua home page no Managed Browser e em seus favoritos, fornecendo menos cliques para acessar qualquer aplicativo que você deseja acessar.</span><span class="sxs-lookup"><span data-stu-id="e0bff-157">You find quick access to my apps on your Managed Browser homepage and in your bookmarks, giving you fewer clicks to reach any application you want to access.</span></span>

<span data-ttu-id="e0bff-158">Ele está disponível na [Apple App Store](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) e na [Google Play Store](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en).</span><span class="sxs-lookup"><span data-stu-id="e0bff-158">It is available in the [Apple App Store](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) and [Google Play Store](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en).</span></span>

![Navegador gerenciado para Meus aplicativos][5]    





## <a name="tips-for-testing-the-user-experience"></a><span data-ttu-id="e0bff-160">Dicas para testar a experiência do usuário</span><span class="sxs-lookup"><span data-stu-id="e0bff-160">Tips for testing the user experience</span></span>

<span data-ttu-id="e0bff-161">Se você for um administrador do Azure e estiver conectado ao Portal do Azure usando uma conta no diretório, será automaticamente conectado ao painel de acesso como sua conta atual.</span><span class="sxs-lookup"><span data-stu-id="e0bff-161">If you are an Azure administrator and you are signed in to the Azure portal by using an account in the directory, you are automatically signed in to the access panel as your current account.</span></span> <span data-ttu-id="e0bff-162">Nesse caso, você pode ver todos os aplicativos atribuídos a você.</span><span class="sxs-lookup"><span data-stu-id="e0bff-162">In this case, you can see all applications that have been assigned to you.</span></span>

<span data-ttu-id="e0bff-163">**Para testar como uma *conta de usuário* diferente:**</span><span class="sxs-lookup"><span data-stu-id="e0bff-163">**To test as a *different* user account:**</span></span>

1. <span data-ttu-id="e0bff-164">Clique no menu de usuário no canto superior direito do Portal do Azure ou no painel de acesso e, em seguida, selecione **Sair**.</span><span class="sxs-lookup"><span data-stu-id="e0bff-164">Click the user menu in the upper-right corner of the Azure portal or the access panel, and then select **Sign Out**.</span></span> 
2. <span data-ttu-id="e0bff-165">Acesse o [painel de acesso](http://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="e0bff-165">Go to the [access panel](http://myapps.microsoft.com).</span></span>
3. <span data-ttu-id="e0bff-166">Na página de entrada, digite o nome de usuário e a senha da conta no diretório que você quer testar.</span><span class="sxs-lookup"><span data-stu-id="e0bff-166">On the sign-in page, type the username and password for the account in your directory you want to test.</span></span>


## <a name="starting-applications"></a><span data-ttu-id="e0bff-167">Iniciar aplicativos</span><span class="sxs-lookup"><span data-stu-id="e0bff-167">Starting applications</span></span>

<span data-ttu-id="e0bff-168">Vários tipos de aplicativos podem aparecer no painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="e0bff-168">Several types of applications can appear on the access panel.</span></span>

### <a name="office-365-applications"></a><span data-ttu-id="e0bff-169">Aplicativos do Office 365</span><span class="sxs-lookup"><span data-stu-id="e0bff-169">Office 365 applications</span></span>

<span data-ttu-id="e0bff-170">Se sua organização estiver usando aplicativos do Office 365 e você for licenciado para eles, os aplicativos do Office 365 serão exibidos no seu painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="e0bff-170">If your organization is using Office 365 applications and you are licensed for them, the Office 365 applications appear on your access panel.</span></span>

<span data-ttu-id="e0bff-171">Quando você clica em um bloco do aplicativo para um aplicativo do Office 365, você é redirecionado para o aplicativo e conectado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e0bff-171">When you click an application tile for an Office 365 application, you are redirected to the application and automatically signed in.</span></span>

### <a name="microsoft-and-third-party-applications-configured-with-federation-based-sso"></a><span data-ttu-id="e0bff-172">Aplicativos da Microsoft e de terceiros configurados com o SSO baseado em federação</span><span class="sxs-lookup"><span data-stu-id="e0bff-172">Microsoft and third-party applications configured with federation-based SSO</span></span>

<span data-ttu-id="e0bff-173">Seu administrador pode adicionar aplicativos na seção Active Directory do Portal do Azure com o modo SSO definido como **Logon único do Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="e0bff-173">Your administrator can add applications in the Active Directory section of the Azure portal with the SSO mode set to **Azure AD Single Sign-On**.</span></span> <span data-ttu-id="e0bff-174">Você somente poderá ver esses aplicativos se seu administrador tiver concedido explicitamente a você acesso aos aplicativos.</span><span class="sxs-lookup"><span data-stu-id="e0bff-174">You can only see these applications if your administrator has explicitly granted you access to the applications.</span></span>

<span data-ttu-id="e0bff-175">Quando você clica em um bloco de um desses aplicativos, você é redirecionado e conectado automaticamente a esse aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e0bff-175">When you click a tile for one of these applications, you are redirected and automatically signed in to the application.</span></span>

### <a name="password-based-sso-without-identity-provisioning"></a><span data-ttu-id="e0bff-176">SSO baseado em senha sem provisionamento de identidade</span><span class="sxs-lookup"><span data-stu-id="e0bff-176">Password-based SSO without identity provisioning</span></span>

<span data-ttu-id="e0bff-177">Seu administrador pode adicionar aplicativos na seção Active Directory do Portal do Azure com o modo SSO definido como **Logon único do baseado em senha**.</span><span class="sxs-lookup"><span data-stu-id="e0bff-177">Your administrator can add applications in the Active Directory section of the Azure portal with the SSO mode set to **Password-based Single Sign-On**.</span></span> <span data-ttu-id="e0bff-178">Todos os usuários no diretório podem ver todos os aplicativos configurados nesse modo.</span><span class="sxs-lookup"><span data-stu-id="e0bff-178">All users in the directory can see all applications that have been configured in this mode.</span></span>

<span data-ttu-id="e0bff-179">Na primeira vez que você clica em um bloco de um desses aplicativos, você recebe uma solicitação para instalar o plug-in do SSO de senha para o Internet Explorer ou Chrome.</span><span class="sxs-lookup"><span data-stu-id="e0bff-179">The first time, you click a tile for one of these applications, you are prompted to install the Password SSO plug-in for Internet Explorer or Chrome.</span></span> <span data-ttu-id="e0bff-180">A instalação pode exigir você a reinicialização do seu navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="e0bff-180">The installation might require you to restart your web browser.</span></span> <span data-ttu-id="e0bff-181">Quando você retorna ao painel de acesso e clica novamente no bloco do aplicativo, você recebe uma solicitação para inserir um nome de usuário e senha para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e0bff-181">When you return to the access panel and click the application tile again, you are prompted for a username and password for the application.</span></span> <span data-ttu-id="e0bff-182">Quando você inseriu o nome de usuário e senha, essas credenciais são armazenadas com segurança no e vinculadas à sua conta no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e0bff-182">When you have entered your username and password, these credentials are securely stored and linked to your account in Azure AD.</span></span>

<span data-ttu-id="e0bff-183">Na próxima vez que você clicar no bloco de aplicativo, será automaticamente conectado ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e0bff-183">The next time you click the application tile, you are automatically signed in to the application.</span></span>  
<span data-ttu-id="e0bff-184">Você não precisará inserir suas credenciais novamente e/ou instalar o plug-in do SSO de senha.</span><span class="sxs-lookup"><span data-stu-id="e0bff-184">You don't have to enter your credentials again and or install the Password SSO plug-in.</span></span>

<span data-ttu-id="e0bff-185">Se suas credenciais de um usuário forem alteradas no aplicativo de terceiros de destino, você também deverá atualizar suas credenciais armazenadas no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e0bff-185">If your credentials have changed in the target third-party application, you must also update your credentials that are stored in Azure AD.</span></span> 

<span data-ttu-id="e0bff-186">**Para atualizar as credenciais:**</span><span class="sxs-lookup"><span data-stu-id="e0bff-186">**To update credentials:**</span></span>

1. <span data-ttu-id="e0bff-187">Selecione o ícone no bloco do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e0bff-187">Select the icon on the application tile.</span></span>
2. <span data-ttu-id="e0bff-188">Selecione **atualizar credenciais** para inserir novamente o nome de usuário e a senha para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e0bff-188">Select **update credentials** to reenter the username and password for the application.</span></span>


### <a name="password-based-sso-with-identity-provisioning"></a><span data-ttu-id="e0bff-189">SSO baseado em senha com provisionamento de identidade</span><span class="sxs-lookup"><span data-stu-id="e0bff-189">Password-based SSO with identity provisioning</span></span>

<span data-ttu-id="e0bff-190">Seu administrador pode adicionar aplicativos na seção **Active Directory** do Portal do Azure com o modo SSO definido como **Logon único do baseado em senha** junto com o provisionamento da identidade.</span><span class="sxs-lookup"><span data-stu-id="e0bff-190">Your administrator can add applications in the **Active Directory** section of the Azure portal with the SSO mode set to **Password-based Single Sign-On**, along with identity provisioning.</span></span>

<span data-ttu-id="e0bff-191">Na primeira vez que você clica em um bloco de aplicativo de um desses aplicativos, você recebe uma solicitação para instalar o **plug-in do SSO de senha para o Internet Explorer ou Chrome**.</span><span class="sxs-lookup"><span data-stu-id="e0bff-191">The first time, you click an application tile for one of these applications, you are prompted to install the **Password SSO plug-in for Internet Explorer or Chrome**.</span></span> <span data-ttu-id="e0bff-192">A instalação pode exigir você a reinicialização do seu navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="e0bff-192">The installation might require you to restart your web browser.</span></span>  
<span data-ttu-id="e0bff-193">Quando você retorna ao painel de acesso e clica novamente no bloco do aplicativo, você é automaticamente conectado ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e0bff-193">When you return to the access panel and click the application tile again, you are automatically signed in to the application.</span></span>

<span data-ttu-id="e0bff-194">Alguns aplicativos podem exigir que você altere sua senha na primeira entrada.</span><span class="sxs-lookup"><span data-stu-id="e0bff-194">Some applications might require you to change your password on the first sign-in.</span></span> <span data-ttu-id="e0bff-195">Se suas credenciais de um usuário forem alteradas no aplicativo de terceiros de destino, você também deverá atualizar as credenciais armazenadas no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e0bff-195">If your credentials have changed in the target third-party application, you must also update the credentials that are stored in Azure AD.</span></span> 

<span data-ttu-id="e0bff-196">**Para atualizar as credenciais:**</span><span class="sxs-lookup"><span data-stu-id="e0bff-196">**To update credentials:**</span></span>

1. <span data-ttu-id="e0bff-197">Selecione o ícone no bloco do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e0bff-197">Select the icon on the application tile.</span></span>
2. <span data-ttu-id="e0bff-198">Selecione **atualizar credenciais** para inserir novamente o nome de usuário e a senha para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e0bff-198">Select **update credentials** to reenter the username and password for the application.</span></span>


### <a name="application-with-existing-sso-solutions"></a><span data-ttu-id="e0bff-199">Aplicativos com soluções de SSO existentes</span><span class="sxs-lookup"><span data-stu-id="e0bff-199">Application with existing SSO solutions</span></span>

<span data-ttu-id="e0bff-200">Para configurar o SSO para um aplicativo, o Portal do Azure fornece uma terceira opção chamada de **Logon Único Existente**.</span><span class="sxs-lookup"><span data-stu-id="e0bff-200">To configure SSO for an application, the Azure portal provides a third option called **Existing Single Sign-On**.</span></span> <span data-ttu-id="e0bff-201">Essa opção permite que o administrador crie um link para um aplicativo e coloque-o no painel de acesso para os usuários selecionados.</span><span class="sxs-lookup"><span data-stu-id="e0bff-201">This option enables your administrator to create a link to an application and place it on the access panel for selected users.</span></span>

<span data-ttu-id="e0bff-202">Por exemplo, se um aplicativo for configurado para autenticar usuários usando o AD FS 2.0, seu administrador poderá usar a opção **Logon Único Existente** para criar um link para ele no painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="e0bff-202">For example, if an application is configured to authenticate users by using AD FS 2.0, your administrator can use the **Existing Single Sign-On** option to create a link to it on the access panel.</span></span> <span data-ttu-id="e0bff-203">Quando os você acessar o link, você é autenticado por meio do AD FS 2.0 ou por qualquer solução de SSO existente fornecida pelo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e0bff-203">When you access the link, you are authenticated through AD FS 2.0 or whatever existing SSO solution the application provides.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e0bff-204">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e0bff-204">Next steps</span></span>

- <span data-ttu-id="e0bff-205">Para ver uma lista de todos os tópicos relacionados ao gerenciamento de aplicativos, consulte o [índice do artigo para gerenciamento de aplicativos no Azure Active Directory](active-directory-apps-index.md).</span><span class="sxs-lookup"><span data-stu-id="e0bff-205">To see a list of all topics that are related to application management, see the [article index for application management in Azure Active Directory](active-directory-apps-index.md).</span></span>
 
- <span data-ttu-id="e0bff-206">Para saber como integrar um aplicativo SaaS no AD do Azure, consulte a [lista de tutoriais sobre como integrar aplicativos SaaS](active-directory-saas-tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="e0bff-206">To learn how to integrate a SaaS app into Azure AD, see the [list of tutorials on how to integrate SaaS apps](active-directory-saas-tutorial-list.md).</span></span>
 
- <span data-ttu-id="e0bff-207">Para saber mais sobre como gerenciar aplicativos com o AD do Azure, consulte a [Introdução ao acesso ao aplicativo de gerenciamento e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e0bff-207">To learn more about managing apps with Azure AD, see the [introduction to single sign-on and managing app access with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>
 
- <span data-ttu-id="e0bff-208">Para obter mais informações sobre provisionamento de usuário, consulte [aplicativos SaaS para provisionamento e desprovisionamento automatizado do usuário](active-directory-saas-app-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="e0bff-208">To learn more about user provisioning, see [automate user provisioning and deprovisioning to SaaS applications](active-directory-saas-app-provisioning.md).</span></span>

<!--Image references-->
[1]: ./media/active-directory-saas-access-panel-introduction/01.png
[2]: ./media/active-directory-saas-access-panel-introduction/02.png
[3]: ./media/active-directory-saas-access-panel-introduction/03.png
[4]: ./media/active-directory-saas-access-panel-introduction/04.png
[5]: ./media/active-directory-saas-access-panel-introduction/05.png
