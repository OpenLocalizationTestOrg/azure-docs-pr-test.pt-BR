---
title: aaaHow tooconfigure senha single sign-on para um aplicativo da Galeria do AD do Azure | Microsoft Docs
description: "Como tooconfigure um aplicativo para proteger com base em senha de logon único quando ele estiver listado em Olá Galeria de aplicativos do Azure AD"
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
ms.openlocfilehash: 7a93bff119b477d946368686fc2d9006ca2722a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="f6f02-103">Como senha tooconfigure o logon único para um aplicativo da Galeria do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f6f02-103">How tooconfigure password single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="f6f02-104">Quando você adicionar um aplicativo de saudação [Galeria de aplicativos do Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery), você tem a opção de saudação de como você deseja que seu toosign usuários no aplicativo toothat.</span><span class="sxs-lookup"><span data-stu-id="f6f02-104">When you add an application from hello [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery), you have hello choice of how you want your users toosign in toothat application.</span></span> <span data-ttu-id="f6f02-105">Você pode configurar essa opção a qualquer momento selecionando Olá **Single Sign-on** item de navegação em um aplicativo corporativo em Olá [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f6f02-105">You can configure this choice at any time by selecting hello **Single Sign-on** navigation item on an Enterprise Application in hello [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="f6f02-106">Uma saudação métodos de logon único disponíveis tooyou é hello [com base em senha de logon único](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) opção.</span><span class="sxs-lookup"><span data-stu-id="f6f02-106">One of hello single sign-on methods available tooyou is hello [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span></span> <span data-ttu-id="f6f02-107">Isso é uma ótima maneira tooget iniciado integrando aplicativos no AD do Azure rapidamente e permite que você:</span><span class="sxs-lookup"><span data-stu-id="f6f02-107">This is a great way tooget started integrating applications into Azure AD quickly, and allows you to:</span></span>

-   <span data-ttu-id="f6f02-108">Habilitar **logon único para seus usuários** armazenando com segurança e repetição de nomes de usuário e senhas para o aplicativo hello integrado com o Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6f02-108">Enable **Single Sign-on for your users** by securely storing and replaying usernames and passwords for hello application you’ve integrated with Azure AD</span></span>

-   <span data-ttu-id="f6f02-109">**Suporte a aplicativos que exigem vários campos de entrada** para aplicativos que exigem o nome de usuário e senha mais do que apenas toosign campos em</span><span class="sxs-lookup"><span data-stu-id="f6f02-109">**Support applications that require multiple sign-in fields** for applications that require more than just username and password fields toosign in</span></span>

-   <span data-ttu-id="f6f02-110">**Personalizar rótulos Olá** dos campos de entrada de usuário e senha Olá os usuários vejam no hello [painel de acesso do aplicativo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) quando eles digitem suas credenciais</span><span class="sxs-lookup"><span data-stu-id="f6f02-110">**Customize hello labels** of hello username and password input fields your users see on hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) when they enter their credentials</span></span>

-   <span data-ttu-id="f6f02-111">Permitir que seu **usuários** tooprovide seus próprios nomes de usuário e senhas para contas de aplicativo existente que estão digitando no manualmente no hello [painel de acesso do aplicativo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span><span class="sxs-lookup"><span data-stu-id="f6f02-111">Allow your **users** tooprovide their own usernames and passwords for any existing application accounts they are typing in manually on hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span></span>

-   <span data-ttu-id="f6f02-112">Permitir que um **membro do grupo de negócios Olá** toospecify Olá os nomes de usuário e senhas atribuídas tooa usuário usando Olá [autoatendimento acesso ao aplicativo](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) recurso</span><span class="sxs-lookup"><span data-stu-id="f6f02-112">Allow a **member of hello business group** toospecify hello usernames and passwords assigned tooa user by using hello [Self-Service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) feature</span></span>

-   <span data-ttu-id="f6f02-113">Permitir que um **administrador** toospecify Olá os nomes de usuário e senhas atribuídas tooa usuário usando credenciais de atualização de saudação recurso quando [atribuindo um aplicativo de tooan do usuário](#assign-a-user-to-an-application-directly)</span><span class="sxs-lookup"><span data-stu-id="f6f02-113">Allow an **administrator** toospecify hello usernames and passwords assigned tooa user by using hello Update Credentials feature when [assigning a user tooan application](#assign-a-user-to-an-application-directly)</span></span>

-   <span data-ttu-id="f6f02-114">Permitir que um **administrador** toospecify Olá compartilhado nome do usuário ou senha usada por um grupo de pessoas, usando as credenciais de atualização de saudação recurso quando [atribuindo um aplicativo de tooan de grupo](#assign-an-application-to-a-group-directly)</span><span class="sxs-lookup"><span data-stu-id="f6f02-114">Allow an **administrator** toospecify hello shared username or password used by a group of people by using hello Update Credentials feature when [assigning a group tooan application](#assign-an-application-to-a-group-directly)</span></span>

<span data-ttu-id="f6f02-115">A seguir descreve como você pode habilitar [com base em senha de logon único](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) tooan aplicativo que já está em Olá [Galeria de aplicativos do Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="f6f02-115">Below describes how you can enable [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) tooan application that is already in hello [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="f6f02-116">Visão geral das etapas necessárias</span><span class="sxs-lookup"><span data-stu-id="f6f02-116">Overview of steps required</span></span>
<span data-ttu-id="f6f02-117">tooconfigure um aplicativo da Galeria do AD do Azure Olá você precisa:</span><span class="sxs-lookup"><span data-stu-id="f6f02-117">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="f6f02-118">Adicionar um aplicativo da Galeria do Azure AD Olá</span><span class="sxs-lookup"><span data-stu-id="f6f02-118">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="f6f02-119">Configurar o aplicativo hello de senha single sign-on</span><span class="sxs-lookup"><span data-stu-id="f6f02-119">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="f6f02-120">Atribuir um grupo ou usuário de tooa de aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="f6f02-120">Assign hello application tooa user or a group</span></span>](#assign-the-application-to-a-user-or-a-group)

    -   [<span data-ttu-id="f6f02-121">Atribuir um aplicativo do usuário tooan diretamente</span><span class="sxs-lookup"><span data-stu-id="f6f02-121">Assign a user tooan application directly</span></span>](#assign-a-user-to-an-application-directly)

    -   [<span data-ttu-id="f6f02-122">Atribuir um grupo de aplicativos tooa diretamente</span><span class="sxs-lookup"><span data-stu-id="f6f02-122">Assign an application tooa group directly</span></span>](#assign-an-application-to-a-group-directly)

## <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="f6f02-123">Adicionar um aplicativo da Galeria do Azure AD Olá</span><span class="sxs-lookup"><span data-stu-id="f6f02-123">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="f6f02-124">tooadd um aplicativo hello Galeria do AD do Azure, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="f6f02-124">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="f6f02-125">Olá abrir [Portal do Azure](https://portal.azure.com) e entre como um **Administrador Global** ou **Co-administrador**</span><span class="sxs-lookup"><span data-stu-id="f6f02-125">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="f6f02-126">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="f6f02-126">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f6f02-127">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="f6f02-127">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f6f02-128">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="f6f02-128">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="f6f02-129">Clique em Olá **adicionar** botão no canto superior direito Olá Olá **aplicativos empresariais** folha</span><span class="sxs-lookup"><span data-stu-id="f6f02-129">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="f6f02-130">Em Olá **Insira um nome** caixa de texto de saudação **adicionar da Galeria Olá** seção, digite o nome de saudação do aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="f6f02-130">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application</span></span>

7.  <span data-ttu-id="f6f02-131">Selecionar aplicativo hello desejar tooconfigure para logon único</span><span class="sxs-lookup"><span data-stu-id="f6f02-131">Select hello application you want tooconfigure for single sign-on</span></span>

8.  <span data-ttu-id="f6f02-132">Antes de adicionar o aplicativo hello, você pode alterar seu nome de saudação **nome** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="f6f02-132">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="f6f02-133">Clique em **adicionar** botão, o aplicativo de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="f6f02-133">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="f6f02-134">Após um curto período, você deve ser folha de configuração do aplicativo do toosee capaz de saudação.</span><span class="sxs-lookup"><span data-stu-id="f6f02-134">After a short period, you be able toosee hello application’s configuration blade.</span></span>

## <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="f6f02-135">Configurar o aplicativo hello de senha single sign-on</span><span class="sxs-lookup"><span data-stu-id="f6f02-135">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="f6f02-136">tooconfigure logon único para um aplicativo, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="f6f02-136">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="f6f02-137">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="f6f02-137">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="f6f02-138">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="f6f02-138">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f6f02-139">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="f6f02-139">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f6f02-140">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="f6f02-140">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="f6f02-141">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="f6f02-141">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="f6f02-142">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="f6f02-142">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="f6f02-143">Selecionar aplicativo hello deseja tooconfigure-logon único</span><span class="sxs-lookup"><span data-stu-id="f6f02-143">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="f6f02-144">Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="f6f02-144">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="f6f02-145">Modo de seleção Olá **com base em senha de logon.**</span><span class="sxs-lookup"><span data-stu-id="f6f02-145">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="f6f02-146">[Atribuir usuários toohello aplicativo](#assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="f6f02-146">[Assign users toohello application](#assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="f6f02-147">Além disso, você também pode fornecer credenciais em nome de usuário de saudação selecionar linhas de saudação de usuários hello e clicando em **credenciais de atualização** e inserindo Olá nome de usuário e senha em nome dos usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="f6f02-147">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="f6f02-148">Caso contrário, os usuários ser solicitadas tooenter Olá credenciais si mesmos após a inicialização.</span><span class="sxs-lookup"><span data-stu-id="f6f02-148">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="assign-a-user-tooan-application-directly"></a><span data-ttu-id="f6f02-149">Atribuir um aplicativo do usuário tooan diretamente</span><span class="sxs-lookup"><span data-stu-id="f6f02-149">Assign a user tooan application directly</span></span>

<span data-ttu-id="f6f02-150">tooassign um ou mais aplicativos de tooan usuários diretamente, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="f6f02-150">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="f6f02-151">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="f6f02-151">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="f6f02-152">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="f6f02-152">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f6f02-153">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="f6f02-153">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f6f02-154">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="f6f02-154">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="f6f02-155">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="f6f02-155">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="f6f02-156">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="f6f02-156">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="f6f02-157">Selecione o aplicativo hello deseja tooassign uma lista de saudação do usuário toofrom.</span><span class="sxs-lookup"><span data-stu-id="f6f02-157">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="f6f02-158">Depois que o aplicativo hello carrega, clique em **usuários e grupos** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="f6f02-158">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="f6f02-159">Clique Olá **adicionar** botão na parte superior Olá **usuários e grupos** Olá de tooopen lista **Adicionar atribuição** folha.</span><span class="sxs-lookup"><span data-stu-id="f6f02-159">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="f6f02-160">Clique em Olá **usuários e grupos** seletor de saudação **Adicionar atribuição** folha.</span><span class="sxs-lookup"><span data-stu-id="f6f02-160">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="f6f02-161">Tipo de saudação **nome completo** ou **endereço de email** do usuário Olá que lhe interessam atribuindo em Olá **pesquisar por nome ou endereço de email** caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="f6f02-161">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="f6f02-162">Passe o mouse sobre Olá **usuário** em Olá lista tooreveal um **caixa de seleção**.</span><span class="sxs-lookup"><span data-stu-id="f6f02-162">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="f6f02-163">Clique em tooadd de foto ou logotipo de perfil do Olá caixa de seleção próxima toohello usuário seu usuário toohello **selecionados** lista.</span><span class="sxs-lookup"><span data-stu-id="f6f02-163">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="f6f02-164">**Opcional:** se você gostaria que muito**adicionar mais de um usuário**, tipo em outro **nome completo** ou **endereço de email** em Olá **pesquisar por nome endereço de email ou** caixa de pesquisa e, em seguida, clique em tooadd de caixa de seleção Olá esse usuário toohello **selecionados** lista.</span><span class="sxs-lookup"><span data-stu-id="f6f02-164">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="f6f02-165">Quando você terminar de selecionar usuários, clique em Olá **selecione** botão tooadd-los toohello lista de usuários e grupos toobe atribuído toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f6f02-165">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="f6f02-166">**Opcional:** clique Olá **Selecionar função** seletor de saudação **Adicionar atribuição** folha tooselect uma função tooassign toohello usuários selecionados.</span><span class="sxs-lookup"><span data-stu-id="f6f02-166">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="f6f02-167">Clique em Olá **atribuir** botão tooassign Olá aplicativo toohello selecionado de usuários.</span><span class="sxs-lookup"><span data-stu-id="f6f02-167">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

## <a name="assign-an-application-tooa-group-directly"></a><span data-ttu-id="f6f02-168">Atribuir um grupo de aplicativos tooa diretamente</span><span class="sxs-lookup"><span data-stu-id="f6f02-168">Assign an application tooa group directly</span></span>

<span data-ttu-id="f6f02-169">tooassign um ou mais grupos de aplicativo tooan diretamente, siga Olá etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="f6f02-169">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="f6f02-170">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="f6f02-170">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="f6f02-171">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="f6f02-171">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f6f02-172">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="f6f02-172">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f6f02-173">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="f6f02-173">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="f6f02-174">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="f6f02-174">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="f6f02-175">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="f6f02-175">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="f6f02-176">Selecione o aplicativo hello deseja tooassign uma lista de saudação do usuário toofrom.</span><span class="sxs-lookup"><span data-stu-id="f6f02-176">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="f6f02-177">Depois que o aplicativo hello carrega, clique em **usuários e grupos** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="f6f02-177">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="f6f02-178">Clique Olá **adicionar** botão na parte superior Olá **usuários e grupos** Olá de tooopen lista **Adicionar atribuição** folha.</span><span class="sxs-lookup"><span data-stu-id="f6f02-178">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="f6f02-179">Clique em Olá **usuários e grupos** seletor de saudação **Adicionar atribuição** folha.</span><span class="sxs-lookup"><span data-stu-id="f6f02-179">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="f6f02-180">Tipo de saudação **nome completo do grupo** do grupo de saudação que lhe interessam atribuindo em Olá **pesquisar por nome ou endereço de email** caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="f6f02-180">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="f6f02-181">Passe o mouse sobre Olá **grupo** em Olá lista tooreveal um **caixa de seleção**.</span><span class="sxs-lookup"><span data-stu-id="f6f02-181">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="f6f02-182">Clique em tooadd de foto ou logotipo de perfil do Olá caixa de seleção próxima toohello grupo seu usuário toohello **selecionados** lista.</span><span class="sxs-lookup"><span data-stu-id="f6f02-182">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="f6f02-183">**Opcional:** se você gostaria que muito**adicionar mais de um grupo**, tipo em outro **nome completo do grupo** em Olá **pesquisar por nome ou endereço de email** caixa de pesquisa e clique em tooadd de caixa de seleção Olá esse grupo toohello **selecionados** lista.</span><span class="sxs-lookup"><span data-stu-id="f6f02-183">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="f6f02-184">Quando você terminar de selecionar os grupos, clique em Olá **selecione** botão tooadd-los toohello lista de usuários e grupos toobe atribuído toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f6f02-184">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="f6f02-185">**Opcional:** clique Olá **Selecionar função** seletor de saudação **Adicionar atribuição** folha tooselect toohello de tooassign uma função grupos selecionados.</span><span class="sxs-lookup"><span data-stu-id="f6f02-185">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="f6f02-186">Clique em Olá **atribuir** grupos selecionados do botão tooassign Olá aplicativo toohello.</span><span class="sxs-lookup"><span data-stu-id="f6f02-186">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="f6f02-187">Após um curto período, os usuários Olá que você selecionou ser capaz de toolaunch esses aplicativos em Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="f6f02-187">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6f02-188">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f6f02-188">Next steps</span></span>
[<span data-ttu-id="f6f02-189">Fornecer aplicativos de tooyour de logon único com o Proxy de aplicativo</span><span class="sxs-lookup"><span data-stu-id="f6f02-189">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
