---
title: "Tutorial: Integração do Azure Active Directory ao GitHub | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o GitHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4395bd95-05de-4deb-87a5-dc3bc8ac4d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 9dc12bc2e313bcb2000724d035156c5054d14e1c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-github"></a><span data-ttu-id="678af-103">Tutorial: Integração do Azure Active Directory ao GitHub</span><span class="sxs-lookup"><span data-stu-id="678af-103">Tutorial: Azure Active Directory integration with GitHub</span></span>

<span data-ttu-id="678af-104">Neste tutorial, você aprenderá a integrar o GitHub ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="678af-104">In this tutorial, you learn how to integrate GitHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="678af-105">A integração do GitHub ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="678af-105">Integrating GitHub with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="678af-106">Você pode controlar no Azure AD quem terá acesso ao GitHub</span><span class="sxs-lookup"><span data-stu-id="678af-106">You can control in Azure AD who has access to GitHub</span></span>
- <span data-ttu-id="678af-107">Você pode permitir que usuários façam logon automaticamente no GitHub usando logon único com as respectivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="678af-107">You can enable your users to automatically get signed-on to GitHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="678af-108">Você pode gerenciar suas contas em um único local - o portal de Gerenciamento do Azure</span><span class="sxs-lookup"><span data-stu-id="678af-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="678af-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="678af-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="678af-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="678af-110">Prerequisites</span></span>

<span data-ttu-id="678af-111">Para configurar a integração do Azure AD com o GitHub, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="678af-111">To configure Azure AD integration with GitHub, you need the following items:</span></span>

- <span data-ttu-id="678af-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="678af-112">An Azure AD subscription</span></span>
- <span data-ttu-id="678af-113">Uma assinatura do GitHub habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="678af-113">A GitHub single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="678af-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="678af-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="678af-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="678af-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="678af-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="678af-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="678af-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="678af-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="678af-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="678af-118">Scenario description</span></span>
<span data-ttu-id="678af-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="678af-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="678af-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="678af-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="678af-121">Adicionar o GitHub da galeria</span><span class="sxs-lookup"><span data-stu-id="678af-121">Adding GitHub from the gallery</span></span>
2. <span data-ttu-id="678af-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="678af-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-github-from-the-gallery"></a><span data-ttu-id="678af-123">Adicionar o GitHub da galeria</span><span class="sxs-lookup"><span data-stu-id="678af-123">Adding GitHub from the gallery</span></span>
<span data-ttu-id="678af-124">Para configurar a integração do GitHub ao Azure AD, você precisará adicionar o GitHub da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="678af-124">To configure the integration of GitHub into Azure AD, you need to add GitHub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="678af-125">**Para adicionar o GitHub por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="678af-125">**To add GitHub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="678af-126">No **[Portal de Gerenciamento do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="678af-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="678af-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="678af-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="678af-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="678af-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="678af-131">Clique em **adicionar** botão na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="678af-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="678af-133">Na caixa de pesquisa, digite **GitHub.com**.</span><span class="sxs-lookup"><span data-stu-id="678af-133">In the search box, type **GitHub.com**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-github-tutorial/tutorial_github_search02.png)

5. <span data-ttu-id="678af-135">No painel de resultados, selecione **GitHub** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="678af-135">In the results panel, select **GitHub**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-github-tutorial/tutorial_github_search_result02.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="678af-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="678af-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="678af-138">Nesta seção, você configurará e testará o logon único do Azure AD com o GitHub, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="678af-138">In this section, you configure and test Azure AD single sign-on with GitHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="678af-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do GitHub é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="678af-139">For single sign-on to work, Azure AD needs to know what the counterpart user in GitHub is to a user in Azure AD.</span></span> <span data-ttu-id="678af-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no GitHub.</span><span class="sxs-lookup"><span data-stu-id="678af-140">In other words, a link relationship between an Azure AD user and the related user in GitHub needs to be established.</span></span>

<span data-ttu-id="678af-141">Essa relação de vínculo é estabelecida atribuindo o valor de **nome de usuário** ao Azure AD como sendo o valor de **Nome de usuário** no GitHub.</span><span class="sxs-lookup"><span data-stu-id="678af-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in GitHub.</span></span>

