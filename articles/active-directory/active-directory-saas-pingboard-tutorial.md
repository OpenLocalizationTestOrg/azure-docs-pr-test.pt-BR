---
title: "Tutorial: Integração do Azure Active Directory com o Pingboard | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Pingboard."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 008c670a8043da0c67ccefde48d5ef721c75d97c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pingboard"></a><span data-ttu-id="e766a-103">Tutorial: Integração do Azure Active Directory ao Pingboard</span><span class="sxs-lookup"><span data-stu-id="e766a-103">Tutorial: Azure Active Directory integration with Pingboard</span></span>

<span data-ttu-id="e766a-104">Neste tutorial, você aprende a integrar o Pingboard ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="e766a-104">In this tutorial, you learn how to integrate Pingboard with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e766a-105">A integração do Pingboard ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="e766a-105">Integrating Pingboard with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e766a-106">No Azure AD, você pode controlar quem tem acesso ao Pingboard</span><span class="sxs-lookup"><span data-stu-id="e766a-106">You can control in Azure AD who has access to Pingboard</span></span>
- <span data-ttu-id="e766a-107">Você pode permitir que os usuários se conectem automaticamente ao SSO (logon único) do Pingboard com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e766a-107">You can enable your users to automatically get signed-on to Pingboard (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e766a-108">Você pode gerenciar suas contas em um único local - o portal de Gerenciamento do Azure</span><span class="sxs-lookup"><span data-stu-id="e766a-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="e766a-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e766a-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e766a-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e766a-110">Prerequisites</span></span>

<span data-ttu-id="e766a-111">Para configurar a integração do Azure AD ao Pingboard, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="e766a-111">To configure Azure AD integration with Pingboard, you need the following items:</span></span>

- <span data-ttu-id="e766a-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e766a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e766a-113">Uma assinatura do Pingboard habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="e766a-113">A Pingboard single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e766a-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="e766a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e766a-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="e766a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e766a-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="e766a-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="e766a-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e766a-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e766a-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="e766a-118">Scenario description</span></span>
<span data-ttu-id="e766a-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="e766a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e766a-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="e766a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e766a-121">Adicionar o Pingboard por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="e766a-121">Adding Pingboard from the gallery</span></span>
2. <span data-ttu-id="e766a-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e766a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pingboard-from-the-gallery"></a><span data-ttu-id="e766a-123">Adicionar o Pingboard por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="e766a-123">Adding Pingboard from the gallery</span></span>
<span data-ttu-id="e766a-124">Para configurar a integração do Pingboard ao Azure AD, você precisa adicionar o Pingboard à sua lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="e766a-124">To configure the integration of Pingboard into Azure AD, you need to add Pingboard from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e766a-125">**Para adicionar o Pingboard por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e766a-125">**To add Pingboard from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e766a-126">No **[Portal de Gerenciamento do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e766a-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e766a-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="e766a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e766a-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e766a-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="e766a-131">Clique em **adicionar** botão na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e766a-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="e766a-133">Na caixa de pesquisa, digite **Pingboard**.</span><span class="sxs-lookup"><span data-stu-id="e766a-133">In the search box, type **Pingboard**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_search.png)

5. <span data-ttu-id="e766a-135">No painel de resultados, selecione **Pingboard** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e766a-135">In the results panel, select **Pingboard**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e766a-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e766a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e766a-138">Nesta seção, você configura e testa o logon único do Azure AD com o Pingboard, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="e766a-138">In this section, you configure and test Azure AD single sign-on with Pingboard based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e766a-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Pingboard é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e766a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Pingboard is to a user in Azure AD.</span></span> <span data-ttu-id="e766a-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Pingboard.</span><span class="sxs-lookup"><span data-stu-id="e766a-140">In other words, a link relationship between an Azure AD user and the related user in Pingboard needs to be established.</span></span>

<span data-ttu-id="e766a-141">Essa relação de vínculo é estabelecida atribuindo o valor de **nome de usuário** no Azure AD como o valor de **Nome de usuário** no Pingboard.</span><span class="sxs-lookup"><span data-stu-id="e766a-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Pingboard.</span></span>

