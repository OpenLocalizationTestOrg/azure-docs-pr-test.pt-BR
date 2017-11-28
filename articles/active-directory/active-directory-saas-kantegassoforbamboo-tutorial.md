---
title: "Tutorial: Integração do Azure Active Directory ao SSO do Kantega para o Bamboo | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Kantega SSO para o Bamboohr."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e238b574-9e9b-43b7-ab98-d2a87ff89d48
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 8bf637ff440e8e3948db882861bee6e73f8aa879
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-bamboo"></a><span data-ttu-id="3fc4f-103">Tutorial: Integração do Azure Active Directory ao SSO do Kantega para o Bamboo</span><span class="sxs-lookup"><span data-stu-id="3fc4f-103">Tutorial: Azure Active Directory integration with Kantega SSO for Bamboo</span></span>

<span data-ttu-id="3fc4f-104">Neste tutorial, você aprenderá como toointegrate Kantega SSO para o Bamboohr com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="3fc4f-104">In this tutorial, you learn how toointegrate Kantega SSO for Bamboo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3fc4f-105">Integrando Kantega SSO para o Bamboohr com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="3fc4f-105">Integrating Kantega SSO for Bamboo with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3fc4f-106">Você pode controlar no AD do Azure que tenha tooKantega acesso SSO para o Bamboohr</span><span class="sxs-lookup"><span data-stu-id="3fc4f-106">You can control in Azure AD who has access tooKantega SSO for Bamboo</span></span>
- <span data-ttu-id="3fc4f-107">Você pode habilitar seu usuários tooautomatically get conectado tooKantega SSO para o Bamboohr (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3fc4f-107">You can enable your users tooautomatically get signed-on tooKantega SSO for Bamboo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3fc4f-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3fc4f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3fc4f-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3fc4f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3fc4f-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3fc4f-110">Prerequisites</span></span>

<span data-ttu-id="3fc4f-111">tooconfigure integração do AD do Azure com Kantega SSO para o Bamboohr, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="3fc4f-111">tooconfigure Azure AD integration with Kantega SSO for Bamboo, you need hello following items:</span></span>

- <span data-ttu-id="3fc4f-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3fc4f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3fc4f-113">Uma assinatura habilitada para logon único do SSO do Kantega para o Bamboo</span><span class="sxs-lookup"><span data-stu-id="3fc4f-113">A Kantega SSO for Bamboo single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3fc4f-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3fc4f-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="3fc4f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3fc4f-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3fc4f-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3fc4f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3fc4f-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="3fc4f-118">Scenario description</span></span>
<span data-ttu-id="3fc4f-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3fc4f-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="3fc4f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3fc4f-121">Adicionando Kantega SSO para Bamboo da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="3fc4f-121">Adding Kantega SSO for Bamboo from hello gallery</span></span>
2. <span data-ttu-id="3fc4f-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3fc4f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kantega-sso-for-bamboo-from-hello-gallery"></a><span data-ttu-id="3fc4f-123">Adicionando Kantega SSO para Bamboo da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="3fc4f-123">Adding Kantega SSO for Bamboo from hello gallery</span></span>
<span data-ttu-id="3fc4f-124">integração de saudação tooconfigure do Kantega SSO para Bamboo no AD do Azure, você precisa tooadd Kantega SSO para Bamboo na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-124">tooconfigure hello integration of Kantega SSO for Bamboo into Azure AD, you need tooadd Kantega SSO for Bamboo from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3fc4f-125">**tooadd Kantega SSO para Bamboo da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="3fc4f-125">**tooadd Kantega SSO for Bamboo from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3fc4f-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3fc4f-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3fc4f-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="3fc4f-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="3fc4f-133">Na caixa de pesquisa hello, digite **Kantega SSO para Bamboo**.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-133">In hello search box, type **Kantega SSO for Bamboo**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_search.png)

