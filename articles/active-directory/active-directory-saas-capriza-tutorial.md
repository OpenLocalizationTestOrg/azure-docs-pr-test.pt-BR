---
title: "Tutorial: Integração do Azure Active Directory ao Capriza Platform | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Capriza Platform."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 48d92247-f00a-47b9-8d4e-137028d9e200
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 668c094d5330be1c5f71d51d2e76170dc69d1bce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-capriza-platform"></a><span data-ttu-id="33cfd-103">Tutorial: Integração do Azure Active Directory ao Capriza Platform</span><span class="sxs-lookup"><span data-stu-id="33cfd-103">Tutorial: Azure Active Directory integration with Capriza Platform</span></span>

<span data-ttu-id="33cfd-104">Neste tutorial, você aprende a integrar o Capriza Platform ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="33cfd-104">In this tutorial, you learn how to integrate Capriza Platform with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="33cfd-105">A integração do Capriza Platform ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="33cfd-105">Integrating Capriza Platform with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="33cfd-106">No Azure AD, é possível controlar quem tem acesso ao Capriza Platform</span><span class="sxs-lookup"><span data-stu-id="33cfd-106">You can control in Azure AD who has access to Capriza Platform</span></span>
- <span data-ttu-id="33cfd-107">É possível permitir que os usuários se conectem automaticamente ao Capriza Platform (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="33cfd-107">You can enable your users to automatically get signed-on to Capriza Platform (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="33cfd-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="33cfd-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="33cfd-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="33cfd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33cfd-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="33cfd-110">Prerequisites</span></span>

<span data-ttu-id="33cfd-111">Para configurar a integração do Azure AD ao Capriza Platform, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="33cfd-111">To configure Azure AD integration with Capriza Platform, you need the following items:</span></span>

- <span data-ttu-id="33cfd-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="33cfd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="33cfd-113">Uma assinatura habilitada para logon único do Capriza Platform</span><span class="sxs-lookup"><span data-stu-id="33cfd-113">A Capriza Platform single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="33cfd-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="33cfd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="33cfd-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="33cfd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="33cfd-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="33cfd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="33cfd-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="33cfd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="33cfd-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="33cfd-118">Scenario description</span></span>
<span data-ttu-id="33cfd-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="33cfd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="33cfd-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="33cfd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="33cfd-121">Adicionando o Capriza Platform por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="33cfd-121">Adding Capriza Platform from the gallery</span></span>
2. <span data-ttu-id="33cfd-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="33cfd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-capriza-platform-from-the-gallery"></a><span data-ttu-id="33cfd-123">Adicionando o Capriza Platform por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="33cfd-123">Adding Capriza Platform from the gallery</span></span>
<span data-ttu-id="33cfd-124">Para configurar a integração do Capriza Platform ao Azure AD, você precisa adicionar o Capriza Platform à lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="33cfd-124">To configure the integration of Capriza Platform into Azure AD, you need to add Capriza Platform from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="33cfd-125">**Para adicionar o Capriza Platform por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="33cfd-125">**To add Capriza Platform from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="33cfd-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="33cfd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="33cfd-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="33cfd-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="33cfd-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="33cfd-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="33cfd-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="33cfd-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="33cfd-133">Na caixa de pesquisa, digite **Capriza Platform**.</span><span class="sxs-lookup"><span data-stu-id="33cfd-133">In the search box, type **Capriza Platform**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_search.png)

5. <span data-ttu-id="33cfd-135">No painel de resultados, selecione **Capriza Platform** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="33cfd-135">In the results panel, select **Capriza Platform**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="33cfd-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="33cfd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="33cfd-138">Nesta seção, você configura e testa o logon único do Azure AD com o Capriza Platform, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="33cfd-138">In this section, you configure and test Azure AD single sign-on with Capriza Platform based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="33cfd-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Capriza Platform é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="33cfd-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Capriza Platform is to a user in Azure AD.</span></span> <span data-ttu-id="33cfd-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Capriza Platform.</span><span class="sxs-lookup"><span data-stu-id="33cfd-140">In other words, a link relationship between an Azure AD user and the related user in Capriza Platform needs to be established.</span></span>

<span data-ttu-id="33cfd-141">No Capriza Platform, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="33cfd-141">In Capriza Platform, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="33cfd-142">Para configurar e testar o logon único do Azure AD com o Capriza Platform, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="33cfd-142">To configure and test Azure AD single sign-on with Capriza Platform, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="33cfd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="33cfd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="33cfd-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="33cfd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="33cfd-145">**[Criando um usuário de teste do Capriza Platform](#creating-a-capriza-platform-test-user)** – para ter um equivalente de Brenda Fernandes no Capriza Platform que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="33cfd-145">**[Creating a Capriza Platform test user](#creating-a-capriza-platform-test-user)** - to have a counterpart of Britta Simon in Capriza Platform that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="33cfd-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="33cfd-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="33cfd-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="33cfd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="33cfd-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="33cfd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="33cfd-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Capriza Platform.</span><span class="sxs-lookup"><span data-stu-id="33cfd-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Capriza Platform application.</span></span>

<span data-ttu-id="33cfd-150">**Para configurar o logon único do Azure AD com o Capriza Platform, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="33cfd-150">**To configure Azure AD single sign-on with Capriza Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="33cfd-151">No portal do Azure, na página de integração do aplicativo do **Capriza Platform**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="33cfd-151">In the Azure portal, on the **Capriza Platform** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="33cfd-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="33cfd-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_samlbase.png)

3. <span data-ttu-id="33cfd-155">Na seção **Domínio e URLs do Capriza Platform**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="33cfd-155">On the **Capriza Platform Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_url.png)

    <span data-ttu-id="33cfd-157">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<companyname>.capriza.com/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="33cfd-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.capriza.com/<tenantid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="33cfd-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="33cfd-158">This value is not real.</span></span> <span data-ttu-id="33cfd-159">Atualize esse valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="33cfd-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="33cfd-160">Contate a [equipe de suporte ao Cliente do Capriza Platform](mailTo:support@capriza.com) para obter esse valor.</span><span class="sxs-lookup"><span data-stu-id="33cfd-160">Contact [Capriza Platform Client support team](mailTo:support@capriza.com) to get this value.</span></span> 

