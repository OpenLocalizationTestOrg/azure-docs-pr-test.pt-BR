---
title: "Aplicativos, permissões e consentimento no Azure Active Directory. | Microsoft Docs"
description: "O Azure AD Connect integrará seus diretórios locais com o Azure Active Directory.  Isso permite que você tooprovide uma identidade comum para aplicativos do Office 365, Azure e SaaS integrada ao AD do Azure."
keywords: "Introdução tooAzure AD, aplicativos, o que é o Azure AD Connect, instalar o active directory"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 25897cc4-7687-49b6-b0d5-71f51302b6b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/31/2017
ms.author: billmath
ms.reviewer: jesakowi
ms.custom: oldportal;it-pro;
ms.openlocfilehash: af0c2669199736fdb41e85876a7e3a7064e80770
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="apps-permissions-and-consent-in-azure-active-directory"></a><span data-ttu-id="38d0c-105">Aplicativos, permissões e consentimento no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="38d0c-105">Apps, permissions, and consent in Azure Active Directory</span></span>
<span data-ttu-id="38d0c-106">No Active Directory do Azure, você pode adicionar o diretório tooyour de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="38d0c-106">Within Azure Active Directory, you can add applications tooyour directory.</span></span>  <span data-ttu-id="38d0c-107">aplicativos de saudação podem variar dependendo do tipo de saudação do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="38d0c-107">hello applications can vary depending on hello type of application.</span></span>  <span data-ttu-id="38d0c-108">aplicativos tooview no portal clássico do hello, selecione um diretório e escolher aplicativos.</span><span class="sxs-lookup"><span data-stu-id="38d0c-108">tooview applications in hello classic portal, select a directory and choose applications.</span></span>

![](media/active-directory-apps-permissions-consent/apps1.png)

