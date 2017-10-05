---
title: "Tutorial: Integração do Azure Active Directory com o Learning at Work | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Learning at Work."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d607174-bea1-4f40-8233-54cabe02c66a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: jeedes
ms.openlocfilehash: 941832740689c583a8e857d706c35f3076fa754f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learning-at-work"></a><span data-ttu-id="d9487-103">Tutorial: Integração do Azure Active Directory com o Learning at Work</span><span class="sxs-lookup"><span data-stu-id="d9487-103">Tutorial: Azure Active Directory integration with Learning at Work</span></span>

<span data-ttu-id="d9487-104">Neste tutorial, você aprenderá a integrar o Learning at Work ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="d9487-104">In this tutorial, you learn how to integrate Learning at Work with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d9487-105">A integração do Learning at Work ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="d9487-105">Integrating Learning at Work with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d9487-106">No Azure AD, você pode controlar quem tem acesso ao Learning at Work</span><span class="sxs-lookup"><span data-stu-id="d9487-106">You can control in Azure AD who has access to Learning at Work</span></span>
- <span data-ttu-id="d9487-107">Você pode habilitar seus usuários a fazerem logon automaticamente no Learning at Work (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9487-107">You can enable your users to automatically get signed-on to Learning at Work (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d9487-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d9487-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d9487-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d9487-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9487-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d9487-110">Prerequisites</span></span>

<span data-ttu-id="d9487-111">Para configurar a integração do Azure AD ao Learning at Work, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="d9487-111">To configure Azure AD integration with Learning at Work, you need the following items:</span></span>

- <span data-ttu-id="d9487-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d9487-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d9487-113">Uma assinatura com logon único habilitado do Learning at Work</span><span class="sxs-lookup"><span data-stu-id="d9487-113">A Learning at Work single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d9487-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="d9487-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d9487-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="d9487-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d9487-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="d9487-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d9487-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d9487-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d9487-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="d9487-118">Scenario description</span></span>
<span data-ttu-id="d9487-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="d9487-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d9487-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="d9487-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d9487-121">Adicionar Learning at Work da galeria</span><span class="sxs-lookup"><span data-stu-id="d9487-121">Adding Learning at Work from the gallery</span></span>
2. <span data-ttu-id="d9487-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d9487-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learning-at-work-from-the-gallery"></a><span data-ttu-id="d9487-123">Adicionar Learning at Work da galeria</span><span class="sxs-lookup"><span data-stu-id="d9487-123">Adding Learning at Work from the gallery</span></span>
<span data-ttu-id="d9487-124">Para configurar a integração do Learning at Work ao Azure AD, você precisa adicionar o Learning at Work por meio da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="d9487-124">To configure the integration of Learning at Work into Azure AD, you need to add Learning at Work from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d9487-125">**Para adicionar o Learning at Work por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="d9487-125">**To add Learning at Work from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d9487-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d9487-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d9487-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="d9487-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d9487-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="d9487-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="d9487-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d9487-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="d9487-133">Na caixa de pesquisa, digite **Learning at Work**.</span><span class="sxs-lookup"><span data-stu-id="d9487-133">In the search box, type **Learning at Work**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_search.png)

5. <span data-ttu-id="d9487-135">No painel de resultados, selecione **Learning at Work** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d9487-135">In the results panel, select **Learning at Work**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d9487-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d9487-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d9487-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Learning at Work, com base em uma usuária de teste chamada "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="d9487-138">In this section, you configure and test Azure AD single sign-on with Learning at Work based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d9487-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Learning at Work é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9487-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Learning at Work is to a user in Azure AD.</span></span> <span data-ttu-id="d9487-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Learning at Work.</span><span class="sxs-lookup"><span data-stu-id="d9487-140">In other words, a link relationship between an Azure AD user and the related user in Learning at Work needs to be established.</span></span>

<span data-ttu-id="d9487-141">Essa relação de vínculo é estabelecida atribuindo o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** no Learning at Work.</span><span class="sxs-lookup"><span data-stu-id="d9487-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Learning at Work.</span></span>

<span data-ttu-id="d9487-142">Para configurar e testar o logon único do Azure AD com o Learning at Work, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="d9487-142">To configure and test Azure AD single sign-on with Learning at Work, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d9487-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="d9487-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d9487-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="d9487-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d9487-145">**[Criação de um usuário de teste do Learning at Work](#creating-a-learning-at-work-test-user)** – para ter um equivalente de Brenda Fernandes no Learning at Work que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9487-145">**[Creating a Learning at Work test user](#creating-a-learning-at-work-test-user)** - to have a counterpart of Britta Simon in Learning at Work that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d9487-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="d9487-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d9487-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="d9487-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d9487-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9487-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d9487-149">Nesta seção, você habilitará o logon único do Azure AD no portal do Azure e configurará o logon único no aplicativo Learning at Work.</span><span class="sxs-lookup"><span data-stu-id="d9487-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Learning at Work application.</span></span>

<span data-ttu-id="d9487-150">**Para configurar o logon único do Azure AD com o Learning at Work, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="d9487-150">**To configure Azure AD single sign-on with Learning at Work, perform the following steps:**</span></span>

1. <span data-ttu-id="d9487-151">No Portal do Azure, na página de integração de aplicativos do **Learning at Work**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="d9487-151">In the Azure portal, on the **Learning at Work** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="d9487-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="d9487-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_samlbase.png)

