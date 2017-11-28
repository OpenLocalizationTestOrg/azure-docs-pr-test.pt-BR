---
title: "Tutorial: integração do Azure Active Directory com o Novatus | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Active Directory do Azure e o Novatus."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2f13779-bdb7-4408-9738-be67ed3de4e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/02/2017
ms.author: jeedes
ms.openlocfilehash: ec67e96309a8877e6fb65b30da1501e4f34a9ee4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-novatus"></a><span data-ttu-id="72853-103">Tutorial: Integração do Active Directory do Azure com o Novatus</span><span class="sxs-lookup"><span data-stu-id="72853-103">Tutorial: Azure Active Directory integration with Novatus</span></span>

<span data-ttu-id="72853-104">Neste tutorial, você aprenderá a integrar o Novatus ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="72853-104">In this tutorial, you learn how to integrate Novatus with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="72853-105">A integração do Novatus ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="72853-105">Integrating Novatus with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="72853-106">No AD do Azure, você pode controlar quem tem acesso ao Novatus</span><span class="sxs-lookup"><span data-stu-id="72853-106">You can control in Azure AD who has access to Novatus</span></span>
- <span data-ttu-id="72853-107">Você pode permitir que os usuários façam logon automaticamente no Novatus (Logon Único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="72853-107">You can enable your users to automatically get signed-on to Novatus (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="72853-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="72853-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="72853-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="72853-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72853-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="72853-110">Prerequisites</span></span>

<span data-ttu-id="72853-111">Para configurar a integração do AD do Azure com o Novatus, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="72853-111">To configure Azure AD integration with Novatus, you need the following items:</span></span>

- <span data-ttu-id="72853-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="72853-112">An Azure AD subscription</span></span>
- <span data-ttu-id="72853-113">Uma assinatura habilitada para logon único do Novatus</span><span class="sxs-lookup"><span data-stu-id="72853-113">A Novatus single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="72853-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="72853-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="72853-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="72853-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="72853-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="72853-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="72853-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="72853-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="72853-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="72853-118">Scenario description</span></span>
<span data-ttu-id="72853-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="72853-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="72853-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="72853-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="72853-121">Adicionando o Novatus por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="72853-121">Adding Novatus from the gallery</span></span>
2. <span data-ttu-id="72853-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="72853-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-novatus-from-the-gallery"></a><span data-ttu-id="72853-123">Adicionando o Novatus por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="72853-123">Adding Novatus from the gallery</span></span>
<span data-ttu-id="72853-124">Para configurar a integração do Novatus no AD do Azure, você precisará adicionar o Novatus por meio da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="72853-124">To configure the integration of Novatus into Azure AD, you need to add Novatus from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="72853-125">**Para adicionar o Novatus por meio  galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="72853-125">**To add Novatus from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="72853-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="72853-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="72853-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="72853-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="72853-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="72853-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="72853-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="72853-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="72853-133">Na caixa de pesquisa, digite **Novatus**.</span><span class="sxs-lookup"><span data-stu-id="72853-133">In the search box, type **Novatus**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_search.png)

5. <span data-ttu-id="72853-135">No painel de resultados, selecione **Novatus** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="72853-135">In the results panel, select **Novatus**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="72853-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="72853-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="72853-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Novatus, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="72853-138">In this section, you configure and test Azure AD single sign-on with Novatus based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="72853-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Novatus é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="72853-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Novatus is to a user in Azure AD.</span></span> <span data-ttu-id="72853-140">Em outras palavras, é necessário estabelecer uma relação de vinculação entre um usuário do Azure AD e o usuário relacionado do Novatus.</span><span class="sxs-lookup"><span data-stu-id="72853-140">In other words, a link relationship between an Azure AD user and the related user in Novatus needs to be established.</span></span>

<span data-ttu-id="72853-141">No Novatus, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="72853-141">In Novatus, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="72853-142">Para configurar e testar o logon único do AD do Azure com o Novatus, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="72853-142">To configure and test Azure AD single sign-on with Novatus, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="72853-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="72853-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="72853-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="72853-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="72853-145">**[Criar um usuário de teste do Novatus](#creating-a-novatus-test-user)**: para ter um equivalente de Brenda Fernandes no Novatus que esteja vinculado à representação desse usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="72853-145">**[Creating a Novatus test user](#creating-a-novatus-test-user)** - to have a counterpart of Britta Simon in Novatus that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="72853-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="72853-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="72853-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="72853-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="72853-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="72853-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="72853-149">Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único no seu aplicativo Novatus.</span><span class="sxs-lookup"><span data-stu-id="72853-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Novatus application.</span></span>

<span data-ttu-id="72853-150">**Para configurar o logon único do AD do Azure com o Novatus, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="72853-150">**To configure Azure AD single sign-on with Novatus, perform the following steps:**</span></span>

1. <span data-ttu-id="72853-151">No Portal do Azure, na página de integração de aplicativos do **Novatus**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="72853-151">In the Azure portal, on the **Novatus** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="72853-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="72853-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_samlbase.png)

3. <span data-ttu-id="72853-155">Na seção **URLs e Domínio do Novatus**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="72853-155">On the **Novatus Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_url.png)

     <span data-ttu-id="72853-157">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://sso.novatuscontracts.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="72853-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://sso.novatuscontracts.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="72853-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="72853-158">This value is not real.</span></span> <span data-ttu-id="72853-159">Atualize esse valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="72853-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="72853-160">Para obter esse valor, entre em contato com a [equipe de suporte do cliente Novatus](mailto:jvinci@novatusinc.com).</span><span class="sxs-lookup"><span data-stu-id="72853-160">Contact [Novatus Client support team](mailto:jvinci@novatusinc.com) to get this value.</span></span> 
 


