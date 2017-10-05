---
title: Aplicativo inesperado em minha lista de aplicativos | Microsoft Docs
description: "Como ver todos os aplicativos em seu locatário e entender como os aplicativos aparecem na lista Todos os Aplicativos em Aplicativos Empresariais"
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
ms.openlocfilehash: 0f8136cb066fa6e3e4a8dd06e34b9f866e3916f6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="unexpected-application-in-my-applications-list"></a><span data-ttu-id="0749c-103">Aplicativo inesperado em minha lista de aplicativos</span><span class="sxs-lookup"><span data-stu-id="0749c-103">Unexpected application in my applications list</span></span>

<span data-ttu-id="0749c-104">Este artigo o ajudará a entender como os aplicativos aparecem na lista **Todos os Aplicativos** em **Aplicativos Empresariais**.</span><span class="sxs-lookup"><span data-stu-id="0749c-104">This article help you to understand how applications appear in your **All Applications** list under **Enterprise Applications**.</span></span> 

## <a name="how-to-see-all-applications-in-your-tenant"></a><span data-ttu-id="0749c-105">Como ver todos os aplicativos em seu locatário</span><span class="sxs-lookup"><span data-stu-id="0749c-105">How to see all applications in your tenant</span></span>

<span data-ttu-id="0749c-106">Para ver todos os aplicativos em seu locatário, você precisa usar o controle de **Filtro** para exibir **Todos os Aplicativos** na lista **Todos os Aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="0749c-106">To see all the applications in your tenant, you need to use the **Filter** control to show **All Applications** under the **All Applications** list.</span></span> <span data-ttu-id="0749c-107">Para fazer isso, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="0749c-107">To do this, follow the steps below:</span></span>

1.  <span data-ttu-id="0749c-108">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="0749c-108">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="0749c-109">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="0749c-109">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="0749c-110">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0749c-110">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="0749c-111">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0749c-111">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="0749c-112">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="0749c-112">click **All Applications** to view a list of all your applications.</span></span>

6.  <span data-ttu-id="0749c-113">Clique para usar o controle de **Filtro** na parte superior do **Lista de Todos os Aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="0749c-113">click the use the **Filter** control at the top of the **All Applications List**.</span></span>

7.  <span data-ttu-id="0749c-114">Na folha **Filtro**, defina a opção **Exibir** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="0749c-114">On the **Filter** blade, set the **Show** option to **All Applications.**</span></span>

## <a name="why-does-a-specific-application-appear-in-my-all-applications-list"></a><span data-ttu-id="0749c-115">Por que um aplicativo específico aparece em minha lista de todos os aplicativos?</span><span class="sxs-lookup"><span data-stu-id="0749c-115">Why does a specific application appear in my all applications list?</span></span>

<span data-ttu-id="0749c-116">Quando filtrada para **Todos os Aplicativos**, a **Lista** **Todos os Aplicativos** mostra todos os objetos de Entidade de Serviço em seu locatário.</span><span class="sxs-lookup"><span data-stu-id="0749c-116">When filtered to **All Applications**, the **All Applications** **List** shows every Service Principal object in your tenant.</span></span> <span data-ttu-id="0749c-117">Objetos de Entidade de Serviço podem aparecer nessa lista de uma várias maneiras:</span><span class="sxs-lookup"><span data-stu-id="0749c-117">Service Principal objects can appear in this list in a various ways:</span></span>

1.  <span data-ttu-id="0749c-118">Quando você adiciona qualquer aplicativo da galeria de aplicativos, incluindo:</span><span class="sxs-lookup"><span data-stu-id="0749c-118">When you add any application from the application gallery, including:</span></span>

   1. <span data-ttu-id="0749c-119">**Aplicativos da Galeria do Azure AD** – um aplicativo que foi integrado previamente para logon único com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0749c-119">**Azure AD Gallery Applications** – An application that has been pre-integrated for single sign-on with Azure AD.</span></span>

   2. <span data-ttu-id="0749c-120">**Aplicativos do Proxy de Aplicativo** – um aplicativo em execução em seu ambiente local para o qual você deseja fornecer logon único seguro externamente.</span><span class="sxs-lookup"><span data-stu-id="0749c-120">**Application Proxy Applications** – An application running in your on-premises environment that you want to provide secure single-sign on to externally.</span></span>

   3. <span data-ttu-id="0749c-121">**Aplicativos desenvolvidos de forma personalizada** – um aplicativo que sua organização deseja desenvolver na Plataforma de Desenvolvimento de Aplicativos do Azure AD, mas que talvez ainda não exista.</span><span class="sxs-lookup"><span data-stu-id="0749c-121">**Custom-developed Applications** – An application that your organization wishes to develop on the Azure AD Application Development Platform, but that may not exist yet.</span></span>

   4. <span data-ttu-id="0749c-122">**Aplicativos inexistentes na Galeria** – traga seus aplicativos!</span><span class="sxs-lookup"><span data-stu-id="0749c-122">**Non-Gallery Applications** – Bring your own applications!</span></span> <span data-ttu-id="0749c-123">Qualquer link da Web desejado, ou qualquer aplicativo que renderiza um campo de nome de usuário e senha, dá suporte aos protocolos SAML ou OpenID Connect ou dá suporte ao SCIM que você deseja integrar para logon único com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0749c-123">Any web link you want, or any application which renders a username and password field, supports SAML or OpenID Connect protocols, or supports SCIM which you wish to integrate for single sign-on with Azure AD.</span></span>

