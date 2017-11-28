---
title: "Tutorial: integração do Azure Active Directory ao Deputy | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e representante."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5665c3ac-5689-4201-80fe-fcc677d4430d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 42f65b758682ce2513b6bb38ef40a19f955c88c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-deputy"></a><span data-ttu-id="7659f-103">Tutorial: integração do Azure Active Directory ao Deputy</span><span class="sxs-lookup"><span data-stu-id="7659f-103">Tutorial: Azure Active Directory integration with Deputy</span></span>

<span data-ttu-id="7659f-104">Neste tutorial, você aprenderá como toointegrate representante com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="7659f-104">In this tutorial, you learn how toointegrate Deputy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7659f-105">Integrando o representante com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="7659f-105">Integrating Deputy with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7659f-106">Você pode controlar no AD do Azure que tenha acesso tooDeputy</span><span class="sxs-lookup"><span data-stu-id="7659f-106">You can control in Azure AD who has access tooDeputy</span></span>
- <span data-ttu-id="7659f-107">Você pode habilitar seu usuários tooautomatically get conectado tooDeputy (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7659f-107">You can enable your users tooautomatically get signed-on tooDeputy (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7659f-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7659f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7659f-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7659f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7659f-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7659f-110">Prerequisites</span></span>

<span data-ttu-id="7659f-111">tooconfigure integração do AD do Azure com o representante, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="7659f-111">tooconfigure Azure AD integration with Deputy, you need hello following items:</span></span>

- <span data-ttu-id="7659f-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7659f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7659f-113">Uma assinatura do Deputy habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="7659f-113">A Deputy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7659f-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="7659f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7659f-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="7659f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7659f-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="7659f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7659f-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7659f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7659f-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="7659f-118">Scenario description</span></span>
<span data-ttu-id="7659f-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="7659f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7659f-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="7659f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7659f-121">Adicionar representante da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="7659f-121">Adding Deputy from hello gallery</span></span>
2. <span data-ttu-id="7659f-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7659f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-deputy-from-hello-gallery"></a><span data-ttu-id="7659f-123">Adicionar representante da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="7659f-123">Adding Deputy from hello gallery</span></span>
<span data-ttu-id="7659f-124">integração de saudação tooconfigure do representante no AD do Azure, você precisa tooadd representante na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="7659f-124">tooconfigure hello integration of Deputy into Azure AD, you need tooadd Deputy from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7659f-125">**tooadd representante da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7659f-125">**tooadd Deputy from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7659f-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="7659f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7659f-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="7659f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7659f-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7659f-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="7659f-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7659f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="7659f-133">Na caixa de pesquisa hello, digite **representante**.</span><span class="sxs-lookup"><span data-stu-id="7659f-133">In hello search box, type **Deputy**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_search.png)

5. <span data-ttu-id="7659f-135">No painel de resultados de saudação, selecione **representante**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="7659f-135">In hello results panel, select **Deputy**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7659f-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7659f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7659f-138">Nesta seção, você configura e testa o logon único do Azure AD com o Deputy com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="7659f-138">In this section, you configure and test Azure AD single sign-on with Deputy based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7659f-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no representante é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="7659f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Deputy is tooa user in Azure AD.</span></span> <span data-ttu-id="7659f-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no representante precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="7659f-140">In other words, a link relationship between an Azure AD user and hello related user in Deputy needs toobe established.</span></span>

<span data-ttu-id="7659f-141">Substituto, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="7659f-141">In Deputy, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7659f-142">tooconfigure e teste de logon único do AD do Azure com o representante, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="7659f-142">tooconfigure and test Azure AD single sign-on with Deputy, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7659f-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="7659f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7659f-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7659f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7659f-145">**[Criar um usuário de teste de representante](#creating-a-deputy-test-user)**  -toohave um equivalente do Britta Simon no representante que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="7659f-145">**[Creating a Deputy test user](#creating-a-deputy-test-user)** - toohave a counterpart of Britta Simon in Deputy that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7659f-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="7659f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7659f-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="7659f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7659f-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7659f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7659f-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de representante.</span><span class="sxs-lookup"><span data-stu-id="7659f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Deputy application.</span></span>

<span data-ttu-id="7659f-150">**tooconfigure AD do Azure-logon único com substituto, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7659f-150">**tooconfigure Azure AD single sign-on with Deputy, perform hello following steps:**</span></span>

1. <span data-ttu-id="7659f-151">Em Olá portal do Azure, Olá **representante** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="7659f-151">In hello Azure portal, on hello **Deputy** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="7659f-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="7659f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_samlbase.png)