<span data-ttu-id="e766a-142">Para configurar e testar o logon único do Azure AD com o Pingboard, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="e766a-142">To configure and test Azure AD single sign-on with Pingboard, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e766a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="e766a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e766a-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e766a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e766a-145">**[Criar um usuário de teste do Pingboard](#creating-a-pingboard-test-user)** – para ter um equivalente de Brenda Fernandes no Pingboard que esteja vinculado à representação dela no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e766a-145">**[Creating a Pingboard test user](#creating-a-pingboard-test-user)** - to have a counterpart of Britta Simon in Pingboard that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="e766a-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** - para habilitar Britta Simon a usar o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="e766a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e766a-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="e766a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e766a-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e766a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e766a-149">Nesta seção, você habilita o logon único do Azure AD no portal de Gerenciamento do Azure e configura o logon único no aplicativo Pingboard.</span><span class="sxs-lookup"><span data-stu-id="e766a-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Pingboard application.</span></span>

<span data-ttu-id="e766a-150">**Para configurar o logon único do Azure AD com o Pingboard, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e766a-150">**To configure Azure AD single sign-on with Pingboard, perform the following steps:**</span></span>

1. <span data-ttu-id="e766a-151">No portal de Gerenciamento do Azure, na página de integração do aplicativo **Pingboard**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="e766a-151">In the Azure Management portal, on the **Pingboard** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="e766a-153">Na caixa de diálogo **Logon único**, como **Modo**, selecione **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="e766a-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_samlbase.png)

3. <span data-ttu-id="e766a-155">Na seção **Domínio e URLs do Pingboard**, realize as seguintes etapas se desejar configurar o aplicativo no modo iniciado pelo **IdP**:</span><span class="sxs-lookup"><span data-stu-id="e766a-155">On the **Pingboard Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_url.png)

    <span data-ttu-id="e766a-157">a.</span><span class="sxs-lookup"><span data-stu-id="e766a-157">a.</span></span> <span data-ttu-id="e766a-158">Na caixa de texto **Identificador**, digite o valor como `http://<entity-id>.pingboard.com/sp`</span><span class="sxs-lookup"><span data-stu-id="e766a-158">In the **Identifier** textbox, type the value as: `http://<entity-id>.pingboard.com/sp`</span></span>

    <span data-ttu-id="e766a-159">b.</span><span class="sxs-lookup"><span data-stu-id="e766a-159">b.</span></span> <span data-ttu-id="e766a-160">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<entity-id>.pingboard.com/auth/saml/consume`</span><span class="sxs-lookup"><span data-stu-id="e766a-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<entity-id>.pingboard.com/auth/saml/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e766a-161">Observe que esses não são os valores reais.</span><span class="sxs-lookup"><span data-stu-id="e766a-161">Please note that these are not the real values.</span></span> <span data-ttu-id="e766a-162">Você precisa atualizar esses valores com o Identificador e a URL de Resposta reais.</span><span class="sxs-lookup"><span data-stu-id="e766a-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="e766a-163">Aqui, sugerimos que você use o valor exclusivo de cadeia de caracteres no Identificador.</span><span class="sxs-lookup"><span data-stu-id="e766a-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="e766a-164">Contate a [equipe de suporte do Pingboard](https://support.pingboard.com/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="e766a-164">Contact [Pingboard Client support team](https://support.pingboard.com/) to get these values.</span></span> 

4. <span data-ttu-id="e766a-165">Marque **Mostrar configurações avançadas de URL**, se quiser configurar o aplicativo no modo iniciado em **SP**:</span><span class="sxs-lookup"><span data-stu-id="e766a-165">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_sp_initiated01.png)

    <span data-ttu-id="e766a-167">a.</span><span class="sxs-lookup"><span data-stu-id="e766a-167">a.</span></span> <span data-ttu-id="e766a-168">Na caixa de texto **URL de Logon**, digite o valor como: `http://<sub-domain>.pingboard.com/sign_in`</span><span class="sxs-lookup"><span data-stu-id="e766a-168">In the **Sign-on URL** textbox, type the value as: `http://<sub-domain>.pingboard.com/sign_in`</span></span>
     
5. <span data-ttu-id="e766a-169">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo XML em seu computador.</span><span class="sxs-lookup"><span data-stu-id="e766a-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_certificate.png) 

6. <span data-ttu-id="e766a-171">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="e766a-171">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-pingboard-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="e766a-173">Para configurar o SSO no lado do Pingboard, abra uma nova janela do navegador e faça logon em sua conta do Pingboard.</span><span class="sxs-lookup"><span data-stu-id="e766a-173">To configure SSO on Pingboard side, open a new browser window and log in to your Pingboard Account.</span></span> <span data-ttu-id="e766a-174">Você deve ser administrador do Pingboard para configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="e766a-174">You must be a Pingboard admin to set up single sign on.</span></span>

