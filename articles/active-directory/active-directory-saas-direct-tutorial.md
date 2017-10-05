---
title: "Tutorial: Integração do Azure Active Directory ao Direct | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Direct."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7c2cd1f0-d14c-42f0-94a8-9b800008b285
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 84582492592613320bd3ec2bdffe08519852d7c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-direct"></a><span data-ttu-id="9ca90-103">Tutorial: integração do Azure Active Directory com o Direct</span><span class="sxs-lookup"><span data-stu-id="9ca90-103">Tutorial: Azure Active Directory integration with Direct</span></span>

<span data-ttu-id="9ca90-104">Neste tutorial, você aprenderá como integrar o Direct ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="9ca90-104">In this tutorial, you learn how to integrate Direct with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9ca90-105">A integração do Direct ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="9ca90-105">Integrating Direct with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9ca90-106">Você pode controlar no Azure AD quem terá acesso ao Direct</span><span class="sxs-lookup"><span data-stu-id="9ca90-106">You can control in Azure AD who has access to Direct</span></span>
- <span data-ttu-id="9ca90-107">Você pode permitir que usuários façam logon automaticamente no Direct (Logon Único) com as respectivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ca90-107">You can enable your users to automatically get signed-on to Direct (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9ca90-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9ca90-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9ca90-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9ca90-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9ca90-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9ca90-110">Prerequisites</span></span>

<span data-ttu-id="9ca90-111">Para configurar a integração do Azure AD ao Direct, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="9ca90-111">To configure Azure AD integration with Direct, you need the following items:</span></span>

- <span data-ttu-id="9ca90-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9ca90-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9ca90-113">Uma assinatura habilitada para logon único do Direct</span><span class="sxs-lookup"><span data-stu-id="9ca90-113">A Direct single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9ca90-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="9ca90-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9ca90-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="9ca90-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9ca90-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="9ca90-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9ca90-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9ca90-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9ca90-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="9ca90-118">Scenario description</span></span>
<span data-ttu-id="9ca90-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="9ca90-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9ca90-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="9ca90-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9ca90-121">Adicionando Direct da galeria</span><span class="sxs-lookup"><span data-stu-id="9ca90-121">Adding Direct from the gallery</span></span>
2. <span data-ttu-id="9ca90-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9ca90-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-direct-from-the-gallery"></a><span data-ttu-id="9ca90-123">Adicionando Direct da galeria</span><span class="sxs-lookup"><span data-stu-id="9ca90-123">Adding Direct from the gallery</span></span>
<span data-ttu-id="9ca90-124">Para configurar a integração do Direct ao Azure AD, você precisará adicionar o Direct da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="9ca90-124">To configure the integration of Direct into Azure AD, you need to add Direct from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9ca90-125">**Para adicionar o Direct da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="9ca90-125">**To add Direct from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9ca90-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9ca90-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9ca90-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="9ca90-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9ca90-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9ca90-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="9ca90-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9ca90-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="9ca90-133">Na caixa de pesquisa, digite **Direct**.</span><span class="sxs-lookup"><span data-stu-id="9ca90-133">In the search box, type **Direct**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-direct-tutorial/tutorial_direct_search.png)

5. <span data-ttu-id="9ca90-135">No painel de resultados, selecione **Direct** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9ca90-135">In the results panel, select **Direct**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-direct-tutorial/tutorial_direct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9ca90-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9ca90-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9ca90-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Direct com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="9ca90-138">In this section, you configure and test Azure AD single sign-on with Direct based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9ca90-139">Para que o logon único funcione, o Azure AD precisará saber qual usuário do Direct é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9ca90-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Direct is to a user in Azure AD.</span></span> <span data-ttu-id="9ca90-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Direct.</span><span class="sxs-lookup"><span data-stu-id="9ca90-140">In other words, a link relationship between an Azure AD user and the related user in Direct needs to be established.</span></span>

