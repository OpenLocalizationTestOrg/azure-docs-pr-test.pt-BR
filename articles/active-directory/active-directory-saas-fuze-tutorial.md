---
title: "Tutorial: integração do Azure Active Directory com o Fuze | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Fuze."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9780b4bf-1fd1-48c1-9ceb-f750225ae08a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeedes
ms.openlocfilehash: c7f7b095aac6202a7ec5248ee2bbb109615287a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fuze"></a><span data-ttu-id="40463-103">Tutorial: integração do Azure Active Directory com o Fuze</span><span class="sxs-lookup"><span data-stu-id="40463-103">Tutorial: Azure Active Directory integration with Fuze</span></span>

<span data-ttu-id="40463-104">Neste tutorial, você aprenderá a integrar o Fuze ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="40463-104">In this tutorial, you learn how to integrate Fuze with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="40463-105">A integração do Fuze com o Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="40463-105">Integrating Fuze with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="40463-106">É possível controlar, no Azure AD, quem terá acesso ao Fuze</span><span class="sxs-lookup"><span data-stu-id="40463-106">You can control in Azure AD who has access to Fuze</span></span>
- <span data-ttu-id="40463-107">É possível permitir que seus usuários façam logon automaticamente no Fuze (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="40463-107">You can enable your users to automatically get signed-on to Fuze (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="40463-108">Você pode gerenciar suas contas em um único local - o portal de Gerenciamento do Azure</span><span class="sxs-lookup"><span data-stu-id="40463-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="40463-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="40463-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40463-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="40463-110">Prerequisites</span></span>

<span data-ttu-id="40463-111">Para configurar a integração do Azure AD com o Fuze, são necessários os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="40463-111">To configure Azure AD integration with Fuze, you need the following items:</span></span>

- <span data-ttu-id="40463-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="40463-112">An Azure AD subscription</span></span>
- <span data-ttu-id="40463-113">Uma assinatura do Fuze habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="40463-113">A Fuze single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="40463-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="40463-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="40463-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="40463-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="40463-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="40463-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="40463-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="40463-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="40463-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="40463-118">Scenario description</span></span>
<span data-ttu-id="40463-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="40463-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="40463-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="40463-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="40463-121">Adicionando o Fuze da galeria</span><span class="sxs-lookup"><span data-stu-id="40463-121">Adding Fuze from the gallery</span></span>
2. <span data-ttu-id="40463-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="40463-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-fuze-from-the-gallery"></a><span data-ttu-id="40463-123">Adicionando o Fuze da galeria</span><span class="sxs-lookup"><span data-stu-id="40463-123">Adding Fuze from the gallery</span></span>
<span data-ttu-id="40463-124">Para configurar a integração do Fuze com o Azure AD, é necessário adicionar o Fuze da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="40463-124">To configure the integration of Fuze into Azure AD, you need to add Fuze from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="40463-125">**Para adicionar o Fuze da galeria, siga as etapas abaixo:**</span><span class="sxs-lookup"><span data-stu-id="40463-125">**To add Fuze from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="40463-126">No **[Portal de Gerenciamento do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="40463-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="40463-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="40463-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="40463-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="40463-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="40463-131">Clique em **adicionar** botão na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="40463-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="40463-133">Na caixa de pesquisa, digite **Fuze**.</span><span class="sxs-lookup"><span data-stu-id="40463-133">In the search box, type **Fuze**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_000.png)

5. <span data-ttu-id="40463-135">No painel de resultados, selecione **Fuze** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="40463-135">In the results panel, select **Fuze**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="40463-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="40463-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="40463-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Fuze, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="40463-138">In this section, you configure and test Azure AD single sign-on with Fuze based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="40463-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Fuze é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="40463-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Fuze is to a user in Azure AD.</span></span> <span data-ttu-id="40463-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Fuze.</span><span class="sxs-lookup"><span data-stu-id="40463-140">In other words, a link relationship between an Azure AD user and the related user in Fuze needs to be established.</span></span>

<span data-ttu-id="40463-141">Essa relação de vínculo é estabelecida atribuindo o valor do **nome de usuário** no Azure AD como sendo o valor de **nome de usuário** no Fuze.</span><span class="sxs-lookup"><span data-stu-id="40463-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Fuze.</span></span>

<span data-ttu-id="40463-142">Para configurar e testar o logon único do Azure AD com o Fuze, é necessário concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="40463-142">To configure and test Azure AD single sign-on with Fuze, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="40463-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="40463-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="40463-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** - para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="40463-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="40463-145">**[Criando um usuário de teste do Fuze](#creating-a-fuze-test-user)** – para ter um equivalente de Brenda Fernandes no Fuze que esteja vinculado à representação dela no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="40463-145">**[Creating a Fuze test user](#creating-a-fuze-test-user)** - to have a counterpart of Britta Simon in Fuze that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="40463-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="40463-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="40463-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="40463-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="40463-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="40463-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="40463-149">Nesta seção, você habilitará o logon único do Azure AD no Portal de Gerenciamento do Azure e configurará o logon único em seu aplicativo Fuze.</span><span class="sxs-lookup"><span data-stu-id="40463-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Fuze application.</span></span>

<span data-ttu-id="40463-150">**Para configurar o logon único do Azure AD com o Fuze, siga as etapas abaixo:**</span><span class="sxs-lookup"><span data-stu-id="40463-150">**To configure Azure AD single sign-on with Fuze, perform the following steps:**</span></span>

1. <span data-ttu-id="40463-151">No Portal de Gerenciamento do Azure, na página de integração de aplicativos do **Fuze**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="40463-151">In the Azure Management portal, on the **Fuze** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="40463-153">Na caixa de diálogo **Logon único**, como **Modo**, selecione **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="40463-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_01.png)

3. <span data-ttu-id="40463-155">Na seção **URLs e Domínio do Fuze**, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="40463-155">On the **Fuze Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar o logon único](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_020.png)
    
    <span data-ttu-id="40463-157">Na caixa de texto **URL de Logon**, digite a URL de logon como: `https://www.thinkingphones.com/jetspeed/portal/`</span><span class="sxs-lookup"><span data-stu-id="40463-157">In the **Sign on URL** textbox, type the Sign-on URL as: `https://www.thinkingphones.com/jetspeed/portal/`</span></span>

4.  <span data-ttu-id="40463-158">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="40463-158">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-fuze-tutorial/tutorial_general_400.png)

5. <span data-ttu-id="40463-160">Na seção **Certificado de Autenticação SAML**, clique em **XML de metadados** e, em seguida, salve o arquivo xml em seu computador.</span><span class="sxs-lookup"><span data-stu-id="40463-160">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the xml file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_05.png) 