4. <span data-ttu-id="33cfd-161">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="33cfd-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_certificate.png) 

5. <span data-ttu-id="33cfd-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="33cfd-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-capriza-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="33cfd-165">Na seção **Configuração do Capriza Platform**, clique em **Configurar o Capriza Platform** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="33cfd-165">On the **Capriza Platform Configuration** section, click **Configure Capriza Platform** to open **Configure sign-on** window.</span></span> <span data-ttu-id="33cfd-166">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="33cfd-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_configure.png) 

7. <span data-ttu-id="33cfd-168">Para configurar o logon único no lado do **Capriza Platform**, é necessário enviar o **Certificado** baixado, a **URL de Saída**, **a ID da Entidade SAML** e a **URL do Serviço de Logon Único SAML** para a [equipe de suporte do Capriza Platform](mailTo:support@capriza.com).</span><span class="sxs-lookup"><span data-stu-id="33cfd-168">To configure single sign-on on **Capriza Platform** side, you need to send the downloaded **Certificate**, **Sign-Out URL**, **SAML Entity ID** and **SAML Single Sign-On Service URL** to [Capriza Platform support team](mailTo:support@capriza.com).</span></span> <span data-ttu-id="33cfd-169">Eles definem essa configuração para ter a conexão de SSO do SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="33cfd-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="33cfd-170">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="33cfd-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="33cfd-171">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="33cfd-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="33cfd-172">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="33cfd-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="33cfd-173">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="33cfd-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="33cfd-174">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="33cfd-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="33cfd-176">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="33cfd-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="33cfd-177">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="33cfd-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-capriza-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="33cfd-179">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="33cfd-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-capriza-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="33cfd-181">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="33cfd-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-capriza-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="33cfd-183">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="33cfd-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-capriza-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="33cfd-185">a.</span><span class="sxs-lookup"><span data-stu-id="33cfd-185">a.</span></span> <span data-ttu-id="33cfd-186">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="33cfd-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="33cfd-187">b.</span><span class="sxs-lookup"><span data-stu-id="33cfd-187">b.</span></span> <span data-ttu-id="33cfd-188">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="33cfd-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="33cfd-189">c.</span><span class="sxs-lookup"><span data-stu-id="33cfd-189">c.</span></span> <span data-ttu-id="33cfd-190">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="33cfd-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="33cfd-191">d.</span><span class="sxs-lookup"><span data-stu-id="33cfd-191">d.</span></span> <span data-ttu-id="33cfd-192">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="33cfd-192">Click **Create**.</span></span>
 
