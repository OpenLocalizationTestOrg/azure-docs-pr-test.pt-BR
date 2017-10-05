---
title: "Tutorial: Integração do Azure Active Directory ao Inkling | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Inkling."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 64c7ee45-ee8a-42f7-bf04-fd0e00833ea9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: 7b0639c6515298731f88346c2e4ca82664653a2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-inkling"></a><span data-ttu-id="2e56b-103">Tutorial: Integração do Azure Active Directory ao Inkling</span><span class="sxs-lookup"><span data-stu-id="2e56b-103">Tutorial: Azure Active Directory integration with Inkling</span></span>

<span data-ttu-id="2e56b-104">Neste tutorial, você aprenderá a integrar o Inkling ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="2e56b-104">In this tutorial, you learn how to integrate Inkling with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2e56b-105">A integração do Inkling ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="2e56b-105">Integrating Inkling with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2e56b-106">Você pode controlar, no Azure AD, quem terá acesso ao Inkling</span><span class="sxs-lookup"><span data-stu-id="2e56b-106">You can control in Azure AD who has access to Inkling</span></span>
- <span data-ttu-id="2e56b-107">Você pode permitir que os usuários entrem automaticamente no Inkling (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e56b-107">You can enable your users to automatically get signed-on to Inkling (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2e56b-108">Você pode gerenciar suas contas em um único local - o portal de Gerenciamento do Azure</span><span class="sxs-lookup"><span data-stu-id="2e56b-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="2e56b-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2e56b-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e56b-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2e56b-110">Prerequisites</span></span>

<span data-ttu-id="2e56b-111">Para configurar a integração do Azure AD ao Inkling, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="2e56b-111">To configure Azure AD integration with Inkling, you need the following items:</span></span>

- <span data-ttu-id="2e56b-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2e56b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2e56b-113">Uma assinatura habilitada para logon único no Inkling</span><span class="sxs-lookup"><span data-stu-id="2e56b-113">An Inkling single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="2e56b-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="2e56b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="2e56b-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="2e56b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2e56b-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="2e56b-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="2e56b-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2e56b-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="2e56b-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="2e56b-118">Scenario description</span></span>
<span data-ttu-id="2e56b-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="2e56b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2e56b-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="2e56b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2e56b-121">Adicionar o Inkling usando a galeria</span><span class="sxs-lookup"><span data-stu-id="2e56b-121">Adding Inkling from the gallery</span></span>
2. <span data-ttu-id="2e56b-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2e56b-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-inkling-from-the-gallery"></a><span data-ttu-id="2e56b-123">Adicionar o Inkling usando a galeria</span><span class="sxs-lookup"><span data-stu-id="2e56b-123">Adding Inkling from the gallery</span></span>
<span data-ttu-id="2e56b-124">Para configurar a integração do Inkling ao Azure AD, você precisa adicionar o Inkling por meio da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="2e56b-124">To configure the integration of Inkling into Azure AD, you need to add Inkling from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2e56b-125">**Para adicionar o Inkling usando a galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="2e56b-125">**To add Inkling from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2e56b-126">No **[Portal de Gerenciamento do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2e56b-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2e56b-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="2e56b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2e56b-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="2e56b-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="2e56b-131">Clique em **adicionar** botão na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2e56b-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="2e56b-133">Na caixa de pesquisa, digite **Inkling**.</span><span class="sxs-lookup"><span data-stu-id="2e56b-133">In the search box, type **Inkling**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_001.png)

5. <span data-ttu-id="2e56b-135">No painel de resultados, selecione **Inkling** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2e56b-135">In the results panel, select **Inkling**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2e56b-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2e56b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2e56b-138">Nesta seção, você configura e testa o logon único do Azure AD com o Inkling, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="2e56b-138">In this section, you configure and test Azure AD single sign-on with Inkling based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2e56b-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Inkling é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2e56b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Inkling is to a user in Azure AD.</span></span> <span data-ttu-id="2e56b-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Inkling.</span><span class="sxs-lookup"><span data-stu-id="2e56b-140">In other words, a link relationship between an Azure AD user and the related user in Inkling needs to be established.</span></span>

<span data-ttu-id="2e56b-141">Essa relação de vínculo é estabelecida atribuindo o valor de **nome de usuário** no Azure AD como o valor de **Nome de usuário** no Inkling.</span><span class="sxs-lookup"><span data-stu-id="2e56b-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Inkling.</span></span>

<span data-ttu-id="2e56b-142">Para configurar e testar o logon único do Azure AD com o Inkling, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="2e56b-142">To configure and test Azure AD single sign-on with Inkling, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2e56b-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="2e56b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2e56b-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** - para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="2e56b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2e56b-145">**[Criando um usuário de teste do Inkling](#creating-an-inkling-test-user)**: para ter um equivalente de Brenda Fernandes no Inkling que esteja vinculado à representação dela no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2e56b-145">**[Creating an Inkling test user](#creating-an-inkling-test-user)** - to have a counterpart of Britta Simon in Inkling that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="2e56b-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** - para habilitar Britta Simon a usar o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2e56b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2e56b-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="2e56b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2e56b-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e56b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2e56b-149">Nesta seção, você habilita o logon único do Azure AD no Portal de Gerenciamento do Azure e configura o logon único em seu aplicativo Inkling.</span><span class="sxs-lookup"><span data-stu-id="2e56b-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Inkling application.</span></span>

<span data-ttu-id="2e56b-150">**Para configurar o logon único do Azure AD com o Inkling, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="2e56b-150">**To configure Azure AD single sign-on with Inkling, perform the following steps:**</span></span>

1. <span data-ttu-id="2e56b-151">No Portal de Gerenciamento do Azure, na página de integração de aplicativos do **Inkling**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="2e56b-151">In the Azure Management portal, on the **Inkling** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="2e56b-153">Na caixa de diálogo **Logon único**, como **Modo**, selecione **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="2e56b-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurar o logon único](./media/active-directory-saas-inkling-tutorial/tutorial_general_300.png)
    
3. <span data-ttu-id="2e56b-155">Na seção **URLs e Domínio do Inkling**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="2e56b-155">On the **Inkling Domain and URLs** section, perform the following steps:</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_01.png)

    <span data-ttu-id="2e56b-157">a.</span><span class="sxs-lookup"><span data-stu-id="2e56b-157">a.</span></span> <span data-ttu-id="2e56b-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://api.inkling.com/saml/v2/metadata/<user-id>`</span><span class="sxs-lookup"><span data-stu-id="2e56b-158">In the **Identifier** textbox, type a URL using the following pattern: `https://api.inkling.com/saml/v2/metadata/<user-id>`</span></span>

    <span data-ttu-id="2e56b-159">b.</span><span class="sxs-lookup"><span data-stu-id="2e56b-159">b.</span></span> <span data-ttu-id="2e56b-160">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://api.inkling.com/saml/v2/acs/<user-id>`</span><span class="sxs-lookup"><span data-stu-id="2e56b-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://api.inkling.com/saml/v2/acs/<user-id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2e56b-161">Observe que esses não são os valores reais.</span><span class="sxs-lookup"><span data-stu-id="2e56b-161">Please note that these are not the real values.</span></span> <span data-ttu-id="2e56b-162">Você precisa atualizar esses valores com o Identificador e a URL de Resposta reais.</span><span class="sxs-lookup"><span data-stu-id="2e56b-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="2e56b-163">Entre em contato com a [equipe de suporte do Inkling](mailto:press@inkling.com) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="2e56b-163">Contact [Inkling support team](mailto:press@inkling.com) to get these values.</span></span>

4. <span data-ttu-id="2e56b-164">Na seção **Certificado de Autenticação SAML**, clique em **Criar novo certificado**.</span><span class="sxs-lookup"><span data-stu-id="2e56b-164">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-inkling-tutorial/tutorial_general_400.png)    