> [!IMPORTANT]
> <span data-ttu-id="38d0c-109">A Microsoft recomenda que você gerencie o AD do Azure usando Olá [Centro de administração do AD do Azure](https://aad.portal.azure.com) em Olá portal do Azure em vez de usar Olá portal clássico do Azure mencionado neste artigo.</span><span class="sxs-lookup"><span data-stu-id="38d0c-109">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span>

## <a name="types-of-apps"></a><span data-ttu-id="38d0c-110">Tipos de aplicativos</span><span class="sxs-lookup"><span data-stu-id="38d0c-110">Types of apps</span></span>

1. <span data-ttu-id="38d0c-111">**Aplicativos de locatário único**</span><span class="sxs-lookup"><span data-stu-id="38d0c-111">**Single-tenant apps**</span></span> </br>
    - <span data-ttu-id="38d0c-112">**Aplicativos de único locatário** -conhecida tooas aplicativos de linha de negócios (LOB).</span><span class="sxs-lookup"><span data-stu-id="38d0c-112">**Single-tenant apps** - Often referred tooas line-of-business (LOB) apps.</span></span> <span data-ttu-id="38d0c-113">Esse é Olá caso em que alguém de sua organização desenvolve seu próprio aplicativo e gostaria que os usuários na organização Olá toosign capaz de toobe no aplicativo toohello.</span><span class="sxs-lookup"><span data-stu-id="38d0c-113">This is hello case where someone within your organization develops their own app, and would like users in hello organization toobe able toosign in toohello app.</span></span>
    ![](media/active-directory-apps-permissions-consent/apps2.png)
    - <span data-ttu-id="38d0c-114">**Aplicativos de Proxy de aplicativo** - quando você expõe um aplicativo local com o Proxy de aplicativo do AD do Azure, um aplicativo de único locatário é registrado no seu locatário (em adição toohello serviço de Proxy de aplicativo).</span><span class="sxs-lookup"><span data-stu-id="38d0c-114">**App Proxy apps** - When you expose an on-prem application with Azure AD App Proxy, a single-tenant app is registered in your tenant (in addition toohello App Proxy service).</span></span> <span data-ttu-id="38d0c-115">Este aplicativo é o que representa seu aplicativo local para todas as interações de nuvem (por exemplo, autenticação).</span><span class="sxs-lookup"><span data-stu-id="38d0c-115">This app is what represents your on-prem application for all cloud interactions (for example, authentication).</span></span> <span data-ttu-id="38d0c-116">(O proxy de aplicativo requer o Azure AD Básico ou superior.)</span><span class="sxs-lookup"><span data-stu-id="38d0c-116">(App Proxy requires Azure AD Basic or higher.)</span></span>


2. <span data-ttu-id="38d0c-117">**Aplicativos multilocatário**</span><span class="sxs-lookup"><span data-stu-id="38d0c-117">**Multi-tenant apps**</span></span>
    - <span data-ttu-id="38d0c-118">**Aplicativos de vários locatários que outras pessoas possam consentir** - semelhante muito "aplicativos de único locatário que desenvolve sua organização".</span><span class="sxs-lookup"><span data-stu-id="38d0c-118">**Multi-tenant apps which others can consent to** - similar too“single-tenant apps that your organization develops”.</span></span> <span data-ttu-id="38d0c-119">a principal diferença Hello (além de lógica de saudação no próprio aplicativo hello) é que os usuários de outros locatários também podem dar consentimento tooand toohello aplicativo de entrada.</span><span class="sxs-lookup"><span data-stu-id="38d0c-119">hello main difference (besides hello logic in hello app itself) is that users from other tenants can also consent tooand sign in toohello app.</span></span></br>
    ![](media/active-directory-apps-permissions-consent/apps4.png)
    - <span data-ttu-id="38d0c-120">**Aplicativos multilocatário desenvolvidos por outros, para os quais a Contoso pode dar consentimento**.</span><span class="sxs-lookup"><span data-stu-id="38d0c-120">**Multi-tenant apps others develop, which Contoso can consent to**.</span></span> <span data-ttu-id="38d0c-121">(Ou "aplicativos com consentimento" de forma abreviada). Isso é Olá outro lado de "aplicativos multilocatários que sua organização desenvolve".</span><span class="sxs-lookup"><span data-stu-id="38d0c-121">(Or “consented apps”, for short.) This is hello flip side of “multi-tenant apps your organization develops”.</span></span> <span data-ttu-id="38d0c-122">Quando outra organização desenvolve um aplicativo multilocatário, os usuários da sua organização podem consentir toohello aplicativo e entrar tooit.</span><span class="sxs-lookup"><span data-stu-id="38d0c-122">When another organization develops a multi-tenant app, users of your organization can consent toohello app and sign in tooit.</span></span>
    - <span data-ttu-id="38d0c-123">**Aplicativos próprios da Microsoft** – aplicativos que representam os serviços da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="38d0c-123">**Microsoft first-party apps** - Apps that represent Microsoft services.</span></span> <span data-ttu-id="38d0c-124">Autorização é orientada por fatos Olá que você se inscrever para o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="38d0c-124">Consent is driven by hello fact that you sign up for hello service.</span></span> <span data-ttu-id="38d0c-125">Às vezes, há especial UX e lógica para determinados aplicativos de terceiros que é frequentemente usada ao estabelecer políticas de acesso toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="38d0c-125">There is sometimes special UX and logic for certain first-party apps that is often used when establishing policies around access toohello app.</span></span></br>
    ![](media/active-directory-apps-permissions-consent/apps3.png)
    - <span data-ttu-id="38d0c-126">**Aplicativos pré-integrados** -aplicativos disponíveis no hello Galeria de aplicativo do Azure AD, você pode adicionar tooyour directory tooprovide single sign-on (e, em alguns casos, o provisionamento) toopopular aplicativos de SaaS.</span><span class="sxs-lookup"><span data-stu-id="38d0c-126">**Pre-integrated apps** - Apps available in hello Azure AD App Gallery, which you can add tooyour directory tooprovide single sign-on (and in some cases, provisioning) toopopular SaaS apps.</span></span>
    - <span data-ttu-id="38d0c-127">**Logon único do Azure AD**: SSO "Real", para aplicativos que podem ser integrados ao Azure AD por meio de um protocolo de entrada com suporte como SAML 2.0 ou OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="38d0c-127">**Azure AD single sign-on**: “Real” SSO, for apps that can be integrated with Azure AD, through a supported sign-in protocol such as SAML 2.0 or OpenID Connect.</span></span> <span data-ttu-id="38d0c-128">Olá assistente o guiará através de configurá-la.</span><span class="sxs-lookup"><span data-stu-id="38d0c-128">hello wizard walks you through setting it up.</span></span>
    - <span data-ttu-id="38d0c-129">**Logon único senha**: AD do Azure armazena com segurança as credenciais do usuário Olá para o aplicativo hello e credenciais Olá são "injetadas" formulário de entrada hello por Olá extensão de navegador de acesso do aplicativo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="38d0c-129">**Password single sign-on**: Azure AD securely stores hello user’s credentials for hello app, and hello credentials are “injected” into hello sign-in form by hello Azure AD App Access browser extension.</span></span> <span data-ttu-id="38d0c-130">Também conhecido como "cofre para senhas".</span><span class="sxs-lookup"><span data-stu-id="38d0c-130">Also known as “password vaulting”.</span></span>

## <a name="permissions"></a><span data-ttu-id="38d0c-131">Permissões</span><span class="sxs-lookup"><span data-stu-id="38d0c-131">Permissions</span></span>

<span data-ttu-id="38d0c-132">Quando um aplicativo é registrado, o usuário de saudação realizar o registro do aplicativo hello (ou seja, o desenvolvedor de saudação) define qual aplicativo de saudação permissões precisa acessar e quais recursos.</span><span class="sxs-lookup"><span data-stu-id="38d0c-132">When an app is registered, hello user performing hello app registration (that is, hello developer) defines which permissions hello app needs access to, and which resources.</span></span> <span data-ttu-id="38d0c-133">(recursos de saudação são, por conta própria, definido como outros aplicativos). Por exemplo, alguém criar um aplicativo de leitor de email, seria estado que seu aplicativo requer a permissão de "Caixas de correio acesso como usuário conectado hello" hello em hello "Office 365 Exchange Online" recurso:</span><span class="sxs-lookup"><span data-stu-id="38d0c-133">(hello resources are, themselves, defined as other apps.) For example, someone building a mail reader app, would state that their app requires hello “Access mailboxes as hello signed-in user” permission in hello “Office 365 Exchange Online” resource:</span></span>
    
![](media/active-directory-apps-permissions-consent/apps6.png)

<span data-ttu-id="38d0c-134">Em ordem para toorequest (cliente de saudação) de um aplicativo determinada permissão de outro aplicativo (recurso de saudação), desenvolvedor de saudação do aplicativo de recurso Olá define permissões de saudação que existem.</span><span class="sxs-lookup"><span data-stu-id="38d0c-134">In order for one app (hello client) toorequest a certain permission from another app (hello resource), hello developer of hello resource app defines hello permissions that exist.</span></span> <span data-ttu-id="38d0c-135">Em nosso exemplo, a Microsoft, o proprietário de saudação do aplicativo de recurso "Office 365 Exchange Online" Olá, definiu uma permissão denominada "Caixas de correio acesso como usuário conectado Olá".</span><span class="sxs-lookup"><span data-stu-id="38d0c-135">In our example, Microsoft, hello owner of hello “Office 365 Exchange Online” resource app, have defined a permission named “Access mailboxes as hello signed-in user”.</span></span>

<span data-ttu-id="38d0c-136">Ao definir permissões, o desenvolvedor do aplicativo hello deve definir se Olá permissão pode ser consentida, ou se ele requer o consentimento do administrador.</span><span class="sxs-lookup"><span data-stu-id="38d0c-136">When defining permissions, hello app developer must define if hello permission can be consented to, or if it requires admin consent.</span></span> <span data-ttu-id="38d0c-137">Isso permite que desenvolvedores tooallow tooconsent de usuários em seus próprios tooapps solicitando somente permissões de baixa confidencialidade, mas requer administradores tooconsent toomore confidenciais permissões.</span><span class="sxs-lookup"><span data-stu-id="38d0c-137">This allows developers tooallow users tooconsent on their own tooapps requesting only low-sensitivity permissions, but require admins tooconsent toomore sensitive permissions.</span></span> <span data-ttu-id="38d0c-138">Por exemplo, Olá "Active Directory do Azure" aplicativo de recurso, tiver sido definida, para que os usuários podem dar consentimento tooapps, solicitando permissões somente leitura limitadas.</span><span class="sxs-lookup"><span data-stu-id="38d0c-138">For example, hello “Azure Active Directory” resource app, has been defined, so users can consent tooapps, requesting limited read-only permissions.</span></span>  <span data-ttu-id="38d0c-139">No entanto, o consentimento do administrador é necessário para permissões de leitura completas e todas as permissões de gravação.</span><span class="sxs-lookup"><span data-stu-id="38d0c-139">However, admin consent is required for full read permissions, and all write permissions.</span></span>

<span data-ttu-id="38d0c-140">Como clientes nativos não são autenticados, um aplicativo definido como um aplicativo cliente nativo somente pode solicitar permissões delegadas.</span><span class="sxs-lookup"><span data-stu-id="38d0c-140">Because native clients are not authenticated, an app defined as a native client app can only request delegated permissions.</span></span> <span data-ttu-id="38d0c-141">Isso significa que sempre deve haver um usuário real envolvido ao obter um token.</span><span class="sxs-lookup"><span data-stu-id="38d0c-141">This means that there must always be an actual user involved when obtaining a token.</span></span> <span data-ttu-id="38d0c-142">Aplicativos Web e APIs Web (clientes confidenciais) devem sempre ser autenticados com o Azure AD ao obter um token de acesso.</span><span class="sxs-lookup"><span data-stu-id="38d0c-142">Web apps and web APIs (confidential clients), must always authenticate with Azure AD when getting an access token.</span></span> <span data-ttu-id="38d0c-143">Que significa que eles também têm a possibilidade de saudação do solicitando permissões somente de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="38d0c-143">Meaning they also have hello possibility of requesting app-only permissions.</span></span> <span data-ttu-id="38d0c-144">Por exemplo, se o serviço de back-end do tooauthenticate tooanother precisa de um serviço de back-end.</span><span class="sxs-lookup"><span data-stu-id="38d0c-144">For example, if one back-end service needs tooauthenticate tooanother back-end service.</span></span> <span data-ttu-id="38d0c-145">Aplicativos solicitando permissões somente do aplicativo sempre exigem o consentimento do administrador.</span><span class="sxs-lookup"><span data-stu-id="38d0c-145">Applications requesting app-only permissions always require administrator consent.</span></span>

<span data-ttu-id="38d0c-146">Resumindo:</span><span class="sxs-lookup"><span data-stu-id="38d0c-146">Summarizing:</span></span>



- <span data-ttu-id="38d0c-147">Um aplicativo (cliente) informa Olá permissões para outros aplicativos (recursos).</span><span class="sxs-lookup"><span data-stu-id="38d0c-147">An app (client) states hello permissions it needs for other apps (resources).</span></span>
- <span data-ttu-id="38d0c-148">Um aplicativo (recurso) informa quais permissões são expostos tooother aplicativos (clientes).</span><span class="sxs-lookup"><span data-stu-id="38d0c-148">An app (resource) states what permissions are exposed tooother apps (clients).</span></span>
- <span data-ttu-id="38d0c-149">Uma permissão pode ser uma permissão somente de aplicativo ou uma permissão delegada.</span><span class="sxs-lookup"><span data-stu-id="38d0c-149">A permission can be an app-only permission, or a delegated permission.</span></span>
- <span data-ttu-id="38d0c-150">Uma permissão delegada pode ser marcada como "permite o consentimento do usuário" ou "requer o consentimento do administrador".</span><span class="sxs-lookup"><span data-stu-id="38d0c-150">A delegated permission can be marked as “allows user consent”, or “requires admin consent”.</span></span>
- <span data-ttu-id="38d0c-151">Um aplicativo pode se comportar como um cliente (declarando que precisa de recursos de tooa permissões), como um recurso (declarando quais permissões expõe), ou ambos.</span><span class="sxs-lookup"><span data-stu-id="38d0c-151">An app can behave as a client (by declaring that it needs permissions tooa resource), as a resource (by declaring which permissions it exposes), or as both.</span></span>

## <a name="controls"></a><span data-ttu-id="38d0c-152">Controles</span><span class="sxs-lookup"><span data-stu-id="38d0c-152">Controls</span></span>

<span data-ttu-id="38d0c-153">a seguir Olá é uma lista de controles de administrador diferentes Olá disponíveis para todos os esse comportamento.</span><span class="sxs-lookup"><span data-stu-id="38d0c-153">hello following is a list of hello different admin controls available for all this behavior.</span></span> <span data-ttu-id="38d0c-154">Olá administrador controles podem ser acessados no portal clássico do hello de configurar no diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="38d0c-154">hello admin controls can be accessed in hello classic portal from configure under hello directory.</span></span>

![](media/active-directory-apps-permissions-consent/apps7.png)

<span data-ttu-id="38d0c-155">Em hello Azure portal em **gerenciar**, **as configurações de usuário**.</span><span class="sxs-lookup"><span data-stu-id="38d0c-155">In hello Azure portal, under **manage**, **user settings**.</span></span>

![](media/active-directory-apps-permissions-consent/apps11.png)



- <span data-ttu-id="38d0c-156">Você pode controlar se os usuários podem dar consentimento tooapps:</span><span class="sxs-lookup"><span data-stu-id="38d0c-156">You can control whether users can consent tooapps:</span></span>

<span data-ttu-id="38d0c-157">No portal clássico do hello, selecione **usuários podem resultar em aplicativos permissões tooaccess seus dados.**
![](media/active-directory-apps-permissions-consent/apps8.png)</span><span class="sxs-lookup"><span data-stu-id="38d0c-157">In hello classic portal, select **Users may give applications permissions tooaccess their data.**
![](media/active-directory-apps-permissions-consent/apps8.png)</span></span>

<span data-ttu-id="38d0c-158">No portal do Azure de Olá, selecione **usuários podem permitir que aplicativos tooaccess seus dados**.</span><span class="sxs-lookup"><span data-stu-id="38d0c-158">In hello Azure portal, select **users can allow apps tooaccess their data**.</span></span>
![](media/active-directory-apps-permissions-consent/apps12.png)



- <span data-ttu-id="38d0c-159">Você pode controlar se os usuários podem registrar seus próprios aplicativos de LOB único locatário: em select portal clássico do hello **os usuários podem adicionar aplicativos integrados.**
![](media/active-directory-apps-permissions-consent/apps9.png)</span><span class="sxs-lookup"><span data-stu-id="38d0c-159">You can control whether users can register their own single-tenant LOB apps: In hello classic portal select **Users may add integrated applications.**
![](media/active-directory-apps-permissions-consent/apps9.png)</span></span>

<span data-ttu-id="38d0c-160">No portal do Azure de Olá, selecione **usuários podem permitir que aplicativos tooaccess seus dados**.</span><span class="sxs-lookup"><span data-stu-id="38d0c-160">In hello Azure portal, select **users can allow apps tooaccess their data**.</span></span>
![](media/active-directory-apps-permissions-consent/apps13.png)

>[!NOTE]
><span data-ttu-id="38d0c-161">Mesmo se você permitir aos usuários aplicativos LOB tooregister único locatário, há limites toowhat pode ser registrado.</span><span class="sxs-lookup"><span data-stu-id="38d0c-161">Even if you do allow users tooregister single-tenant LOB apps, there are limits toowhat can be registered.</span></span>  
><span data-ttu-id="38d0c-162">Por exemplo, os desenvolvedores que não são administradores de diretório.</span><span class="sxs-lookup"><span data-stu-id="38d0c-162">For example, developers who are not directory admins.</span></span>
>
>- <span data-ttu-id="38d0c-163">Os usuários não podem transformar um aplicativo de locatário único em um aplicativo multilocatário.</span><span class="sxs-lookup"><span data-stu-id="38d0c-163">Users cannot make a single-tenant app a multi-tenant app.</span></span>
>- <span data-ttu-id="38d0c-164">Ao registrar os aplicativos LOB único locatário, os usuários não podem solicitar permissões somente de aplicativo tooother aplicativos.</span><span class="sxs-lookup"><span data-stu-id="38d0c-164">When registering single-tenant LOB apps, users cannot request app-only permissions tooother apps.</span></span>
>- <span data-ttu-id="38d0c-165">Ao registrar os aplicativos LOB único locatário, os usuários não podem solicitar permissões delegadas tooother aplicativos se essas permissões exigem consentimento do administrador.</span><span class="sxs-lookup"><span data-stu-id="38d0c-165">When registering single-tenant LOB apps, users cannot request delegated permissions tooother apps if those permissions require admin consent.</span></span>
>- <span data-ttu-id="38d0c-166">Os usuários não podem fazer tooapps alterações que não são proprietários do.</span><span class="sxs-lookup"><span data-stu-id="38d0c-166">Users cannot make changes tooapps that they are not owners of.</span></span>



- <span data-ttu-id="38d0c-167">Você pode controlar se os usuários podem ou não adicionar por conta própria aplicativos pré-integrados que usam o SSO de senha (também conhecido como "cofre para senhas") ![](media/active-directory-apps-permissions-consent/apps10.png)</span><span class="sxs-lookup"><span data-stu-id="38d0c-167">You can control whether users can themselves add pre-integrated apps that use password SSO (aka “password vaulting”) ![](media/active-directory-apps-permissions-consent/apps10.png)</span></span>



- <span data-ttu-id="38d0c-168">Você pode controlar as condições sob as quais aplicativos podem ser acessados (ou seja, acesso condicional).</span><span class="sxs-lookup"><span data-stu-id="38d0c-168">You can control under which conditions applications can be accessed (that is, conditional access).</span></span> <span data-ttu-id="38d0c-169">Lembre-se de que isso se aplica a toohello aplicativo de cliente e o aplicativo de recurso toohello.</span><span class="sxs-lookup"><span data-stu-id="38d0c-169">Be aware this applies both toohello client app and toohello resource app.</span></span> <span data-ttu-id="38d0c-170">Portanto, digamos que você definir uma política de acesso condicional que afirma que o aplicativo hello "Office 365 Exchange Online" só pode ser acessado de computadores, que são compatíveis.</span><span class="sxs-lookup"><span data-stu-id="38d0c-170">So, say you set a conditional access policy that says that hello “Office 365 Exchange Online” app can only be accessed from machines, which are compliant.</span></span>  <span data-ttu-id="38d0c-171">Essa política também será iniciada quando um usuário tenta toouse um aplicativo cliente que solicita permissões tooExchange on-line.</span><span class="sxs-lookup"><span data-stu-id="38d0c-171">This policy will also kick in when a user attempts toouse a client app which requests permissions tooExchange Online.</span></span>



- <span data-ttu-id="38d0c-172">Você tem visibilidade no qual aplicativos foram consentido tooand quais estão sendo usados.</span><span class="sxs-lookup"><span data-stu-id="38d0c-172">You have visibility into which apps have been consented tooand which ones are being used.</span></span>

1.  <span data-ttu-id="38d0c-173">Quando um usuário consente tooan aplicativo um objeto ServicePrincipal é criado no locatário hello.</span><span class="sxs-lookup"><span data-stu-id="38d0c-173">When a user consents tooan app, a ServicePrincipal object is created in hello tenant.</span></span> <span data-ttu-id="38d0c-174">Criação de ServicePrincipal é incluída no relatório de auditoria de saudação.</span><span class="sxs-lookup"><span data-stu-id="38d0c-174">ServicePrincipal creation is included in hello audit report.</span></span>
2.  <span data-ttu-id="38d0c-175">Relatórios de atividade de entrada do usuário dizer qual usuário do aplicativo hello está tentando entrar.</span><span class="sxs-lookup"><span data-stu-id="38d0c-175">User sign-in activity reports tell you which app hello user is signing in to.</span></span> 

## <a name="example"></a><span data-ttu-id="38d0c-176">Exemplo</span><span class="sxs-lookup"><span data-stu-id="38d0c-176">Example</span></span>

<span data-ttu-id="38d0c-177">Por exemplo, vamos hello "FabrikamMail para o Office 365" aplicativo, que você tenha percebido usuários em seu locatário estão tentando entrar.</span><span class="sxs-lookup"><span data-stu-id="38d0c-177">As an example, let’s take hello “FabrikamMail for Office 365” app, which you’ve noticed users in your tenant are signing in to.</span></span> <span data-ttu-id="38d0c-178">"FabrikamMail" é um aplicativo de leitor de email para o Android, publicado pela "Fabrikam, Inc.".</span><span class="sxs-lookup"><span data-stu-id="38d0c-178">“FabrikamMail” is a mail reader app for Android, published by “Fabrikam, Inc.”.</span></span> <span data-ttu-id="38d0c-179">Isso se encaixa hello "aplicativos multilocatários outros desenvolver, que a Contoso pode consentir".</span><span class="sxs-lookup"><span data-stu-id="38d0c-179">This falls into hello “multi-tenant apps other develop, which Contoso can consent to”.</span></span>

<span data-ttu-id="38d0c-180">Se os usuários têm permissão tooconsent, recebem uma saudação de prompt de consentimento primeira vez que entrar no:![](media/active-directory-apps-permissions-consent/apps14.png)</span><span class="sxs-lookup"><span data-stu-id="38d0c-180">If users are allowed tooconsent, they get a consent prompt hello first time they sign in: ![](media/active-directory-apps-permissions-consent/apps14.png)</span></span>

<span data-ttu-id="38d0c-181">"Acessar suas caixas de correio" é a cadeia de caracteres do hello voltado ao usuário autorização para permissão de "Acesso as caixas de correio como usuário conectado hello" hello exposto por "Office 365 Exchange Online" (ou seja, Exchange).</span><span class="sxs-lookup"><span data-stu-id="38d0c-181">“Access your mailboxes” is hello user-facing consent string for hello “Access mailboxes as hello signed-in user” permission exposed by “Office 365 Exchange Online” (that is, Exchange).</span></span>

<span data-ttu-id="38d0c-182">Você pode ver permissões Olá procurando objeto ServicePrincipal de saudação do Exchange (recurso de saudação), que foi adicionado ao se inscrever para o Office 365.</span><span class="sxs-lookup"><span data-stu-id="38d0c-182">You can see hello permissions by looking up hello ServicePrincipal object for Exchange (hello resource), which was added when you signed up for Office 365.</span></span> <span data-ttu-id="38d0c-183">Você pode pensar no objeto ServicePrincipal de saudação de uma "instância" do aplicativo hello em seu locatário, que é usado para gravar as configurações e opções diferentes.</span><span class="sxs-lookup"><span data-stu-id="38d0c-183">You can think of hello ServicePrincipal object of an “instance” of hello app in your tenant, which is used for recording different options and configurations.</span></span>  <span data-ttu-id="38d0c-184">Você pode ver isso usando Olá `Get-AzureADServicePrincipal` no PowerShell.</span><span class="sxs-lookup"><span data-stu-id="38d0c-184">You can see this by using hello `Get-AzureADServicePrincipal` in PowerShell.</span></span>

    PS C:\> Get-AzureADServicePrincipal -ObjectId 383f7b97-6754-4d3d-9474-3908ebcba1c6 | fl *
    
    DeletionTimeStamp         : 
    ObjectId                  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    ObjectType                : ServicePrincipal
    AccountEnabled            : True
    AppDisplayName            : Office 365 Exchange Online
    AppId                     : 00000002-0000-0ff1-ce00-000000000000
    AppOwnerTenantId          : 
    AppRoleAssignmentRequired : False
    AppRoles                  : {...}
    DisplayName               : Microsoft.Exchange
    ErrorUrl                  : 
    Homepage                  : 
    KeyCredentials            : {}
    LogoutUrl                 : 
    Oauth2Permissions         : {...
                                , class OAuth2Permission {
                                  AdminConsentDescription : Allows hello app toohave hello same access toomailboxes as hello signed-in user via Exchange Web Services.
                                  AdminConsentDisplayName : Access mailboxes as hello signed-in user via Exchange Web Services
                                  Id                      : 3b5f3d61-589b-4a3c-a359-5dd4b5ee5bd5
                                  IsEnabled               : True
                                  Type                    : User
                                  UserConsentDescription  : Allows hello app full access tooyour mailboxes on your behalf.
                                  UserConsentDisplayName  : Access your mailboxes
                                  Value                   : full_access_as_user
                                },
                                ...}
    PasswordCredentials       : {}
    PublisherName             : 
    ReplyUrl                  : 
    SamlMetadataUrl           : 
    ServicePrincipalNames     : {00000002-0000-0ff1-ce00-000000000000/outlook.office365.com, 00000002-0000-0ff1-ce00-000000000000/mail.office365.com, 00000002-0000-0ff1-ce00-000000000000/outlook.com, 
                                00000002-0000-0ff1-ce00-000000000000/*.outlook.com...}
    Tags                      : {}

<span data-ttu-id="38d0c-185">Consentimento é iniciado quando o usuário Olá clicar em "Aceitar".</span><span class="sxs-lookup"><span data-stu-id="38d0c-185">Consent is initiated when hello user clicks “Accept”.</span></span> <span data-ttu-id="38d0c-186">Primeiro, um objeto ServicePrincipal para "FabrikamMail para o Office 365" é criado no locatário hello.</span><span class="sxs-lookup"><span data-stu-id="38d0c-186">First, a ServicePrincipal object for “FabrikamMail for Office 365” is created in hello tenant.</span></span> <span data-ttu-id="38d0c-187">Olá ServicePrincipal parecida com esta:</span><span class="sxs-lookup"><span data-stu-id="38d0c-187">hello ServicePrincipal looks something like this:</span></span>

    PS C:\> Get-AzureADServicePrincipal -SearchString "FabrikamMail for Office 365" | fl *
    
    DeletionTimeStamp         : 
    ObjectId                  : a8b16333-851d-42e8-acd2-eac155849b37
    ObjectType                : ServicePrincipal
    AccountEnabled            : True
    AppDisplayName            : FabrikamMail for Office 365
    AppId                     : aba7c072-2267-4031-8960-e7a2db6e0590
    AppOwnerTenantId          : 4a4076e0-a70f-41c6-b819-6f9c4a86df89
    AppRoleAssignmentRequired : False
    AppRoles                  : {}
    DisplayName               : FabrikamMail for Office 365
    ErrorUrl                  : 
    Homepage                  : 
    KeyCredentials            : {}
    LogoutUrl                 : 
    Oauth2Permissions         : {}
    PasswordCredentials       : {}
    PublisherName             : Fabrikam, Inc.
    ReplyUrl                  : 
    SamlMetadataUrl           : 
    ServicePrincipalNames     : {aba7c072-2267-4031-8960-e7a2db6e0590}
    Tags                      : {WindowsAzureActiveDirectoryIntegratedApp}

<span data-ttu-id="38d0c-188">Consentimento tooan aplicativo cria um link de Oauth2PermissionGrant entre seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="38d0c-188">Consenting tooan app creates an Oauth2PermissionGrant link between hello following:</span></span>
  
- <span data-ttu-id="38d0c-189">objeto de usuário Olá</span><span class="sxs-lookup"><span data-stu-id="38d0c-189">hello user object</span></span>
- <span data-ttu-id="38d0c-190">aplicativos de cliente Olá ServicePrincipalName (SPN)</span><span class="sxs-lookup"><span data-stu-id="38d0c-190">hello client apps ServicePrincipalName (SPN)</span></span>
- <span data-ttu-id="38d0c-191">aplicativos de recurso Olá ServicePrincipalName (SPN)</span><span class="sxs-lookup"><span data-stu-id="38d0c-191">hello resource apps ServicePrincipalName (SPN)</span></span>
- <span data-ttu-id="38d0c-192">permissões no aplicativo de recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="38d0c-192">permissions in hello resource app.</span></span>  

<span data-ttu-id="38d0c-193">No caso de saudação de FabrikamMail, parece que algo assim:</span><span class="sxs-lookup"><span data-stu-id="38d0c-193">In hello case of FabrikamMail, it looks something like this:</span></span>

    PS C:\> Get-AzureADUserOAuth2PermissionGrant -ObjectId ddiggle@aadpremiumlab.onmicrosoft.com | fl *
    
    ClientId    : a8b16333-851d-42e8-acd2-eac155849b37
    ConsentType : Principal
    ExpiryTime  : 05/15/2017 07:02:39 AM
    ObjectId    : M2OxqB2F6EKs0urBVYSbN5d7PzhUZz1NlH25COvLocbJjoxkUFfRQauryBKwBWet
    PrincipalId : 648c8ec9-5750-41d1-abab-c812b00567ad
    ResourceId  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    Scope       : full_access_as_user
    StartTime   : 01/01/0001 12:00:00 AM

<span data-ttu-id="38d0c-194">(**ClientId** é a ID de objeto principal de serviço do FabrikamMail (Olá que foi criada apenas), **PrincipalId** é a ID de objeto de usuário hello (saudação do usuário do que consentimento), **ResourceId**é o serviço do Exchange ID de objeto principal, o escopo é a permissão de saudação do Exchange foi consentimento).</span><span class="sxs-lookup"><span data-stu-id="38d0c-194">(**ClientId** is FabrikamMail’s service principal object ID (hello one that just got created), **PrincipalId** is hello user object ID (of hello user who consented), **ResourceId** is Exchange’s service principal object ID, Scope is hello permission in Exchange that was consented to).</span></span>

<span data-ttu-id="38d0c-195">Se os usuários não são permitidos tooconsent, eles verão uma tela que diz que essa permissão é necessária.</span><span class="sxs-lookup"><span data-stu-id="38d0c-195">If users are not allowed tooconsent, they will see a screen that says that permission is required.</span></span>

