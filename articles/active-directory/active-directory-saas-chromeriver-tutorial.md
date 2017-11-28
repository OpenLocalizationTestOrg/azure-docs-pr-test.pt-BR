---
title: "Tutorial: integração do Azure Active Directory com o Chromeriver | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Chromeriver."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 445c5600-e340-4724-a9cb-3cfaf5770b70
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: jeedes
ms.openlocfilehash: 6ee3316a8258ee27e4fa4ec22badbf4fe047a844
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-chromeriver"></a><span data-ttu-id="c5b3f-103">Tutorial: Integração do Active Directory do Azure ao Chromeriver</span><span class="sxs-lookup"><span data-stu-id="c5b3f-103">Tutorial: Azure Active Directory integration with Chromeriver</span></span>

<span data-ttu-id="c5b3f-104">Neste tutorial, você aprende a integrar o Chromeriver ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="c5b3f-104">In this tutorial, you learn how to integrate Chromeriver with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c5b3f-105">A integração do Chromeriver ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="c5b3f-105">Integrating Chromeriver with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c5b3f-106">No Azure AD, é possível controlar quem tem acesso ao Chromeriver</span><span class="sxs-lookup"><span data-stu-id="c5b3f-106">You can control in Azure AD who has access to Chromeriver</span></span>
- <span data-ttu-id="c5b3f-107">É possível permitir que os usuários se conectem automaticamente ao Chromeriver (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5b3f-107">You can enable your users to automatically get signed-on to Chromeriver (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c5b3f-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c5b3f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c5b3f-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c5b3f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c5b3f-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c5b3f-110">Prerequisites</span></span>

<span data-ttu-id="c5b3f-111">Para configurar a integração do Azure AD ao Chromeriver, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="c5b3f-111">To configure Azure AD integration with Chromeriver, you need the following items:</span></span>

- <span data-ttu-id="c5b3f-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c5b3f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c5b3f-113">Uma assinatura habilitada para logon único do Chromeriver</span><span class="sxs-lookup"><span data-stu-id="c5b3f-113">A Chromeriver single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c5b3f-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c5b3f-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="c5b3f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c5b3f-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c5b3f-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c5b3f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c5b3f-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="c5b3f-118">Scenario description</span></span>
<span data-ttu-id="c5b3f-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c5b3f-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="c5b3f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c5b3f-121">Adicionando o Chromeriver por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="c5b3f-121">Adding Chromeriver from the gallery</span></span>
2. <span data-ttu-id="c5b3f-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c5b3f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-chromeriver-from-the-gallery"></a><span data-ttu-id="c5b3f-123">Adicionando o Chromeriver por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="c5b3f-123">Adding Chromeriver from the gallery</span></span>
<span data-ttu-id="c5b3f-124">Para configurar a integração do Chromeriver ao Azure AD, você precisa adicionar o Chromeriver à lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-124">To configure the integration of Chromeriver into Azure AD, you need to add Chromeriver from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c5b3f-125">**Para adicionar o Chromeriver por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c5b3f-125">**To add Chromeriver from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c5b3f-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c5b3f-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c5b3f-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="c5b3f-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="c5b3f-133">Na caixa de pesquisa, digite **Chromeriver**.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-133">In the search box, type **Chromeriver**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-chromeriver-tutorial/tutorial_chromeriver_search.png)

5. <span data-ttu-id="c5b3f-135">No painel de resultados, selecione **Chromeriver** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-135">In the results panel, select **Chromeriver**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-chromeriver-tutorial/tutorial_chromeriver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c5b3f-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c5b3f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c5b3f-138">Nesta seção, você configura e testa o logon único do Azure AD com o Chromeriver, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-138">In this section, you configure and test Azure AD single sign-on with Chromeriver based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c5b3f-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Chromeriver é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Chromeriver is to a user in Azure AD.</span></span> <span data-ttu-id="c5b3f-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Chromeriver.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-140">In other words, a link relationship between an Azure AD user and the related user in Chromeriver needs to be established.</span></span>

<span data-ttu-id="c5b3f-141">No Chromeriver, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-141">In Chromeriver, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c5b3f-142">Para configurar e testar o logon único do Azure AD com o Chromeriver, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="c5b3f-142">To configure and test Azure AD single sign-on with Chromeriver, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c5b3f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c5b3f-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c5b3f-145">**[Criando um usuário de teste do Chromeriver](#creating-a-chromeriver-test-user)** – para ter um equivalente de Brenda Fernandes no Chromeriver que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-145">**[Creating a Chromeriver test user](#creating-a-chromeriver-test-user)** - to have a counterpart of Britta Simon in Chromeriver that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c5b3f-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c5b3f-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c5b3f-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5b3f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c5b3f-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Chromeriver.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Chromeriver application.</span></span>

<span data-ttu-id="c5b3f-150">**Para configurar o logon único do Azure AD com o Chromeriver, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c5b3f-150">**To configure Azure AD single sign-on with Chromeriver, perform the following steps:**</span></span>

1. <span data-ttu-id="c5b3f-151">No portal do Azure, na página de integração do aplicativo do **Chromeriver**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-151">In the Azure portal, on the **Chromeriver** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="c5b3f-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-chromeriver-tutorial/tutorial_chromeriver_samlbase.png)

3. <span data-ttu-id="c5b3f-155">Na seção **Domínio e URLs do Chromeriver**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c5b3f-155">On the **Chromeriver Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-chromeriver-tutorial/tutorial_chromeriver_url.png)

    <span data-ttu-id="c5b3f-157">a.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-157">a.</span></span> <span data-ttu-id="c5b3f-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<subdomain>.chromeriver.com`</span><span class="sxs-lookup"><span data-stu-id="c5b3f-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.chromeriver.com`</span></span>

    <span data-ttu-id="c5b3f-159">b.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-159">b.</span></span> <span data-ttu-id="c5b3f-160">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<subdomain>.chromeriver.com/login/sso/saml/consume?customerId=<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="c5b3f-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.chromeriver.com/login/sso/saml/consume?customerId=<uniqueid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c5b3f-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-161">These values are not real.</span></span> <span data-ttu-id="c5b3f-162">Atualize esses valores com o Identificador e a URL de Resposta reais.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="c5b3f-163">Contate a [equipe de suporte do Chromeriver](https://www.chromeriver.com/services/support) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-163">Contact [Chromeriver support team](https://www.chromeriver.com/services/support) to get these values.</span></span>
 


4. <span data-ttu-id="c5b3f-164">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-chromeriver-tutorial/tutorial_chromeriver_certificate.png) 

5. <span data-ttu-id="c5b3f-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="c5b3f-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-chromeriver-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c5b3f-168">Para configurar o logon único no lado do **Chromeriver**, é necessário enviar o **XML de Metadados** baixado para a [equipe de suporte do Chromeriver](https://www.chromeriver.com/services/support).</span><span class="sxs-lookup"><span data-stu-id="c5b3f-168">To configure single sign-on on **Chromeriver** side, you need to send the downloaded **Metadata XML** to [Chromeriver support team](https://www.chromeriver.com/services/support).</span></span> <span data-ttu-id="c5b3f-169">Você receberá uma notificação quando o SSO tiver sido habilitado para sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-169">You will get a notification when SSO has been enabled for your subscription.</span></span>

> [!TIP]
> <span data-ttu-id="c5b3f-170">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="c5b3f-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c5b3f-171">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c5b3f-172">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c5b3f-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c5b3f-173">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c5b3f-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="c5b3f-174">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="c5b3f-176">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c5b3f-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c5b3f-177">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-chromeriver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c5b3f-179">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-chromeriver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c5b3f-181">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-chromeriver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c5b3f-183">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c5b3f-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-chromeriver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c5b3f-185">a.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-185">a.</span></span> <span data-ttu-id="c5b3f-186">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c5b3f-187">b.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-187">b.</span></span> <span data-ttu-id="c5b3f-188">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c5b3f-189">c.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-189">c.</span></span> <span data-ttu-id="c5b3f-190">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c5b3f-191">d.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-191">d.</span></span> <span data-ttu-id="c5b3f-192">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-192">Click **Create**.</span></span>
 
### <a name="creating-a-chromeriver-test-user"></a><span data-ttu-id="c5b3f-193">Criando um usuário de teste do Chromeriver</span><span class="sxs-lookup"><span data-stu-id="c5b3f-193">Creating a Chromeriver test user</span></span>

<span data-ttu-id="c5b3f-194">Para permitir que os usuários do Azure AD façam logon no Chromeriver, eles devem ser provisionados no Chromeriver.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-194">To enable Azure AD users to log in to Chromeriver, they must be provisioned into Chromeriver.</span></span>  

<span data-ttu-id="c5b3f-195">No caso do Chromeriver, as contas de usuário precisam ser criadas pela [equipe de suporte do Chromeriver](https://www.chromeriver.com/services/support).</span><span class="sxs-lookup"><span data-stu-id="c5b3f-195">In the case of Chromeriver, the user accounts need to be created by your [Chromeriver support team](https://www.chromeriver.com/services/support).</span></span>

>[!NOTE]
><span data-ttu-id="c5b3f-196">Você pode usar qualquer outra ferramenta de criação da conta de usuário do Chromeriver ou as APIs fornecidas pelo Chromeriver para provisionar as contas de usuário do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-196">You can use any other Chromeriver user account creation tools or APIs provided by Chromeriver to provision Azure Active Directory user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c5b3f-197">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c5b3f-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c5b3f-198">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Chromeriver.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Chromeriver.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="c5b3f-200">**Para atribuir Brenda Fernandes ao Chromeriver, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c5b3f-200">**To assign Britta Simon to Chromeriver, perform the following steps:**</span></span>

1. <span data-ttu-id="c5b3f-201">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="c5b3f-203">Na lista de aplicativos, selecione **Chromeriver**.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-203">In the applications list, select **Chromeriver**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-chromeriver-tutorial/tutorial_chromeriver_app.png) 

3. <span data-ttu-id="c5b3f-205">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="c5b3f-207">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-207">Click **Add** button.</span></span> <span data-ttu-id="c5b3f-208">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="c5b3f-210">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c5b3f-211">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c5b3f-212">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c5b3f-213">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="c5b3f-213">Testing single sign-on</span></span>

<span data-ttu-id="c5b3f-214">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-214">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c5b3f-215">Quando você clicar no bloco Chromeriver no Painel de Acesso, deverá ser automaticamente conectado ao aplicativo Chromeriver.</span><span class="sxs-lookup"><span data-stu-id="c5b3f-215">When you click the Chromeriver tile in the Access Panel, you should get automatically signed-on to your Chromeriver application.</span></span> <span data-ttu-id="c5b3f-216">Para obter mais detalhes sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c5b3f-216">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c5b3f-217">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="c5b3f-217">Additional resources</span></span>

* [<span data-ttu-id="c5b3f-218">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="c5b3f-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c5b3f-219">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c5b3f-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_203.png

