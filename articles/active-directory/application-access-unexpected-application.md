---
title: aplicativo de aaaUnexpected na minha lista de aplicativos | Microsoft Docs
description: "Como toosee todos os aplicativos em seu locatário e entender como os aplicativos aparecem na sua lista de todos os aplicativos em aplicativos corporativos"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 2f974046b655bc36a05f002c56511a8a988cd01c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-application-in-my-applications-list"></a><span data-ttu-id="fbcb6-103">Aplicativo inesperado em minha lista de aplicativos</span><span class="sxs-lookup"><span data-stu-id="fbcb6-103">Unexpected application in my applications list</span></span>

<span data-ttu-id="fbcb6-104">Este artigo ajuda toounderstand como os aplicativos são exibidos em seu **todos os aplicativos** lista sob **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="fbcb6-104">This article help you toounderstand how applications appear in your **All Applications** list under **Enterprise Applications**.</span></span> 

## <a name="how-toosee-all-applications-in-your-tenant"></a><span data-ttu-id="fbcb6-105">Como toosee todos os aplicativos em seu locatário</span><span class="sxs-lookup"><span data-stu-id="fbcb6-105">How toosee all applications in your tenant</span></span>

<span data-ttu-id="fbcb6-106">toosee Olá a todos os aplicativos em seu locatário, é necessário Olá toouse **filtro** controlar tooshow **todos os aplicativos** em Olá **todos os aplicativos** lista.</span><span class="sxs-lookup"><span data-stu-id="fbcb6-106">toosee all hello applications in your tenant, you need toouse hello **Filter** control tooshow **All Applications** under hello **All Applications** list.</span></span> <span data-ttu-id="fbcb6-107">toodo isso, execute Olá estas etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="fbcb6-107">toodo this, follow hello steps below:</span></span>

1.  <span data-ttu-id="fbcb6-108">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="fbcb6-108">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="fbcb6-109">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="fbcb6-109">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fbcb6-110">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="fbcb6-110">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fbcb6-111">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="fbcb6-111">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="fbcb6-112">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="fbcb6-112">click **All Applications** tooview a list of all your applications.</span></span>

6.  <span data-ttu-id="fbcb6-113">Clique em Olá use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="fbcb6-113">click hello use hello **Filter** control at hello top of hello **All Applications List**.</span></span>

7.  <span data-ttu-id="fbcb6-114">Em Olá **filtro** folha, Olá conjunto **Mostrar** opção muito**todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="fbcb6-114">On hello **Filter** blade, set hello **Show** option too**All Applications.**</span></span>

## <a name="why-does-a-specific-application-appear-in-my-all-applications-list"></a><span data-ttu-id="fbcb6-115">Por que um aplicativo específico aparece em minha lista de todos os aplicativos?</span><span class="sxs-lookup"><span data-stu-id="fbcb6-115">Why does a specific application appear in my all applications list?</span></span>

<span data-ttu-id="fbcb6-116">Quando filtrada muito**todos os aplicativos**, Olá **todos os aplicativos** **lista** mostra todos os objetos de entidade de serviço no seu locatário.</span><span class="sxs-lookup"><span data-stu-id="fbcb6-116">When filtered too**All Applications**, hello **All Applications** **List** shows every Service Principal object in your tenant.</span></span> <span data-ttu-id="fbcb6-117">Objetos de Entidade de Serviço podem aparecer nessa lista de uma várias maneiras:</span><span class="sxs-lookup"><span data-stu-id="fbcb6-117">Service Principal objects can appear in this list in a various ways:</span></span>

1.  <span data-ttu-id="fbcb6-118">Quando você adicionar qualquer aplicativo da Galeria de aplicativo hello, incluindo:</span><span class="sxs-lookup"><span data-stu-id="fbcb6-118">When you add any application from hello application gallery, including:</span></span>

   1. <span data-ttu-id="fbcb6-119">**Aplicativos da Galeria do Azure AD** – um aplicativo que foi integrado previamente para logon único com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fbcb6-119">**Azure AD Gallery Applications** – An application that has been pre-integrated for single sign-on with Azure AD.</span></span>

   2. <span data-ttu-id="fbcb6-120">**Aplicativos de Proxy de aplicativo** – um aplicativo em execução no seu ambiente local que você deseja tooprovide segura de logon único tooexternally.</span><span class="sxs-lookup"><span data-stu-id="fbcb6-120">**Application Proxy Applications** – An application running in your on-premises environment that you want tooprovide secure single-sign on tooexternally.</span></span>

   3. <span data-ttu-id="fbcb6-121">**Aplicativos personalizado** – Olá de um aplicativo que sua organização deseja toodevelop na plataforma de desenvolvimento de aplicativo do Azure AD, mas que talvez ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="fbcb6-121">**Custom-developed Applications** – An application that your organization wishes toodevelop on hello Azure AD Application Development Platform, but that may not exist yet.</span></span>

   4. <span data-ttu-id="fbcb6-122">**Aplicativos inexistentes na Galeria** – traga seus aplicativos!</span><span class="sxs-lookup"><span data-stu-id="fbcb6-122">**Non-Gallery Applications** – Bring your own applications!</span></span> <span data-ttu-id="fbcb6-123">Qualquer link da web que você deseja, qualquer aplicativo que processa um campo de nome de usuário e senha, oferece suporte a protocolos SAML ou OpenID Connect ou oferece suporte a SCIM que você deseja toointegrate para logon único com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fbcb6-123">Any web link you want, or any application which renders a username and password field, supports SAML or OpenID Connect protocols, or supports SCIM which you wish toointegrate for single sign-on with Azure AD.</span></span>