3. <span data-ttu-id="d9487-155">Na seção **Domínio e URLs do Learning at Work**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="d9487-155">On the **Learning at Work Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_url.png)

    <span data-ttu-id="d9487-157">a.</span><span class="sxs-lookup"><span data-stu-id="d9487-157">a.</span></span> <span data-ttu-id="d9487-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<subdomain>.sabacloud.com/Saba/Web/<company code>`</span><span class="sxs-lookup"><span data-stu-id="d9487-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.sabacloud.com/Saba/Web/<company code>`</span></span>

    <span data-ttu-id="d9487-159">b.</span><span class="sxs-lookup"><span data-stu-id="d9487-159">b.</span></span> <span data-ttu-id="d9487-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<subdomain>.sabacloud.com/Saba/saml/SSO/alias/<company name>`</span><span class="sxs-lookup"><span data-stu-id="d9487-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.sabacloud.com/Saba/saml/SSO/alias/<company name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d9487-161">Esses não são os valores reais.</span><span class="sxs-lookup"><span data-stu-id="d9487-161">These values are not the real.</span></span> <span data-ttu-id="d9487-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="d9487-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d9487-163">Contate a [equipe de suporte do Cliente Learning at Work](https://www.learninga-z.com/site/contact/support) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="d9487-163">Contact [Learning at Work Client support team](https://www.learninga-z.com/site/contact/support) to get these values.</span></span> 
 
4. <span data-ttu-id="d9487-164">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="d9487-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_certificate.png) 

5. <span data-ttu-id="d9487-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="d9487-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d9487-168">Na seção **Configuração do Learning at Work**, clique em **Configurar Learning at Work** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="d9487-168">On the **Learning at Work Configuration** section, click **Configure Learning at Work** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d9487-169">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="d9487-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_configure.png) 

7. <span data-ttu-id="d9487-171">Para configurar o logon único no lado do **Learning at Work**, é necessário enviar o **XML de Metadados** baixado, a **ID da Entidade SAML**, a **URL do Serviço de Logon Único do SAML** e a **URL de Saída** para a [equipe de suporte do Learning at Work](https://www.learninga-z.com/site/contact/support).</span><span class="sxs-lookup"><span data-stu-id="d9487-171">To configure single sign-on on **Learning at Work** side, you need to send the downloaded **Metadata XML**, **SAML Entity ID**, **SAML Single Sign-On Service URL**, and **Sign-Out URL** to [Learning at Work support](https://www.learninga-z.com/site/contact/support).</span></span>

> [!TIP]
> <span data-ttu-id="d9487-172">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="d9487-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d9487-173">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="d9487-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d9487-174">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d9487-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d9487-175">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d9487-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="d9487-176">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="d9487-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="d9487-178">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="d9487-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d9487-179">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d9487-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d9487-181">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="d9487-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d9487-183">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d9487-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d9487-185">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="d9487-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d9487-187">a.</span><span class="sxs-lookup"><span data-stu-id="d9487-187">a.</span></span> <span data-ttu-id="d9487-188">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="d9487-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d9487-189">b.</span><span class="sxs-lookup"><span data-stu-id="d9487-189">b.</span></span> <span data-ttu-id="d9487-190">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="d9487-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d9487-191">c.</span><span class="sxs-lookup"><span data-stu-id="d9487-191">c.</span></span> <span data-ttu-id="d9487-192">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="d9487-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d9487-193">d.</span><span class="sxs-lookup"><span data-stu-id="d9487-193">d.</span></span> <span data-ttu-id="d9487-194">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d9487-194">Click **Create**.</span></span>
 
### <a name="creating-a-learning-at-work-test-user"></a><span data-ttu-id="d9487-195">Criar um usuário de teste do Learning at Work</span><span class="sxs-lookup"><span data-stu-id="d9487-195">Creating a Learning at Work test user</span></span>

<span data-ttu-id="d9487-196">Nesta seção, você deve criar uma usuária chamada Brenda Fernandes no Learning at Work.</span><span class="sxs-lookup"><span data-stu-id="d9487-196">In this section, you create a user called Britta Simon in Learning at Work.</span></span> <span data-ttu-id="d9487-197">Trabalhe com a [equipe de suporte do Learning at Work](https://www.learninga-z.com/site/contact/support) para adicionar usuários na plataforma Learning at Work.</span><span class="sxs-lookup"><span data-stu-id="d9487-197">Work with [Learning at Work support](https://www.learninga-z.com/site/contact/support) to add the users in the Learning at Work platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d9487-198">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d9487-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d9487-199">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Learning at Work.</span><span class="sxs-lookup"><span data-stu-id="d9487-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Learning at Work.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="d9487-201">**Para atribuir Brenda Fernandes ao Learning at Work, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="d9487-201">**To assign Britta Simon to Learning at Work, perform the following steps:**</span></span>

1. <span data-ttu-id="d9487-202">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="d9487-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="d9487-204">Na lista de aplicativos, selecione **Learning at Work**.</span><span class="sxs-lookup"><span data-stu-id="d9487-204">In the applications list, select **Learning at Work**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_app.png) 

3. <span data-ttu-id="d9487-206">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="d9487-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="d9487-208">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d9487-208">Click **Add** button.</span></span> <span data-ttu-id="d9487-209">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d9487-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="d9487-211">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="d9487-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d9487-212">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d9487-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d9487-213">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d9487-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d9487-214">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="d9487-214">Testing single sign-on</span></span>

<span data-ttu-id="d9487-215">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="d9487-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d9487-216">Quando você clicar no bloco Learning at Work no Painel de Acesso, deverá ser automaticamente conectado ao aplicativo Learning at Work.</span><span class="sxs-lookup"><span data-stu-id="d9487-216">When you click the Learning at Work tile in the Access Panel, you should get automatically signed-on to your Learning at Work application.</span></span>
<span data-ttu-id="d9487-217">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d9487-217">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d9487-218">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="d9487-218">Additional resources</span></span>

* [<span data-ttu-id="d9487-219">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="d9487-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d9487-220">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d9487-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_203.png