2.  <span data-ttu-id="0749c-124">Ao se inscrever ou entrar em um aplicativo de <sup>terceiros</sup> integrado ao Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0749c-124">When signing up for, or signing in to, a 3<sup>rd</sup> party application integrated with Azure Active Directory.</span></span> <span data-ttu-id="0749c-125">Um exemplo disso é o [Smartsheet](https://app.smartsheet.com/b/home) ou o [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).</span><span class="sxs-lookup"><span data-stu-id="0749c-125">One example of this is [Smartsheet](https://app.smartsheet.com/b/home) or [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).</span></span>

3.  <span data-ttu-id="0749c-126">Ao se inscrever ou adicionar uma licença a um usuário ou grupo para um aplicativo interno, como o [Microsoft Office 365](http://products.office.com/).</span><span class="sxs-lookup"><span data-stu-id="0749c-126">When signing up for, or adding a license to a user or a group to a first party application, like [Microsoft Office 365](http://products.office.com/).</span></span>

4.  <span data-ttu-id="0749c-127">Quando você adiciona um novo registro de aplicativo criando um aplicativo personalizado usando o [Registro de Aplicativos](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).</span><span class="sxs-lookup"><span data-stu-id="0749c-127">When you add a new application registration by creating a custom-developed application using the [Application Registry](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).</span></span>

5.  <span data-ttu-id="0749c-128">Quando você adiciona um novo registro de aplicativo criando um aplicativo personalizado usando o [Portal de Registro de Aplicativos V2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal).</span><span class="sxs-lookup"><span data-stu-id="0749c-128">When you add a new application registration by creating a custom-developed application using the [V2.0 Application Registration Portal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal).</span></span>

6.  <span data-ttu-id="0749c-129">Quando você adiciona um aplicativo que está desenvolvendo usando os [Métodos de autenticação do ASP.net](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) ou os [Serviços Conectados](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx) do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0749c-129">When you add an application you’re developing using Visual Studio’s [ASP.net Authentication Methods](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) or [Connected Services](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx).</span></span>

7.  <span data-ttu-id="0749c-130">Quando você cria um objeto de entidade de serviço usando o [Módulo do PowerShell do Azure AD](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="0749c-130">When you create a service principal object using the [Azure AD PowerShell Module](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

8.  <span data-ttu-id="0749c-131">Quando você [dá consentimento a um aplicativo](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) como administrador para usar dados em seu locatário.</span><span class="sxs-lookup"><span data-stu-id="0749c-131">When you [consent to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) as an administrator to use data in your tenant.</span></span>

9.  <span data-ttu-id="0749c-132">Quando um [usuário dá consentimento para um aplicativo](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) usar dados no seu locatário.</span><span class="sxs-lookup"><span data-stu-id="0749c-132">When a [user consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) to use data in your tenant.</span></span>

10. <span data-ttu-id="0749c-133">Quando você habilita determinados serviços que armazenam dados em seu locatário.</span><span class="sxs-lookup"><span data-stu-id="0749c-133">When you enable certain services that store data in your tenant.</span></span> <span data-ttu-id="0749c-134">Um exemplo disso é a Redefinição de Senha, que é modelada como uma entidade de serviço para armazenar sua senha de redefinição de senha com segurança.</span><span class="sxs-lookup"><span data-stu-id="0749c-134">One example of this is Password Reset, which is modeled as a service principal to store your password reset policy securely.</span></span>

<span data-ttu-id="0749c-135">Para obter mais detalhes sobre como aplicativos são adicionados ao seu diretório, leia [Como e por que os aplicativos são adicionados ao Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).</span><span class="sxs-lookup"><span data-stu-id="0749c-135">To get more details on how apps are added to your directory, read [How and why applications are added to Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).</span></span>

## <a name="i-want-to-remove-a-specific-users-or-groups-assignment-to-an-application"></a><span data-ttu-id="0749c-136">Quero remover a atribuição de um usuário ou grupo específico para um aplicativo</span><span class="sxs-lookup"><span data-stu-id="0749c-136">I want to remove a specific user’s or group’s assignment to an application</span></span>

<span data-ttu-id="0749c-137">Para remover uma atribuição de um usuário ou grupo a um aplicativo, siga as etapas listadas no artigo [Remover uma atribuição de usuário ou grupo de um aplicativo empresarial no Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="0749c-137">To remove a user or group assignment to an application, follow the steps listed in the [Remove a user or group assignment from an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) article.</span></span>

## <a name="i-want-to-disable-all-access-to-an-application-for-every-user"></a><span data-ttu-id="0749c-138">Quero desabilitar todo o acesso a um aplicativo para todos os usuários</span><span class="sxs-lookup"><span data-stu-id="0749c-138">I want to disable all access to an application for every user</span></span>

<span data-ttu-id="0749c-139">Para desabilitar todos os logons de usuário em um aplicativo, siga as etapas listadas no artigo [Desabilitar logons de usuário para um aplicativo empresarial no Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="0749c-139">To disable all user sign-ins to an application, follow the steps listed in the [Disable user sign-ins for an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) article.</span></span>

## <a name="i-want-to-delete-an-application-entirely"></a><span data-ttu-id="0749c-140">Quero excluir um aplicativo completamente</span><span class="sxs-lookup"><span data-stu-id="0749c-140">I want to delete an application entirely</span></span>

<span data-ttu-id="0749c-141">Para **excluir um aplicativo**, siga as instruções abaixo:</span><span class="sxs-lookup"><span data-stu-id="0749c-141">To **delete an application**, follow the instructions below:</span></span>

1.  <span data-ttu-id="0749c-142">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="0749c-142">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="0749c-143">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="0749c-143">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="0749c-144">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0749c-144">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="0749c-145">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0749c-145">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="0749c-146">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="0749c-146">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="0749c-147">Se você não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="0749c-147">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="0749c-148">Selecione o aplicativo que deseja excluir.</span><span class="sxs-lookup"><span data-stu-id="0749c-148">Select the application you want to delete.</span></span>

7.  <span data-ttu-id="0749c-149">Após o aplicativo ser carregado, clique no ícone **Excluir** na folha **Visão Geral** superior do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0749c-149">Once the application loads, click **Delete** icon from the top application’s **Overview** blade.</span></span>

## <a name="i-want-to-disable-all-future-user-consent-operations-to-any-application"></a><span data-ttu-id="0749c-150">Quero desabilitar todas as futuras operações de consentimento do usuário para qualquer aplicativo</span><span class="sxs-lookup"><span data-stu-id="0749c-150">I want to disable all future user consent operations to any application</span></span>

<span data-ttu-id="0749c-151">Desabilitar o consentimento do usuário para todo o seu diretório impede que os usuários finais consintam com qualquer aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0749c-151">Disabling user consent for your entire directory prevent end users from consenting to any application.</span></span> <span data-ttu-id="0749c-152">Os administradores ainda podem consentir em nome dos usuários.</span><span class="sxs-lookup"><span data-stu-id="0749c-152">Administrators can still consent on user’s behalves.</span></span> <span data-ttu-id="0749c-153">Para saber mais sobre o consentimento de aplicativos e por que você pode ou não querer fazer isso, leia [Entendendo o consentimento do usuário e do administrador](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span><span class="sxs-lookup"><span data-stu-id="0749c-153">To learn more about application consent, and why you may or may not wish to do this, read [Understanding user and admin consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span></span>

<span data-ttu-id="0749c-154">Para **desabilitar todas as futuras operações de consentimento do usuário no diretório inteiro**, siga as instruções abaixo:</span><span class="sxs-lookup"><span data-stu-id="0749c-154">To **disable all future user consent operations in your entire directory**, follow the instructions below:</span></span>

1.  <span data-ttu-id="0749c-155">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="0749c-155">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="0749c-156">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="0749c-156">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="0749c-157">Digite **"Azure Active Directory**" na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0749c-157">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="0749c-158">Clique em **Usuários e grupos** no menu de navegação.</span><span class="sxs-lookup"><span data-stu-id="0749c-158">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="0749c-159">Clique em **Configurações de usuário**.</span><span class="sxs-lookup"><span data-stu-id="0749c-159">click **User settings**.</span></span>

6.  <span data-ttu-id="0749c-160">Desabilite todas as futuras operações de consentimento do usuário definindo o controle de alternância **Os usuários podem permitir que os aplicativos acessem seus dados** como **Não** e clique no botão **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="0749c-160">Disable all future user consent operations by setting the **Users can allow apps to access their data** toggle to **No** and click the **Save** button.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0749c-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0749c-161">Next steps</span></span>
[<span data-ttu-id="0749c-162">Gerenciando aplicativos com o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0749c-162">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