8. <span data-ttu-id="e766a-175">No menu superior, selecione **Aplicativos > Integrações**</span><span class="sxs-lookup"><span data-stu-id="e766a-175">From the top menu select **Apps > Integrations**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-pingboard-tutorial/Pingboard_integration.png)

9.  <span data-ttu-id="e766a-177">Na página **Integrações**, localize o bloco **"Azure Active Directory"** e clique nele.</span><span class="sxs-lookup"><span data-stu-id="e766a-177">On the **Integrations** page, find the **"Azure Active Directory"** tile, and click it.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-pingboard-tutorial/Pingboard_aad.png)

10. <span data-ttu-id="e766a-179">No modal que vem a seguir, clique em **"Configurar"**</span><span class="sxs-lookup"><span data-stu-id="e766a-179">In the modal that follows click **"Configure"**</span></span>

    ![Configurar o logon único](./media/active-directory-saas-pingboard-tutorial/Pingboard_configure.png)

11. <span data-ttu-id="e766a-181">Na página seguinte, você notará que a "Integração de SSO do Azure está habilitada.".</span><span class="sxs-lookup"><span data-stu-id="e766a-181">On the following page, you will notice that "Azure SSO Integration is enabled.".</span></span> <span data-ttu-id="e766a-182">Abra o arquivo Metadados XML baixado em um bloco de notas e cole o conteúdo em **Metadados IDP**.</span><span class="sxs-lookup"><span data-stu-id="e766a-182">Open the downloaded Metadata XML file in a notepad and paste the content in **IDP Metadata**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-pingboard-tutorial/Pingboard_sso_configure.png)

12. <span data-ttu-id="e766a-184">O arquivo será validado e, se tudo estiver correto, o logon único estará habilitado</span><span class="sxs-lookup"><span data-stu-id="e766a-184">The file will be validated, and if everything is correct, single sign on will now be enabled</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e766a-185">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e766a-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="e766a-186">O objetivo desta seção é criar um usuário de teste no Portal de Gerenciamento do Azure chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e766a-186">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="e766a-188">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e766a-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e766a-189">No **portal de Gerenciamento do Azure**, no painel navegação à esquerda, clique em **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e766a-189">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pingboard-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e766a-191">Vá para **usuários e grupos** e clique em **todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="e766a-191">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pingboard-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e766a-193">Na parte superior da caixa de diálogo clique **adicionar** para abrir o **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e766a-193">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pingboard-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e766a-195">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e766a-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pingboard-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e766a-197">a.</span><span class="sxs-lookup"><span data-stu-id="e766a-197">a.</span></span> <span data-ttu-id="e766a-198">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="e766a-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e766a-199">b.</span><span class="sxs-lookup"><span data-stu-id="e766a-199">b.</span></span> <span data-ttu-id="e766a-200">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e766a-200">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e766a-201">c.</span><span class="sxs-lookup"><span data-stu-id="e766a-201">c.</span></span> <span data-ttu-id="e766a-202">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="e766a-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e766a-203">d.</span><span class="sxs-lookup"><span data-stu-id="e766a-203">d.</span></span> <span data-ttu-id="e766a-204">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e766a-204">Click **Create**.</span></span>
 
### <a name="creating-a-pingboard-test-user"></a><span data-ttu-id="e766a-205">Criando um usuário de teste do Pingboard</span><span class="sxs-lookup"><span data-stu-id="e766a-205">Creating a Pingboard test user</span></span>

<span data-ttu-id="e766a-206">Para permitir que os usuários do Azure AD façam logon no Pingboard, eles devem ser provisionados no Pingboard.</span><span class="sxs-lookup"><span data-stu-id="e766a-206">In order to enable Azure AD users to log into Pingboard, they must be provisioned into Pingboard.</span></span>  
<span data-ttu-id="e766a-207">No caso do Pingboard, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="e766a-207">In the case of Pingboard, provisioning is a manual task.</span></span>

<span data-ttu-id="e766a-208">**Para provisionar contas de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e766a-208">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="e766a-209">Faça logon em seu site de empresa do Pingboard como administrador.</span><span class="sxs-lookup"><span data-stu-id="e766a-209">Log in to your Pingboard company site as an administrator.</span></span>

