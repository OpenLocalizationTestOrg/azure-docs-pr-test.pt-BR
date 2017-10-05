---
title: "Tutorial: integração do Azure Active Directory com o JobScore | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e JobScore."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 30f51b32-e55c-4c66-96e8-50a2f9c2194a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: f6ed2d362f7b027bfdc38ba2fdaa03948ff5632c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobscore"></a><span data-ttu-id="c8ce8-103">Tutorial: Integração do Azure Active Directory com o JobScore</span><span class="sxs-lookup"><span data-stu-id="c8ce8-103">Tutorial: Azure Active Directory integration with JobScore</span></span>

<span data-ttu-id="c8ce8-104">Neste tutorial, você aprenderá a integrar o JobScore ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="c8ce8-104">In this tutorial, you learn how to integrate JobScore with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c8ce8-105">A integração do JobScore ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="c8ce8-105">Integrating JobScore with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c8ce8-106">Você pode controlar no Azure AD quem tem acesso ao JobScore</span><span class="sxs-lookup"><span data-stu-id="c8ce8-106">You can control in Azure AD who has access to JobScore</span></span>
- <span data-ttu-id="c8ce8-107">Você pode permitir que seus usuários façam logon automaticamente no JobScore (Logon Único) com as contas do Azure AD deles</span><span class="sxs-lookup"><span data-stu-id="c8ce8-107">You can enable your users to automatically get signed-on to JobScore (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c8ce8-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c8ce8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c8ce8-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c8ce8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c8ce8-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c8ce8-110">Prerequisites</span></span>

<span data-ttu-id="c8ce8-111">Para configurar a integração do Azure AD ao JobScore, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="c8ce8-111">To configure Azure AD integration with JobScore, you need the following items:</span></span>

- <span data-ttu-id="c8ce8-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c8ce8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c8ce8-113">Uma assinatura do JobScore habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="c8ce8-113">A JobScore single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c8ce8-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c8ce8-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="c8ce8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c8ce8-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c8ce8-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c8ce8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c8ce8-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="c8ce8-118">Scenario description</span></span>
<span data-ttu-id="c8ce8-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c8ce8-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="c8ce8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c8ce8-121">Adição do JobScore da galeria</span><span class="sxs-lookup"><span data-stu-id="c8ce8-121">Adding JobScore from the gallery</span></span>
2. <span data-ttu-id="c8ce8-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c8ce8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jobscore-from-the-gallery"></a><span data-ttu-id="c8ce8-123">Adição do JobScore da galeria</span><span class="sxs-lookup"><span data-stu-id="c8ce8-123">Adding JobScore from the gallery</span></span>
<span data-ttu-id="c8ce8-124">Para configurar a integração do JobScore ao Azure AD, você precisará adicionar o JobScore da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-124">To configure the integration of JobScore into Azure AD, you need to add JobScore from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c8ce8-125">**Para adicionar o JobScore por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c8ce8-125">**To add JobScore from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c8ce8-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c8ce8-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c8ce8-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="c8ce8-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="c8ce8-133">Na caixa de pesquisa, digite **JobScore**.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-133">In the search box, type **JobScore**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_search.png)

5. <span data-ttu-id="c8ce8-135">No painel de resultados, selecione **JobScore** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-135">In the results panel, select **JobScore**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c8ce8-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c8ce8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c8ce8-138">Nesta seção, você configura e testa o logon único do Azure AD com o JobScore com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-138">In this section, you configure and test Azure AD single sign-on with JobScore based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c8ce8-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do JobScore é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in JobScore is to a user in Azure AD.</span></span> <span data-ttu-id="c8ce8-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no JobScore.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-140">In other words, a link relationship between an Azure AD user and the related user in JobScore needs to be established.</span></span>

<span data-ttu-id="c8ce8-141">No JobScore, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-141">In JobScore, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c8ce8-142">Para configurar e testar o logon único do Azure AD com o JobScore, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="c8ce8-142">To configure and test Azure AD single sign-on with JobScore, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c8ce8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c8ce8-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c8ce8-145">**[Como criar um usuário de teste do JobScore](#creating-a-jobscore-test-user)** – para ter um equivalente de Brenda Fernandes no JobScore que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-145">**[Creating a JobScore test user](#creating-a-jobscore-test-user)** - to have a counterpart of Britta Simon in JobScore that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c8ce8-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c8ce8-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c8ce8-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8ce8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c8ce8-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo JobScore.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your JobScore application.</span></span>

<span data-ttu-id="c8ce8-150">**Para configurar o logon único do Azure AD com o JobScore, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c8ce8-150">**To configure Azure AD single sign-on with JobScore, perform the following steps:**</span></span>

1. <span data-ttu-id="c8ce8-151">No portal do Azure, na página de integração de aplicativos do **JobScore**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-151">In the Azure portal, on the **JobScore** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="c8ce8-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_samlbase.png)

3. <span data-ttu-id="c8ce8-155">Na seção **URLs e Domínio do JobScore**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c8ce8-155">On the **JobScore Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_url.png)

    <span data-ttu-id="c8ce8-157">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://hire.jobscore.com/auth/adfs/<company name>`</span><span class="sxs-lookup"><span data-stu-id="c8ce8-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://hire.jobscore.com/auth/adfs/<company name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c8ce8-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-158">This value is not real.</span></span> <span data-ttu-id="c8ce8-159">Atualize esse valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="c8ce8-160">Para obter esse valor, entre em contato com a [equipe de suporte ao Cliente do JobScore](mailto:support@jobscore.com).</span><span class="sxs-lookup"><span data-stu-id="c8ce8-160">Contact [JobScore Client support team](mailto:support@jobscore.com) to get this value.</span></span> 
 
4. <span data-ttu-id="c8ce8-161">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_certificate.png) 

