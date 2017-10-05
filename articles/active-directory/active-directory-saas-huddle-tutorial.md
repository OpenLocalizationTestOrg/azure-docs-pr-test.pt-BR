---
title: "Tutorial: Integração do Azure Active Directory ao Huddle | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Huddle."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8389ba4c-f5f8-4ede-b2f4-32eae844ceb0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 59d4019545d39ec76bf401696338140f430630c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-huddle"></a><span data-ttu-id="f69a3-103">Tutorial: integração do Active Directory do Azure ao Huddle</span><span class="sxs-lookup"><span data-stu-id="f69a3-103">Tutorial: Azure Active Directory integration with Huddle</span></span>

<span data-ttu-id="f69a3-104">Neste tutorial, você aprenderá a integrar o Huddle ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="f69a3-104">In this tutorial, you learn how to integrate Huddle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f69a3-105">A integração do Huddle ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="f69a3-105">Integrating Huddle with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f69a3-106">Você pode controlar no Azure AD quem terá acesso ao Huddle</span><span class="sxs-lookup"><span data-stu-id="f69a3-106">You can control in Azure AD who has access to Huddle</span></span>
- <span data-ttu-id="f69a3-107">Você pode permitir que usuários façam logon automaticamente no Huddle (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f69a3-107">You can enable your users to automatically get signed-on to Huddle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f69a3-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f69a3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f69a3-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f69a3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f69a3-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f69a3-110">Prerequisites</span></span>

<span data-ttu-id="f69a3-111">Para configurar a integração do Azure AD ao Huddle, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="f69a3-111">To configure Azure AD integration with Huddle, you need the following items:</span></span>

- <span data-ttu-id="f69a3-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f69a3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f69a3-113">Uma assinatura habilitada para logon único do Huddle</span><span class="sxs-lookup"><span data-stu-id="f69a3-113">A Huddle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f69a3-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="f69a3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f69a3-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="f69a3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f69a3-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="f69a3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f69a3-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f69a3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f69a3-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="f69a3-118">Scenario description</span></span>

<span data-ttu-id="f69a3-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="f69a3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f69a3-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="f69a3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f69a3-121">Como adicionar o Huddle por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="f69a3-121">Adding Huddle from the gallery</span></span>
2. <span data-ttu-id="f69a3-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f69a3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-huddle-from-the-gallery"></a><span data-ttu-id="f69a3-123">Como adicionar o Huddle por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="f69a3-123">Adding Huddle from the gallery</span></span>
<span data-ttu-id="f69a3-124">Para configurar a integração do Huddle ao Azure AD, você precisará adicionar o Huddle por meio da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="f69a3-124">To configure the integration of Huddle into Azure AD, you need to add Huddle from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f69a3-125">**Para adicionar o Huddle por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f69a3-125">**To add Huddle from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f69a3-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f69a3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f69a3-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="f69a3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f69a3-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f69a3-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="f69a3-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f69a3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="f69a3-133">Na caixa de pesquisa, digite **Huddle**.</span><span class="sxs-lookup"><span data-stu-id="f69a3-133">In the search box, type **Huddle**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_search.png)

5. <span data-ttu-id="f69a3-135">No painel de resultados, selecione **Huddle** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f69a3-135">In the results panel, select **Huddle**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f69a3-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f69a3-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="f69a3-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Huddle, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="f69a3-138">In this section, you configure and test Azure AD single sign-on with Huddle based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f69a3-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Huddle é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f69a3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Huddle is to a user in Azure AD.</span></span> <span data-ttu-id="f69a3-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Huddle.</span><span class="sxs-lookup"><span data-stu-id="f69a3-140">In other words, a link relationship between an Azure AD user and the related user in Huddle needs to be established.</span></span>

<span data-ttu-id="f69a3-141">No Huddle, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="f69a3-141">In Huddle, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f69a3-142">Para configurar e testar o logon único do Azure AD com o Huddle, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="f69a3-142">To configure and test Azure AD single sign-on with Huddle, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f69a3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="f69a3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>

2. <span data-ttu-id="f69a3-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="f69a3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>

3. <span data-ttu-id="f69a3-145">**[Criar um usuário de teste do Huddle](#creating-a-huddle-test-user)**: para ter um equivalente de Brenda Fernandes no Huddle que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f69a3-145">**[Creating a Huddle test user](#creating-a-huddle-test-user)** - to have a counterpart of Britta Simon in Huddle that is linked to the Azure AD representation of user.</span></span>

4. <span data-ttu-id="f69a3-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="f69a3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>

5. <span data-ttu-id="f69a3-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="f69a3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f69a3-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f69a3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f69a3-149">Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único no aplicativo Huddle.</span><span class="sxs-lookup"><span data-stu-id="f69a3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Huddle application.</span></span>

<span data-ttu-id="f69a3-150">**Para configurar o logon único do Azure AD com o Huddle, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f69a3-150">**To configure Azure AD single sign-on with Huddle, perform the following steps:**</span></span>

1. <span data-ttu-id="f69a3-151">No Portal do Azure, na página de integração de aplicativos do **Huddle**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="f69a3-151">In the Azure portal, on the **Huddle** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="f69a3-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="f69a3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_samlbase.png)