2.  <span data-ttu-id="fbcb6-124">Ao se inscrever ou entrar em um aplicativo de <sup>terceiros</sup> integrado ao Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fbcb6-124">When signing up for, or signing in to, a 3<sup>rd</sup> party application integrated with Azure Active Directory.</span></span> <span data-ttu-id="fbcb6-125">Um exemplo disso é o [Smartsheet](https://app.smartsheet.com/b/home) ou o [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).</span><span class="sxs-lookup"><span data-stu-id="fbcb6-125">One example of this is [Smartsheet](https://app.smartsheet.com/b/home) or [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).</span></span>

3.  <span data-ttu-id="fbcb6-126">Quando se inscrever ou adicionar um usuário de tooa de licença ou um grupo tooa primeiro aplicativo, como [Microsoft Office 365](http://products.office.com/).</span><span class="sxs-lookup"><span data-stu-id="fbcb6-126">When signing up for, or adding a license tooa user or a group tooa first party application, like [Microsoft Office 365](http://products.office.com/).</span></span>

4.  <span data-ttu-id="fbcb6-127">Quando você adiciona um novo registro de aplicativo, criando um aplicativo personalizado usando Olá [registro de aplicativos](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).</span><span class="sxs-lookup"><span data-stu-id="fbcb6-127">When you add a new application registration by creating a custom-developed application using hello [Application Registry](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).</span></span>

5.  <span data-ttu-id="fbcb6-128">Quando você adiciona um novo registro de aplicativo, criando um aplicativo personalizado usando Olá [Portal de registro de aplicativo v 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal).</span><span class="sxs-lookup"><span data-stu-id="fbcb6-128">When you add a new application registration by creating a custom-developed application using hello [V2.0 Application Registration Portal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal).</span></span>

6.  <span data-ttu-id="fbcb6-129">Quando você adiciona um aplicativo que está desenvolvendo usando os [Métodos de autenticação do ASP.net](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) ou os [Serviços Conectados](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx) do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fbcb6-129">When you add an application you’re developing using Visual Studio’s [ASP.net Authentication Methods](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) or [Connected Services](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx).</span></span>

7.  <span data-ttu-id="fbcb6-130">Quando você cria um objeto de entidade de serviço usando Olá [módulo PowerShell do AD do Azure](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="fbcb6-130">When you create a service principal object using hello [Azure AD PowerShell Module](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

8.  <span data-ttu-id="fbcb6-131">Quando você [consentimento de aplicativo tooan](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) como dados de toouse um administrador no seu locatário.</span><span class="sxs-lookup"><span data-stu-id="fbcb6-131">When you [consent tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) as an administrator toouse data in your tenant.</span></span>

9.  <span data-ttu-id="fbcb6-132">Quando um [tooan aplicativo consentimento do usuário](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toouse dados em seu locatário.</span><span class="sxs-lookup"><span data-stu-id="fbcb6-132">When a [user consents tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toouse data in your tenant.</span></span>

10. <span data-ttu-id="fbcb6-133">Quando você habilita determinados serviços que armazenam dados em seu locatário.</span><span class="sxs-lookup"><span data-stu-id="fbcb6-133">When you enable certain services that store data in your tenant.</span></span> <span data-ttu-id="fbcb6-134">Um exemplo disso é a redefinição de senha, que é modelada como um toostore principal do serviço sua senha redefinida política com segurança.</span><span class="sxs-lookup"><span data-stu-id="fbcb6-134">One example of this is Password Reset, which is modeled as a service principal toostore your password reset policy securely.</span></span>

<span data-ttu-id="fbcb6-135">tooget obter mais detalhes sobre como os aplicativos são adicionados tooyour diretório, leia [como e por que os aplicativos são adicionados tooAzure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).</span><span class="sxs-lookup"><span data-stu-id="fbcb6-135">tooget more details on how apps are added tooyour directory, read [How and why applications are added tooAzure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).</span></span>

## <a name="i-want-tooremove-a-specific-users-or-groups-assignment-tooan-application"></a><span data-ttu-id="fbcb6-136">Desejo tooremove aplicativos de tooan de atribuição de um usuário específico ou do grupo</span><span class="sxs-lookup"><span data-stu-id="fbcb6-136">I want tooremove a specific user’s or group’s assignment tooan application</span></span>

<span data-ttu-id="fbcb6-137">tooremove um usuário ou grupo atribuição tooan aplicativo, execute as etapas de saudação listadas no hello [remover uma atribuição de usuário ou grupo de um aplicativo de empresa no Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) artigo.</span><span class="sxs-lookup"><span data-stu-id="fbcb6-137">tooremove a user or group assignment tooan application, follow hello steps listed in hello [Remove a user or group assignment from an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) article.</span></span>

## <a name="i-want-toodisable-all-access-tooan-application-for-every-user"></a><span data-ttu-id="fbcb6-138">Desejo toodisable todos os aplicativos de tooan de acesso para cada usuário</span><span class="sxs-lookup"><span data-stu-id="fbcb6-138">I want toodisable all access tooan application for every user</span></span>

<span data-ttu-id="fbcb6-139">toodisable todos os usuário entradas tooan de aplicativos, siga etapas de saudação listadas Olá [desabilitar entradas do usuário para um aplicativo de empresa no Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) artigo.</span><span class="sxs-lookup"><span data-stu-id="fbcb6-139">toodisable all user sign-ins tooan application, follow hello steps listed in hello [Disable user sign-ins for an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) article.</span></span>

## <a name="i-want-toodelete-an-application-entirely"></a><span data-ttu-id="fbcb6-140">Desejo toodelete um aplicativo totalmente</span><span class="sxs-lookup"><span data-stu-id="fbcb6-140">I want toodelete an application entirely</span></span>

<span data-ttu-id="fbcb6-141">muito**excluir um aplicativo**, siga as instruções de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="fbcb6-141">too**delete an application**, follow hello instructions below:</span></span>

1.  <span data-ttu-id="fbcb6-142">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="fbcb6-142">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="fbcb6-143">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="fbcb6-143">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fbcb6-144">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="fbcb6-144">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fbcb6-145">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="fbcb6-145">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="fbcb6-146">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="fbcb6-146">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="fbcb6-147">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="fbcb6-147">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="fbcb6-148">Selecione o aplicativo hello deseja toodelete.</span><span class="sxs-lookup"><span data-stu-id="fbcb6-148">Select hello application you want toodelete.</span></span>

7.  <span data-ttu-id="fbcb6-149">Depois que o aplicativo hello carrega, clique em **excluir** ícone do aplicativo de superior hello **visão geral** folha.</span><span class="sxs-lookup"><span data-stu-id="fbcb6-149">Once hello application loads, click **Delete** icon from hello top application’s **Overview** blade.</span></span>

## <a name="i-want-toodisable-all-future-user-consent-operations-tooany-application"></a><span data-ttu-id="fbcb6-150">Desejo toodisable todos os aplicativos do usuário futuras consentimento operações tooany</span><span class="sxs-lookup"><span data-stu-id="fbcb6-150">I want toodisable all future user consent operations tooany application</span></span>

<span data-ttu-id="fbcb6-151">Desabilitando o consentimento do usuário para seu diretório de todo a impedir que usuários finais de consentimento tooany aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fbcb6-151">Disabling user consent for your entire directory prevent end users from consenting tooany application.</span></span> <span data-ttu-id="fbcb6-152">Os administradores ainda podem consentir em nome dos usuários.</span><span class="sxs-lookup"><span data-stu-id="fbcb6-152">Administrators can still consent on user’s behalves.</span></span> <span data-ttu-id="fbcb6-153">toolearn mais sobre o aplicativo de consentimento e por que você pode ou não poderá toodo, leitura [usuário conhecimento e consentimento do administrador](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span><span class="sxs-lookup"><span data-stu-id="fbcb6-153">toolearn more about application consent, and why you may or may not wish toodo this, read [Understanding user and admin consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span></span>

<span data-ttu-id="fbcb6-154">muito**desabilitar todas as operações de consentimento do usuário futuras em seu diretório inteiro**, siga as instruções de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="fbcb6-154">too**disable all future user consent operations in your entire directory**, follow hello instructions below:</span></span>

1.  <span data-ttu-id="fbcb6-155">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="fbcb6-155">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fbcb6-156">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="fbcb6-156">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fbcb6-157">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="fbcb6-157">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fbcb6-158">Clique em **usuários e grupos** no menu de navegação hello.</span><span class="sxs-lookup"><span data-stu-id="fbcb6-158">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="fbcb6-159">Clique em **Configurações de usuário**.</span><span class="sxs-lookup"><span data-stu-id="fbcb6-159">click **User settings**.</span></span>

6.  <span data-ttu-id="fbcb6-160">Desabilitar todas as operações de consentimento do usuário futuro por configuração Olá **usuários podem permitir que aplicativos tooaccess seus dados** alternar muito**não** e clique em Olá **salvar** botão.</span><span class="sxs-lookup"><span data-stu-id="fbcb6-160">Disable all future user consent operations by setting hello **Users can allow apps tooaccess their data** toggle too**No** and click hello **Save** button.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fbcb6-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fbcb6-161">Next steps</span></span>
[<span data-ttu-id="fbcb6-162">Gerenciando aplicativos com o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fbcb6-162">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
