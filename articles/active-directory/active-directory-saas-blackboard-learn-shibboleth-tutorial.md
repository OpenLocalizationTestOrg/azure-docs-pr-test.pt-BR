---
title: "Tutorial: integração do Azure Active Directory ao Blackboard Learn - Shibboleth | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Blackboard Learn - Shibboleth."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e435cbb4-c0f0-400e-943c-5c923fa8ddf2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jeedes
ms.openlocfilehash: 014b0671eb8604235a823c2cf4324a49d94df702
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-blackboard-learn---shibboleth"></a><span data-ttu-id="097c7-103">Tutorial: integração do Azure Active Directory ao Blackboard Learn - Shibboleth</span><span class="sxs-lookup"><span data-stu-id="097c7-103">Tutorial: Azure Active Directory integration with Blackboard Learn - Shibboleth</span></span>

<span data-ttu-id="097c7-104">Neste tutorial, você aprenderá a integrar o Blackboard Learn - Shibboleth ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="097c7-104">In this tutorial, you learn how to integrate Blackboard Learn - Shibboleth with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="097c7-105">A integração do Blackboard Learn - Shibboleth ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="097c7-105">Integrating Blackboard Learn - Shibboleth with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="097c7-106">Você pode controlar no Azure AD quem tem acesso ao Blackboard Learn - Shibboleth</span><span class="sxs-lookup"><span data-stu-id="097c7-106">You can control in Azure AD who has access to Blackboard Learn - Shibboleth</span></span>
- <span data-ttu-id="097c7-107">Você pode permitir que seus usuários façam logon automaticamente no Blackboard Learn - Shibboleth (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="097c7-107">You can enable your users to automatically get signed-on to Blackboard Learn - Shibboleth (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="097c7-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="097c7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="097c7-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="097c7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="097c7-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="097c7-110">Prerequisites</span></span>

<span data-ttu-id="097c7-111">Para configurar a integração do Azure AD ao Blackboard Learn - Shibboleth, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="097c7-111">To configure Azure AD integration with Blackboard Learn - Shibboleth, you need the following items:</span></span>

- <span data-ttu-id="097c7-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="097c7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="097c7-113">Uma assinatura com logon único habilitado do Blackboard Learn - Shibboleth</span><span class="sxs-lookup"><span data-stu-id="097c7-113">A Blackboard Learn - Shibboleth single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="097c7-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="097c7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="097c7-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="097c7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="097c7-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="097c7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="097c7-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="097c7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="097c7-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="097c7-118">Scenario description</span></span>
<span data-ttu-id="097c7-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="097c7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="097c7-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="097c7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="097c7-121">Adicionar o Blackboard Learn - Shibboleth da galeria</span><span class="sxs-lookup"><span data-stu-id="097c7-121">Adding Blackboard Learn - Shibboleth from the gallery</span></span>
2. <span data-ttu-id="097c7-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="097c7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-blackboard-learn---shibboleth-from-the-gallery"></a><span data-ttu-id="097c7-123">Adicionar o Blackboard Learn - Shibboleth da galeria</span><span class="sxs-lookup"><span data-stu-id="097c7-123">Adding Blackboard Learn - Shibboleth from the gallery</span></span>
<span data-ttu-id="097c7-124">Para configurar a integração do Blackboard Learn - Shibboleth ao Azure AD, você precisará adicionar o Blackboard Learn - Shibboleth da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="097c7-124">To configure the integration of Blackboard Learn - Shibboleth into Azure AD, you need to add Blackboard Learn - Shibboleth from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="097c7-125">**Para adicionar o Blackboard Learn - Shibboleth por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="097c7-125">**To add Blackboard Learn - Shibboleth from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="097c7-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="097c7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="097c7-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="097c7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="097c7-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="097c7-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="097c7-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="097c7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="097c7-133">Na caixa de pesquisa, digite **Blackboard Learn - Shibboleth**.</span><span class="sxs-lookup"><span data-stu-id="097c7-133">In the search box, type **Blackboard Learn - Shibboleth**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_search.png)

5. <span data-ttu-id="097c7-135">No painel de resultados, selecione **Blackboard Learn – Shibboleth** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="097c7-135">In the results panel, select **Blackboard Learn - Shibboleth**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="097c7-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="097c7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="097c7-138">Nesta seção, você configura e testa o logon único do Azure AD com o Blackboard Learn – Shibboleth, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="097c7-138">In this section, you configure and test Azure AD single sign-on with Blackboard Learn - Shibboleth based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="097c7-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Blackboard Learn - Shibboleth é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="097c7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Blackboard Learn - Shibboleth is to a user in Azure AD.</span></span> <span data-ttu-id="097c7-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Blackboard Learn - Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="097c7-140">In other words, a link relationship between an Azure AD user and the related user in Blackboard Learn - Shibboleth needs to be established.</span></span>

<span data-ttu-id="097c7-141">No Blackboard Learn – Shibboleth, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="097c7-141">In Blackboard Learn - Shibboleth, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="097c7-142">Para configurar e testar o logon único do Azure AD o com Blackboard Learn - Shibboleth, você precisará realizar as seguintes tarefas básicas:</span><span class="sxs-lookup"><span data-stu-id="097c7-142">To configure and test Azure AD single sign-on with Blackboard Learn - Shibboleth, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="097c7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="097c7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="097c7-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="097c7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="097c7-145">**[Criando um usuário de teste do Blackboard Learn – Shibboleth](#creating-a-blackboard-learn---shibboleth-test-user)** – para ter um equivalente de Brenda Fernandes no Blackboard Learn – Shibboleth que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="097c7-145">**[Creating a Blackboard Learn - Shibboleth test user](#creating-a-blackboard-learn---shibboleth-test-user)** - to have a counterpart of Britta Simon in Blackboard Learn - Shibboleth that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="097c7-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="097c7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="097c7-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="097c7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="097c7-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="097c7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="097c7-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Blackboard Learn – Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="097c7-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Blackboard Learn - Shibboleth application.</span></span>

<span data-ttu-id="097c7-150">**Para configurar o logon único do Azure AD com o Blackboard Learn - Shibboleth, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="097c7-150">**To configure Azure AD single sign-on with Blackboard Learn - Shibboleth, perform the following steps:**</span></span>

1. <span data-ttu-id="097c7-151">No portal do Azure, na página de integração do aplicativo do **Blackboard Learn – Shibboleth**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="097c7-151">In the Azure portal, on the **Blackboard Learn - Shibboleth** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="097c7-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="097c7-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_samlbase.png)

3. <span data-ttu-id="097c7-155">Na seção **Domínio e URLs do Blackboard Learn – Shibboleth**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="097c7-155">On the **Blackboard Learn - Shibboleth Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_url.png)

    <span data-ttu-id="097c7-157">a.</span><span class="sxs-lookup"><span data-stu-id="097c7-157">a.</span></span> <span data-ttu-id="097c7-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/Login`</span><span class="sxs-lookup"><span data-stu-id="097c7-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/Login`</span></span>

    <span data-ttu-id="097c7-159">b.</span><span class="sxs-lookup"><span data-stu-id="097c7-159">b.</span></span> <span data-ttu-id="097c7-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<yourblackoardlearnserver>.blackboardlearn.com/shibboleth-sp`</span><span class="sxs-lookup"><span data-stu-id="097c7-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/shibboleth-sp`</span></span>

    <span data-ttu-id="097c7-161">c.</span><span class="sxs-lookup"><span data-stu-id="097c7-161">c.</span></span> <span data-ttu-id="097c7-162">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/SAML2/POST`</span><span class="sxs-lookup"><span data-stu-id="097c7-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/SAML2/POST`</span></span>
 
    > [!NOTE] 
    > <span data-ttu-id="097c7-163">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="097c7-163">These values are not real.</span></span> <span data-ttu-id="097c7-164">Atualize esses valores com o Identificador real, a URL de Resposta e a URL de Entrada.</span><span class="sxs-lookup"><span data-stu-id="097c7-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="097c7-165">Contate a [equipe de suporte ao Cliente do Blackboard Learn – Shibboleth](https://www.blackboard.com/forms/contact-us_form.aspx) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="097c7-165">Contact [Blackboard Learn - Shibboleth Client support team](https://www.blackboard.com/forms/contact-us_form.aspx) to get these values.</span></span> 