3. <span data-ttu-id="f69a3-155">Na seção **URLs e Domínio do Huddle**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f69a3-155">On the **Huddle Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_url.png)

    <span data-ttu-id="f69a3-157">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `http://<company name>.huddle.com`</span><span class="sxs-lookup"><span data-stu-id="f69a3-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://<company name>.huddle.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f69a3-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="f69a3-158">This value is not real.</span></span> <span data-ttu-id="f69a3-159">Atualize esse valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="f69a3-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="f69a3-160">Para obter esse valor, entre em contato com a [equipe de suporte do cliente Huddle](https://huddle.zendesk.com).</span><span class="sxs-lookup"><span data-stu-id="f69a3-160">Contact [Huddle Client support team](https://huddle.zendesk.com) to get this value.</span></span> 

4. <span data-ttu-id="f69a3-161">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="f69a3-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_certificate.png) 

5. <span data-ttu-id="f69a3-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="f69a3-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-huddle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f69a3-165">Na seção **Configuração do Huddle**, clique em **Configurar Huddle** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="f69a3-165">On the **Huddle Configuration** section, click **Configure Huddle** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f69a3-166">Copie a **ID da Entidade SAML e a URL do Serviço de Logon Único do SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="f69a3-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_configure.png) 
    
7. <span data-ttu-id="f69a3-168">Para configurar o logon único no lado do Huddle, é necessário enviar o **Certificado** baixado, a **URL do Serviço de Logon Único SAML** e a **ID da Entidade SAML** para a [equipe de suporte do Huddle](https://huddle.zendesk.com).</span><span class="sxs-lookup"><span data-stu-id="f69a3-168">To configure single sign-on on Huddle side, you need to send the downloaded  **Certificate**, **SAML Single Sign-On Service URL**, and **SAML Entity ID** to [Huddle Client support team](https://huddle.zendesk.com).</span></span> <span data-ttu-id="f69a3-169">Eles definem essa configuração para ter a conexão de SSO do SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="f69a3-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>  
   
    >[!NOTE]
    > <span data-ttu-id="f69a3-170">O logon único precisa ser habilitado pela equipe de suporte do Huddle.</span><span class="sxs-lookup"><span data-stu-id="f69a3-170">Single sign-on needs to be enabled by the Huddle support team.</span></span> <span data-ttu-id="f69a3-171">Assim que a configuração for concluída, você receberá uma notificação.</span><span class="sxs-lookup"><span data-stu-id="f69a3-171">You get a notification when the configuration has been completed.</span></span> 
    > 

> [!TIP]
> <span data-ttu-id="f69a3-172">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="f69a3-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f69a3-173">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="f69a3-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f69a3-174">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f69a3-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 
   
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f69a3-175">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f69a3-175">Creating an Azure AD test user</span></span>

<span data-ttu-id="f69a3-176">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="f69a3-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="f69a3-178">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f69a3-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f69a3-179">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f69a3-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-huddle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f69a3-181">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="f69a3-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-huddle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f69a3-183">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f69a3-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-huddle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f69a3-185">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f69a3-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-huddle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f69a3-187">a.</span><span class="sxs-lookup"><span data-stu-id="f69a3-187">a.</span></span> <span data-ttu-id="f69a3-188">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="f69a3-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f69a3-189">b.</span><span class="sxs-lookup"><span data-stu-id="f69a3-189">b.</span></span> <span data-ttu-id="f69a3-190">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="f69a3-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f69a3-191">c.</span><span class="sxs-lookup"><span data-stu-id="f69a3-191">c.</span></span> <span data-ttu-id="f69a3-192">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="f69a3-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f69a3-193">d.</span><span class="sxs-lookup"><span data-stu-id="f69a3-193">d.</span></span> <span data-ttu-id="f69a3-194">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f69a3-194">Click **Create**.</span></span>
 
### <a name="creating-a-huddle-test-user"></a><span data-ttu-id="f69a3-195">Criação de um usuário de teste do Huddle</span><span class="sxs-lookup"><span data-stu-id="f69a3-195">Creating a Huddle test user</span></span>

<span data-ttu-id="f69a3-196">Para permitir que os usuários do Azure AD façam logon no Huddle, eles deverão ser provisionados no Huddle.</span><span class="sxs-lookup"><span data-stu-id="f69a3-196">To enable Azure AD users to log in to Huddle, they must be provisioned into Huddle.</span></span> <span data-ttu-id="f69a3-197">No caso do Huddle, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="f69a3-197">In the case of Huddle, provisioning is a manual task.</span></span>

<span data-ttu-id="f69a3-198">**Para configurar o provisionamento de usuários, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f69a3-198">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="f69a3-199">Faça logon em seu site de empresa do **Huddle** como administrador.</span><span class="sxs-lookup"><span data-stu-id="f69a3-199">Log in to your **Huddle** company site as administrator.</span></span>
2. <span data-ttu-id="f69a3-200">Clique em **Espaço de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="f69a3-200">Click **Workspace**.</span></span>
3. <span data-ttu-id="f69a3-201">Clique em **Pessoas \> Convidar Pessoas**.</span><span class="sxs-lookup"><span data-stu-id="f69a3-201">Click **People \> Invite People**.</span></span>
   
   <span data-ttu-id="f69a3-202">![Pessoas](./media/active-directory-saas-huddle-tutorial/IC787838.png "Pessoas")</span><span class="sxs-lookup"><span data-stu-id="f69a3-202">![People](./media/active-directory-saas-huddle-tutorial/IC787838.png "People")</span></span>

4. <span data-ttu-id="f69a3-203">Na seção **Criar novo convite** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f69a3-203">In the **Create a new invitation** section, perform the following steps:</span></span>
   
   <span data-ttu-id="f69a3-204">![Novo Convite](./media/active-directory-saas-huddle-tutorial/IC787839.png "Novo Convite")</span><span class="sxs-lookup"><span data-stu-id="f69a3-204">![New Invitation](./media/active-directory-saas-huddle-tutorial/IC787839.png "New Invitation")</span></span>
   
   <span data-ttu-id="f69a3-205">a.</span><span class="sxs-lookup"><span data-stu-id="f69a3-205">a.</span></span> <span data-ttu-id="f69a3-206">Na lista **Escolha uma equipe para convidar pessoas para participar**, selecione **equipe**.</span><span class="sxs-lookup"><span data-stu-id="f69a3-206">In the **Choose a team to invite people to join** list, select **team**.</span></span>

   <span data-ttu-id="f69a3-207">b.</span><span class="sxs-lookup"><span data-stu-id="f69a3-207">b.</span></span> <span data-ttu-id="f69a3-208">Insira o **Endereço de Email** de uma conta do Azure AD válida que você deseja provisionar na caixa de texto **Inserir endereço de email para pessoas que você gostaria de convidar**.</span><span class="sxs-lookup"><span data-stu-id="f69a3-208">Type the **Email Address** of a valid Azure AD account you want to provision in to **Enter email address for people you'd like to invite** textbox.</span></span>

   <span data-ttu-id="f69a3-209">c.</span><span class="sxs-lookup"><span data-stu-id="f69a3-209">c.</span></span> <span data-ttu-id="f69a3-210">Clique em **Convidar**.</span><span class="sxs-lookup"><span data-stu-id="f69a3-210">Click **Invite**.</span></span>   
   
    >[!NOTE]
    > <span data-ttu-id="f69a3-211">O titular da conta do Azure AD receberá um email com um link de confirmação de conta para que ela se torne ativa.</span><span class="sxs-lookup"><span data-stu-id="f69a3-211">The Azure AD account holder will receive an email including a link to confirm the account before it becomes active.</span></span> 
    > 

>[!NOTE]
><span data-ttu-id="f69a3-212">É possível usar qualquer outra ferramenta de criação da conta de usuário do Huddle ou as APIs fornecidas pelo Huddle para provisionar as contas de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f69a3-212">You can use any other Huddle user account creation tools or APIs provided by Huddle to provision Azure AD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f69a3-213">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f69a3-213">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f69a3-214">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure ao conceder acesso ao Huddle.</span><span class="sxs-lookup"><span data-stu-id="f69a3-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Huddle.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="f69a3-216">**Para atribuir Brenda Fernandes ao Huddle, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f69a3-216">**To assign Britta Simon to Huddle, perform the following steps:**</span></span>

1. <span data-ttu-id="f69a3-217">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f69a3-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="f69a3-219">Na lista de aplicativos, selecione **Huddle**.</span><span class="sxs-lookup"><span data-stu-id="f69a3-219">In the applications list, select **Huddle**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_app.png) 

3. <span data-ttu-id="f69a3-221">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="f69a3-221">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="f69a3-223">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f69a3-223">Click **Add** button.</span></span> <span data-ttu-id="f69a3-224">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f69a3-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="f69a3-226">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="f69a3-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f69a3-227">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f69a3-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f69a3-228">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f69a3-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f69a3-229">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="f69a3-229">Testing single sign-on</span></span>

<span data-ttu-id="f69a3-230">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="f69a3-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f69a3-231">Ao clicar no bloco Huddle no Painel de Acesso, você deverá ser conectado automaticamente à página de logon do aplicativo de Huddle.</span><span class="sxs-lookup"><span data-stu-id="f69a3-231">When you click the Huddle tile in the Access Panel, you should get automatically login page of Huddle application.</span></span>
<span data-ttu-id="f69a3-232">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f69a3-232">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f69a3-233">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="f69a3-233">Additional resources</span></span>

* [<span data-ttu-id="f69a3-234">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="f69a3-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f69a3-235">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f69a3-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_04.png
[100]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_203.png
