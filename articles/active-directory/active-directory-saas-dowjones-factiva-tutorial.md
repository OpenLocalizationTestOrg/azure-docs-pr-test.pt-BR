---
title: "Tutorial: Integração do Azure Active Directory ao Dow Jones Factiva | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Dow Jones Factiva."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b36e97e8-37a6-4096-a894-530427ee1331
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/11/2017
ms.author: jeedes
ms.openlocfilehash: dab48c24ff25fd68df1ee540bb8f0929e7e81bcb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-dow-jones-factiva"></a><span data-ttu-id="33b03-103">Tutorial: Integração do Azure Active Directory com o Dow Jones Factiva</span><span class="sxs-lookup"><span data-stu-id="33b03-103">Tutorial: Azure Active Directory integration with Dow Jones Factiva</span></span>

<span data-ttu-id="33b03-104">Neste tutorial, você aprenderá a integrar o Dow Jones Factiva ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="33b03-104">In this tutorial, you learn how to integrate Dow Jones Factiva with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="33b03-105">A integração do Dow Jones Factiva ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="33b03-105">Integrating Dow Jones Factiva with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="33b03-106">No Azure AD, é possível controlar quem tem acesso ao Dow Jones Factiva</span><span class="sxs-lookup"><span data-stu-id="33b03-106">You can control in Azure AD who has access to Dow Jones Factiva</span></span>
- <span data-ttu-id="33b03-107">Você pode permitir que usuários façam logon automaticamente no Dow Jones Factiva (Logon Único) com as respectivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="33b03-107">You can enable your users to automatically get signed-on to Dow Jones Factiva (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="33b03-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="33b03-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="33b03-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="33b03-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33b03-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="33b03-110">Prerequisites</span></span>

<span data-ttu-id="33b03-111">Para configurar a integração do Azure AD ao Dow Jones Factiva, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="33b03-111">To configure Azure AD integration with Dow Jones Factiva, you need the following items:</span></span>

- <span data-ttu-id="33b03-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="33b03-112">An Azure AD subscription</span></span>
- <span data-ttu-id="33b03-113">Uma assinatura habilitada para logon único do Dow Jones Factiva</span><span class="sxs-lookup"><span data-stu-id="33b03-113">A Dow Jones Factiva single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="33b03-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="33b03-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="33b03-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="33b03-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="33b03-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="33b03-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="33b03-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="33b03-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="33b03-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="33b03-118">Scenario description</span></span>
<span data-ttu-id="33b03-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="33b03-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="33b03-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="33b03-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="33b03-121">Adição do Dow Jones Factiva da galeria</span><span class="sxs-lookup"><span data-stu-id="33b03-121">Adding Dow Jones Factiva from the gallery</span></span>
2. <span data-ttu-id="33b03-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="33b03-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-dow-jones-factiva-from-the-gallery"></a><span data-ttu-id="33b03-123">Adição do Dow Jones Factiva da galeria</span><span class="sxs-lookup"><span data-stu-id="33b03-123">Adding Dow Jones Factiva from the gallery</span></span>
<span data-ttu-id="33b03-124">Para configurar a integração do Dow Jones Factiva ao Azure AD, você precisará adicionar o Dow Jones Factiva da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="33b03-124">To configure the integration of Dow Jones Factiva into Azure AD, you need to add Dow Jones Factiva from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="33b03-125">**Para adicionar o Dow Jones Factiva da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="33b03-125">**To add Dow Jones Factiva from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="33b03-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="33b03-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="33b03-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="33b03-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="33b03-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="33b03-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="33b03-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="33b03-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="33b03-133">Na caixa de pesquisa, digite **Dow Jones Factiva**.</span><span class="sxs-lookup"><span data-stu-id="33b03-133">In the search box, type **Dow Jones Factiva**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_search.png)

5. <span data-ttu-id="33b03-135">No painel de resultados, selecione **Dow Jones Factiva** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="33b03-135">In the results panel, select **Dow Jones Factiva**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="33b03-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="33b03-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="33b03-138">Nesta seção, você configura e testa o logon único do Azure AD com o Dow Jones Factiva com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="33b03-138">In this section, you configure and test Azure AD single sign-on with Dow Jones Factiva based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="33b03-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Dow Jones Factiva é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="33b03-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Dow Jones Factiva is to a user in Azure AD.</span></span> <span data-ttu-id="33b03-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Dow Jones Factiva.</span><span class="sxs-lookup"><span data-stu-id="33b03-140">In other words, a link relationship between an Azure AD user and the related user in Dow Jones Factiva needs to be established.</span></span>

<span data-ttu-id="33b03-141">No Dow Jones Factiva, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="33b03-141">In Dow Jones Factiva, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="33b03-142">Para configurar e testar o logon único do Azure AD com o Dow Jones Factiva, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="33b03-142">To configure and test Azure AD single sign-on with Dow Jones Factiva, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="33b03-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="33b03-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="33b03-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="33b03-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="33b03-145">**[Criação de um usuário de teste do Dow Jones Factiva](#creating-a-dow-jones-factiva-test-user)** – para ter um equivalente de Brenda Fernandes no Dow Jones Factiva que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="33b03-145">**[Creating a Dow Jones Factiva test user](#creating-a-dow-jones-factiva-test-user)** - to have a counterpart of Britta Simon in Dow Jones Factiva that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="33b03-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="33b03-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="33b03-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="33b03-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="33b03-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="33b03-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="33b03-149">Nesta seção, você habilitará o logon único do Azure AD no portal do Azure e configurará o logon único em seu aplicativo Dow Jones Factiva.</span><span class="sxs-lookup"><span data-stu-id="33b03-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Dow Jones Factiva application.</span></span>

<span data-ttu-id="33b03-150">**Para configurar o logon único do Azure AD com o Dow Jones Factiva, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="33b03-150">**To configure Azure AD single sign-on with Dow Jones Factiva, perform the following steps:**</span></span>

1. <span data-ttu-id="33b03-151">No portal do Azure, na página de integração de aplicativos do **Dow Jones Factiva**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="33b03-151">In the Azure portal, on the **Dow Jones Factiva** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="33b03-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="33b03-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_samlbase.png)