5. <span data-ttu-id="3fc4f-135">No painel de resultados de saudação, selecione **Kantega SSO para Bamboo**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-135">In hello results panel, select **Kantega SSO for Bamboo**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3fc4f-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3fc4f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3fc4f-138">Nesta seção, você configura e testa o logon único do Azure AD com o SSO do Kantega para o Bamboo, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for Bamboo based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3fc4f-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Kantega SSO para Bamboo é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kantega SSO for Bamboo is tooa user in Azure AD.</span></span> <span data-ttu-id="3fc4f-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Kantega SSO para Bamboo precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-140">In other words, a link relationship between an Azure AD user and hello related user in Kantega SSO for Bamboo needs toobe established.</span></span>

<span data-ttu-id="3fc4f-141">Kantega SSO para o Bamboohr, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-141">In Kantega SSO for Bamboo, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3fc4f-142">tooconfigure e teste de logon único do AD do Azure com Kantega SSO para o Bamboohr, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="3fc4f-142">tooconfigure and test Azure AD single sign-on with Kantega SSO for Bamboo, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3fc4f-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3fc4f-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3fc4f-145">**[Criando um Kantega SSO para o usuário de teste Bamboo](#creating-a-kantega-sso-for-bamboo-test-user)**  -toohave um equivalente do Britta Simon em Kantega SSO para Bamboo é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-145">**[Creating a Kantega SSO for Bamboo test user](#creating-a-kantega-sso-for-bamboo-test-user)** - toohave a counterpart of Britta Simon in Kantega SSO for Bamboo that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3fc4f-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3fc4f-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3fc4f-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3fc4f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3fc4f-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no seu Kantega SSO para aplicativos do Bamboohr.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kantega SSO for Bamboo application.</span></span>

<span data-ttu-id="3fc4f-150">**tooconfigure logon único do AD do Azure com Kantega SSO para o Bamboohr, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="3fc4f-150">**tooconfigure Azure AD single sign-on with Kantega SSO for Bamboo, perform hello following steps:**</span></span>

1. <span data-ttu-id="3fc4f-151">Em Olá portal do Azure, Olá **Kantega SSO para Bamboo** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-151">In hello Azure portal, on hello **Kantega SSO for Bamboo** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="3fc4f-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_samlbase.png)

3. <span data-ttu-id="3fc4f-155">Em **IDP** iniciada modo em Olá **Kantega SSO para o domínio do Bamboohr e URLs** seção executar Olá etapa a seguir:</span><span class="sxs-lookup"><span data-stu-id="3fc4f-155">In **IDP** initiated mode, on hello **Kantega SSO for Bamboo Domain and URLs** section perform hello following step :</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_url1.png)
    
    <span data-ttu-id="3fc4f-157">a.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-157">a.</span></span> <span data-ttu-id="3fc4f-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="3fc4f-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    <span data-ttu-id="3fc4f-159">b.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-159">b.</span></span> <span data-ttu-id="3fc4f-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="3fc4f-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

4. <span data-ttu-id="3fc4f-161">Em **SP** modo iniciado, verifique **Mostrar configurações de URL avançadas** e executar Olá etapa a seguir:</span><span class="sxs-lookup"><span data-stu-id="3fc4f-161">In **SP** initiated mode, check **Show advanced URL settings** and  perform hello following step :</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_url2.png)
    
    <span data-ttu-id="3fc4f-163">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="3fc4f-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="3fc4f-164">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-164">These values are not real.</span></span> <span data-ttu-id="3fc4f-165">Atualizar esses valores com hello real identificador, URL de resposta e URL de logon.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-165">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="3fc4f-166">Esses valores são recebidos durante a configuração de saudação do Bamboohr plug-in que é explicada posteriormente no tutorial de saudação.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-166">These values are recieved during hello configuration of Bamboo plugin which is explained later in hello tutorial.</span></span>

5. <span data-ttu-id="3fc4f-167">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_certificate.png) 

6. <span data-ttu-id="3fc4f-169">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="3fc4f-169">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="3fc4f-171">Em uma janela de navegador web diferente, faça logon em tooyour Bamboo no servidor local como um administrador.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-171">In a different web browser window, log in tooyour Bamboo  on premise server as an administrator.</span></span>