4. <span data-ttu-id="72853-161">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="72853-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_certificate.png) 

5. <span data-ttu-id="72853-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="72853-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-novatus-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="72853-165">Na seção **Configuração do Novatus**, clique em **Configurar o Novatus** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="72853-165">On the **Novatus Configuration** section, click **Configure Novatus** to open **Configure sign-on** window.</span></span> <span data-ttu-id="72853-166">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="72853-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_configure.png) 

7. <span data-ttu-id="72853-168">Para obter o SSO configurado para seu aplicativo, entre em contato com a [equipe de suporte do Novatus](mailto:jvinci@novatusinc.com).</span><span class="sxs-lookup"><span data-stu-id="72853-168">To get SSO configured for your application, contact your [Novatus support team](mailto:jvinci@novatusinc.com).</span></span> <span data-ttu-id="72853-169">Anexe o arquivo de **certificado baixado** ao seu email e compartilhe as **URLs de metadados** (**URL de Logout, ID da Entidade do SAML e URL de Serviço de Logon Único SAML**) com a equipe do Novatus para configurar o SSO no lado deles.</span><span class="sxs-lookup"><span data-stu-id="72853-169">Attach the **downloaded certificate** file to your mail and share the **metadata urls** (**Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL**) with Novatus team to set up SSO on their side.</span></span>

> [!TIP]
> <span data-ttu-id="72853-170">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="72853-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="72853-171">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="72853-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="72853-172">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="72853-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="72853-173">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="72853-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="72853-174">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="72853-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="72853-176">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="72853-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="72853-177">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="72853-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-novatus-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="72853-179">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="72853-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-novatus-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="72853-181">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="72853-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-novatus-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="72853-183">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="72853-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-novatus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="72853-185">a.</span><span class="sxs-lookup"><span data-stu-id="72853-185">a.</span></span> <span data-ttu-id="72853-186">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="72853-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="72853-187">b.</span><span class="sxs-lookup"><span data-stu-id="72853-187">b.</span></span> <span data-ttu-id="72853-188">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="72853-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="72853-189">c.</span><span class="sxs-lookup"><span data-stu-id="72853-189">c.</span></span> <span data-ttu-id="72853-190">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="72853-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="72853-191">d.</span><span class="sxs-lookup"><span data-stu-id="72853-191">d.</span></span> <span data-ttu-id="72853-192">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="72853-192">Click **Create**.</span></span>
 
### <a name="creating-a-novatus-test-user"></a><span data-ttu-id="72853-193">Criar um usuário de teste do Novatus</span><span class="sxs-lookup"><span data-stu-id="72853-193">Creating a Novatus test user</span></span>

<span data-ttu-id="72853-194">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no Novatus.</span><span class="sxs-lookup"><span data-stu-id="72853-194">The objective of this section is to create a user called Britta Simon in Novatus.</span></span> <span data-ttu-id="72853-195">O Novatus dá suporte ao provisionamento just-in-time, que é habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="72853-195">Novatus supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="72853-196">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="72853-196">There is no action item for you in this section.</span></span> <span data-ttu-id="72853-197">Um novo usuário será criado durante uma tentativa de acessar o Novatus, se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="72853-197">A new user will be created during an attempt to access Novatus if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="72853-198">Se precisar criar um usuário manualmente, entre em contato com a [equipe de suporte do Novatus](mailto:jvinci@novatusinc.com).</span><span class="sxs-lookup"><span data-stu-id="72853-198">If you need to create an user manually, you need to contact the [Novatus support team](mailto:jvinci@novatusinc.com).</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="72853-199">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="72853-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="72853-200">Nesta seção, você concederá a Brenda Fernandes acesso ao Novatus para que ela fique habilitada a usar o logon único do Azure.</span><span class="sxs-lookup"><span data-stu-id="72853-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Novatus.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="72853-202">**Para atribuir Brenda Fernandes ao Novatus, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="72853-202">**To assign Britta Simon to Novatus, perform the following steps:**</span></span>

1. <span data-ttu-id="72853-203">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="72853-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="72853-205">Na lista de aplicativos, selecione **Novatus**.</span><span class="sxs-lookup"><span data-stu-id="72853-205">In the applications list, select **Novatus**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_app.png) 

3. <span data-ttu-id="72853-207">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="72853-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="72853-209">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="72853-209">Click **Add** button.</span></span> <span data-ttu-id="72853-210">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="72853-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="72853-212">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="72853-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="72853-213">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="72853-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="72853-214">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="72853-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="72853-215">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="72853-215">Testing single sign-on</span></span>

<span data-ttu-id="72853-216">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="72853-216">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="72853-217">Ao clicar no bloco Novatus no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo Novatus.</span><span class="sxs-lookup"><span data-stu-id="72853-217">When you click the Novatus tile in the Access Panel, you should get automatically signed-on to your Novatus application.</span></span> <span data-ttu-id="72853-218">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="72853-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="72853-219">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="72853-219">Additional resources</span></span>

* [<span data-ttu-id="72853-220">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="72853-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="72853-221">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="72853-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_203.png