3. <span data-ttu-id="7659f-155">Em Olá **domínio representante e URLs** seção, se desejar que o aplicativo hello tooconfigure **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="7659f-155">On hello **Deputy Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url1.png)

    <span data-ttu-id="7659f-157">a.</span><span class="sxs-lookup"><span data-stu-id="7659f-157">a.</span></span> <span data-ttu-id="7659f-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="7659f-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    |  |
    | ----|
    | `https://<subdomain>.<region>.au.deputy.com` |
    | `https://<subdomain>.<region>.ent-au.deputy.com` |
    | `https://<subdomain>.<region>.na.deputy.com`|
    | `https://<subdomain>.<region>.ent-na.deputy.com`|
    | `https://<subdomain>.<region>.eu.deputy.com` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com` |
    | `https://<subdomain>.<region>.as.deputy.com` |
    | `https://<subdomain>.<region>.ent-as.deputy.com` |
    | `https://<subdomain>.<region>.la.deputy.com` |
    | `https://<subdomain>.<region>.ent-la.deputy.com` |
    | `https://<subdomain>.<region>.af.deputy.com` |
    | `https://<subdomain>.<region>.ent-af.deputy.com` |
    | `https://<subdomain>.<region>.an.deputy.com` |
    | `https://<subdomain>.<region>.ent-an.deputy.com` |
    | `https://<subdomain>.<region>.deputy.com` |

    <span data-ttu-id="7659f-159">b.</span><span class="sxs-lookup"><span data-stu-id="7659f-159">b.</span></span> <span data-ttu-id="7659f-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="7659f-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |----|
    | `https://<subdomain>.<region>.au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.deputy.com/exec/devapp/samlacs.` |

4. <span data-ttu-id="7659f-161">Marque **Mostrar configurações de URL avançadas**.</span><span class="sxs-lookup"><span data-stu-id="7659f-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="7659f-162">Se desejar que o aplicativo hello tooconfigure **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="7659f-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url2.png)

    <span data-ttu-id="7659f-164">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<your-subdomain>.<region>.deputy.com`</span><span class="sxs-lookup"><span data-stu-id="7659f-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<your-subdomain>.<region>.deputy.com`</span></span>
    
    >[!NOTE]
    > <span data-ttu-id="7659f-165">O sufixo de região do Deputy é opcional ou ele deve usar uma destas opções: au | na | eu |as |la |af |an |ent-au |ent-na |ent-eu |ent-as | ent-la | ent-af | ent-an</span><span class="sxs-lookup"><span data-stu-id="7659f-165">Deputy region suffix is optional, or it should use one of these: au | na | eu |as |la |af |an |ent-au |ent-na |ent-eu |ent-as | ent-la | ent-af | ent-an</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7659f-166">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="7659f-166">These values are not real.</span></span> <span data-ttu-id="7659f-167">Atualizar esses valores com hello real identificador, URL de resposta e URL de logon.</span><span class="sxs-lookup"><span data-stu-id="7659f-167">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="7659f-168">Entre em contato com [equipe de suporte de representante](https://www.deputy.com/call-centers-customer-support-scheduling-software) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="7659f-168">Contact [Deputy support team](https://www.deputy.com/call-centers-customer-support-scheduling-software) tooget these values.</span></span> 

5. <span data-ttu-id="7659f-169">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="7659f-169">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_certificate.png) 

6. <span data-ttu-id="7659f-171">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="7659f-171">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-deputy-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="7659f-173">Em Olá **representante configuração** seção, clique em **representante configurar** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="7659f-173">On hello **Deputy Configuration** section, click **Configure Deputy** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7659f-174">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="7659f-174">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_configure.png) 

8. <span data-ttu-id="7659f-176">Navegue toohello URL a seguir:[https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config).</span><span class="sxs-lookup"><span data-stu-id="7659f-176">Navigate toohello following URL:[https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config).</span></span> <span data-ttu-id="7659f-177">Vá muito**as configurações de segurança** e clique em **editar**.</span><span class="sxs-lookup"><span data-stu-id="7659f-177">Go too**Security Settings** and click **Edit**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_004.png)