<span data-ttu-id="9ca90-141">No Direct, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="9ca90-141">In Direct, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9ca90-142">Para configurar e testar o logon único do Azure AD com o Direct, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="9ca90-142">To configure and test Azure AD single sign-on with Direct, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9ca90-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="9ca90-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9ca90-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="9ca90-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9ca90-145">**[Criação de um usuário de teste do Direct](#creating-a-direct-test-user)** – para ter um equivalente de Brenda Fernandes no Direct que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9ca90-145">**[Creating a Direct test user](#creating-a-direct-test-user)** - to have a counterpart of Britta Simon in Direct that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9ca90-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="9ca90-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9ca90-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="9ca90-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9ca90-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ca90-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9ca90-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Direct.</span><span class="sxs-lookup"><span data-stu-id="9ca90-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Direct application.</span></span>

<span data-ttu-id="9ca90-150">**Para configurar o logon único do Azure AD com o Direct, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="9ca90-150">**To configure Azure AD single sign-on with Direct, perform the following steps:**</span></span>

1. <span data-ttu-id="9ca90-151">No portal do Azure, na página de integração de aplicativos do **Direct**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="9ca90-151">In the Azure portal, on the **Direct** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="9ca90-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="9ca90-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-direct-tutorial/tutorial_direct_samlbase.png)

3. <span data-ttu-id="9ca90-155">Na seção **Domínio e URLs do Direct**, se você desejar configurar o aplicativo no modo iniciado pelo **IDP**:</span><span class="sxs-lookup"><span data-stu-id="9ca90-155">On the **Direct Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-direct-tutorial/tutorial_direct_url.png)

    <span data-ttu-id="9ca90-157">Na caixa de texto **Identificador**, digite a URL: `https://direct4b.com/`</span><span class="sxs-lookup"><span data-stu-id="9ca90-157">In the **Identifier** textbox, type the URL: `https://direct4b.com/`</span></span>

4. <span data-ttu-id="9ca90-158">Marque **Mostrar configurações avançadas de URL** se quiser configurar o aplicativo no modo iniciado em **SP**:</span><span class="sxs-lookup"><span data-stu-id="9ca90-158">Check **Show advanced URL settings**, If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-direct-tutorial/tutorial_direct_url1.png)

     <span data-ttu-id="9ca90-160">Na caixa de texto **URL de Logon**, digite a URL: `https://direct4b.com/sso`</span><span class="sxs-lookup"><span data-stu-id="9ca90-160">In the **Sign-on URL** textbox, type the URL: `https://direct4b.com/sso`</span></span> 
    
5. <span data-ttu-id="9ca90-161">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="9ca90-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-direct-tutorial/tutorial_direct_certificate.png) 