5. <span data-ttu-id="2e56b-166">Na caixa de diálogo **Criar um Novo Certificado**, clique no ícone de calendário e selecione uma **data de expiração**.</span><span class="sxs-lookup"><span data-stu-id="2e56b-166">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="2e56b-167">Em seguida, clique no botão **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="2e56b-167">Then click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-inkling-tutorial/tutorial_general_500.png)

6. <span data-ttu-id="2e56b-169">Na seção **Certificado de Autenticação SAML**, selecione **Ativar o novo certificado** e clique no botão **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="2e56b-169">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_02.png)

7. <span data-ttu-id="2e56b-171">Na janela pop-up **Certificado de substituição**, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="2e56b-171">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-inkling-tutorial/tutorial_general_600.png)

8. <span data-ttu-id="2e56b-173">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="2e56b-173">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_03.png) 

9. <span data-ttu-id="2e56b-175">Para que o SSO seja configurado para o aplicativo, entre em contato com a [equipe de suporte do Inkling](mailto:press@inkling.com) e forneça os **metadados** baixados.</span><span class="sxs-lookup"><span data-stu-id="2e56b-175">To get SSO configured for your application, contact [Inkling support team](mailto:press@inkling.com) and provide them with downloaded **metadata**.</span></span> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2e56b-176">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2e56b-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="2e56b-177">O objetivo desta seção é criar um usuário de teste no Portal de Gerenciamento do Azure chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2e56b-177">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="2e56b-179">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="2e56b-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2e56b-180">No **portal de Gerenciamento do Azure**, no painel navegação à esquerda, clique em **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2e56b-180">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-inkling-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2e56b-182">Vá para **usuários e grupos** e clique em **todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="2e56b-182">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-inkling-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2e56b-184">Na parte superior da caixa de diálogo clique **adicionar** para abrir o **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2e56b-184">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-inkling-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2e56b-186">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="2e56b-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-inkling-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2e56b-188">a.</span><span class="sxs-lookup"><span data-stu-id="2e56b-188">a.</span></span> <span data-ttu-id="2e56b-189">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="2e56b-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2e56b-190">b.</span><span class="sxs-lookup"><span data-stu-id="2e56b-190">b.</span></span> <span data-ttu-id="2e56b-191">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="2e56b-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2e56b-192">c.</span><span class="sxs-lookup"><span data-stu-id="2e56b-192">c.</span></span> <span data-ttu-id="2e56b-193">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="2e56b-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2e56b-194">d.</span><span class="sxs-lookup"><span data-stu-id="2e56b-194">d.</span></span> <span data-ttu-id="2e56b-195">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="2e56b-195">Click **Create**.</span></span> 