9. <span data-ttu-id="7659f-179">Na página **Configurações de Segurança** , execute etapas abaixo.</span><span class="sxs-lookup"><span data-stu-id="7659f-179">On this **Security Settings** page, perform below steps.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_005.png)
    
    <span data-ttu-id="7659f-181">a.</span><span class="sxs-lookup"><span data-stu-id="7659f-181">a.</span></span> <span data-ttu-id="7659f-182">Habilite o **Logon Social**.</span><span class="sxs-lookup"><span data-stu-id="7659f-182">Enable **Social Login**.</span></span>
   
    <span data-ttu-id="7659f-183">b.</span><span class="sxs-lookup"><span data-stu-id="7659f-183">b.</span></span> <span data-ttu-id="7659f-184">Abra seu certificado codificado na Base64 que baixou do portal do Azure no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado OpenSSL** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="7659f-184">Open your Base64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **OpenSSL Certificate** textbox.</span></span>
   
    <span data-ttu-id="7659f-185">c.</span><span class="sxs-lookup"><span data-stu-id="7659f-185">c.</span></span> <span data-ttu-id="7659f-186">Na caixa de texto de URL SSO SAML Olá, digite`https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span><span class="sxs-lookup"><span data-stu-id="7659f-186">In hello SAML SSO URL textbox, type `https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span></span>
    
    <span data-ttu-id="7659f-187">d.</span><span class="sxs-lookup"><span data-stu-id="7659f-187">d.</span></span> <span data-ttu-id="7659f-188">Na caixa de texto de URL SSO SAML Olá, substitua `<your subdomain>` com seu subdomínio.</span><span class="sxs-lookup"><span data-stu-id="7659f-188">In hello SAML SSO URL textbox, replace `<your subdomain>` with your subdomain.</span></span>
   
    <span data-ttu-id="7659f-189">e.</span><span class="sxs-lookup"><span data-stu-id="7659f-189">e.</span></span> <span data-ttu-id="7659f-190">Na caixa de texto de URL SSO SAML Olá, substitua `<saml sso url>` com hello **Single Sign-On URL do serviço SAML** você copiou da saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7659f-190">In hello SAML SSO URL textbox, replace `<saml sso url>` with hello **SAML Single Sign-On Service URL** you have copied from hello Azure portal.</span></span>
   
    <span data-ttu-id="7659f-191">f.</span><span class="sxs-lookup"><span data-stu-id="7659f-191">f.</span></span> <span data-ttu-id="7659f-192">Clique em **Salvar Configurações**.</span><span class="sxs-lookup"><span data-stu-id="7659f-192">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="7659f-193">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="7659f-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7659f-194">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="7659f-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7659f-195">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7659f-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7659f-196">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7659f-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="7659f-197">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7659f-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="7659f-199">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7659f-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7659f-200">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="7659f-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-deputy-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7659f-202">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="7659f-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-deputy-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7659f-204">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="7659f-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-deputy-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7659f-206">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7659f-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-deputy-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7659f-208">a.</span><span class="sxs-lookup"><span data-stu-id="7659f-208">a.</span></span> <span data-ttu-id="7659f-209">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7659f-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7659f-210">b.</span><span class="sxs-lookup"><span data-stu-id="7659f-210">b.</span></span> <span data-ttu-id="7659f-211">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7659f-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7659f-212">c.</span><span class="sxs-lookup"><span data-stu-id="7659f-212">c.</span></span> <span data-ttu-id="7659f-213">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="7659f-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7659f-214">d.</span><span class="sxs-lookup"><span data-stu-id="7659f-214">d.</span></span> <span data-ttu-id="7659f-215">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="7659f-215">Click **Create**.</span></span>
 
### <a name="creating-a-deputy-test-user"></a><span data-ttu-id="7659f-216">Criando um usuário de teste do Deputy</span><span class="sxs-lookup"><span data-stu-id="7659f-216">Creating a Deputy test user</span></span>

<span data-ttu-id="7659f-217">tooenable AD do Azure usuários toolog em tooDeputy, eles devem ser provisionados no representante.</span><span class="sxs-lookup"><span data-stu-id="7659f-217">tooenable Azure AD users toolog in tooDeputy, they must be provisioned into Deputy.</span></span> <span data-ttu-id="7659f-218">No caso do Deputy, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="7659f-218">In case of Deputy, provisioning is a manual task.</span></span>

#### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="7659f-219">tooprovision uma conta de usuário, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7659f-219">tooprovision a user account, perform hello following steps:</span></span>
1. <span data-ttu-id="7659f-220">Faça logon no site da empresa tooyour representante como um administrador.</span><span class="sxs-lookup"><span data-stu-id="7659f-220">Log in tooyour Deputy company site as an administrator.</span></span>

2. <span data-ttu-id="7659f-221">No painel de navegação superior hello, clique em **pessoas**.</span><span class="sxs-lookup"><span data-stu-id="7659f-221">On hello top navigation pane, click **People**.</span></span>
   
   <span data-ttu-id="7659f-222">![Pessoas](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "Pessoas")</span><span class="sxs-lookup"><span data-stu-id="7659f-222">![People](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "People")</span></span>