8. <span data-ttu-id="3fc4f-172">Passe o mouse sobre engrenagem e clique em Olá **complementos**.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-172">Hover on cog and click hello **Add-ons**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon1.png)

9. <span data-ttu-id="3fc4f-174">Na seção da guia Complementos, clique em **Localizar novos complementos**.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-174">Under Add-ons tab section, click **Find new add-ons**.</span></span> <span data-ttu-id="3fc4f-175">Pesquisa **Kantega SSO para o Bamboohr (SAML e Kerberos)** e clique em **instalar** tooinstall botão Olá novo plug-in SAML.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-175">Search **Kantega SSO for Bamboo (SAML & Kerberos)** and click **Install** button tooinstall hello new SAML plugin.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon2.png)

10. <span data-ttu-id="3fc4f-177">instalação do plug-in de saudação será iniciado.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-177">hello plugin installation will start.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon21.png)

11. <span data-ttu-id="3fc4f-179">Após a conclusão da instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-179">Once hello installation is complete.</span></span> <span data-ttu-id="3fc4f-180">Clique em **fechar**</span><span class="sxs-lookup"><span data-stu-id="3fc4f-180">Click **Close**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon33.png)

12. <span data-ttu-id="3fc4f-182">Clique em **Gerenciar**.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-182">Click **Manage**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon34.png)
    
13. <span data-ttu-id="3fc4f-184">Clique em **configurar** tooconfigure Olá novo plug-in.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-184">Click **Configure** tooconfigure hello new plugin.</span></span>  

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon3.png)

14. <span data-ttu-id="3fc4f-186">Em Olá **SAML** seção.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-186">In hello **SAML** section.</span></span> <span data-ttu-id="3fc4f-187">Selecione **do Azure Active Directory (AD do Azure)** de saudação **Adicionar provedor de identidade** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-187">Select **Azure Active Directory (Azure AD)** from hello **Add identity provider** dropdown.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon4.png)

15. <span data-ttu-id="3fc4f-189">Selecione o nível de assinatura como **Básico**.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-189">Select subscription level as **Basic**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon5.png)

16. <span data-ttu-id="3fc4f-191">Em Olá **propriedades do aplicativo** seção, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3fc4f-191">On hello **App properties** section, perform following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon6.png)

    <span data-ttu-id="3fc4f-193">a.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-193">a.</span></span> <span data-ttu-id="3fc4f-194">Saudação de cópia **URI da ID do aplicativo** valor e usá-lo como **identificador, o URL de resposta e a URL de logon** em Olá **Kantega SSO para o domínio do Bamboohr e URLs** seção no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-194">Copy hello **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on hello **Kantega SSO for Bamboo Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="3fc4f-195">b.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-195">b.</span></span> <span data-ttu-id="3fc4f-196">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-196">Click **Next**.</span></span>

17. <span data-ttu-id="3fc4f-197">Em Olá **importar metadados** seção, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3fc4f-197">On hello **Metadata import** section, perform following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon7.png)

    <span data-ttu-id="3fc4f-199">a.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-199">a.</span></span> <span data-ttu-id="3fc4f-200">Selecione **Arquivo de metadados no meu computador** e carregue um arquivo de metadados baixado no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-200">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="3fc4f-201">b.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-201">b.</span></span> <span data-ttu-id="3fc4f-202">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-202">Click **Next**.</span></span>

18. <span data-ttu-id="3fc4f-203">Em Olá **nome e SSO local** seção, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3fc4f-203">On hello **Name and SSO location** section, perform following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon8.png)

    <span data-ttu-id="3fc4f-205">a.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-205">a.</span></span> <span data-ttu-id="3fc4f-206">Adicionar o nome do provedor de identidade de saudação em **nome do provedor de identidade** caixa de texto (por exemplo, o AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="3fc4f-206">Add Name of hello Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span></span>

    <span data-ttu-id="3fc4f-207">b.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-207">b.</span></span> <span data-ttu-id="3fc4f-208">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-208">Click **Next**.</span></span>