3. <span data-ttu-id="33b03-155">Na seção **URLs e Domínio do Dow Jones Factiva**, o usuário não precisa seguir as etapas, já que o aplicativo está previamente integrado ao Azure.</span><span class="sxs-lookup"><span data-stu-id="33b03-155">On the **Dow Jones Factiva Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_url.png)

4. <span data-ttu-id="33b03-157">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="33b03-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_certificate.png) 

5. <span data-ttu-id="33b03-159">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="33b03-159">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="33b03-161">Para configurar o logon único no lado do **Dow Jones Factiva**, você precisa enviar o **XML de Metadados** baixado para a [equipe de suporte do Dow Jones Factiva](https://www.dowjones.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="33b03-161">To configure single sign-on on **Dow Jones Factiva** side, you need to send the downloaded **Metadata XML** to [Dow Jones Factiva support team](https://www.dowjones.com/contact/).</span></span> <span data-ttu-id="33b03-162">Eles definem essa configuração para ter a conexão de SSO do SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="33b03-162">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="33b03-163">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="33b03-163">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="33b03-164">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="33b03-164">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="33b03-165">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="33b03-165">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="33b03-166">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="33b03-166">Creating an Azure AD test user</span></span>
<span data-ttu-id="33b03-167">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="33b03-167">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="33b03-169">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="33b03-169">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="33b03-170">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="33b03-170">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="33b03-172">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="33b03-172">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="33b03-174">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="33b03-174">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="33b03-176">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="33b03-176">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="33b03-178">a.</span><span class="sxs-lookup"><span data-stu-id="33b03-178">a.</span></span> <span data-ttu-id="33b03-179">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="33b03-179">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="33b03-180">b.</span><span class="sxs-lookup"><span data-stu-id="33b03-180">b.</span></span> <span data-ttu-id="33b03-181">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="33b03-181">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="33b03-182">c.</span><span class="sxs-lookup"><span data-stu-id="33b03-182">c.</span></span> <span data-ttu-id="33b03-183">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="33b03-183">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="33b03-184">d.</span><span class="sxs-lookup"><span data-stu-id="33b03-184">d.</span></span> <span data-ttu-id="33b03-185">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="33b03-185">Click **Create**.</span></span>
 
### <a name="creating-a-dow-jones-factiva-test-user"></a><span data-ttu-id="33b03-186">Como criar um usuário de teste do Dow Jones Factiva</span><span class="sxs-lookup"><span data-stu-id="33b03-186">Creating a Dow Jones Factiva test user</span></span>

<span data-ttu-id="33b03-187">Nesta seção, você criará uma usuária chamada Brenda Fernandes no Dow Jones Factiva.</span><span class="sxs-lookup"><span data-stu-id="33b03-187">In this section, you create a user called Britta Simon in Dow Jones Factiva.</span></span> <span data-ttu-id="33b03-188">Trabalhe com a [equipe de suporte do Dow Jones Factiva](https://www.dowjones.com/contact/) para adicionar os usuários à plataforma do Dow Jones Factiva.</span><span class="sxs-lookup"><span data-stu-id="33b03-188">Please work with Dow [Jones Factiva support team](https://www.dowjones.com/contact/) to add the users in the Dow Jones Factiva platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="33b03-189">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="33b03-189">Assigning the Azure AD test user</span></span>

<span data-ttu-id="33b03-190">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo acesso ao Dow Jones Factiva.</span><span class="sxs-lookup"><span data-stu-id="33b03-190">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Dow Jones Factiva.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="33b03-192">**Para atribuir Brenda Fernandes ao Dow Jones Factiva, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="33b03-192">**To assign Britta Simon to Dow Jones Factiva, perform the following steps:**</span></span>

1. <span data-ttu-id="33b03-193">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="33b03-193">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="33b03-195">Na lista de aplicativos, selecione **Dow Jones Factiva**.</span><span class="sxs-lookup"><span data-stu-id="33b03-195">In the applications list, select **Dow Jones Factiva**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_app.png) 

3. <span data-ttu-id="33b03-197">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="33b03-197">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="33b03-199">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="33b03-199">Click **Add** button.</span></span> <span data-ttu-id="33b03-200">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="33b03-200">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="33b03-202">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="33b03-202">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="33b03-203">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="33b03-203">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="33b03-204">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="33b03-204">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="33b03-205">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="33b03-205">Testing single sign-on</span></span>

<span data-ttu-id="33b03-206">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="33b03-206">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="33b03-207">Quando você clicar no bloco Dow Jones Factiva no Painel de Acesso, deverá fazer logon automaticamente no seu aplicativo Dow Jones Factiva.</span><span class="sxs-lookup"><span data-stu-id="33b03-207">When you click the Dow Jones Factiva tile in the Access Panel, you should get automatically signed-on to your Dow Jones Factiva application.</span></span>
<span data-ttu-id="33b03-208">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="33b03-208">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="33b03-209">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="33b03-209">Additional resources</span></span>

* [<span data-ttu-id="33b03-210">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="33b03-210">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="33b03-211">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="33b03-211">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_203.png

