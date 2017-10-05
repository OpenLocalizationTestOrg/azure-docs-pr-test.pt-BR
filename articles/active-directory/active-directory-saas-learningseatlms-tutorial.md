---
title: "Tutorial: integração do Azure Active Directory com o Learning Seat LMS | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Learning Seat LMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bb056fcf-4135-478e-85b1-5015d1f07b85
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: jeedes
ms.openlocfilehash: 877e0288fdd1f590acf064c204aff0741539b112
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learning-seat-lms"></a><span data-ttu-id="16f49-103">Tutorial: integração do Azure Active Directory com o Learning Seat LMS</span><span class="sxs-lookup"><span data-stu-id="16f49-103">Tutorial: Azure Active Directory integration with Learning Seat LMS</span></span>

<span data-ttu-id="16f49-104">Neste tutorial, você aprenderá a integrar o Learning Seat LMS ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="16f49-104">In this tutorial, you learn how to integrate Learning Seat LMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="16f49-105">A integração do Learning Seat LMS ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="16f49-105">Integrating Learning Seat LMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="16f49-106">No Azure AD, você pode controlar quem tem acesso ao Learning Seat LMS</span><span class="sxs-lookup"><span data-stu-id="16f49-106">You can control in Azure AD who has access to Learning Seat LMS</span></span>
- <span data-ttu-id="16f49-107">Você pode habilitar seus usuários a fazerem logon automaticamente no Learning Seat LMS (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="16f49-107">You can enable your users to automatically get signed-on to Learning Seat LMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="16f49-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="16f49-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="16f49-109">Se você quiser saber mais detalhes sobre a integração de aplicativos SaaS com o Azure AD, consulte.</span><span class="sxs-lookup"><span data-stu-id="16f49-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="16f49-110">[O que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="16f49-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16f49-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="16f49-111">Prerequisites</span></span>

<span data-ttu-id="16f49-112">Para configurar a integração do Azure AD ao Learning Seat LMS, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="16f49-112">To configure Azure AD integration with Learning Seat LMS, you need the following items:</span></span>

- <span data-ttu-id="16f49-113">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="16f49-113">An Azure AD subscription</span></span>
- <span data-ttu-id="16f49-114">Uma assinatura com logon único habilitado do Learning Seat LMS</span><span class="sxs-lookup"><span data-stu-id="16f49-114">A Learning Seat LMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="16f49-115">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="16f49-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="16f49-116">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="16f49-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="16f49-117">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="16f49-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="16f49-118">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="16f49-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="16f49-119">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="16f49-119">Scenario description</span></span>
<span data-ttu-id="16f49-120">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="16f49-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="16f49-121">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="16f49-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="16f49-122">Como adicionar Learning Seat LMS na galeria</span><span class="sxs-lookup"><span data-stu-id="16f49-122">Adding Learning Seat LMS from the gallery</span></span>
2. <span data-ttu-id="16f49-123">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="16f49-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learning-seat-lms-from-the-gallery"></a><span data-ttu-id="16f49-124">Como adicionar Learning Seat LMS na galeria</span><span class="sxs-lookup"><span data-stu-id="16f49-124">Adding Learning Seat LMS from the gallery</span></span>
<span data-ttu-id="16f49-125">Para configurar a integração do Learning Seat LMS ao Azure AD, você precisará adicionar o Learning Seat LMS por meio da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="16f49-125">To configure the integration of Learning Seat LMS into Azure AD, you need to add Learning Seat LMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="16f49-126">**Para adicionar o Learning Seat LMS por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="16f49-126">**To add Learning Seat LMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="16f49-127">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="16f49-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="16f49-129">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="16f49-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="16f49-130">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="16f49-130">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="16f49-132">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="16f49-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="16f49-134">Na caixa de pesquisa, digite **Learning Seat LMS**.</span><span class="sxs-lookup"><span data-stu-id="16f49-134">In the search box, type **Learning Seat LMS**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_search.png)

5. <span data-ttu-id="16f49-136">No painel de resultados, selecione **Learning Seat LMS** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="16f49-136">In the results panel, select **Learning Seat LMS**, and then click **Add** button to add the application.</span></span>


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="16f49-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="16f49-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="16f49-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Learning Seat LMS, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="16f49-138">In this section, you configure and test Azure AD single sign-on with Learning Seat LMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="16f49-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Learning Seat LMS é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="16f49-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Learning Seat LMS is to a user in Azure AD.</span></span> <span data-ttu-id="16f49-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="16f49-140">In other words, a link relationship between an Azure AD user and the related user in Learning Seat LMS needs to be established.</span></span>

<span data-ttu-id="16f49-141">Essa relação de vínculo é estabelecida ao atribuir o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** no Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="16f49-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Learning Seat LMS.</span></span>

<span data-ttu-id="16f49-142">Para configurar e testar o logon único do Azure AD com o Learning Seat LMS, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="16f49-142">To configure and test Azure AD single sign-on with Learning Seat LMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="16f49-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="16f49-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="16f49-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="16f49-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="16f49-145">**[Criação de um usuário de teste do Learning Seat LMS](#creating-a-learnconnect-test-user)**: para ter um equivalente de Brenda Fernandes no Learning Seat LMS que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="16f49-145">**[Creating a Learning Seat LMS test user](#creating-a-learnconnect-test-user)** - to have a counterpart of Britta Simon in Learning Seat LMS that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="16f49-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="16f49-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="16f49-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="16f49-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="16f49-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="16f49-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="16f49-149">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único em seu aplicativo Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="16f49-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Learning Seat LMS application.</span></span>

<span data-ttu-id="16f49-150">**Para configurar o logon único do Azure AD com o Learning Seat LMS, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="16f49-150">**To configure Azure AD single sign-on with Learning Seat LMS, perform the following steps:**</span></span>

1. <span data-ttu-id="16f49-151">No Portal do Azure, na página de integração de aplicativos do **Learning Seat LMS**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="16f49-151">In the Azure portal, on the **Learning Seat LMS** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="16f49-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="16f49-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_samlbase.png)

3. <span data-ttu-id="16f49-155">Na seção **Domínio e URLs do Learning Seat LMS**, execute as seguintes etapas se desejar configurar o aplicativo no modo iniciado pelo **IDP**:</span><span class="sxs-lookup"><span data-stu-id="16f49-155">On the **Learning Seat LMS Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_url.png)

    <span data-ttu-id="16f49-157">a.</span><span class="sxs-lookup"><span data-stu-id="16f49-157">a.</span></span> <span data-ttu-id="16f49-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<subdomain>.learningseatlms.com`</span><span class="sxs-lookup"><span data-stu-id="16f49-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.learningseatlms.com`</span></span>

    <span data-ttu-id="16f49-159">b.</span><span class="sxs-lookup"><span data-stu-id="16f49-159">b.</span></span> <span data-ttu-id="16f49-160">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<subdomain>.learningseatlms.com/Account/AssertionConsumerService`</span><span class="sxs-lookup"><span data-stu-id="16f49-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.learningseatlms.com/Account/AssertionConsumerService`</span></span>

