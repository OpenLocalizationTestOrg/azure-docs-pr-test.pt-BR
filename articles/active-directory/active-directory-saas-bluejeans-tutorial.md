---
title: "Tutorial: integração do Azure Active Directory com o BlueJeans | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure com BlueJeans."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dfc634fd-1b55-4ba8-94a8-b8288429b6a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: jeedes
ms.openlocfilehash: 67613303a9f854afbf4619418cc1607d329caf94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bluejeans"></a><span data-ttu-id="f2ae3-103">Tutorial: Integração do Azure Active Directory ao BlueJeans</span><span class="sxs-lookup"><span data-stu-id="f2ae3-103">Tutorial: Azure Active Directory integration with BlueJeans</span></span>

<span data-ttu-id="f2ae3-104">Neste tutorial, você aprenderá como toointegrate BlueJeans com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="f2ae3-104">In this tutorial, you learn how toointegrate BlueJeans with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f2ae3-105">Integrando BlueJeans com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2ae3-105">Integrating BlueJeans with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f2ae3-106">Você pode controlar no AD do Azure que tenha acesso tooBlueJeans</span><span class="sxs-lookup"><span data-stu-id="f2ae3-106">You can control in Azure AD who has access tooBlueJeans</span></span>
- <span data-ttu-id="f2ae3-107">Você pode habilitar seus usuários tooautomatically get conectado tooBlueJeans (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f2ae3-107">You can enable your users tooautomatically get signed-on tooBlueJeans (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f2ae3-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f2ae3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f2ae3-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f2ae3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f2ae3-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f2ae3-110">Prerequisites</span></span>

<span data-ttu-id="f2ae3-111">tooconfigure integração do AD do Azure com BlueJeans, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2ae3-111">tooconfigure Azure AD integration with BlueJeans, you need hello following items:</span></span>

- <span data-ttu-id="f2ae3-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f2ae3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f2ae3-113">Uma assinatura habilitada para logon único do BlueJeans</span><span class="sxs-lookup"><span data-stu-id="f2ae3-113">A BlueJeans single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f2ae3-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f2ae3-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="f2ae3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f2ae3-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f2ae3-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f2ae3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f2ae3-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="f2ae3-118">Scenario description</span></span>
<span data-ttu-id="f2ae3-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f2ae3-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="f2ae3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f2ae3-121">Adicionando BlueJeans da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="f2ae3-121">Adding BlueJeans from hello gallery</span></span>
2. <span data-ttu-id="f2ae3-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f2ae3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bluejeans-from-hello-gallery"></a><span data-ttu-id="f2ae3-123">Adicionando BlueJeans da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="f2ae3-123">Adding BlueJeans from hello gallery</span></span>
<span data-ttu-id="f2ae3-124">integração de saudação tooconfigure do BlueJeans no AD do Azure, você precisa tooadd BlueJeans da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-124">tooconfigure hello integration of BlueJeans into Azure AD, you need tooadd BlueJeans from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f2ae3-125">**tooadd BlueJeans da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f2ae3-125">**tooadd BlueJeans from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f2ae3-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f2ae3-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f2ae3-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="f2ae3-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="f2ae3-133">Na caixa de pesquisa hello, digite **BlueJeans**.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-133">In hello search box, type **BlueJeans**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_search.png)

5. <span data-ttu-id="f2ae3-135">No painel de resultados de saudação, selecione **BlueJeans**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-135">In hello results panel, select **BlueJeans**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f2ae3-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f2ae3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f2ae3-138">Nesta seção, você configura e testa o logon único do Azure AD com o BlueJeans, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-138">In this section, you configure and test Azure AD single sign-on with BlueJeans based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f2ae3-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no BlueJeans é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BlueJeans is tooa user in Azure AD.</span></span> <span data-ttu-id="f2ae3-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no BlueJeans precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-140">In other words, a link relationship between an Azure AD user and hello related user in BlueJeans needs toobe established.</span></span>

<span data-ttu-id="f2ae3-141">No BlueJeans, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-141">In BlueJeans, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f2ae3-142">tooconfigure e teste de logon único do AD do Azure com BlueJeans, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2ae3-142">tooconfigure and test Azure AD single sign-on with BlueJeans, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f2ae3-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f2ae3-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f2ae3-145">**[Criar um usuário de teste do BlueJeans](#creating-a-bluejeans-test-user)**  -toohave um equivalente do Britta Simon no BlueJeans que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-145">**[Creating a BlueJeans test user](#creating-a-bluejeans-test-user)** - toohave a counterpart of Britta Simon in BlueJeans that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f2ae3-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f2ae3-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f2ae3-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f2ae3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f2ae3-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BlueJeans application.</span></span>

<span data-ttu-id="f2ae3-150">**tooconfigure AD do Azure-logon único com BlueJeans, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f2ae3-150">**tooconfigure Azure AD single sign-on with BlueJeans, perform hello following steps:**</span></span>

1. <span data-ttu-id="f2ae3-151">Em Olá portal do Azure, Olá **BlueJeans** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-151">In hello Azure portal, on hello **BlueJeans** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="f2ae3-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_samlbase.png)

3. <span data-ttu-id="f2ae3-155">Em Olá **BlueJeans domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2ae3-155">On hello **BlueJeans Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_url.png)

    <span data-ttu-id="f2ae3-157">a.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-157">a.</span></span> <span data-ttu-id="f2ae3-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.BlueJeans.com`</span><span class="sxs-lookup"><span data-stu-id="f2ae3-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.BlueJeans.com`</span></span>

    <span data-ttu-id="f2ae3-159">b.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-159">b.</span></span> <span data-ttu-id="f2ae3-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.BlueJeans.com`</span><span class="sxs-lookup"><span data-stu-id="f2ae3-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.BlueJeans.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f2ae3-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-161">These values are not real.</span></span> <span data-ttu-id="f2ae3-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f2ae3-163">Entre em contato com [equipe de suporte do cliente BlueJeans](https://support.bluejeans.com/contact) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-163">Contact [BlueJeans Client support team](https://support.bluejeans.com/contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="f2ae3-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_certificate.png) 

5. <span data-ttu-id="f2ae3-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="f2ae3-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bluejeans-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f2ae3-168">Em Olá **BlueJeans configuração** seção, clique em **configurar BlueJeans** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-168">On hello **BlueJeans Configuration** section, click **Configure BlueJeans** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f2ae3-169">Saudação de cópia **URL de logout, alterar a URL da senha e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="f2ae3-169">Copy hello **Sign-Out URL, Change Password URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_configure.png) 

7. <span data-ttu-id="f2ae3-171">Em uma janela do navegador web diferente, faça logon no tooyour **BlueJeans** site da empresa como um administrador.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-171">In a different web browser window, log in tooyour **BlueJeans** company site as an administrator.</span></span>

8. <span data-ttu-id="f2ae3-172">Vá muito**ADMIN \> as configurações de grupo \> segurança**.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-172">Go too**ADMIN \> Group Settings \> Security**.</span></span>
   
   <span data-ttu-id="f2ae3-173">![Admin](./media/active-directory-saas-bluejeans-tutorial/IC785868.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="f2ae3-173">![Admin](./media/active-directory-saas-bluejeans-tutorial/IC785868.png "Admin")</span></span>

9. <span data-ttu-id="f2ae3-174">Em Olá **segurança** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2ae3-174">In hello **Security** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="f2ae3-175">![Logon Único do SAML](./media/active-directory-saas-bluejeans-tutorial/IC785869.png "Logon Único do SAML")</span><span class="sxs-lookup"><span data-stu-id="f2ae3-175">![SAML Single Sign On](./media/active-directory-saas-bluejeans-tutorial/IC785869.png "SAML Single Sign On")</span></span>   
   
   <span data-ttu-id="f2ae3-176">a.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-176">a.</span></span> <span data-ttu-id="f2ae3-177">Selecione **Logon Único do SAML**.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-177">Select **SAML Single Sign On**.</span></span>
  
   <span data-ttu-id="f2ae3-178">b.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-178">b.</span></span> <span data-ttu-id="f2ae3-179">Selecione **Habilitar provisionamento automático**.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-179">Select **Enable automatic provisioning**.</span></span>

10. <span data-ttu-id="f2ae3-180">Passar por hello etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2ae3-180">Move on with hello following steps:</span></span>

    <span data-ttu-id="f2ae3-181">![Caminho de Certificado](./media/active-directory-saas-bluejeans-tutorial/IC785870.png "Caminho de Certificado")</span><span class="sxs-lookup"><span data-stu-id="f2ae3-181">![Certificate Path](./media/active-directory-saas-bluejeans-tutorial/IC785870.png "Certificate Path")</span></span>
    
    <span data-ttu-id="f2ae3-182">a.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-182">a.</span></span> <span data-ttu-id="f2ae3-183">Clique em **Escolher arquivo**e, em seguida, carregue o certificado de saudação baixado.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-183">Click **Choose File**, and then upload hello downloaded certificate.</span></span>
   
    <span data-ttu-id="f2ae3-184">b.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-184">b.</span></span> <span data-ttu-id="f2ae3-185">Colar **Single Sign-On URL do serviço SAML** em Olá **URL de logon** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-185">Paste **SAML Single Sign-On Service URL** into hello **Login URL** textbox.</span></span>
   
    <span data-ttu-id="f2ae3-186">c.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-186">c.</span></span> <span data-ttu-id="f2ae3-187">Colar **alterar a URL da senha** em Olá **alterar a URL da senha** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-187">Paste **Change Password URL** into hello **Password Change URL** textbox.</span></span>
   
    <span data-ttu-id="f2ae3-188">d.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-188">d.</span></span> <span data-ttu-id="f2ae3-189">Colar **URL de logout** em Olá **URL de Logout** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-189">Paste **Sign-Out URL** into hello **Logout URL** textbox.</span></span>

11. <span data-ttu-id="f2ae3-190">Passar por hello etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2ae3-190">Move on with hello following steps:</span></span>
    
    <span data-ttu-id="f2ae3-191">![Salvar Alterações](./media/active-directory-saas-bluejeans-tutorial/IC785874.png "Salvar Alterações")</span><span class="sxs-lookup"><span data-stu-id="f2ae3-191">![Save Changes](./media/active-directory-saas-bluejeans-tutorial/IC785874.png "Save Changes")</span></span>
    
    <span data-ttu-id="f2ae3-192">a.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-192">a.</span></span> <span data-ttu-id="f2ae3-193">Em Olá **id de usuário** caixa de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-193">In hello **User id** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
   
    <span data-ttu-id="f2ae3-194">b.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-194">b.</span></span> <span data-ttu-id="f2ae3-195">Em Olá **Email** caixa de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-195">In hello **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
   
    <span data-ttu-id="f2ae3-196">c.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-196">c.</span></span> <span data-ttu-id="f2ae3-197">Clique em **Salvar Alterações**.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-197">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="f2ae3-198">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="f2ae3-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f2ae3-199">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f2ae3-200">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f2ae3-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f2ae3-201">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f2ae3-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="f2ae3-202">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="f2ae3-204">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f2ae3-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f2ae3-205">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f2ae3-207">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f2ae3-209">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f2ae3-211">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2ae3-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f2ae3-213">a.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-213">a.</span></span> <span data-ttu-id="f2ae3-214">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f2ae3-215">b.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-215">b.</span></span> <span data-ttu-id="f2ae3-216">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f2ae3-217">c.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-217">c.</span></span> <span data-ttu-id="f2ae3-218">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f2ae3-219">d.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-219">d.</span></span> <span data-ttu-id="f2ae3-220">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-220">Click **Create**.</span></span>
 
### <a name="creating-a-bluejeans-test-user"></a><span data-ttu-id="f2ae3-221">Criando um usuário de teste do BlueJeans</span><span class="sxs-lookup"><span data-stu-id="f2ae3-221">Creating a BlueJeans test user</span></span>

<span data-ttu-id="f2ae3-222">tooenable AD do Azure usuários toolog em tooBlueJeans, eles devem ser provisionados no BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-222">tooenable Azure AD users toolog in tooBlueJeans, they must be provisioned into BlueJeans.</span></span>  

<span data-ttu-id="f2ae3-223">No caso do BlueJeans, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-223">In case of BlueJeans, provisioning is a manual task.</span></span>

<span data-ttu-id="f2ae3-224">**tooprovision contas de usuário, executar Olá seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f2ae3-224">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="f2ae3-225">Faça logon no tooyour **BlueJeans** site da empresa como um administrador.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-225">Log in tooyour **BlueJeans** company site as an administrator.</span></span>

2. <span data-ttu-id="f2ae3-226">Vá muito**ADMIN \> gerenciar usuários \> adicionar usuário**.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-226">Go too**ADMIN \> Manage Users \> Add User**.</span></span>
   
   <span data-ttu-id="f2ae3-227">![Admin](./media/active-directory-saas-bluejeans-tutorial/IC785877.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="f2ae3-227">![Admin](./media/active-directory-saas-bluejeans-tutorial/IC785877.png "Admin")</span></span>
   
   >[!IMPORTANT]
   ><span data-ttu-id="f2ae3-228">Olá **adicionar usuário** guia está disponível somente se, no hello **guia Segurança**, **habilitar o provisionamento automático** está desmarcada.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-228">hello **Add User** tab is only available if, in hello **Security tab**, **Enable automatic provisioning** is unchecked.</span></span> 
   
3. <span data-ttu-id="f2ae3-229">Em Olá **adicionar usuário** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2ae3-229">In hello **Add User** section, perform hello following steps:</span></span>

    <span data-ttu-id="f2ae3-230">![Adicionar Usuário](./media/active-directory-saas-bluejeans-tutorial/IC785886.png "Adicionar Usuário")</span><span class="sxs-lookup"><span data-stu-id="f2ae3-230">![Add User](./media/active-directory-saas-bluejeans-tutorial/IC785886.png "Add User")</span></span>
    
    <span data-ttu-id="f2ae3-231">a.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-231">a.</span></span> <span data-ttu-id="f2ae3-232">Digite um **nome de usuário do BlueJeans**, uma **endereço de Email**, um **ID de reunião BlueJeans**, um **senha de moderador**, um **nome completo** , Olá **empresa** de uma conta válida do AAD você deseja tooprovision em Olá relacionados caixas de texto.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-232">Type a **BlueJeans Username**, an **Email address**, a **BlueJeans Meeting ID**, a **Moderator Passcode**, a **Full Name**, hello **Company** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
    
    <span data-ttu-id="f2ae3-233">b.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-233">b.</span></span> <span data-ttu-id="f2ae3-234">Clique em **Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-234">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="f2ae3-235">Você pode usar qualquer ferramenta de criação outros BlueJeans usuário conta ou APIs fornecidas pelo BlueJeans tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-235">You can use any other BlueJeans user account creation tools or APIs provided by BlueJeans tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f2ae3-236">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f2ae3-236">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f2ae3-237">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooBlueJeans.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-237">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBlueJeans.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="f2ae3-239">**tooassign Britta Simon tooBlueJeans, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f2ae3-239">**tooassign Britta Simon tooBlueJeans, perform hello following steps:**</span></span>

1. <span data-ttu-id="f2ae3-240">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-240">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="f2ae3-242">Na lista de aplicativos hello, selecione **BlueJeans**.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-242">In hello applications list, select **BlueJeans**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_app.png) 

3. <span data-ttu-id="f2ae3-244">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-244">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="f2ae3-246">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-246">Click **Add** button.</span></span> <span data-ttu-id="f2ae3-247">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-247">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="f2ae3-249">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-249">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f2ae3-250">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-250">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f2ae3-251">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-251">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f2ae3-252">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="f2ae3-252">Testing single sign-on</span></span>

<span data-ttu-id="f2ae3-253">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-253">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f2ae3-254">Quando você clica em Olá BlueJeans bloco no painel de acesso de saudação, você deve obter a página de logon do aplicativo BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="f2ae3-254">When you click hello BlueJeans tile in hello Access Panel, you should get login page of BlueJeans application.</span></span>
<span data-ttu-id="f2ae3-255">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f2ae3-255">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f2ae3-256">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="f2ae3-256">Additional resources</span></span>

* [<span data-ttu-id="f2ae3-257">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="f2ae3-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f2ae3-258">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f2ae3-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_203.png