5. <span data-ttu-id="c8ce8-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="c8ce8-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-jobscore-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c8ce8-165">Para configurar o logon único no lado do **JobScore**, é necessário enviar o **XML de metadados** baixado para a [equipe de suporte do JobScore](mailto:support@jobscore.com).</span><span class="sxs-lookup"><span data-stu-id="c8ce8-165">To configure single sign-on on **JobScore** side, you need to send the downloaded **Metadata XML** to [JobScore support team](mailto:support@jobscore.com).</span></span> 

> [!TIP]
> <span data-ttu-id="c8ce8-166">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="c8ce8-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c8ce8-167">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c8ce8-168">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c8ce8-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c8ce8-169">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c8ce8-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="c8ce8-170">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="c8ce8-172">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c8ce8-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c8ce8-173">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jobscore-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c8ce8-175">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-175">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jobscore-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c8ce8-177">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-177">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jobscore-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c8ce8-179">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c8ce8-179">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jobscore-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c8ce8-181">a.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-181">a.</span></span> <span data-ttu-id="c8ce8-182">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-182">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c8ce8-183">b.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-183">b.</span></span> <span data-ttu-id="c8ce8-184">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-184">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c8ce8-185">c.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-185">c.</span></span> <span data-ttu-id="c8ce8-186">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-186">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c8ce8-187">d.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-187">d.</span></span> <span data-ttu-id="c8ce8-188">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-188">Click **Create**.</span></span>
 
### <a name="creating-a-jobscore-test-user"></a><span data-ttu-id="c8ce8-189">Criando um usuário de teste do JobScore</span><span class="sxs-lookup"><span data-stu-id="c8ce8-189">Creating a JobScore test user</span></span>

<span data-ttu-id="c8ce8-190">Nesta seção, você criará um usuário chamado Brenda Fernandes no JobScore.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-190">In this section, you create a user called Britta Simon in JobScore.</span></span> <span data-ttu-id="c8ce8-191">Trabalhe com a [equipe de suporte do JobScore](mailto:support@jobscore.com) para adicionar os usuários à plataforma do JobScore.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-191">Work with [JobScore support team](mailto:support@jobscore.com) to add the users in the JobScore platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c8ce8-192">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c8ce8-192">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c8ce8-193">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao JobScore.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-193">In this section, you enable Britta Simon to use Azure single sign-on by granting access to JobScore.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="c8ce8-195">**Para atribuir Brenda Fernandes ao JobScore, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c8ce8-195">**To assign Britta Simon to JobScore, perform the following steps:**</span></span>

1. <span data-ttu-id="c8ce8-196">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-196">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="c8ce8-198">Na lista de aplicativos, escolha **JobScore**.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-198">In the applications list, select **JobScore**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_app.png) 

3. <span data-ttu-id="c8ce8-200">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-200">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="c8ce8-202">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-202">Click **Add** button.</span></span> <span data-ttu-id="c8ce8-203">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="c8ce8-205">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-205">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c8ce8-206">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-206">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c8ce8-207">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c8ce8-208">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="c8ce8-208">Testing single sign-on</span></span>

<span data-ttu-id="c8ce8-209">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-209">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c8ce8-210">Ao clicar no bloco do JobScore no Painel de Acesso, você deverá ser conectado automaticamente ao aplicativo do JobScore.</span><span class="sxs-lookup"><span data-stu-id="c8ce8-210">When you click the JobScore tile in the Access Panel, you should get automatically signed-on to your JobScore application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c8ce8-211">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="c8ce8-211">Additional resources</span></span>

* [<span data-ttu-id="c8ce8-212">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="c8ce8-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c8ce8-213">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c8ce8-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_203.png