4. <span data-ttu-id="16f49-161">Marque **Mostrar configurações avançadas de URL**, se quiser configurar o aplicativo no modo iniciado em **SP**:</span><span class="sxs-lookup"><span data-stu-id="16f49-161">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_url2.png)

    <span data-ttu-id="16f49-163">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<subdomain>.learningseatlms.com`</span><span class="sxs-lookup"><span data-stu-id="16f49-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.learningseatlms.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="16f49-164">Esses não são os valores reais.</span><span class="sxs-lookup"><span data-stu-id="16f49-164">These values are not the real values.</span></span> <span data-ttu-id="16f49-165">Atualize esses valores com o Identificador, a URL de Resposta e a URL de Logon reais.</span><span class="sxs-lookup"><span data-stu-id="16f49-165">Update these values with the actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="16f49-166">Contate a [equipe de suporte do Learning Seat](http://help.learningseatlms.com/help) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="16f49-166">Contact [Learning Seat support team](http://help.learningseatlms.com/help) to get these values.</span></span> 

5. <span data-ttu-id="16f49-167">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="16f49-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_certificate.png) 

6. <span data-ttu-id="16f49-169">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="16f49-169">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-learnconnect-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="16f49-171">Para configurar o logon único no lado do **Learning Seat LMS**, é necessário enviar o **XML de Metadados** baixado para a [equipe de suporte do Learning Seat LMS](http://help.learningseatlms.com/help).</span><span class="sxs-lookup"><span data-stu-id="16f49-171">To configure single sign-on on **Learning Seat LMS** side, you need to send the downloaded **Metadata XML** to [Learning Seat support team](http://help.learningseatlms.com/help).</span></span>

> [!TIP]
> <span data-ttu-id="16f49-172">Agora, é possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="16f49-172">You can now read a concise version of these instructions inside the [Azure  portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="16f49-173">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="16f49-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="16f49-174">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD](https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="16f49-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="16f49-175">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="16f49-175">Creating an Azure AD test user</span></span>

<span data-ttu-id="16f49-176">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="16f49-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="16f49-178">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="16f49-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="16f49-179">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="16f49-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="16f49-181">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="16f49-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="16f49-183">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="16f49-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="16f49-185">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="16f49-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="16f49-187">a.</span><span class="sxs-lookup"><span data-stu-id="16f49-187">a.</span></span> <span data-ttu-id="16f49-188">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="16f49-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="16f49-189">b.</span><span class="sxs-lookup"><span data-stu-id="16f49-189">b.</span></span> <span data-ttu-id="16f49-190">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="16f49-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="16f49-191">c.</span><span class="sxs-lookup"><span data-stu-id="16f49-191">c.</span></span> <span data-ttu-id="16f49-192">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="16f49-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="16f49-193">d.</span><span class="sxs-lookup"><span data-stu-id="16f49-193">d.</span></span> <span data-ttu-id="16f49-194">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="16f49-194">Click **Create**.</span></span>
 
### <a name="creating-a-learning-seat-lms-test-user"></a><span data-ttu-id="16f49-195">Criação de um usuário de teste do Learning Seat LMS</span><span class="sxs-lookup"><span data-stu-id="16f49-195">Creating a Learning Seat LMS test user</span></span>

<span data-ttu-id="16f49-196">Nesta seção, você deve criar um usuário chamado Brenda Fernandes no Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="16f49-196">In this section, you create a user called Britta Simon in Learning Seat LMS.</span></span> <span data-ttu-id="16f49-197">Contate a [equipe de suporte do Learning Seat LMS](http://help.learningseatlms.com/help) com todas as informações do usuário para adicionar os usuários no aplicativo Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="16f49-197">Contact [Learning Seat support team](http://help.learningseatlms.com/help) with all the user information to add the users in the Learning Seat LMS application.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="16f49-198">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="16f49-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="16f49-199">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure ao conceder acesso ao Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="16f49-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Learning Seat LMS.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="16f49-201">**Para atribuir Brenda Fernandes ao Learning Seat LMS, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="16f49-201">**To assign Britta Simon to Learning Seat LMS, perform the following steps:**</span></span>

1. <span data-ttu-id="16f49-202">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="16f49-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="16f49-204">Na lista de aplicativos, selecione **Learning Seat LMS**.</span><span class="sxs-lookup"><span data-stu-id="16f49-204">In the applications list, select **Learning Seat LMS**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_app.png) 

3. <span data-ttu-id="16f49-206">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="16f49-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="16f49-208">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="16f49-208">Click **Add** button.</span></span> <span data-ttu-id="16f49-209">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="16f49-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="16f49-211">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="16f49-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="16f49-212">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="16f49-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="16f49-213">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="16f49-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="16f49-214">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="16f49-214">Testing single sign-on</span></span>

<span data-ttu-id="16f49-215">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="16f49-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span> 

<span data-ttu-id="16f49-216">Clique no bloco Learning Seat LMS no Painel de Acesso e você será conectado automaticamente ao seu aplicativo Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="16f49-216">Click the Learning Seat LMS tile in the Access Panel, you will be automatically signed-on to your Learning Seat LMS application.</span></span> <span data-ttu-id="16f49-217">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="16f49-217">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="16f49-218">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="16f49-218">Additional resources</span></span>

* [<span data-ttu-id="16f49-219">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="16f49-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="16f49-220">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="16f49-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_203.png