3. <span data-ttu-id="7659f-223">Clique em Olá **adicionar pessoas** botão e clique em **adicionar uma única pessoa**.</span><span class="sxs-lookup"><span data-stu-id="7659f-223">Click hello **Add People** button and click **Add a single person**.</span></span>
   
   <span data-ttu-id="7659f-224">![Adicionar Pessoas](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "Adicionar Pessoas")</span><span class="sxs-lookup"><span data-stu-id="7659f-224">![Add People](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "Add People")</span></span>

4. <span data-ttu-id="7659f-225">Execute Olá etapas a seguir e clique em **salvar e convidar**.</span><span class="sxs-lookup"><span data-stu-id="7659f-225">Perform hello following steps and click **Save & Invite**.</span></span>
   
   <span data-ttu-id="7659f-226">![Novo Usuário](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "Novo Usuário")</span><span class="sxs-lookup"><span data-stu-id="7659f-226">![New User](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "New User")</span></span>

   <span data-ttu-id="7659f-227">a.</span><span class="sxs-lookup"><span data-stu-id="7659f-227">a.</span></span> <span data-ttu-id="7659f-228">Em Olá **nome** caixa de texto Nome do tipo de usuário hello como **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7659f-228">In hello **Name** textbox, type name of hello user like **BrittaSimon**.</span></span>
   
   <span data-ttu-id="7659f-229">b.</span><span class="sxs-lookup"><span data-stu-id="7659f-229">b.</span></span> <span data-ttu-id="7659f-230">Em Olá **Email** caixa de texto, endereço de email de saudação do tipo de uma conta do AD do Azure você deseja tooprovision.</span><span class="sxs-lookup"><span data-stu-id="7659f-230">In hello **Email** textbox, type hello email address of an Azure AD account you want tooprovision.</span></span>
   
   <span data-ttu-id="7659f-231">c.</span><span class="sxs-lookup"><span data-stu-id="7659f-231">c.</span></span> <span data-ttu-id="7659f-232">Em Olá **trabalhar em** caixa de texto Nome do tipo hello comercial.</span><span class="sxs-lookup"><span data-stu-id="7659f-232">In hello **Work at** textbox, type hello business name.</span></span>
   
   <span data-ttu-id="7659f-233">d.</span><span class="sxs-lookup"><span data-stu-id="7659f-233">d.</span></span> <span data-ttu-id="7659f-234">Clique no botão **Salvar e Convidar**.</span><span class="sxs-lookup"><span data-stu-id="7659f-234">Click **Save & Invite** button.</span></span>

5. <span data-ttu-id="7659f-235">proprietário de conta do AAD Olá recebe um email e segue um link tooconfirm sua conta antes de se tornar ativa.</span><span class="sxs-lookup"><span data-stu-id="7659f-235">hello AAD account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span> <span data-ttu-id="7659f-236">Você pode usar qualquer ferramenta de criação outros representante usuário conta ou APIs fornecidas pelo representante tooprovision AAD contas de usuário.</span><span class="sxs-lookup"><span data-stu-id="7659f-236">You can use any other Deputy user account creation tools or APIs provided by Deputy tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7659f-237">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7659f-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7659f-238">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooDeputy.</span><span class="sxs-lookup"><span data-stu-id="7659f-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDeputy.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="7659f-240">**tooassign Britta Simon tooDeputy, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7659f-240">**tooassign Britta Simon tooDeputy, perform hello following steps:**</span></span>

1. <span data-ttu-id="7659f-241">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7659f-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="7659f-243">Na lista de aplicativos hello, selecione **representante**.</span><span class="sxs-lookup"><span data-stu-id="7659f-243">In hello applications list, select **Deputy**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_app.png) 

3. <span data-ttu-id="7659f-245">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="7659f-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="7659f-247">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="7659f-247">Click **Add** button.</span></span> <span data-ttu-id="7659f-248">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7659f-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="7659f-250">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="7659f-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7659f-251">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7659f-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7659f-252">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7659f-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7659f-253">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="7659f-253">Testing single sign-on</span></span>

<span data-ttu-id="7659f-254">Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="7659f-254">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="7659f-255">Quando você clica em Olá representante bloco no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo de representante.</span><span class="sxs-lookup"><span data-stu-id="7659f-255">When you click hello Deputy tile in hello Access Panel, you should get automatically signed-on tooyour Deputy application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7659f-256">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="7659f-256">Additional resources</span></span>

* [<span data-ttu-id="7659f-257">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="7659f-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7659f-258">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7659f-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_203.png

