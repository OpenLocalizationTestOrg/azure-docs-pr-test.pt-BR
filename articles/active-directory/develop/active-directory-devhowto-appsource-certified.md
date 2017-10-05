---
title: Como certificar o AppSource para o Azure Active Directory| Microsoft Docs
description: Detalhes sobre como certificar o AppSource do seu aplicativo para o Azure Active Directory.
services: active-directory
documentationcenter: 
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 21206407-49f8-4c0b-84d1-c25e17cd4183
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/03/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: d8e2f8fc19ff879e6a7b632f033fd0ed9d77392a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-get-appsource-certified-for-azure-active-directory"></a><span data-ttu-id="8f47c-103">Como certificar o AppSource para o Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f47c-103">How to get AppSource Certified for Azure Active Directory</span></span>
<span data-ttu-id="8f47c-104">O [Microsoft AppSource](https://appsource.microsoft.com/) é um local onde os usuários de negócios podem descobrir, experimentar e gerenciar aplicativos SaaS de linha de negócios (SaaS autônomos e o complemento para produtos SaaS da Microsoft existentes).</span><span class="sxs-lookup"><span data-stu-id="8f47c-104">[Microsoft AppSource](https://appsource.microsoft.com/) is a destination for business users to discover, try, and manage line-of-business SaaS applications (standalone SaaS and add-on to existing Microsoft SaaS products).</span></span>

<span data-ttu-id="8f47c-105">Para listar um aplicativo SaaS autônomo no AppSource, seu aplicativo deve aceitar logon único de contas corporativas de qualquer empresa ou organização que possua o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8f47c-105">To list a standalone SaaS application on AppSource, your application must accept single sign-on from work accounts from any company or organization that has Azure Active Directory.</span></span> <span data-ttu-id="8f47c-106">O processo de entrada deve usar o protocolo [OpenID Connect](./active-directory-protocols-openid-connect-code.md) ou [OAuth 2.0](./active-directory-protocols-oauth-code.md).</span><span class="sxs-lookup"><span data-stu-id="8f47c-106">The sign-in process must use the [OpenID Connect](./active-directory-protocols-openid-connect-code.md) or [OAuth 2.0](./active-directory-protocols-oauth-code.md) protocols.</span></span> <span data-ttu-id="8f47c-107">A integração SAML não é aceita para certificação AppSource.</span><span class="sxs-lookup"><span data-stu-id="8f47c-107">SAML integration is not accepted for AppSource certification.</span></span>

## <a name="guides-and-code-samples"></a><span data-ttu-id="8f47c-108">Guias e exemplos de código</span><span class="sxs-lookup"><span data-stu-id="8f47c-108">Guides and code samples</span></span>
<span data-ttu-id="8f47c-109">Se você quiser saber mais sobre como integrar seu aplicativo com o Azure Active Directory usando Open ID Connect, siga nossos guias e exemplos de código no [guia do desenvolvedor do Azure Active Directory](./active-directory-developers-guide.md#get-started "Introdução ao Azure AD para desenvolvedores").</span><span class="sxs-lookup"><span data-stu-id="8f47c-109">If you want to learn about how to integrate your application with Azure Active Directory using Open ID connect, follow our guides and code samples in the [Azure Active Directory developer's guide](./active-directory-developers-guide.md#get-started "Get Started with Azure AD for developers").</span></span>

## <a name="multi-tenant-applications"></a><span data-ttu-id="8f47c-110">Aplicativos multilocatários</span><span class="sxs-lookup"><span data-stu-id="8f47c-110">Multi-tenant applications</span></span>

<span data-ttu-id="8f47c-111">Um aplicativo que aceita entradas de usuários de qualquer empresa ou organização que tenha o Azure Active Directory sem a necessidade de uma instância, configuração ou implantação separada é conhecido como *aplicativo multilocatário*.</span><span class="sxs-lookup"><span data-stu-id="8f47c-111">An application that accepts sign-ins from users from any company or organization that have Azure Active Directory without requiring a separate instance, configuration, or deployment is known as a *multi-tenant application*.</span></span> <span data-ttu-id="8f47c-112">O AppSource recomenda que os aplicativos implementem multilocação para habilitar a experiência de avaliação com um *clique simples*.</span><span class="sxs-lookup"><span data-stu-id="8f47c-112">AppSource recommends that applications implement multi-tenancy to enable the *single-click* free trial experience.</span></span>

<span data-ttu-id="8f47c-113">Para habilitar a multilocação em seu aplicativo:</span><span class="sxs-lookup"><span data-stu-id="8f47c-113">In order to enable multi-tenancy on your application:</span></span>
- <span data-ttu-id="8f47c-114">Defina a propriedade `Multi-Tenanted` como `Yes` nas informações do registro do aplicativo no [Portal do Azure](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) (por padrão, os aplicativos criados no Portal do Azure são configurados como *único locatário*)</span><span class="sxs-lookup"><span data-stu-id="8f47c-114">Set `Multi-Tenanted` property to `Yes` on your application registration's information in the [Azure Portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) (by default, applications created in the Azure Portal are configured as *single-tenant*)</span></span>
- <span data-ttu-id="8f47c-115">Atualize seu código para enviar solicitações para o ponto de extremidade '`common`' (atualize o ponto de extremidade em *https://login.microsoftonline.com/{seulocatario}* para *https://login.microsoftonline.com/common*)</span><span class="sxs-lookup"><span data-stu-id="8f47c-115">Update your code to send requests to the '`common`' endpoint (update the endpoint from *https://login.microsoftonline.com/{yourtenant}* to *https://login.microsoftonline.com/common*)</span></span>
- <span data-ttu-id="8f47c-116">Para algumas plataformas, como o ASP.NET, você também precisa atualizar seu código para aceitar vários emissores</span><span class="sxs-lookup"><span data-stu-id="8f47c-116">For some platforms, like ASP.NET, you need also to update your code to accept multiple issuers</span></span>

<span data-ttu-id="8f47c-117">Para saber mais sobre multilocação, confira: [Como conectar qualquer usuário do Azure AD (Active Directory) usando o padrão de aplicativo multilocatário](./active-directory-devhowto-multi-tenant-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8f47c-117">For more information about multi-tenancy, see: [How to sign in any Azure Active Directory (AD) user using the multi-tenant application pattern](./active-directory-devhowto-multi-tenant-overview.md).</span></span>

### <a name="single-tenant-applications"></a><span data-ttu-id="8f47c-118">Aplicativos de locatário único</span><span class="sxs-lookup"><span data-stu-id="8f47c-118">Single-tenant applications</span></span>
<span data-ttu-id="8f47c-119">Aplicativos que só aceitam entradas de usuários de uma instância definida do Azure Active Directory são conhecidos como *aplicativo de locatário único*.</span><span class="sxs-lookup"><span data-stu-id="8f47c-119">Applications that only accept sign-ins from users of a defined Azure Active Directory instance are known as *single-tenant application*.</span></span> <span data-ttu-id="8f47c-120">Os usuários externos (incluindo as contas corporativas ou de estudante de outras organizações, ou conta pessoal) podem entrar em um aplicativo de locatário único depois de adicionar cada usuário como *conta convidado* à instância do Azure Active Directory em que o aplicativo está registrado.</span><span class="sxs-lookup"><span data-stu-id="8f47c-120">External users (including Work or School accounts from other organizations, or personal account) can sign in to a single-tenant application after adding each user as *guest account* to the Azure Active Directory instance that the application is registered.</span></span> <span data-ttu-id="8f47c-121">Você pode adicionar usuários como contas de convidado a um Azure Active Directory por meio de [ *colaboração B2B do Azure AD* ](../active-directory-b2b-what-is-azure-ad-b2b.md), e isso pode ser feito [programaticamente](../active-directory-b2b-code-samples.md).</span><span class="sxs-lookup"><span data-stu-id="8f47c-121">You can add users as guest accounts to an Azure Active Directory via the [*Azure AD B2B collaboration*](../active-directory-b2b-what-is-azure-ad-b2b.md) - and it can be done [programatically](../active-directory-b2b-code-samples.md).</span></span> <span data-ttu-id="8f47c-122">Quando você adiciona um usuário como conta de convidado a um Azure Active Directory, um email de convite é enviado para o usuário, que tem de aceitar o convite clicando no link no email de convite.</span><span class="sxs-lookup"><span data-stu-id="8f47c-122">When you add a user as guest account to an Azure Active Directory, an invitation email is sent to the user, who has to accept the invitation by clicking on the link in the invitation email.</span></span> <span data-ttu-id="8f47c-123">Convites enviados para um usuário adicional em uma organização que convida e também é membro da organização do parceiro não são necessários para se aceitar um convite para entrar.</span><span class="sxs-lookup"><span data-stu-id="8f47c-123">Invitations that are sent to an additional user in an inviting organization that is also a member of the partner organization are not required to accept an invitation to sign in.</span></span>

<span data-ttu-id="8f47c-124">Os aplicativos de único locatário podem habilitar a experiência *Entre em Contato Comigo*, mas se você deseja habilitar a experiência de avaliação gratuita/clique simples recomendada pelo AppSource, habilite a multilocação em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8f47c-124">Single-tenant applications can enable the *Contact Me* experience, but if you want to enable the single-click/ free trial experience that AppSource recommends, enable multi-tenancy on your application instead.</span></span>


## <a name="appsource-trial-experiences"></a><span data-ttu-id="8f47c-125">Experiências de avaliação do AppSource</span><span class="sxs-lookup"><span data-stu-id="8f47c-125">AppSource trial experiences</span></span>

### <a name="free-trial-customer-led-trial-experience"></a><span data-ttu-id="8f47c-126">Avaliação gratuita (experiência de avaliação orientada pelo cliente)</span><span class="sxs-lookup"><span data-stu-id="8f47c-126">Free Trial (Customer-led trial experience)</span></span> 
<span data-ttu-id="8f47c-127">A *avaliação orientada pelo cliente* é a experiência que o AppSource recomenda, pois oferece acesso a seu aplicativo com um clique simples.</span><span class="sxs-lookup"><span data-stu-id="8f47c-127">The *customer-led trial* is the experience that AppSource recommends as it offers a single-click access to your application.</span></span> <span data-ttu-id="8f47c-128">Abaixo, uma ilustração de como essa experiência se parece:</span><span class="sxs-lookup"><span data-stu-id="8f47c-128">Below an illustration of how this experience looks like:</span></span><br/><br/>

<table >
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step1.png" width="85%"/><ul><li><span data-ttu-id="8f47c-129">O usuário localiza o aplicativo no Site do AppSource</span><span class="sxs-lookup"><span data-stu-id="8f47c-129">User finds your application in AppSource Web Site</span></span></li><li><span data-ttu-id="8f47c-130">Seleciona a opção “Avaliação gratuita”</span><span class="sxs-lookup"><span data-stu-id="8f47c-130">Selects ‘Free trial’ option</span></span></li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step2.png" width="85%" /><ul><li><span data-ttu-id="8f47c-131">O AppSource redireciona o usuário para uma URL no seu site</span><span class="sxs-lookup"><span data-stu-id="8f47c-131">AppSource redirects user to a URL in your web site</span></span></li><li><span data-ttu-id="8f47c-132">Seu site inicia o processo <i>single-sign-on</i> automaticamente (no carregamento da página)</span><span class="sxs-lookup"><span data-stu-id="8f47c-132">Your web site starts the <i>single-sign-on</i> process automatically (on page load)</span></span></li></ul></td>
    <td valign="top" width="33%">3.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step3.png" width="85%"/><ul><li><span data-ttu-id="8f47c-133">O usuário é redirecionado para a página de entrada da Microsoft</span><span class="sxs-lookup"><span data-stu-id="8f47c-133">User is redirected to Microsoft Sign-in page</span></span></li><li><span data-ttu-id="8f47c-134">O usuário fornece credenciais para entrar</span><span class="sxs-lookup"><span data-stu-id="8f47c-134">User provides credentials to sign in</span></span></li></ul></td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step4.png" width="85%"/><ul><li><span data-ttu-id="8f47c-135">O usuário dá consentimento ao seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="8f47c-135">User gives consent for your application</span></span></li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li><span data-ttu-id="8f47c-136">A entrada é concluída e o usuário é redirecionado ao seu site</span><span class="sxs-lookup"><span data-stu-id="8f47c-136">Sign-in completes and user is redirected back to your web site</span></span></li><li><span data-ttu-id="8f47c-137">O usuário começa a avaliação gratuita</span><span class="sxs-lookup"><span data-stu-id="8f47c-137">User starts the free trial</span></span></li></ul></td>
    <td></td>
</tr>
</table>

### <a name="contact-me-partner-led-trial-experience"></a><span data-ttu-id="8f47c-138">Entre em Contato Comigo (experiência de avaliação orientada pelo parceiro)</span><span class="sxs-lookup"><span data-stu-id="8f47c-138">Contact Me (Partner-led trial experience)</span></span>
<span data-ttu-id="8f47c-139">A *experiência de avaliação do parceiro* pode ser usada quando uma operação de longo prazo ou manual precisa ser feita para provisionar o usuário ou a empresa: por exemplo, seu aplicativo precisa provisionar máquinas virtuais, instâncias de banco de dados ou operações que levam muito tempo para serem concluídas.</span><span class="sxs-lookup"><span data-stu-id="8f47c-139">The *partner trial experience* can be used when a manual or a long-term operation needs to happen to provision the user/ company: for example, your application needs to provision virtual machines, database instances, or operations that take much time to complete.</span></span> <span data-ttu-id="8f47c-140">Nesse caso, após o usuário selecionar o botão *'Solicitar avaliação'* e preencher um formulário, o AppSource enviará as informações de contato do usuário.</span><span class="sxs-lookup"><span data-stu-id="8f47c-140">In this case, after user selects the *'Request Trial'* button and fills out a form, AppSource sends you the user's contact information.</span></span> <span data-ttu-id="8f47c-141">Depois de receber essas informações, provisione o ambiente e envie instruções para o usuário sobre como acessar a experiência de avaliação:</span><span class="sxs-lookup"><span data-stu-id="8f47c-141">Upon receiving this information, you then provision the environment and send the instructions to the user on how to access the trial experience:</span></span><br/><br/>

<table valign="top">
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step1.png" width="85%"/><ul><li><span data-ttu-id="8f47c-142">O usuário localiza o aplicativo no Site do AppSource</span><span class="sxs-lookup"><span data-stu-id="8f47c-142">User finds your application in AppSource web site</span></span></li><li><span data-ttu-id="8f47c-143">Seleciona a opção “Entrar em contato comigo”</span><span class="sxs-lookup"><span data-stu-id="8f47c-143">Selects ‘Contact Me’ option</span></span></li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step2.png" width="85%"/><ul><li><span data-ttu-id="8f47c-144">Preenche um formulário com as informações de contato</span><span class="sxs-lookup"><span data-stu-id="8f47c-144">Fills out a form with contact information</span></span></li></ul></td>
     <td valign="top" width="33%">3.<br/><br/>
        <table bgcolor="#f7f7f7">
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/UserContact.png" width="55%"/></td>
            <td><span data-ttu-id="8f47c-145">Você recebe as informações do usuário</span><span class="sxs-lookup"><span data-stu-id="8f47c-145">You receive user information</span></span></td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/SetupEnv.png" width="55%"/></td>
            <td><span data-ttu-id="8f47c-146">Configure o ambiente</span><span class="sxs-lookup"><span data-stu-id="8f47c-146">Setup environment</span></span></td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/ContactCustomer.png" width="55%"/></td>
            <td><span data-ttu-id="8f47c-147">Entre em contato com usuário com as informações da avaliação</span><span class="sxs-lookup"><span data-stu-id="8f47c-147">Contact user with trial info</span></span></td>
        </tr>
        </table><br/><br/>
        <ul><li><span data-ttu-id="8f47c-148">Você recebe informações do usuário e configura a instância de avaliação</span><span class="sxs-lookup"><span data-stu-id="8f47c-148">You receive user's information and setup trial instance</span></span></li><li><span data-ttu-id="8f47c-149">Você envia o hiperlink de acesso ao aplicativo para o usuário</span><span class="sxs-lookup"><span data-stu-id="8f47c-149">You send the hyperlink to access your application to the user</span></span></li></ul>
    </td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step3.png" width="85%"/><ul><li><span data-ttu-id="8f47c-150">O usuário acessa o seu aplicativo e conclui o processo de logon único</span><span class="sxs-lookup"><span data-stu-id="8f47c-150">User accesses your application and complete the single-sign-on process</span></span></li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step4.png" width="85%"/><ul><li><span data-ttu-id="8f47c-151">O usuário dá consentimento ao seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="8f47c-151">User gives consent for your application</span></span></li></ul></td>
    <td valign="top" width="33%">6.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li><span data-ttu-id="8f47c-152">A entrada é concluída e o usuário é redirecionado ao seu site</span><span class="sxs-lookup"><span data-stu-id="8f47c-152">Sign-in completes and user is redirected back to your web site</span></span></li><li><span data-ttu-id="8f47c-153">O usuário começa a avaliação gratuita</span><span class="sxs-lookup"><span data-stu-id="8f47c-153">User starts the free trial</span></span></li></ul></td>
   
</tr>
</table>

### <a name="more-information"></a><span data-ttu-id="8f47c-154">Mais informações</span><span class="sxs-lookup"><span data-stu-id="8f47c-154">More information</span></span>
<span data-ttu-id="8f47c-155">Para saber mais sobre a experiência de avaliação do AppSource, confira [este vídeo](https://aka.ms/trialexperienceforwebapps).</span><span class="sxs-lookup"><span data-stu-id="8f47c-155">For more information about the AppSource trial experience, see [this video](https://aka.ms/trialexperienceforwebapps).</span></span> 
 
## <a name="next-steps"></a><span data-ttu-id="8f47c-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8f47c-156">Next Steps</span></span>

- <span data-ttu-id="8f47c-157">Para saber mais sobre como criar aplicativos que dão suporte a logons do Azure Active Directory, confira [Cenários de autenticação do Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios)</span><span class="sxs-lookup"><span data-stu-id="8f47c-157">For more information on building applications that support Azure Active Directory sign-ins, see [Authentication Scenarios for Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios)</span></span> 

- <span data-ttu-id="8f47c-158">Para saber mais sobre como listar seu aplicativo SaaS no AppSource, confira [Informações de parceiro do AppSource](https://appsource.microsoft.com/partners)</span><span class="sxs-lookup"><span data-stu-id="8f47c-158">For information on how to list your SaaS application in AppSource, go see [AppSource Partner Information](https://appsource.microsoft.com/partners)</span></span>


## <a name="get-support"></a><span data-ttu-id="8f47c-159">Obtenha suporte</span><span class="sxs-lookup"><span data-stu-id="8f47c-159">Get Support</span></span>
<span data-ttu-id="8f47c-160">Para a integração do Azure Active Directory, usamos [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory) com a comunidade para suporte.</span><span class="sxs-lookup"><span data-stu-id="8f47c-160">For Azure Active Directory integration, we use [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory) with the community to provide support.</span></span> 

<span data-ttu-id="8f47c-161">Recomendamos fazer suas perguntas no Stack Overflow primeiro e navegar pelos problemas existentes para ver se alguém já fez sua pergunta antes.</span><span class="sxs-lookup"><span data-stu-id="8f47c-161">We highly recommend you ask your questions on Stack Overflow first and browse existing issues to see if someone has asked your question before.</span></span> <span data-ttu-id="8f47c-162">Marque suas perguntas ou comentários com `[azure-active-directory]`.</span><span class="sxs-lookup"><span data-stu-id="8f47c-162">Make sure that your questions or comments are tagged with `[azure-active-directory]`.</span></span>

<span data-ttu-id="8f47c-163">Use a seção de comentários a seguir para fornecer seus comentários e nos ajudar a aprimorar e adaptar nosso conteúdo.</span><span class="sxs-lookup"><span data-stu-id="8f47c-163">Use the following comments section to provide feedback and help us refine and shape our content.</span></span>

<!--Reference style links -->
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Auth-Scenarios-Browser-To-WebApp]: ./active-directory-authentication-scenarios.md#web-browser-to-web-application
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Howto-Multitenant-Overview]: ./active-directory-devhowto-multi-tenant-overview.md
[AAD-QuickStart-Web-Apps]: ./active-directory-developers-guide.md#get-started


<!--Image references-->