<span data-ttu-id="678af-142">Para configurar e testar o logon único do Azure AD com o GitHub, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="678af-142">To configure and test Azure AD single sign-on with GitHub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="678af-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="678af-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="678af-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="678af-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="678af-145">**[Criar um usuário de teste do GitHub](#creating-a-GitHub-test-user)** - para ter um equivalente de Brenda Fernandes no GitHub que esteja vinculado à representação dela no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="678af-145">**[Creating a GitHub test user](#creating-a-GitHub-test-user)** - to have a counterpart of Britta Simon in GitHub that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="678af-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="678af-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="678af-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="678af-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="678af-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="678af-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="678af-149">Nesta seção, você habilita o logon único do Azure AD no portal de Gerenciamento do Azure e configura o logon único em seu aplicativo GitHub.</span><span class="sxs-lookup"><span data-stu-id="678af-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your GitHub application.</span></span>

<span data-ttu-id="678af-150">**Para configurar o logon único do Azure AD com o GitHub, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="678af-150">**To configure Azure AD single sign-on with GitHub, perform the following steps:**</span></span>

1. <span data-ttu-id="678af-151">No portal de Gerenciamento do Azure, na página de integração do aplicativo **GitHub**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="678af-151">In the Azure Management portal, on the **GitHub** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="678af-153">Na caixa de diálogo **Logon único**, como **Modo**, selecione **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="678af-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurar o logon único](./media/active-directory-saas-github-tutorial/tutorial_github_01.png)

3. <span data-ttu-id="678af-155">Na seção **URLs e Domínio do GitHub**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="678af-155">On the **GitHub Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar o logon único](./media/active-directory-saas-github-tutorial/tutorial_github_saml011.png)

    <span data-ttu-id="678af-157">a.</span><span class="sxs-lookup"><span data-stu-id="678af-157">a.</span></span> <span data-ttu-id="678af-158">Na caixa de texto **URL de Logon**, digite o valor como: `https://github.com/orgs/<entity-id>/sso`</span><span class="sxs-lookup"><span data-stu-id="678af-158">In the **Sign-on URL** textbox, type the value as: `https://github.com/orgs/<entity-id>/sso`</span></span>

    <span data-ttu-id="678af-159">b.</span><span class="sxs-lookup"><span data-stu-id="678af-159">b.</span></span> <span data-ttu-id="678af-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://github.com/orgs/<entity-id>`</span><span class="sxs-lookup"><span data-stu-id="678af-160">In the **Identifier** textbox, type a URL using the following pattern: `https://github.com/orgs/<entity-id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="678af-161">Observe que esses não são os valores reais.</span><span class="sxs-lookup"><span data-stu-id="678af-161">Please note that these are not the real values.</span></span> <span data-ttu-id="678af-162">É necessário atualizar esses valores com a URL de Logon e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="678af-162">You have to update these values with the actual Sing-on URL and Identifier.</span></span> <span data-ttu-id="678af-163">Aqui, sugerimos que você use o valor exclusivo de cadeia de caracteres no Identificador.</span><span class="sxs-lookup"><span data-stu-id="678af-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="678af-164">Acesse a seção Administração do GitHub para recuperar esses valores.</span><span class="sxs-lookup"><span data-stu-id="678af-164">Go to GitHub Admin section to retrieve these values.</span></span> 

4. <span data-ttu-id="678af-165">Na seção **Atributos do Usuário**, selecione **Identificador de Usuário** como user.mail.</span><span class="sxs-lookup"><span data-stu-id="678af-165">On the **User Attributes** section, select **User Identifier** as user.mail.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-github-tutorial/tutorial_github_attribute_new01.png)
    
5. <span data-ttu-id="678af-167">Sobre o **certificado de autenticação SAML** seção, clique em **criar novo certificado**.</span><span class="sxs-lookup"><span data-stu-id="678af-167">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-github-tutorial/tutorial_github_03.png)

6. <span data-ttu-id="678af-169">Na caixa de diálogo **Criar um Novo Certificado**, clique no ícone de calendário e selecione uma **data de expiração**.</span><span class="sxs-lookup"><span data-stu-id="678af-169">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="678af-170">Em seguida, clique no botão **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="678af-170">Then click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-github-tutorial/tutorial_general_300.png)

7. <span data-ttu-id="678af-172">Na seção **Certificado de Autenticação SAML**, selecione **Ativar o novo certificado** e clique no botão **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="678af-172">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-github-tutorial/tutorial_github_04.png)

8. <span data-ttu-id="678af-174">Na janela pop-up **Certificado de substituição**, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="678af-174">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-github-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="678af-176">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="678af-176">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-github-tutorial/tutorial_github_05.png) 

10. <span data-ttu-id="678af-178">Na seção **Configuração do GitHub**, clique em **Configurar o GitHub** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="678af-178">On the **GitHub Configuration** section, click **Configure GitHub** to open **Configure sign-on** window.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-github-tutorial/tutorial_github_06.png) 

    ![Configurar o logon único](./media/active-directory-saas-github-tutorial/tutorial_github_07.png)

11. <span data-ttu-id="678af-181">Em outra janela do navegador da Web, faça logon em seu site de organização do GitHub como administrador.</span><span class="sxs-lookup"><span data-stu-id="678af-181">In a different web browser window, log into your GitHub organization site as an administrator.</span></span>