19. <span data-ttu-id="3fc4f-209">Verifique se o certificado de autenticação de saudação e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-209">Verify hello Signing certificate and click **Next**.</span></span>    

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon9.png)

20. <span data-ttu-id="3fc4f-211">Em Olá **contas de usuário do Bamboohr** seção, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3fc4f-211">On hello **Bamboo user accounts** section, perform following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon10.png)

    <span data-ttu-id="3fc4f-213">a.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-213">a.</span></span> <span data-ttu-id="3fc4f-214">Selecione **criar usuários no diretório interno do Bamboohr, se necessário** e insira nome apropriado saudação do grupo de saudação para usuários (pode ser não vários.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-214">Select **Create users in Bamboo's internal Directory if needed** and enter hello appropriate name of hello group for users (can be multiple no.</span></span> <span data-ttu-id="3fc4f-215">de grupos separados por vírgula).</span><span class="sxs-lookup"><span data-stu-id="3fc4f-215">of groups separated by comma).</span></span>

    <span data-ttu-id="3fc4f-216">b.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-216">b.</span></span> <span data-ttu-id="3fc4f-217">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-217">Click **Next**.</span></span>

21. <span data-ttu-id="3fc4f-218">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-218">Click **Finish**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon11.png)

22. <span data-ttu-id="3fc4f-220">Em Olá **conhecido domínios do AD do Azure** seção, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3fc4f-220">On hello **Known domains for Azure AD** section, perform following steps:</span></span>   

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon12.png)

    <span data-ttu-id="3fc4f-222">a.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-222">a.</span></span> <span data-ttu-id="3fc4f-223">Selecione **conhecido domínios** do painel esquerdo de saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-223">Select **Known domains** from hello left panel of hello page.</span></span>

    <span data-ttu-id="3fc4f-224">b.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-224">b.</span></span> <span data-ttu-id="3fc4f-225">Digite o nome de domínio em Olá **conhecido domínios** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-225">Enter domain name in hello **Known domains** textbox.</span></span>

    <span data-ttu-id="3fc4f-226">c.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-226">c.</span></span> <span data-ttu-id="3fc4f-227">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-227">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="3fc4f-228">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="3fc4f-228">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3fc4f-229">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-229">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3fc4f-230">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3fc4f-230">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3fc4f-231">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3fc4f-231">Creating an Azure AD test user</span></span>
<span data-ttu-id="3fc4f-232">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-232">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="3fc4f-234">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="3fc4f-234">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3fc4f-235">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-235">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3fc4f-237">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-237">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3fc4f-239">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-239">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3fc4f-241">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="3fc4f-241">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3fc4f-243">a.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-243">a.</span></span> <span data-ttu-id="3fc4f-244">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-244">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3fc4f-245">b.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-245">b.</span></span> <span data-ttu-id="3fc4f-246">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-246">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3fc4f-247">c.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-247">c.</span></span> <span data-ttu-id="3fc4f-248">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-248">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3fc4f-249">d.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-249">d.</span></span> <span data-ttu-id="3fc4f-250">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-250">Click **Create**.</span></span>
 
### <a name="creating-a-kantega-sso-for-bamboo-test-user"></a><span data-ttu-id="3fc4f-251">Criando um usuário de teste do SSO do Kantega para o Bamboo</span><span class="sxs-lookup"><span data-stu-id="3fc4f-251">Creating a Kantega SSO for Bamboo test user</span></span>

<span data-ttu-id="3fc4f-252">tooenable AD do Azure usuários toolog em tooBamboo, eles devem ser provisionados no Bamboohr.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-252">tooenable Azure AD users toolog in tooBamboo, they must be provisioned into Bamboo.</span></span> <span data-ttu-id="3fc4f-253">No SSO do Kantega para o Bamboo, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-253">In Kantega SSO for Bamboo, provisioning is a manual task.</span></span>

<span data-ttu-id="3fc4f-254">**tooprovision uma conta de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="3fc4f-254">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="3fc4f-255">Faça logon tooyour Bamboo no servidor local como um administrador.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-255">Log in tooyour Bamboo on premise server as an administrator.</span></span>

