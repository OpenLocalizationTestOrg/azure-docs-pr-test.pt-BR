---
title: "Tutorial: Integração do Azure Active Directory com o Innotas | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Innotas."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: eb9e9c2c-4b09-4177-bbab-423fd657448e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 674d01b2c0818dc10fdab5844a23c5ebf29bb2d2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-innotas"></a><span data-ttu-id="c9cdc-103">Tutorial: Integração do Active Directory do Azure com o Innotas</span><span class="sxs-lookup"><span data-stu-id="c9cdc-103">Tutorial: Azure Active Directory integration with Innotas</span></span>

<span data-ttu-id="c9cdc-104">Neste tutorial, você aprenderá a integrar o Innotas ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="c9cdc-104">In this tutorial, you learn how to integrate Innotas with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c9cdc-105">A integração do Innotas ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="c9cdc-105">Integrating Innotas with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c9cdc-106">Você pode controlar no Azure AD quem terá acesso ao Innotas</span><span class="sxs-lookup"><span data-stu-id="c9cdc-106">You can control in Azure AD who has access to Innotas</span></span>
- <span data-ttu-id="c9cdc-107">Você pode permitir que seus usuários entrem automaticamente no Innotas (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9cdc-107">You can enable your users to automatically get signed-on to Innotas (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c9cdc-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c9cdc-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c9cdc-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c9cdc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c9cdc-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c9cdc-110">Prerequisites</span></span>

<span data-ttu-id="c9cdc-111">Para configurar a integração do Azure AD ao Innotas, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="c9cdc-111">To configure Azure AD integration with Innotas, you need the following items:</span></span>

- <span data-ttu-id="c9cdc-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c9cdc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c9cdc-113">Uma assinatura habilitada para logon único do Innotas</span><span class="sxs-lookup"><span data-stu-id="c9cdc-113">An Innotas single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c9cdc-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c9cdc-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="c9cdc-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c9cdc-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c9cdc-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c9cdc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c9cdc-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="c9cdc-118">Scenario description</span></span>

<span data-ttu-id="c9cdc-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c9cdc-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="c9cdc-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c9cdc-121">Como adicionar o Innotas por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="c9cdc-121">Adding Innotas from the gallery</span></span>
2. <span data-ttu-id="c9cdc-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c9cdc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-innotas-from-the-gallery"></a><span data-ttu-id="c9cdc-123">Como adicionar o Innotas por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="c9cdc-123">Adding Innotas from the gallery</span></span>
<span data-ttu-id="c9cdc-124">Para configurar a integração do Innotas ao Azure AD, você precisará adicionar o Innotas da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-124">To configure the integration of Innotas into Azure AD, you need to add Innotas from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c9cdc-125">**Para adicionar o Innotas por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c9cdc-125">**To add Innotas from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c9cdc-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c9cdc-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c9cdc-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="c9cdc-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="c9cdc-133">Na caixa de pesquisa, digite **Innotas**.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-133">In the search box, type **Innotas**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_search.png)

5. <span data-ttu-id="c9cdc-135">No painel de resultados, selecione **Innotas** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-135">In the results panel, select **Innotas**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c9cdc-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c9cdc-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="c9cdc-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Innotas, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-138">In this section, you configure and test Azure AD single sign-on with Innotas based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c9cdc-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Innotas é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Innotas is to a user in Azure AD.</span></span> <span data-ttu-id="c9cdc-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Innotas.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-140">In other words, a link relationship between an Azure AD user and the related user in Innotas needs to be established.</span></span>

<span data-ttu-id="c9cdc-141">No Innotas, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-141">In Innotas, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c9cdc-142">Para configurar e testar o logon único do Azure AD com o Innotas, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="c9cdc-142">To configure and test Azure AD single sign-on with Innotas, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c9cdc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c9cdc-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c9cdc-145">**[Criação de um usuário de teste do Innotas](#creating-an-innotas-test-user)**: para ter um equivalente de Brenda Fernandes no Innotas, que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-145">**[Creating an Innotas test user](#creating-an-innotas-test-user)** - to have a counterpart of Britta Simon in Innotas that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c9cdc-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c9cdc-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c9cdc-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9cdc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c9cdc-149">Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único no seu aplicativo Innotas.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Innotas application.</span></span>

<span data-ttu-id="c9cdc-150">**Para configurar o logon único do Azure AD com o Innotas, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c9cdc-150">**To configure Azure AD single sign-on with Innotas, perform the following steps:**</span></span>

1. <span data-ttu-id="c9cdc-151">No Portal do Azure, na página de integração de aplicativos do **Innotas**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-151">In the Azure portal, on the **Innotas** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="c9cdc-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_samlbase.png)

3. <span data-ttu-id="c9cdc-155">Na seção **URLs e Domínio do Innotas**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c9cdc-155">On the **Innotas Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_url.png)

    <span data-ttu-id="c9cdc-157">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<tenant-name>.Innotas.com`</span><span class="sxs-lookup"><span data-stu-id="c9cdc-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.Innotas.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c9cdc-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-158">This value is not real.</span></span> <span data-ttu-id="c9cdc-159">Atualize esse valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="c9cdc-160">Para obter esse valor, entre em contato com a [equipe de suporte do cliente Innotas](https://www.innotas.com/contact).</span><span class="sxs-lookup"><span data-stu-id="c9cdc-160">Contact [Innotas Client support team](https://www.innotas.com/contact) to get this value.</span></span> 
 
4. <span data-ttu-id="c9cdc-161">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_certificate.png) 

5. <span data-ttu-id="c9cdc-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="c9cdc-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-innotas-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c9cdc-165">Para configurar o logon único no lado do **Innotas**, é necessário enviar o **XML de Metadados** baixado para a [equipe de suporte Innotas](https://www.innotas.com/contact).</span><span class="sxs-lookup"><span data-stu-id="c9cdc-165">To configure single sign-on on **Innotas** side, you need to send the downloaded **Metadata XML** to [Innotas support team](https://www.innotas.com/contact).</span></span> <span data-ttu-id="c9cdc-166">Eles definem essa configuração para ter a conexão de SSO do SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="c9cdc-167">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="c9cdc-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c9cdc-168">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c9cdc-169">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c9cdc-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c9cdc-170">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c9cdc-170">Creating an Azure AD test user</span></span>

<span data-ttu-id="c9cdc-171">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="c9cdc-173">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c9cdc-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c9cdc-174">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-innotas-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c9cdc-176">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-innotas-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c9cdc-178">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-innotas-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c9cdc-180">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c9cdc-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-innotas-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c9cdc-182">a.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-182">a.</span></span> <span data-ttu-id="c9cdc-183">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c9cdc-184">b.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-184">b.</span></span> <span data-ttu-id="c9cdc-185">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c9cdc-186">c.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-186">c.</span></span> <span data-ttu-id="c9cdc-187">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c9cdc-188">d.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-188">d.</span></span> <span data-ttu-id="c9cdc-189">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-189">Click **Create**.</span></span>
 
### <a name="creating-an-innotas-test-user"></a><span data-ttu-id="c9cdc-190">Criação de um usuário de teste do Innotas</span><span class="sxs-lookup"><span data-stu-id="c9cdc-190">Creating an Innotas test user</span></span>

<span data-ttu-id="c9cdc-191">Não há nenhum item de ação para a configuração de provisionamento de usuário para o Innotas.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-191">There is no action item for you to configure user provisioning to Innotas.</span></span>  
<span data-ttu-id="c9cdc-192">Quando um usuário atribuído tenta fazer logon no Innotas usando o painel de acesso, o Innotas verifica se o usuário existe.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-192">When an assigned user tries to log in to Innotas using the access panel, Innotas checks whether the user exists.</span></span>  

>[!NOTE]
><span data-ttu-id="c9cdc-193">Se não houver conta de usuário ainda, ela é criada automaticamente pelo Innotas.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-193">If there is no user account available yet, it is automatically created by Innotas.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c9cdc-194">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c9cdc-194">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c9cdc-195">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure ao conceder acesso ao Fuse.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Innotas.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="c9cdc-197">**Para atribuir Brenda Fernandes ao Innotas, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c9cdc-197">**To assign Britta Simon to Innotas, perform the following steps:**</span></span>

1. <span data-ttu-id="c9cdc-198">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="c9cdc-200">Na lista de aplicativos, selecione **Innotas**.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-200">In the applications list, select **Innotas**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_app.png) 

3. <span data-ttu-id="c9cdc-202">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-202">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="c9cdc-204">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-204">Click **Add** button.</span></span> <span data-ttu-id="c9cdc-205">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="c9cdc-207">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c9cdc-208">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c9cdc-209">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c9cdc-210">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="c9cdc-210">Testing single sign-on</span></span>

<span data-ttu-id="c9cdc-211">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-211">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c9cdc-212">Ao clicar no bloco Innotas no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo Innotas.</span><span class="sxs-lookup"><span data-stu-id="c9cdc-212">When you click the Innotas tile in the Access Panel, you should get automatically signed-on to your Innotas application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c9cdc-213">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="c9cdc-213">Additional resources</span></span>

* [<span data-ttu-id="c9cdc-214">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="c9cdc-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c9cdc-215">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c9cdc-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_203.png