4. <span data-ttu-id="097c7-166">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="097c7-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_certificate.png) 

5. <span data-ttu-id="097c7-168">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="097c7-168">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="097c7-170">Na seção **Configuração do Blackboard Learn – Shibboleth**, clique em **Configurar o Blackboard Learn – Shibboleth** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="097c7-170">On the **Blackboard Learn - Shibboleth Configuration** section, click **Configure Blackboard Learn - Shibboleth** to open **Configure sign-on** window.</span></span> <span data-ttu-id="097c7-171">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="097c7-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_configure.png) 

7. <span data-ttu-id="097c7-173">Para configurar o logon único no lado do **Blackboard Learn – Shibboleth**, é necessário enviar o **XML de Metadados** baixado e a **URL de Saída, ID da Entidade SAML e URL do Serviço de Logon Único SAML** para a [equipe de suporte do Blackboard Learn – Shibboleth](https://www.blackboard.com/forms/contact-us_form.aspx).</span><span class="sxs-lookup"><span data-stu-id="097c7-173">To configure single sign-on on **Blackboard Learn - Shibboleth** side, you need to send the downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Blackboard Learn - Shibboleth support team](https://www.blackboard.com/forms/contact-us_form.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="097c7-174">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="097c7-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="097c7-175">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="097c7-175">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="097c7-176">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="097c7-176">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="097c7-177">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="097c7-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="097c7-178">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="097c7-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="097c7-180">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="097c7-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="097c7-181">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="097c7-181">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="097c7-183">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="097c7-183">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="097c7-185">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="097c7-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="097c7-187">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="097c7-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="097c7-189">a.</span><span class="sxs-lookup"><span data-stu-id="097c7-189">a.</span></span> <span data-ttu-id="097c7-190">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="097c7-190">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="097c7-191">b.</span><span class="sxs-lookup"><span data-stu-id="097c7-191">b.</span></span> <span data-ttu-id="097c7-192">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="097c7-192">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="097c7-193">c.</span><span class="sxs-lookup"><span data-stu-id="097c7-193">c.</span></span> <span data-ttu-id="097c7-194">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="097c7-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="097c7-195">d.</span><span class="sxs-lookup"><span data-stu-id="097c7-195">d.</span></span> <span data-ttu-id="097c7-196">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="097c7-196">Click **Create**.</span></span>
 
### <a name="creating-a-blackboard-learn---shibboleth-test-user"></a><span data-ttu-id="097c7-197">Criando um usuário de teste do Blackboard Learn – Shibboleth</span><span class="sxs-lookup"><span data-stu-id="097c7-197">Creating a Blackboard Learn - Shibboleth test user</span></span>

<span data-ttu-id="097c7-198">Nesta seção, você deve criar um usuário chamado Brenda Fernandes no Blackboard Learn - Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="097c7-198">In this section, you create a user called Britta Simon in Blackboard Learn - Shibboleth.</span></span> <span data-ttu-id="097c7-199">Trabalhe com a [equipe de suporte do Blackboard Learn – Shibboleth](https://www.blackboard.com/forms/contact-us_form.aspx) para adicionar os usuários à plataforma Blackboard Learn – Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="097c7-199">Work with your [Blackboard Learn - Shibboleth support team](https://www.blackboard.com/forms/contact-us_form.aspx) to add the users in the Blackboard Learn - Shibboleth platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="097c7-200">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="097c7-200">Assigning the Azure AD test user</span></span>

<span data-ttu-id="097c7-201">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Blackboard Learn – Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="097c7-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Blackboard Learn - Shibboleth.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="097c7-203">**Para atribuir Brenda Fernandes ao Blackboard Learn - Shibboleth, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="097c7-203">**To assign Britta Simon to Blackboard Learn - Shibboleth, perform the following steps:**</span></span>

1. <span data-ttu-id="097c7-204">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="097c7-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="097c7-206">Na lista de aplicativos, selecione **Blackboard Learn - Shibboleth**.</span><span class="sxs-lookup"><span data-stu-id="097c7-206">In the applications list, select **Blackboard Learn - Shibboleth**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_app.png) 

3. <span data-ttu-id="097c7-208">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="097c7-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="097c7-210">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="097c7-210">Click **Add** button.</span></span> <span data-ttu-id="097c7-211">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="097c7-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="097c7-213">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="097c7-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="097c7-214">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="097c7-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="097c7-215">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="097c7-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="097c7-216">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="097c7-216">Testing single sign-on</span></span>

<span data-ttu-id="097c7-217">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="097c7-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="097c7-218">Quando você clica no bloco Blackboard Learn - Shibboleth no painel de acesso, deve fazer logon automaticamente no aplicativo do Blackboard Learn - Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="097c7-218">When you click the Blackboard Learn - Shibboleth tile in the Access Panel, you should get automatically signed-on to your Blackboard Learn - Shibboleth application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="097c7-219">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="097c7-219">Additional resources</span></span>

* [<span data-ttu-id="097c7-220">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="097c7-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="097c7-221">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="097c7-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_203.png