6. <span data-ttu-id="40463-162">Para configurar o logon único no lado do **Fuze**, é necessário enviar o **XML de metadados** baixado para a [equipe de suporte Fuze](https://www.fuze.com/support).</span><span class="sxs-lookup"><span data-stu-id="40463-162">To configure single sign-on on **Fuze** side, you need to send the downloaded **Metadata XML** to [Fuze support team](https://www.fuze.com/support).</span></span> <span data-ttu-id="40463-163">Isso será configurado para que a conexão de SSO do SAML seja definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="40463-163">They will set this up in order to have the SAML SSO connection set properly on both sides.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="40463-164">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="40463-164">Creating an Azure AD test user</span></span>
<span data-ttu-id="40463-165">O objetivo desta seção é criar um usuário de teste no Portal de Gerenciamento do Azure chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="40463-165">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="40463-167">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="40463-167">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="40463-168">No **portal de Gerenciamento do Azure**, no painel navegação à esquerda, clique em **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="40463-168">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-fuze-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="40463-170">Vá para **usuários e grupos** e clique em **todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="40463-170">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-fuze-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="40463-172">Na parte superior da caixa de diálogo clique **adicionar** para abrir o **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="40463-172">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-fuze-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="40463-174">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="40463-174">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-fuze-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="40463-176">a.</span><span class="sxs-lookup"><span data-stu-id="40463-176">a.</span></span> <span data-ttu-id="40463-177">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="40463-177">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="40463-178">b.</span><span class="sxs-lookup"><span data-stu-id="40463-178">b.</span></span> <span data-ttu-id="40463-179">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="40463-179">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="40463-180">c.</span><span class="sxs-lookup"><span data-stu-id="40463-180">c.</span></span> <span data-ttu-id="40463-181">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="40463-181">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="40463-182">d.</span><span class="sxs-lookup"><span data-stu-id="40463-182">d.</span></span> <span data-ttu-id="40463-183">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="40463-183">Click **Create**.</span></span> 


### <a name="creating-a-fuze-test-user"></a><span data-ttu-id="40463-184">Criando um usuário de teste do Fuze</span><span class="sxs-lookup"><span data-stu-id="40463-184">Creating a Fuze test user</span></span>

<span data-ttu-id="40463-185">O aplicativo Fuze dá suporte ao provisionamento de usuário just-in-time completo. Dessa forma, os usuários serão criados automaticamente quando eles conectarem.</span><span class="sxs-lookup"><span data-stu-id="40463-185">Fuze application supports full Just in time user provision, so users will get created automatically when they sign-in.</span></span> <span data-ttu-id="40463-186">Para outros esclarecimentos, contate o [suporte](https://www.fuze.com/support) Fuze.</span><span class="sxs-lookup"><span data-stu-id="40463-186">For any other clarification, please contact Fuze [support](https://www.fuze.com/support).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="40463-187">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="40463-187">Assigning the Azure AD test user</span></span>

<span data-ttu-id="40463-188">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Fuze.</span><span class="sxs-lookup"><span data-stu-id="40463-188">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Fuze.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="40463-190">**Para atribuir Brenda Fernandes ao Fuze, siga as etapas abaixo:**</span><span class="sxs-lookup"><span data-stu-id="40463-190">**To assign Britta Simon to Fuze, perform the following steps:**</span></span>

1. <span data-ttu-id="40463-191">No portal de gerenciamento do Azure, abra a exibição de aplicativos e, em seguida, navegue até o modo de exibição de diretório e vá para **aplicativos empresariais** e clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="40463-191">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="40463-193">Na lista de aplicativos, selecione **Fuze**.</span><span class="sxs-lookup"><span data-stu-id="40463-193">In the applications list, select **Fuze**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_50.png) 

3. <span data-ttu-id="40463-195">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="40463-195">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="40463-197">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="40463-197">Click **Add** button.</span></span> <span data-ttu-id="40463-198">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="40463-198">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="40463-200">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="40463-200">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="40463-201">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="40463-201">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="40463-202">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="40463-202">Click **Assign** button on **Add Assignment** dialog.</span></span>
    

### <a name="testing-single-sign-on"></a><span data-ttu-id="40463-203">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="40463-203">Testing single sign-on</span></span>

<span data-ttu-id="40463-204">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="40463-204">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="40463-205">Ao clicar no bloco Fuze no Painel de Acesso, seu logon deverá ser feito automaticamente no aplicativo Fuze.</span><span class="sxs-lookup"><span data-stu-id="40463-205">When you click the Fuze tile in the Access Panel, you should get automatically signed-on to your Fuze application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="40463-206">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="40463-206">Additional resources</span></span>

* [<span data-ttu-id="40463-207">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="40463-207">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="40463-208">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="40463-208">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_203.png