12. <span data-ttu-id="678af-182">Navegue até **Configurações** e clique em **Segurança**</span><span class="sxs-lookup"><span data-stu-id="678af-182">Navigate to **Settings** and click **Security**</span></span>

    ![Configurações](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_03.png)

13. <span data-ttu-id="678af-184">Marque a caixa **Habilitar autenticação SAML**, revelando os campos de configuração de Logon Único.</span><span class="sxs-lookup"><span data-stu-id="678af-184">Check the **Enable SAML authentication** box, revealing the Single Sign-on configuration fields.</span></span> <span data-ttu-id="678af-185">Em seguida, use o valor de URL de logon único para atualizar a URL de Logon Único na configuração do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="678af-185">Then, use the single sign-on URL value to update the Single sign-on URL on Azure AD configuration.</span></span>

    ![Configurações](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_13.png)

14. <span data-ttu-id="678af-187">Configure os seguintes campos:</span><span class="sxs-lookup"><span data-stu-id="678af-187">Configure the following fields:</span></span>

    <span data-ttu-id="678af-188">a.</span><span class="sxs-lookup"><span data-stu-id="678af-188">a.</span></span> <span data-ttu-id="678af-189">**URL de Logon**: insira **URL de Serviço de logon único de SAML** na seção **Configurar o GitHub** no Azure AD</span><span class="sxs-lookup"><span data-stu-id="678af-189">**Sign on URL**: Enter **SAML Single sign-on Service URL** from the **Configure GitHub** section on Azure AD</span></span>

    <span data-ttu-id="678af-190">b.</span><span class="sxs-lookup"><span data-stu-id="678af-190">b.</span></span> <span data-ttu-id="678af-191">**Emissor**: insira **ID da Entidade SAML** na seção **Configurar GitHub** do Azure AD</span><span class="sxs-lookup"><span data-stu-id="678af-191">**Issuer**: Enter **SAML Entity ID** from the **Configure GitHub** section on Azure AD</span></span>

    <span data-ttu-id="678af-192">c.</span><span class="sxs-lookup"><span data-stu-id="678af-192">c.</span></span> <span data-ttu-id="678af-193">**Certificado Público**: abra o certificado baixado no Azure AD em um bloco de notas e copie o conteúdo, incluindo "BEGIN CERTIFICATE" e "END CERTIFICATE"</span><span class="sxs-lookup"><span data-stu-id="678af-193">**Public Certificate**: Open the downloaded certificate from Azure AD in a notepad and copy the content including "BEGIN CERTIFICATE" and "END CERTIFICATE"</span></span>

    ![Configurações](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_051.png)

15. <span data-ttu-id="678af-195">Clique em **Testar configuração de SAML** para confirmar que não há falhas de validação ou erros durante o SSO.</span><span class="sxs-lookup"><span data-stu-id="678af-195">Click on **Test SAML configuration** to confirm that no validation failures or errors during SSO.</span></span>

    ![Configurações](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_06.png)

16. <span data-ttu-id="678af-197">Clique em **Salvar**</span><span class="sxs-lookup"><span data-stu-id="678af-197">Click **Save**</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="678af-198">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="678af-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="678af-199">O objetivo desta seção é criar um usuário de teste no Portal de Gerenciamento do Azure chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="678af-199">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="678af-201">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="678af-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="678af-202">No **portal de Gerenciamento do Azure**, no painel navegação à esquerda, clique em **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="678af-202">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-github-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="678af-204">Vá para **usuários e grupos** e clique em **todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="678af-204">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-github-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="678af-206">Na parte superior da caixa de diálogo clique **adicionar** para abrir o **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="678af-206">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-github-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="678af-208">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="678af-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-github-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="678af-210">a.</span><span class="sxs-lookup"><span data-stu-id="678af-210">a.</span></span> <span data-ttu-id="678af-211">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="678af-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="678af-212">b.</span><span class="sxs-lookup"><span data-stu-id="678af-212">b.</span></span> <span data-ttu-id="678af-213">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="678af-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="678af-214">c.</span><span class="sxs-lookup"><span data-stu-id="678af-214">c.</span></span> <span data-ttu-id="678af-215">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="678af-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="678af-216">d.</span><span class="sxs-lookup"><span data-stu-id="678af-216">d.</span></span> <span data-ttu-id="678af-217">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="678af-217">Click **Create**.</span></span> 


### <a name="creating-a-github-test-user"></a><span data-ttu-id="678af-218">Criar um usuário de teste do GitHub</span><span class="sxs-lookup"><span data-stu-id="678af-218">Creating a GitHub test user</span></span>