### <a name="creating-a-capriza-platform-test-user"></a><span data-ttu-id="33cfd-193">Criando um usuário de teste do Capriza Platform</span><span class="sxs-lookup"><span data-stu-id="33cfd-193">Creating a Capriza Platform test user</span></span>

<span data-ttu-id="33cfd-194">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no Capriza.</span><span class="sxs-lookup"><span data-stu-id="33cfd-194">The objective of this section is to create a user called Britta Simon in Capriza.</span></span> <span data-ttu-id="33cfd-195">O Capriza dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="33cfd-195">Capriza supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="33cfd-196">**Verifique se o nome de domínio está configurado no Capriza para o provisionamento de usuário. Depois disso, somente o provisionamento de usuário just-in-time funciona.**</span><span class="sxs-lookup"><span data-stu-id="33cfd-196">**Please make sure that your domain name is configured with Capriza for user provisioning. After that only the just-in-time user provisioning will work.**</span></span>

<span data-ttu-id="33cfd-197">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="33cfd-197">There is no action item for you in this section.</span></span> <span data-ttu-id="33cfd-198">Um novo usuário será criado durante uma tentativa de acessar o Capriza, caso ainda não exista.</span><span class="sxs-lookup"><span data-stu-id="33cfd-198">A new user will be created during an attempt to access Capriza if it doesn't exist yet.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="33cfd-199">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="33cfd-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="33cfd-200">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Capriza Platform.</span><span class="sxs-lookup"><span data-stu-id="33cfd-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Capriza Platform.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="33cfd-202">**Para atribuir Brenda Fernandes ao Capriza Platform, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="33cfd-202">**To assign Britta Simon to Capriza Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="33cfd-203">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="33cfd-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="33cfd-205">Na lista de aplicativos, selecione **Capriza Platform**.</span><span class="sxs-lookup"><span data-stu-id="33cfd-205">In the applications list, select **Capriza Platform**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_app.png) 

3. <span data-ttu-id="33cfd-207">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="33cfd-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="33cfd-209">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="33cfd-209">Click **Add** button.</span></span> <span data-ttu-id="33cfd-210">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="33cfd-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="33cfd-212">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="33cfd-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="33cfd-213">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="33cfd-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="33cfd-214">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="33cfd-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="33cfd-215">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="33cfd-215">Testing single sign-on</span></span>

<span data-ttu-id="33cfd-216">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="33cfd-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="33cfd-217">Quando você clicar no bloco Capriza Platform no Painel de Acesso, deverá ser automaticamente conectado ao aplicativo Capriza Platform.</span><span class="sxs-lookup"><span data-stu-id="33cfd-217">When you click the Capriza Platform tile in the Access Panel, you should get automatically signed-on to your Capriza application.</span></span> <span data-ttu-id="33cfd-218">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="33cfd-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="33cfd-219">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="33cfd-219">Additional resources</span></span>

* [<span data-ttu-id="33cfd-220">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="33cfd-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="33cfd-221">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="33cfd-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_203.png