6. <span data-ttu-id="9ca90-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="9ca90-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-direct-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="9ca90-165">Para configurar o logon único no lado do **Direct**, é necessário enviar o **XML de metadados** baixado para a [equipe de suporte do Direct](https://direct4b.com/ja/support.html#inquiry).</span><span class="sxs-lookup"><span data-stu-id="9ca90-165">To configure single sign-on on **Direct** side, you need to send the downloaded **Metadata XML** to [Direct support team](https://direct4b.com/ja/support.html#inquiry).</span></span> 

> [!TIP]
> <span data-ttu-id="9ca90-166">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="9ca90-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9ca90-167">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="9ca90-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9ca90-168">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9ca90-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9ca90-169">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9ca90-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="9ca90-170">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="9ca90-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="9ca90-172">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="9ca90-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9ca90-173">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9ca90-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-direct-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9ca90-175">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="9ca90-175">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-direct-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9ca90-177">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9ca90-177">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-direct-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9ca90-179">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="9ca90-179">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-direct-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9ca90-181">a.</span><span class="sxs-lookup"><span data-stu-id="9ca90-181">a.</span></span> <span data-ttu-id="9ca90-182">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="9ca90-182">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9ca90-183">b.</span><span class="sxs-lookup"><span data-stu-id="9ca90-183">b.</span></span> <span data-ttu-id="9ca90-184">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="9ca90-184">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9ca90-185">c.</span><span class="sxs-lookup"><span data-stu-id="9ca90-185">c.</span></span> <span data-ttu-id="9ca90-186">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="9ca90-186">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9ca90-187">d.</span><span class="sxs-lookup"><span data-stu-id="9ca90-187">d.</span></span> <span data-ttu-id="9ca90-188">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="9ca90-188">Click **Create**.</span></span>
 
### <a name="creating-a-direct-test-user"></a><span data-ttu-id="9ca90-189">Como criar um usuário de teste do Direct</span><span class="sxs-lookup"><span data-stu-id="9ca90-189">Creating a Direct test user</span></span>

<span data-ttu-id="9ca90-190">Nesta seção, você criará um usuário chamado Brenda Fernandes no Direct.</span><span class="sxs-lookup"><span data-stu-id="9ca90-190">In this section, you create a user called Britta Simon in Direct.</span></span> <span data-ttu-id="9ca90-191">Trabalhe com [a equipe de suporte do Direct](https://direct4b.com/ja/support.html#inquiry) para adicionar os usuários à plataforma do Direct.</span><span class="sxs-lookup"><span data-stu-id="9ca90-191">Work with [Direct support team](https://direct4b.com/ja/support.html#inquiry) to add the users in the Direct platform.</span></span> <span data-ttu-id="9ca90-192">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="9ca90-192">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9ca90-193">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9ca90-193">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9ca90-194">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Direct.</span><span class="sxs-lookup"><span data-stu-id="9ca90-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Direct.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="9ca90-196">**Para atribuir Brenda Fernandes ao Direct, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="9ca90-196">**To assign Britta Simon to Direct, perform the following steps:**</span></span>

1. <span data-ttu-id="9ca90-197">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9ca90-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="9ca90-199">Na lista de aplicativos, selecione **Direct**.</span><span class="sxs-lookup"><span data-stu-id="9ca90-199">In the applications list, select **Direct**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-direct-tutorial/tutorial_direct_app.png) 

3. <span data-ttu-id="9ca90-201">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="9ca90-201">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="9ca90-203">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="9ca90-203">Click **Add** button.</span></span> <span data-ttu-id="9ca90-204">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9ca90-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="9ca90-206">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="9ca90-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9ca90-207">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9ca90-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9ca90-208">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9ca90-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9ca90-209">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="9ca90-209">Testing single sign-on</span></span>

<span data-ttu-id="9ca90-210">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="9ca90-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

1. <span data-ttu-id="9ca90-211">Se você quiser testar no **Modo iniciado por IDP**:</span><span class="sxs-lookup"><span data-stu-id="9ca90-211">If you wish to test in **IDP Initiated Mode**:</span></span>

    <span data-ttu-id="9ca90-212">Quando você clicar no bloco **Direct** no Painel de Acesso, deverá fazer logon automaticamente no seu aplicativo **Direct**.</span><span class="sxs-lookup"><span data-stu-id="9ca90-212">When you click the **Direct** tile in the Access Panel, you should get automatically signed-on to your **Direct** application.</span></span>

2. <span data-ttu-id="9ca90-213">Se você quiser testar no **Modo iniciado por SP**:</span><span class="sxs-lookup"><span data-stu-id="9ca90-213">If you wish to test in **SP Initiated Mode**:</span></span>
    
    <span data-ttu-id="9ca90-214">a.</span><span class="sxs-lookup"><span data-stu-id="9ca90-214">a.</span></span> <span data-ttu-id="9ca90-215">Clique no bloco **Direct** no Painel de Acesso e será redirecionado para a página de logon do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9ca90-215">Click on the **Direct** tile in the Access Panel and you will be redirected to the application sign-on page.</span></span>

    <span data-ttu-id="9ca90-216">b.</span><span class="sxs-lookup"><span data-stu-id="9ca90-216">b.</span></span> <span data-ttu-id="9ca90-217">Insira seu `subdomain` na caixa de texto e pressione “次へ (Avançar)” e você deverá ser automaticamente conectado ao seu aplicativo **Direct**.</span><span class="sxs-lookup"><span data-stu-id="9ca90-217">Input your `subdomain` in the textbox displayed and press '次へ (Next)' and you should get automatically signed-on to your **Direct** application .</span></span>
    
<span data-ttu-id="9ca90-218">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9ca90-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9ca90-219">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="9ca90-219">Additional resources</span></span>

* [<span data-ttu-id="9ca90-220">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="9ca90-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9ca90-221">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9ca90-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-direct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-direct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-direct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-direct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-direct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-direct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-direct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-direct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-direct-tutorial/tutorial_general_203.png