2. <span data-ttu-id="3fc4f-256">Passe o mouse sobre engrenagem e clique em Olá **gerenciamento de usuário**.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-256">Hover on cog and click hello **User management**.</span></span>

    ![Adicionar Funcionário](./media/active-directory-saas-kantegassoforbamboo-tutorial/user1.png) 

3. <span data-ttu-id="3fc4f-258">Clique em **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-258">Click **Users**.</span></span> <span data-ttu-id="3fc4f-259">Em Olá **adicionar usuário** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3fc4f-259">Under hello **Add user** section, Perform follwing steps:</span></span>

    ![Adicionar Funcionário](./media/active-directory-saas-kantegassoforbamboo-tutorial/user2.png) 

    <span data-ttu-id="3fc4f-261">a.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-261">a.</span></span> <span data-ttu-id="3fc4f-262">Em Olá **Username** caixa de texto, como o email de saudação do tipo de usuário Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-262">In hello **Username** textbox, type hello email of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="3fc4f-263">b.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-263">b.</span></span> <span data-ttu-id="3fc4f-264">Em Olá **senha** caixa de texto, digite a senha de saudação do usuário.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-264">In hello **Password** textbox, type hello password of user.</span></span>

    <span data-ttu-id="3fc4f-265">c.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-265">c.</span></span> <span data-ttu-id="3fc4f-266">Em Olá **Confirmar senha** caixa de texto, redigite a senha de saudação do usuário.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-266">In hello **Confirm Password** textbox, reenter hello password of user.</span></span>
    
    <span data-ttu-id="3fc4f-267">d.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-267">d.</span></span> <span data-ttu-id="3fc4f-268">Em Olá **nome completo** caixa de texto, nome completo do tipo de usuário hello como Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-268">In hello **Full Name** textbox, type full name of hello user like Britta Simon.</span></span>
    
    <span data-ttu-id="3fc4f-269">e.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-269">e.</span></span> <span data-ttu-id="3fc4f-270">Em Olá **Email** caixa de texto, como o endereço de email do tipo saudação do usuário Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-270">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="3fc4f-271">f.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-271">f.</span></span> <span data-ttu-id="3fc4f-272">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-272">Click **Save**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3fc4f-273">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3fc4f-273">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3fc4f-274">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooKantega SSO para o Bamboohr.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-274">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKantega SSO for Bamboo.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="3fc4f-276">**tooassign Britta Simon tooKantega SSO para o Bamboohr, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="3fc4f-276">**tooassign Britta Simon tooKantega SSO for Bamboo, perform hello following steps:**</span></span>

1. <span data-ttu-id="3fc4f-277">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-277">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="3fc4f-279">Na lista de aplicativos hello, selecione **Kantega SSO para Bamboo**.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-279">In hello applications list, select **Kantega SSO for Bamboo**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_app.png) 

3. <span data-ttu-id="3fc4f-281">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-281">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="3fc4f-283">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-283">Click **Add** button.</span></span> <span data-ttu-id="3fc4f-284">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-284">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="3fc4f-286">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-286">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3fc4f-287">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-287">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3fc4f-288">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-288">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3fc4f-289">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="3fc4f-289">Testing single sign-on</span></span>

<span data-ttu-id="3fc4f-290">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-290">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3fc4f-291">Quando você clica em hello Kantega SSO para bloco Bamboo Olá painel de acesso, você deve obter automaticamente assinado em tooyour Kantega SSO para o aplicativo Bamboohr.</span><span class="sxs-lookup"><span data-stu-id="3fc4f-291">When you click hello Kantega SSO for Bamboo tile in hello Access Panel, you should get automatically signed-on tooyour Kantega SSO for Bamboo application.</span></span>
<span data-ttu-id="3fc4f-292">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3fc4f-292">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3fc4f-293">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="3fc4f-293">Additional resources</span></span>

* [<span data-ttu-id="3fc4f-294">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="3fc4f-294">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3fc4f-295">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3fc4f-295">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_203.png