<span data-ttu-id="678af-219">Para permitir que os usuários do Azure AD façam logon no GitHub, eles deverão ser provisionados no GitHub.</span><span class="sxs-lookup"><span data-stu-id="678af-219">In order to enable Azure AD users to log into GitHub, they must be provisioned into GitHub.</span></span>  
<span data-ttu-id="678af-220">No caso do GitHub, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="678af-220">In the case of GitHub, provisioning is a manual task.</span></span>

<span data-ttu-id="678af-221">**Para provisionar contas de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="678af-221">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="678af-222">Faça logon em seu site de empresa do GitHub como administrador.</span><span class="sxs-lookup"><span data-stu-id="678af-222">Log in to your GitHub company site as an administrator.</span></span>

2. <span data-ttu-id="678af-223">Clique em **Pessoas**.</span><span class="sxs-lookup"><span data-stu-id="678af-223">Click **People**.</span></span>

    <span data-ttu-id="678af-224">![Pessoas](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "Pessoas")</span><span class="sxs-lookup"><span data-stu-id="678af-224">![People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "People")</span></span>

3. <span data-ttu-id="678af-225">Clique em **Convidar membro**.</span><span class="sxs-lookup"><span data-stu-id="678af-225">Click **Invite member**.</span></span>

    <span data-ttu-id="678af-226">![Convidar Usuários](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "Convidar Usuários")</span><span class="sxs-lookup"><span data-stu-id="678af-226">![Invite Users](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "Invite Users")</span></span>

4. <span data-ttu-id="678af-227">Na caixa de diálogo **Convidar membro**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="678af-227">On the **Invite member** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="678af-228">a.</span><span class="sxs-lookup"><span data-stu-id="678af-228">a.</span></span> <span data-ttu-id="678af-229">Na caixa de texto **Email**, digite o endereço de email da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="678af-229">In the **Email** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="678af-230">![Convidar Pessoas](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "Convidar Pessoas")</span><span class="sxs-lookup"><span data-stu-id="678af-230">![Invite People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "Invite People")</span></span>
    
    <span data-ttu-id="678af-231">b.</span><span class="sxs-lookup"><span data-stu-id="678af-231">b.</span></span> <span data-ttu-id="678af-232">Clique em **Enviar Convite**.</span><span class="sxs-lookup"><span data-stu-id="678af-232">Click **Send Invitation**.</span></span>

    <span data-ttu-id="678af-233">![Convidar Pessoas](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "Convidar Pessoas")</span><span class="sxs-lookup"><span data-stu-id="678af-233">![Invite People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "Invite People")</span></span>

    > [!NOTE]
    > <span data-ttu-id="678af-234">O titular da conta do Active Directory do Azure receberá um email e seguirá um link para confirmar a conta antes que ela se torne ativa.</span><span class="sxs-lookup"><span data-stu-id="678af-234">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="678af-235">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="678af-235">Assigning the Azure AD test user</span></span>

<span data-ttu-id="678af-236">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao GitHub.</span><span class="sxs-lookup"><span data-stu-id="678af-236">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to GitHub.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="678af-238">**Para atribuir Brenda Fernandes ao GitHub, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="678af-238">**To assign Britta Simon to GitHub, perform the following steps:**</span></span>

1. <span data-ttu-id="678af-239">No portal de gerenciamento do Azure, abra a exibição de aplicativos e, em seguida, navegue até o modo de exibição de diretório e vá para **aplicativos empresariais** e clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="678af-239">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="678af-241">Na lista de aplicativos, selecione **GitHub.com**.</span><span class="sxs-lookup"><span data-stu-id="678af-241">In the applications list, select **GitHub.com**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-github-tutorial/tutorial_github_search_result021.png) 

3. <span data-ttu-id="678af-243">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="678af-243">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="678af-245">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="678af-245">Click **Add** button.</span></span> <span data-ttu-id="678af-246">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="678af-246">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="678af-248">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="678af-248">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="678af-249">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="678af-249">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="678af-250">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="678af-250">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="678af-251">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="678af-251">Testing single sign-on</span></span>

<span data-ttu-id="678af-252">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="678af-252">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="678af-253">Ao clicar no bloco do GitHub no Painel de Acesso, você deverá ser conectado automaticamente ao aplicativo GitHub.</span><span class="sxs-lookup"><span data-stu-id="678af-253">When you click the GitHub tile in the Access Panel, you should get signed-on to your GitHub application.</span></span> <span data-ttu-id="678af-254">Você entrará como uma conta de Organização, mas precisará fazer logon com sua conta pessoal.</span><span class="sxs-lookup"><span data-stu-id="678af-254">You'll be logging in as an Organization account but then need to log in with your personal account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="678af-255">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="678af-255">Additional resources</span></span>

* [<span data-ttu-id="678af-256">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="678af-256">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="678af-257">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="678af-257">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-github-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-github-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-github-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-github-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-github-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-github-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-github-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-github-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-github-tutorial/tutorial_general_203.png