2. <span data-ttu-id="e766a-210">Clique no botão **"Adicionar Funcionário"** na página **Diretório**.</span><span class="sxs-lookup"><span data-stu-id="e766a-210">Click **“Add Employee”** button on **Directory** page.</span></span>

    ![Adicionar Funcionário](./media/active-directory-saas-pingboard-tutorial/create_testuser_add.png)

3. <span data-ttu-id="e766a-212">Na página do diálogo **“Adicionar Funcionário”**, execute as seguintes etapas.</span><span class="sxs-lookup"><span data-stu-id="e766a-212">On the **“Add Employee”** dialog page, perform the following steps.</span></span>

    ![Convidar Pessoas](./media/active-directory-saas-pingboard-tutorial/create_testuser_name.png)

    <span data-ttu-id="e766a-214">a.</span><span class="sxs-lookup"><span data-stu-id="e766a-214">a.</span></span> <span data-ttu-id="e766a-215">Na caixa de texto **Nome Completo**, digite o nome completo de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e766a-215">In the **Full Name** textbox, type the full name of Britta Simon.</span></span>

    <span data-ttu-id="e766a-216">b.</span><span class="sxs-lookup"><span data-stu-id="e766a-216">b.</span></span> <span data-ttu-id="e766a-217">Na caixa de texto **Email**, digite o endereço de email da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e766a-217">In the **Email** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="e766a-218">c.</span><span class="sxs-lookup"><span data-stu-id="e766a-218">c.</span></span> <span data-ttu-id="e766a-219">Na caixa de texto **Cargo**, digite o cargo de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e766a-219">In the **Job Title** textbox, type the job title of Britta Simon.</span></span>

    <span data-ttu-id="e766a-220">d.</span><span class="sxs-lookup"><span data-stu-id="e766a-220">d.</span></span> <span data-ttu-id="e766a-221">Na lista suspensa **Local**, selecione o local de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e766a-221">In the **Location** dropdown, select the location  of Britta Simon.</span></span>
    
    <span data-ttu-id="e766a-222">e.</span><span class="sxs-lookup"><span data-stu-id="e766a-222">e.</span></span> <span data-ttu-id="e766a-223">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e766a-223">Click **Add**.</span></span>   

4. <span data-ttu-id="e766a-224">Uma tela de confirmação aparecerá para confirmar a adição do usuário.</span><span class="sxs-lookup"><span data-stu-id="e766a-224">A confirmation screen will come up to confirm the addition of user.</span></span>
    
    ![confirmar](./media/active-directory-saas-pingboard-tutorial/create_testuser_confirm.png)
        
    > [!NOTE]
    > <span data-ttu-id="e766a-226">O titular da conta do Active Directory do Azure receberá um email e seguirá um link para confirmar a conta antes que ela se torne ativa.</span><span class="sxs-lookup"><span data-stu-id="e766a-226">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e766a-227">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e766a-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e766a-228">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Pingboard.</span><span class="sxs-lookup"><span data-stu-id="e766a-228">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Pingboard.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="e766a-230">**Para atribuir Brenda Fernandes ao Pingboard, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e766a-230">**To assign Britta Simon to Pingboard, perform the following steps:**</span></span>

1. <span data-ttu-id="e766a-231">No portal de gerenciamento do Azure, abra a exibição de aplicativos e, em seguida, navegue até o modo de exibição de diretório e vá para **aplicativos empresariais** e clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e766a-231">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="e766a-233">Na lista de aplicativos, selecione **Pingboard**.</span><span class="sxs-lookup"><span data-stu-id="e766a-233">In the applications list, select **Pingboard**.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_app.png) 

3. <span data-ttu-id="e766a-235">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="e766a-235">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="e766a-237">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e766a-237">Click **Add** button.</span></span> <span data-ttu-id="e766a-238">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e766a-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="e766a-240">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="e766a-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e766a-241">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e766a-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e766a-242">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e766a-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e766a-243">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="e766a-243">Testing single sign-on</span></span>

<span data-ttu-id="e766a-244">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="e766a-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e766a-245">Ao clicar no bloco Pingboard no Painel de Acesso, você deverá ser conectado automaticamente ao aplicativo Pingboard.</span><span class="sxs-lookup"><span data-stu-id="e766a-245">When you click the Pingboard tile in the Access Panel, you should get automatically signed-on to your Pingboard application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e766a-246">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="e766a-246">Additional resources</span></span>

* [<span data-ttu-id="e766a-247">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="e766a-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e766a-248">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e766a-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_203.png
