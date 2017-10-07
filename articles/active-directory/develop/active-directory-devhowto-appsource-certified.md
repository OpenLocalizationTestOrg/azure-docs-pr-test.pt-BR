---
title: aaaHow tooget AppSource certificado para o Active Directory do Azure | Microsoft Docs
description: Obter detalhes sobre como tooget seu aplicativo AppSource certificados para o Active Directory do Azure.
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
ms.openlocfilehash: e9f07e9220afcba1120b987122fe770fe5225eed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-appsource-certified-for-azure-active-directory"></a><span data-ttu-id="be111-103">Como tooget AppSource certificados para o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="be111-103">How tooget AppSource Certified for Azure Active Directory</span></span>
<span data-ttu-id="be111-104">[Microsoft AppSource](https://appsource.microsoft.com/) é um destino para toodiscover de usuários de negócios, tente e gerenciar aplicativos SaaS de linha de negócios (autônomo SaaS e o complemento tooexisting Microsoft SaaS produtos).</span><span class="sxs-lookup"><span data-stu-id="be111-104">[Microsoft AppSource](https://appsource.microsoft.com/) is a destination for business users toodiscover, try, and manage line-of-business SaaS applications (standalone SaaS and add-on tooexisting Microsoft SaaS products).</span></span>

<span data-ttu-id="be111-105">toolist um aplicativo SaaS em AppSource autônomo, seu aplicativo deve aceitar logon único de contas de trabalho de qualquer empresa ou organização que possui o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="be111-105">toolist a standalone SaaS application on AppSource, your application must accept single sign-on from work accounts from any company or organization that has Azure Active Directory.</span></span> <span data-ttu-id="be111-106">processo de entrada Hello deve usar Olá [OpenID Connect](./active-directory-protocols-openid-connect-code.md) ou [OAuth 2.0](./active-directory-protocols-oauth-code.md) protocolos.</span><span class="sxs-lookup"><span data-stu-id="be111-106">hello sign-in process must use hello [OpenID Connect](./active-directory-protocols-openid-connect-code.md) or [OAuth 2.0](./active-directory-protocols-oauth-code.md) protocols.</span></span> <span data-ttu-id="be111-107">A integração SAML não é aceita para certificação AppSource.</span><span class="sxs-lookup"><span data-stu-id="be111-107">SAML integration is not accepted for AppSource certification.</span></span>

## <a name="guides-and-code-samples"></a><span data-ttu-id="be111-108">Guias e exemplos de código</span><span class="sxs-lookup"><span data-stu-id="be111-108">Guides and code samples</span></span>
<span data-ttu-id="be111-109">Se você quiser toolearn sobre como toointegrate o aplicativo com o Azure Active Directory usando Open ID se conectar, siga nosso guias e Olá amostras de código [guia do desenvolvedor do Active Directory do Azure](./active-directory-developers-guide.md#get-started "começar com O AD do Azure para desenvolvedores").</span><span class="sxs-lookup"><span data-stu-id="be111-109">If you want toolearn about how toointegrate your application with Azure Active Directory using Open ID connect, follow our guides and code samples in hello [Azure Active Directory developer's guide](./active-directory-developers-guide.md#get-started "Get Started with Azure AD for developers").</span></span>

## <a name="multi-tenant-applications"></a><span data-ttu-id="be111-110">Aplicativos multilocatários</span><span class="sxs-lookup"><span data-stu-id="be111-110">Multi-tenant applications</span></span>

<span data-ttu-id="be111-111">Um aplicativo que aceita entradas de usuários de qualquer empresa ou organização que tenha o Azure Active Directory sem a necessidade de uma instância, configuração ou implantação separada é conhecido como *aplicativo multilocatário*.</span><span class="sxs-lookup"><span data-stu-id="be111-111">An application that accepts sign-ins from users from any company or organization that have Azure Active Directory without requiring a separate instance, configuration, or deployment is known as a *multi-tenant application*.</span></span> <span data-ttu-id="be111-112">AppSource recomenda a aplicativos implementar Olá multilocação tooenable *único clique* livre experiência de avaliação.</span><span class="sxs-lookup"><span data-stu-id="be111-112">AppSource recommends that applications implement multi-tenancy tooenable hello *single-click* free trial experience.</span></span>

<span data-ttu-id="be111-113">Em ordem tooenable multilocação em seu aplicativo:</span><span class="sxs-lookup"><span data-stu-id="be111-113">In order tooenable multi-tenancy on your application:</span></span>
- <span data-ttu-id="be111-114">Definir `Multi-Tenanted` propriedade muito`Yes` nas informações do registro do aplicativo hello [Portal do Azure](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) (por padrão, os aplicativos criados no hello Portal do Azure são configurados como *únicolocatário*)</span><span class="sxs-lookup"><span data-stu-id="be111-114">Set `Multi-Tenanted` property too`Yes` on your application registration's information in hello [Azure Portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) (by default, applications created in hello Azure Portal are configured as *single-tenant*)</span></span>
- <span data-ttu-id="be111-115">Atualizar seu toohello de solicitações do código toosend '`common`' ponto de extremidade (atualizar o ponto de extremidade de saudação do *https://login.microsoftonline.com/ {yourtenant}* muito*https://login.microsoftonline.com/common*)</span><span class="sxs-lookup"><span data-stu-id="be111-115">Update your code toosend requests toohello '`common`' endpoint (update hello endpoint from *https://login.microsoftonline.com/{yourtenant}* too*https://login.microsoftonline.com/common*)</span></span>
- <span data-ttu-id="be111-116">Para algumas plataformas, como o ASP.NET, você precisa também tooupdate tooaccept seu código vários emissores</span><span class="sxs-lookup"><span data-stu-id="be111-116">For some platforms, like ASP.NET, you need also tooupdate your code tooaccept multiple issuers</span></span>

<span data-ttu-id="be111-117">Para obter mais informações sobre multilocação, consulte: [como toosign em qualquer usuário do Azure AD (Active Directory) usando Olá padrão de aplicativo multilocatário](./active-directory-devhowto-multi-tenant-overview.md).</span><span class="sxs-lookup"><span data-stu-id="be111-117">For more information about multi-tenancy, see: [How toosign in any Azure Active Directory (AD) user using hello multi-tenant application pattern](./active-directory-devhowto-multi-tenant-overview.md).</span></span>

### <a name="single-tenant-applications"></a><span data-ttu-id="be111-118">Aplicativos de locatário único</span><span class="sxs-lookup"><span data-stu-id="be111-118">Single-tenant applications</span></span>
<span data-ttu-id="be111-119">Aplicativos que só aceitam entradas de usuários de uma instância definida do Azure Active Directory são conhecidos como *aplicativo de locatário único*.</span><span class="sxs-lookup"><span data-stu-id="be111-119">Applications that only accept sign-ins from users of a defined Azure Active Directory instance are known as *single-tenant application*.</span></span> <span data-ttu-id="be111-120">Os usuários externos (incluindo as contas de trabalho ou escola de outras organizações ou conta pessoal) podem entrar no aplicativo de único locatário tooa depois de adicionar cada usuário como *conta convidado* instância toohello Active Directory do Azure aplicativo Hello está registrado.</span><span class="sxs-lookup"><span data-stu-id="be111-120">External users (including Work or School accounts from other organizations, or personal account) can sign in tooa single-tenant application after adding each user as *guest account* toohello Azure Active Directory instance that hello application is registered.</span></span> <span data-ttu-id="be111-121">Você pode adicionar usuários como tooan de contas de convidado do Azure Active Directory por meio de saudação [ *colaboração B2B do Azure AD* ](../active-directory-b2b-what-is-azure-ad-b2b.md) - e isso pode ser feito [programaticamente](../active-directory-b2b-code-samples.md).</span><span class="sxs-lookup"><span data-stu-id="be111-121">You can add users as guest accounts tooan Azure Active Directory via hello [*Azure AD B2B collaboration*](../active-directory-b2b-what-is-azure-ad-b2b.md) - and it can be done [programatically](../active-directory-b2b-code-samples.md).</span></span> <span data-ttu-id="be111-122">Quando você adiciona um usuário como conta de convidado tooan Active Directory do Azure, um email de convite é enviado toohello usuário, que tem o convite de saudação tooaccept clicando no link Olá no email de convite de saudação.</span><span class="sxs-lookup"><span data-stu-id="be111-122">When you add a user as guest account tooan Azure Active Directory, an invitation email is sent toohello user, who has tooaccept hello invitation by clicking on hello link in hello invitation email.</span></span> <span data-ttu-id="be111-123">Convites enviados tooan adicional do usuário em uma organização convidar que também seja um membro da organização do parceiro de saudação são tooaccept necessária não toosign um convite no.</span><span class="sxs-lookup"><span data-stu-id="be111-123">Invitations that are sent tooan additional user in an inviting organization that is also a member of hello partner organization are not required tooaccept an invitation toosign in.</span></span>

<span data-ttu-id="be111-124">Aplicativos de locatário único podem habilitar Olá *contato Me* experiência, mas se você quiser tooenable Olá clique simples / livre experiência de avaliação que recomenda AppSource, habilitar a multilocação em seu aplicativo em vez disso.</span><span class="sxs-lookup"><span data-stu-id="be111-124">Single-tenant applications can enable hello *Contact Me* experience, but if you want tooenable hello single-click/ free trial experience that AppSource recommends, enable multi-tenancy on your application instead.</span></span>


## <a name="appsource-trial-experiences"></a><span data-ttu-id="be111-125">Experiências de avaliação do AppSource</span><span class="sxs-lookup"><span data-stu-id="be111-125">AppSource trial experiences</span></span>

### <a name="free-trial-customer-led-trial-experience"></a><span data-ttu-id="be111-126">Avaliação gratuita (experiência de avaliação orientada pelo cliente)</span><span class="sxs-lookup"><span data-stu-id="be111-126">Free Trial (Customer-led trial experience)</span></span> 
<span data-ttu-id="be111-127">Olá *avaliação orientada pelo cliente* é experiência Olá AppSource recomenda que oferece um aplicativo de tooyour acesso único clique.</span><span class="sxs-lookup"><span data-stu-id="be111-127">hello *customer-led trial* is hello experience that AppSource recommends as it offers a single-click access tooyour application.</span></span> <span data-ttu-id="be111-128">Abaixo, uma ilustração de como essa experiência se parece:</span><span class="sxs-lookup"><span data-stu-id="be111-128">Below an illustration of how this experience looks like:</span></span><br/><br/>

<table >
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step1.png" width="85%"/><ul><li><span data-ttu-id="be111-129">O usuário localiza o aplicativo no Site do AppSource</span><span class="sxs-lookup"><span data-stu-id="be111-129">User finds your application in AppSource Web Site</span></span></li><li><span data-ttu-id="be111-130">Seleciona a opção “Avaliação gratuita”</span><span class="sxs-lookup"><span data-stu-id="be111-130">Selects ‘Free trial’ option</span></span></li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step2.png" width="85%" /><ul><li><span data-ttu-id="be111-131">AppSource redireciona o usuário tooa URL no seu site da web</span><span class="sxs-lookup"><span data-stu-id="be111-131">AppSource redirects user tooa URL in your web site</span></span></li><li><span data-ttu-id="be111-132">O site inicia Olá <i>single-sign-on</i> processar automaticamente (no carregamento da página)</span><span class="sxs-lookup"><span data-stu-id="be111-132">Your web site starts hello <i>single-sign-on</i> process automatically (on page load)</span></span></li></ul></td>
    <td valign="top" width="33%">3.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step3.png" width="85%"/><ul><li><span data-ttu-id="be111-133">Usuário é redirecionado tooMicrosoft entrar página</span><span class="sxs-lookup"><span data-stu-id="be111-133">User is redirected tooMicrosoft Sign-in page</span></span></li><li><span data-ttu-id="be111-134">O usuário fornece credenciais toosign em</span><span class="sxs-lookup"><span data-stu-id="be111-134">User provides credentials toosign in</span></span></li></ul></td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step4.png" width="85%"/><ul><li><span data-ttu-id="be111-135">O usuário dá consentimento ao seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="be111-135">User gives consent for your application</span></span></li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li><span data-ttu-id="be111-136">Entrar for concluída e o usuário é redirecionado tooyour back web site</span><span class="sxs-lookup"><span data-stu-id="be111-136">Sign-in completes and user is redirected back tooyour web site</span></span></li><li><span data-ttu-id="be111-137">Usuário começa a avaliação gratuita Olá</span><span class="sxs-lookup"><span data-stu-id="be111-137">User starts hello free trial</span></span></li></ul></td>
    <td></td>
</tr>
</table>

### <a name="contact-me-partner-led-trial-experience"></a><span data-ttu-id="be111-138">Entre em Contato Comigo (experiência de avaliação orientada pelo parceiro)</span><span class="sxs-lookup"><span data-stu-id="be111-138">Contact Me (Partner-led trial experience)</span></span>
<span data-ttu-id="be111-139">Olá *experiência de avaliação do parceiro* pode ser usado quando um manual ou uma operação de longo prazo precisa de usuário de saudação do toohappen tooprovision / da empresa: por exemplo, seu aplicativo precisa de máquinas virtuais de tooprovision, instâncias de banco de dados, ou operações que levam muito tempo toocomplete.</span><span class="sxs-lookup"><span data-stu-id="be111-139">hello *partner trial experience* can be used when a manual or a long-term operation needs toohappen tooprovision hello user/ company: for example, your application needs tooprovision virtual machines, database instances, or operations that take much time toocomplete.</span></span> <span data-ttu-id="be111-140">Nesse caso, após o usuário selecionará Olá *'Solicitação avaliação'* botão e preenche um formulário, AppSource envia Olá informações de contato do usuário.</span><span class="sxs-lookup"><span data-stu-id="be111-140">In this case, after user selects hello *'Request Trial'* button and fills out a form, AppSource sends you hello user's contact information.</span></span> <span data-ttu-id="be111-141">Ao receber essas informações, em seguida, provisionar ambiente hello e enviar Olá instruções toohello usuário como tooaccess Olá experiência de avaliação:</span><span class="sxs-lookup"><span data-stu-id="be111-141">Upon receiving this information, you then provision hello environment and send hello instructions toohello user on how tooaccess hello trial experience:</span></span><br/><br/>

<table valign="top">
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step1.png" width="85%"/><ul><li><span data-ttu-id="be111-142">O usuário localiza o aplicativo no Site do AppSource</span><span class="sxs-lookup"><span data-stu-id="be111-142">User finds your application in AppSource web site</span></span></li><li><span data-ttu-id="be111-143">Seleciona a opção “Entrar em contato comigo”</span><span class="sxs-lookup"><span data-stu-id="be111-143">Selects ‘Contact Me’ option</span></span></li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step2.png" width="85%"/><ul><li><span data-ttu-id="be111-144">Preenche um formulário com as informações de contato</span><span class="sxs-lookup"><span data-stu-id="be111-144">Fills out a form with contact information</span></span></li></ul></td>
     <td valign="top" width="33%">3.<br/><br/>
        <table bgcolor="#f7f7f7">
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/UserContact.png" width="55%"/></td>
            <td><span data-ttu-id="be111-145">Você recebe as informações do usuário</span><span class="sxs-lookup"><span data-stu-id="be111-145">You receive user information</span></span></td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/SetupEnv.png" width="55%"/></td>
            <td><span data-ttu-id="be111-146">Configure o ambiente</span><span class="sxs-lookup"><span data-stu-id="be111-146">Setup environment</span></span></td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/ContactCustomer.png" width="55%"/></td>
            <td><span data-ttu-id="be111-147">Entre em contato com usuário com as informações da avaliação</span><span class="sxs-lookup"><span data-stu-id="be111-147">Contact user with trial info</span></span></td>
        </tr>
        </table><br/><br/>
        <ul><li><span data-ttu-id="be111-148">Você recebe informações do usuário e configura a instância de avaliação</span><span class="sxs-lookup"><span data-stu-id="be111-148">You receive user's information and setup trial instance</span></span></li><li><span data-ttu-id="be111-149">Enviar Olá hiperlink tooaccess sua toohello de usuário do aplicativo</span><span class="sxs-lookup"><span data-stu-id="be111-149">You send hello hyperlink tooaccess your application toohello user</span></span></li></ul>
    </td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step3.png" width="85%"/><ul><li><span data-ttu-id="be111-150">Usuário acessar seu aplicativo e o processo de logon único do hello concluída</span><span class="sxs-lookup"><span data-stu-id="be111-150">User accesses your application and complete hello single-sign-on process</span></span></li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step4.png" width="85%"/><ul><li><span data-ttu-id="be111-151">O usuário dá consentimento ao seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="be111-151">User gives consent for your application</span></span></li></ul></td>
    <td valign="top" width="33%">6.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li><span data-ttu-id="be111-152">Entrar for concluída e o usuário é redirecionado tooyour back web site</span><span class="sxs-lookup"><span data-stu-id="be111-152">Sign-in completes and user is redirected back tooyour web site</span></span></li><li><span data-ttu-id="be111-153">Usuário começa a avaliação gratuita Olá</span><span class="sxs-lookup"><span data-stu-id="be111-153">User starts hello free trial</span></span></li></ul></td>
   
</tr>
</table>

### <a name="more-information"></a><span data-ttu-id="be111-154">Mais informações</span><span class="sxs-lookup"><span data-stu-id="be111-154">More information</span></span>
<span data-ttu-id="be111-155">Para obter mais informações sobre a experiência de avaliação do hello AppSource, consulte [este vídeo](https://aka.ms/trialexperienceforwebapps).</span><span class="sxs-lookup"><span data-stu-id="be111-155">For more information about hello AppSource trial experience, see [this video](https://aka.ms/trialexperienceforwebapps).</span></span> 
 
## <a name="next-steps"></a><span data-ttu-id="be111-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="be111-156">Next Steps</span></span>

- <span data-ttu-id="be111-157">Para saber mais sobre como criar aplicativos que dão suporte a logons do Azure Active Directory, confira [Cenários de autenticação do Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios)</span><span class="sxs-lookup"><span data-stu-id="be111-157">For more information on building applications that support Azure Active Directory sign-ins, see [Authentication Scenarios for Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios)</span></span> 

- <span data-ttu-id="be111-158">Para obter informações sobre como toolist seu aplicativo SaaS no AppSource, vá consulte [AppSource informações do parceiro](https://appsource.microsoft.com/partners)</span><span class="sxs-lookup"><span data-stu-id="be111-158">For information on how toolist your SaaS application in AppSource, go see [AppSource Partner Information](https://appsource.microsoft.com/partners)</span></span>


## <a name="get-support"></a><span data-ttu-id="be111-159">Obtenha suporte</span><span class="sxs-lookup"><span data-stu-id="be111-159">Get Support</span></span>
<span data-ttu-id="be111-160">Integração do Active Directory do Azure, usamos [estouro de pilha](http://stackoverflow.com/questions/tagged/azure-active-directory) com suporte de tooprovide Olá da comunidade.</span><span class="sxs-lookup"><span data-stu-id="be111-160">For Azure Active Directory integration, we use [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory) with hello community tooprovide support.</span></span> 

<span data-ttu-id="be111-161">É altamente recomendável fazer suas perguntas sobre estouro de pilha primeiro e procurar existente toosee de problemas, se alguém fez sua pergunta antes.</span><span class="sxs-lookup"><span data-stu-id="be111-161">We highly recommend you ask your questions on Stack Overflow first and browse existing issues toosee if someone has asked your question before.</span></span> <span data-ttu-id="be111-162">Marque suas perguntas ou comentários com `[azure-active-directory]`.</span><span class="sxs-lookup"><span data-stu-id="be111-162">Make sure that your questions or comments are tagged with `[azure-active-directory]`.</span></span>

<span data-ttu-id="be111-163">Use Olá comentários de tooprovide seção comentários a seguir e ajudar a refinar e formatar o nosso conteúdo.</span><span class="sxs-lookup"><span data-stu-id="be111-163">Use hello following comments section tooprovide feedback and help us refine and shape our content.</span></span>

<!--Reference style links -->
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Auth-Scenarios-Browser-To-WebApp]: ./active-directory-authentication-scenarios.md#web-browser-to-web-application
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Howto-Multitenant-Overview]: ./active-directory-devhowto-multi-tenant-overview.md
[AAD-QuickStart-Web-Apps]: ./active-directory-developers-guide.md#get-started


<!--Image references-->