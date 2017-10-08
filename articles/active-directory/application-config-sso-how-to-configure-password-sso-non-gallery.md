---
title: "aaaHow tooconfigure senha single sign-on para uma galeria não applicationn | Microsoft Docs"
description: "Como tooconfigure um aplicativo não Galeria personalizado para proteger com base em senha de logon único quando ele não estiver listado na Olá Galeria de aplicativos do Azure AD"
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
ms.openlocfilehash: e3d0e658f792a0a63110a198811edc66acd6ccf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="719f4-103">Como senha tooconfigure o logon único para um aplicativo não Galeria</span><span class="sxs-lookup"><span data-stu-id="719f4-103">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="719f4-104">Além disso toohello opções encontrado na Galeria de aplicativos de saudação do AD do Azure, você também tem Olá opção tooadd um **aplicativo Galeria não** ao aplicativo hello desejado não estiver listado.</span><span class="sxs-lookup"><span data-stu-id="719f4-104">In addition toohello choices found within hello Azure AD Application Gallery, you also have hello option tooadd a **non-gallery application** when hello application you want is not listed there.</span></span> <span data-ttu-id="719f4-105">Usando esse recurso, você pode adicionar qualquer aplicativo que já existe em sua organização, ou qualquer aplicativo de terceiros que você pode usar de um fornecedor que não ainda faz parte do hello [Galeria de aplicativos do Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="719f4-105">Using this capability, you can add any application that already exists in your organization, or any third-party application that you might use from a vendor who is not already part of hello [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span></span>

<span data-ttu-id="719f4-106">Quando você adicionar um aplicativo não galeria, você pode configurar Olá único método de logon usa este aplicativo, selecionando Olá **Single Sign-on** item de navegação em um aplicativo corporativo em Olá [Portal do Azure ](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="719f4-106">Once you add a non-gallery application, you can then configure hello Single sign-on method this application uses by selecting hello **Single Sign-on** navigation item on an Enterprise Application in hello [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="719f4-107">Uma saudação SSO métodos disponível tooyou é hello [com base em senha de logon único](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) opção.</span><span class="sxs-lookup"><span data-stu-id="719f4-107">One of hello Single Sign-on methods available tooyou is hello [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span></span> <span data-ttu-id="719f4-108">Com hello **adicionar um aplicativo da Galeria não** experiência, você pode integrar qualquer aplicativo que processa um nome de usuário com base em HTML e a senha de entrada campo, mesmo se ele não está em nosso conjunto de aplicativos pré-integrados.</span><span class="sxs-lookup"><span data-stu-id="719f4-108">With hello **add a non-gallery application** experience, you can integrate any application that renders an HTML-based username and password input field, even if it is not in our set of pre-integrated applications.</span></span>

<span data-ttu-id="719f4-109">Olá acontece é por uma página de captura de tecnologia que faz parte da saudação extensão do painel de acesso que nos permite tooauto-detectar os campos de entrada de nome de usuário e senha, armazená-las com segurança para a instância do aplicativo específico.</span><span class="sxs-lookup"><span data-stu-id="719f4-109">hello way this works is by a page scraping technology that is part of hello Access Panel extension that allows us tooauto-detect username and password input fields, store them securely for your specific application instance.</span></span> <span data-ttu-id="719f4-110">Em seguida, repetir com segurança os nomes de usuário e campos de toothose senhas quando um usuário navega toothat aplicativo no painel de acesso do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="719f4-110">Then securely replay usernames and passwords toothose fields when a user navigates toothat application on hello application access panel.</span></span>

<span data-ttu-id="719f4-111">Isso é uma ótima maneira tooget iniciado a integração de qualquer tipo de aplicativo ao AD do Azure rapidamente e permite que você:</span><span class="sxs-lookup"><span data-stu-id="719f4-111">This is a great way tooget started integrating any kind of application into Azure AD quickly, and allows you to:</span></span>

-   <span data-ttu-id="719f4-112">Integrar **qualquer aplicativo em Olá, mundo** com seu locatário de AD do Azure, contanto que ele renderiza um campo de chamadas entrada de usuário e senha HTML</span><span class="sxs-lookup"><span data-stu-id="719f4-112">Integrate **any application in hello world** with your Azure AD tenant, so long as it renders an HTML username and password input field</span></span>

-   <span data-ttu-id="719f4-113">Habilitar **logon único para seus usuários** armazenando com segurança e repetição de nomes de usuário e senhas para o aplicativo hello integrado com o Azure AD</span><span class="sxs-lookup"><span data-stu-id="719f4-113">Enable **Single Sign-on for your users** by securely storing and replaying usernames and passwords for hello application you’ve integrated with Azure AD</span></span>

-   <span data-ttu-id="719f4-114">**Detecção automática de entrada** campos para qualquer aplicativo e permitem que você toomanually detectar esses campos usando Olá extensão de navegador do painel de acesso, no caso de detecção automática não encontrá-los</span><span class="sxs-lookup"><span data-stu-id="719f4-114">**Auto-detect input** fields for any application and allow you toomanually detect those fields using hello Access Panel Browser Extension, in case auto-detection does not find them</span></span>

-   <span data-ttu-id="719f4-115">**Suporte a aplicativos que exigem vários campos de entrada** para aplicativos que exigem o nome de usuário e senha mais do que apenas toosign campos em</span><span class="sxs-lookup"><span data-stu-id="719f4-115">**Support applications that require multiple sign-in fields** for applications that require more than just username and password fields toosign in</span></span>

-   <span data-ttu-id="719f4-116">**Personalizar rótulos Olá** dos campos de entrada de usuário e senha Olá os usuários vejam no hello [painel de acesso do aplicativo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) quando eles digitem suas credenciais</span><span class="sxs-lookup"><span data-stu-id="719f4-116">**Customize hello labels** of hello username and password input fields your users see on hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) when they enter their credentials</span></span>

-   <span data-ttu-id="719f4-117">Permitir que seu **usuários** tooprovide seus próprios nomes de usuário e senhas para contas de aplicativo existente que estão digitando no manualmente no hello [painel de acesso do aplicativo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span><span class="sxs-lookup"><span data-stu-id="719f4-117">Allow your **users** tooprovide their own usernames and passwords for any existing application accounts they are typing in manually on hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span></span>

-   <span data-ttu-id="719f4-118">Permitir que um **membro do grupo de negócios Olá** toospecify Olá os nomes de usuário e senhas atribuídas tooa usuário usando Olá [autoatendimento acesso ao aplicativo](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) recurso</span><span class="sxs-lookup"><span data-stu-id="719f4-118">Allow a **member of hello business group** toospecify hello usernames and passwords assigned tooa user by using hello [Self-Service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) feature</span></span>

-   <span data-ttu-id="719f4-119">Permitir que um **administrador** toospecify Olá os nomes de usuário e senhas atribuídas tooa usuário usando credenciais de atualização de saudação recurso quando [atribuindo um aplicativo de tooan do usuário](#_How_to_configure_1)</span><span class="sxs-lookup"><span data-stu-id="719f4-119">Allow an **administrator** toospecify hello usernames and passwords assigned tooa user by using hello Update Credentials feature when [assigning a user tooan application](#_How_to_configure_1)</span></span>

-   <span data-ttu-id="719f4-120">Permitir que um **administrador** toospecify Olá compartilhado nome do usuário ou senha usada por um grupo de pessoas, usando as credenciais de atualização de saudação recurso quando [atribuindo um aplicativo de tooan de grupo](#assign-an-application-to-a-group-directly)</span><span class="sxs-lookup"><span data-stu-id="719f4-120">Allow an **administrator** toospecify hello shared username or password used by a group of people by using hello Update Credentials feature when [assigning a group tooan application](#assign-an-application-to-a-group-directly)</span></span>

<span data-ttu-id="719f4-121">A seguir descreve como você pode habilitar [com base em senha de logon único](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) tooany aplicativo que você adicione usando Olá **adicionar um aplicativo da Galeria não** experiência.</span><span class="sxs-lookup"><span data-stu-id="719f4-121">Below describes how you can enable [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) tooany application that you add using hello **add a non-gallery application** experience.</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="719f4-122">Visão geral das etapas necessárias</span><span class="sxs-lookup"><span data-stu-id="719f4-122">Overview of steps required</span></span>

<span data-ttu-id="719f4-123">tooconfigure um aplicativo da Galeria do AD do Azure Olá você precisa:</span><span class="sxs-lookup"><span data-stu-id="719f4-123">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="719f4-124">Adicionar um aplicativo inexistente na galeria</span><span class="sxs-lookup"><span data-stu-id="719f4-124">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="719f4-125">Configurar o aplicativo hello de senha single sign-on</span><span class="sxs-lookup"><span data-stu-id="719f4-125">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="719f4-126">Atribuir um grupo ou usuário de tooa de aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="719f4-126">Assign hello application tooa user or a group</span></span>](#assign-the-application-to-a-user-or-a-group)

    -   [<span data-ttu-id="719f4-127">Atribuir um aplicativo do usuário tooan diretamente</span><span class="sxs-lookup"><span data-stu-id="719f4-127">Assign a user tooan application directly</span></span>](#assign-a-user-to-an-application-directly)

    -   [<span data-ttu-id="719f4-128">Atribuir um grupo de aplicativos tooa diretamente</span><span class="sxs-lookup"><span data-stu-id="719f4-128">Assign an application tooa group directly</span></span>](#assign-an-application-to-a-group-directly)

## <a name="add-a-non-gallery-application"></a><span data-ttu-id="719f4-129">Adicionar um aplicativo inexistente na galeria</span><span class="sxs-lookup"><span data-stu-id="719f4-129">Add a non-gallery application</span></span>

<span data-ttu-id="719f4-130">tooadd um aplicativo hello Galeria do AD do Azure, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="719f4-130">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="719f4-131">Olá abrir [Portal do Azure](https://portal.azure.com) e entre como um **Administrador Global** ou **Co-administrador**</span><span class="sxs-lookup"><span data-stu-id="719f4-131">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="719f4-132">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="719f4-132">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="719f4-133">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="719f4-133">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="719f4-134">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="719f4-134">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="719f4-135">Clique em Olá **adicionar** botão no canto superior direito Olá Olá **aplicativos empresariais** folha</span><span class="sxs-lookup"><span data-stu-id="719f4-135">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="719f4-136">clique em **Aplicativo inexistente na galeria.**</span><span class="sxs-lookup"><span data-stu-id="719f4-136">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="719f4-137">Insira o nome de saudação do seu aplicativo em Olá **nome** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="719f4-137">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="719f4-138">Selecione **Adicionar.**</span><span class="sxs-lookup"><span data-stu-id="719f4-138">Select **Add.**</span></span>

<span data-ttu-id="719f4-139">Após um curto período, você deve ser folha de configuração do aplicativo do toosee capaz de saudação.</span><span class="sxs-lookup"><span data-stu-id="719f4-139">After a short period, you be able toosee hello application’s configuration blade.</span></span>

## <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="719f4-140">Configurar o aplicativo hello de senha single sign-on</span><span class="sxs-lookup"><span data-stu-id="719f4-140">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="719f4-141">tooconfigure logon único para um aplicativo, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="719f4-141">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="719f4-142">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="719f4-142">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="719f4-143">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="719f4-143">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="719f4-144">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="719f4-144">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="719f4-145">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="719f4-145">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="719f4-146">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="719f4-146">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="719f4-147">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="719f4-147">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="719f4-148">Selecione aplicativo hello deseja tooconfigure-logon único.</span><span class="sxs-lookup"><span data-stu-id="719f4-148">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="719f4-149">Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="719f4-149">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="719f4-150">Modo de seleção Olá **com base em senha de logon.**</span><span class="sxs-lookup"><span data-stu-id="719f4-150">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="719f4-151">Digite hello **URL de logon**.</span><span class="sxs-lookup"><span data-stu-id="719f4-151">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="719f4-152">Isso é Olá URL onde os usuários digitarão seu nome de usuário e senha toosign em para.</span><span class="sxs-lookup"><span data-stu-id="719f4-152">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="719f4-153">Certifique-se de campos de entrada hello são visíveis na URL de saudação.</span><span class="sxs-lookup"><span data-stu-id="719f4-153">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="719f4-154">Atribua usuários toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="719f4-154">Assign users toohello application.</span></span>

11. <span data-ttu-id="719f4-155">Além disso, você também pode fornecer credenciais em nome de usuário de saudação selecionar linhas de saudação de usuários hello e clicando em **credenciais de atualização** e inserindo Olá nome de usuário e senha em nome dos usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="719f4-155">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="719f4-156">Caso contrário, os usuários ser solicitadas tooenter Olá credenciais si mesmos após a inicialização.</span><span class="sxs-lookup"><span data-stu-id="719f4-156">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="assign-a-user-tooan-application-directly"></a><span data-ttu-id="719f4-157">Atribuir um aplicativo do usuário tooan diretamente</span><span class="sxs-lookup"><span data-stu-id="719f4-157">Assign a user tooan application directly</span></span>

<span data-ttu-id="719f4-158">tooassign um ou mais aplicativos de tooan usuários diretamente, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="719f4-158">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="719f4-159">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="719f4-159">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="719f4-160">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="719f4-160">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="719f4-161">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="719f4-161">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="719f4-162">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="719f4-162">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="719f4-163">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="719f4-163">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="719f4-164">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="719f4-164">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="719f4-165">Selecione o aplicativo hello deseja tooassign uma lista de saudação do usuário toofrom.</span><span class="sxs-lookup"><span data-stu-id="719f4-165">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="719f4-166">Depois que o aplicativo hello carrega, clique em **usuários e grupos** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="719f4-166">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="719f4-167">Clique Olá **adicionar** botão na parte superior Olá **usuários e grupos** Olá de tooopen lista **Adicionar atribuição** folha.</span><span class="sxs-lookup"><span data-stu-id="719f4-167">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="719f4-168">Clique em Olá **usuários e grupos** seletor de saudação **Adicionar atribuição** folha.</span><span class="sxs-lookup"><span data-stu-id="719f4-168">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="719f4-169">Tipo de saudação **nome completo** ou **endereço de email** do usuário Olá que lhe interessam atribuindo em Olá **pesquisar por nome ou endereço de email** caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="719f4-169">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="719f4-170">Passe o mouse sobre Olá **usuário** em Olá lista tooreveal um **caixa de seleção**.</span><span class="sxs-lookup"><span data-stu-id="719f4-170">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="719f4-171">Clique em tooadd de foto ou logotipo de perfil do Olá caixa de seleção próxima toohello usuário seu usuário toohello **selecionados** lista.</span><span class="sxs-lookup"><span data-stu-id="719f4-171">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="719f4-172">**Opcional:** se você gostaria que muito**adicionar mais de um usuário**, tipo em outro **nome completo** ou **endereço de email** em Olá **pesquisar por nome endereço de email ou** caixa de pesquisa e, em seguida, clique em tooadd de caixa de seleção Olá esse usuário toohello **selecionados** lista.</span><span class="sxs-lookup"><span data-stu-id="719f4-172">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="719f4-173">Quando você terminar de selecionar usuários, clique em Olá **selecione** botão tooadd-los toohello lista de usuários e grupos toobe atribuído toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="719f4-173">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="719f4-174">**Opcional:** clique Olá **Selecionar função** seletor de saudação **Adicionar atribuição** folha tooselect uma função tooassign toohello usuários selecionados.</span><span class="sxs-lookup"><span data-stu-id="719f4-174">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="719f4-175">Clique em Olá **atribuir** botão tooassign Olá aplicativo toohello selecionado de usuários.</span><span class="sxs-lookup"><span data-stu-id="719f4-175">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

## <a name="assign-an-application-tooa-group-directly"></a><span data-ttu-id="719f4-176">Atribuir um grupo de aplicativos tooa diretamente</span><span class="sxs-lookup"><span data-stu-id="719f4-176">Assign an application tooa group directly</span></span>

<span data-ttu-id="719f4-177">tooassign um ou mais grupos de aplicativo tooan diretamente, siga Olá etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="719f4-177">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="719f4-178">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="719f4-178">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="719f4-179">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="719f4-179">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="719f4-180">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="719f4-180">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="719f4-181">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="719f4-181">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="719f4-182">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="719f4-182">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="719f4-183">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="719f4-183">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="719f4-184">Selecione o aplicativo hello deseja tooassign uma lista de saudação do usuário toofrom.</span><span class="sxs-lookup"><span data-stu-id="719f4-184">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="719f4-185">Depois que o aplicativo hello carrega, clique em **usuários e grupos** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="719f4-185">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="719f4-186">Clique Olá **adicionar** botão na parte superior Olá **usuários e grupos** Olá de tooopen lista **Adicionar atribuição** folha.</span><span class="sxs-lookup"><span data-stu-id="719f4-186">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="719f4-187">Clique em Olá **usuários e grupos** seletor de saudação **Adicionar atribuição** folha.</span><span class="sxs-lookup"><span data-stu-id="719f4-187">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="719f4-188">Tipo de saudação **nome completo do grupo** do grupo de saudação que lhe interessam atribuindo em Olá **pesquisar por nome ou endereço de email** caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="719f4-188">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="719f4-189">Passe o mouse sobre Olá **grupo** em Olá lista tooreveal um **caixa de seleção**.</span><span class="sxs-lookup"><span data-stu-id="719f4-189">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="719f4-190">Clique em tooadd de foto ou logotipo de perfil do Olá caixa de seleção próxima toohello grupo seu usuário toohello **selecionados** lista.</span><span class="sxs-lookup"><span data-stu-id="719f4-190">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="719f4-191">**Opcional:** se você gostaria que muito**adicionar mais de um grupo**, tipo em outro **nome completo do grupo** em Olá **pesquisar por nome ou endereço de email** caixa de pesquisa e clique em tooadd de caixa de seleção Olá esse grupo toohello **selecionados** lista.</span><span class="sxs-lookup"><span data-stu-id="719f4-191">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="719f4-192">Quando você terminar de selecionar os grupos, clique em Olá **selecione** botão tooadd-los toohello lista de usuários e grupos toobe atribuído toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="719f4-192">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="719f4-193">**Opcional:** clique Olá **Selecionar função** seletor de saudação **Adicionar atribuição** folha tooselect toohello de tooassign uma função grupos selecionados.</span><span class="sxs-lookup"><span data-stu-id="719f4-193">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="719f4-194">Clique em Olá **atribuir** grupos selecionados do botão tooassign Olá aplicativo toohello.</span><span class="sxs-lookup"><span data-stu-id="719f4-194">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="719f4-195">Após um curto período, os usuários Olá que você selecionou ser capaz de toolaunch esses aplicativos em Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="719f4-195">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="719f4-196">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="719f4-196">Next steps</span></span>
[<span data-ttu-id="719f4-197">Fornecer aplicativos de tooyour de logon único com o Proxy de aplicativo</span><span class="sxs-lookup"><span data-stu-id="719f4-197">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