### <a name="creating-an-inkling-test-user"></a><span data-ttu-id="2e56b-196">Criando um usuário de teste do Inkling</span><span class="sxs-lookup"><span data-stu-id="2e56b-196">Creating an Inkling test user</span></span>

<span data-ttu-id="2e56b-197">Nesta seção, você cria um usuário chamado Brenda Fernandes no Inkling.</span><span class="sxs-lookup"><span data-stu-id="2e56b-197">In this section, you create a user called Britta Simon in Inkling.</span></span> <span data-ttu-id="2e56b-198">Trabalhe com a [equipe de suporte do Inkling](mailto:press@inkling.com) para adicionar usuários à plataforma Inkling.</span><span class="sxs-lookup"><span data-stu-id="2e56b-198">Please work with [Inkling support team](mailto:press@inkling.com) to add the users in the Inkling platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2e56b-199">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2e56b-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2e56b-200">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Inkling.</span><span class="sxs-lookup"><span data-stu-id="2e56b-200">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Inkling.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="2e56b-202">**Para atribuir Brenda Fernandes ao Inkling, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="2e56b-202">**To assign Britta Simon to Inkling, perform the following steps:**</span></span>

1. <span data-ttu-id="2e56b-203">No Portal de Gerenciamento do Azure, abra a exibição de aplicativos e, em seguida, navegue até o modo de exibição de diretório, vá para **Aplicativos empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="2e56b-203">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="2e56b-205">Na lista de aplicativos, escolha **Inkling**.</span><span class="sxs-lookup"><span data-stu-id="2e56b-205">In the applications list, select **Inkling**.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_50.png) 

3. <span data-ttu-id="2e56b-207">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="2e56b-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="2e56b-209">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="2e56b-209">Click **Add** button.</span></span> <span data-ttu-id="2e56b-210">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2e56b-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="2e56b-212">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="2e56b-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2e56b-213">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2e56b-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2e56b-214">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2e56b-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="2e56b-215">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="2e56b-215">Testing single sign-on</span></span>

<span data-ttu-id="2e56b-216">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="2e56b-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2e56b-217">Ao clicar no bloco Inkling no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo Inkling.</span><span class="sxs-lookup"><span data-stu-id="2e56b-217">When you click the Inkling tile in the Access Panel, you should get automatically signed-on to your Inkling application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="2e56b-218">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="2e56b-218">Additional resources</span></span>

* [<span data-ttu-id="2e56b-219">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="2e56b-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2e56b-220">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2e56b-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_203.png