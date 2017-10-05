---
title: "Tutorial: integração do Azure Active Directory com o Flatter Files | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Active Directory do Azure e o Flatter Files."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f86fe5e3-0e91-40d6-869c-3df6912d27ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: e02150cb27768d7b403bdca191bc1f189821def4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-flatter-files"></a><span data-ttu-id="d5124-103">Tutorial: Integração do Active Directory do Azure ao Flatter Files</span><span class="sxs-lookup"><span data-stu-id="d5124-103">Tutorial: Azure Active Directory integration with Flatter Files</span></span>

<span data-ttu-id="d5124-104">Neste tutorial, você aprenderá a integrar o Flatter Files ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="d5124-104">In this tutorial, you learn how to integrate Flatter Files with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d5124-105">A integração do Flatter Files ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="d5124-105">Integrating Flatter Files with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d5124-106">No AD do Azure, você pode controlar quem tem acesso ao Flatter Files</span><span class="sxs-lookup"><span data-stu-id="d5124-106">You can control in Azure AD who has access to Flatter Files</span></span>
- <span data-ttu-id="d5124-107">Você pode permitir que seus usuários façam logon automaticamente no Flatter Files (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d5124-107">You can enable your users to automatically get signed-on to Flatter Files (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d5124-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d5124-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d5124-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d5124-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d5124-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d5124-110">Prerequisites</span></span>

<span data-ttu-id="d5124-111">Para configurar a integração do AD do Azure ao Flatter Files, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="d5124-111">To configure Azure AD integration with Flatter Files, you need the following items:</span></span>

- <span data-ttu-id="d5124-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d5124-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d5124-113">Uma assinatura do Flatter Files com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="d5124-113">A Flatter Files single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d5124-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="d5124-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d5124-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="d5124-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d5124-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="d5124-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d5124-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d5124-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d5124-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="d5124-118">Scenario description</span></span>
<span data-ttu-id="d5124-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="d5124-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d5124-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="d5124-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d5124-121">Adicionando Flatter Files da galeria</span><span class="sxs-lookup"><span data-stu-id="d5124-121">Adding Flatter Files from the gallery</span></span>
2. <span data-ttu-id="d5124-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d5124-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-flatter-files-from-the-gallery"></a><span data-ttu-id="d5124-123">Adicionando Flatter Files da galeria</span><span class="sxs-lookup"><span data-stu-id="d5124-123">Adding Flatter Files from the gallery</span></span>
<span data-ttu-id="d5124-124">Para configurar a integração do Flatter Files ao AD do Azure, você precisará adicionar o Flatter Files da galeria à sua lista de aplicativos de SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="d5124-124">To configure the integration of Flatter Files into Azure AD, you need to add Flatter Files from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d5124-125">**Para adicionar o Flatter Files da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="d5124-125">**To add Flatter Files from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d5124-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d5124-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d5124-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="d5124-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d5124-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="d5124-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="d5124-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d5124-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="d5124-133">Na caixa de pesquisa, digite **Flatter Files**.</span><span class="sxs-lookup"><span data-stu-id="d5124-133">In the search box, type **Flatter Files**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_search.png)

5. <span data-ttu-id="d5124-135">No painel de resultados, selecione **Flatter Files** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d5124-135">In the results panel, select **Flatter Files**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d5124-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d5124-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d5124-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Flatter Files com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="d5124-138">In this section, you configure and test Azure AD single sign-on with Flatter Files based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d5124-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Flatter Files é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d5124-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Flatter Files is to a user in Azure AD.</span></span> <span data-ttu-id="d5124-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Flatter Files.</span><span class="sxs-lookup"><span data-stu-id="d5124-140">In other words, a link relationship between an Azure AD user and the related user in Flatter Files needs to be established.</span></span>

<span data-ttu-id="d5124-141">No Flatter Files, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="d5124-141">In Flatter Files, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d5124-142">Para configurar e testar o logon único do AD do Azure com o Flatter Files, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="d5124-142">To configure and test Azure AD single sign-on with Flatter Files, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d5124-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="d5124-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d5124-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="d5124-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d5124-145">**[Criação de um usuário de teste do Flatter Files](#creating-a-flatter-files-test-user)** – para ter um equivalente de Brenda Fernandes no Flatter Files que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d5124-145">**[Creating a Flatter Files test user](#creating-a-flatter-files-test-user)** - to have a counterpart of Britta Simon in Flatter Files that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d5124-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="d5124-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d5124-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="d5124-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d5124-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d5124-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d5124-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Flatter Files.</span><span class="sxs-lookup"><span data-stu-id="d5124-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Flatter Files application.</span></span>

<span data-ttu-id="d5124-150">**Para configurar o logon único do AD do Azure com o Flatter Files, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="d5124-150">**To configure Azure AD single sign-on with Flatter Files, perform the following steps:**</span></span>

1. <span data-ttu-id="d5124-151">No portal do Azure, na página de integração de aplicativos do **Flatter Files**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="d5124-151">In the Azure portal, on the **Flatter Files** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="d5124-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="d5124-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_samlbase.png)

3. <span data-ttu-id="d5124-155">Na seção **URLs e Domínio do Flatter Files**, o usuário não precisa executar nenhuma etapa, já que o aplicativo já está integrado ao Azure.</span><span class="sxs-lookup"><span data-stu-id="d5124-155">On the **Flatter Files Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_url.png)
 
4. <span data-ttu-id="d5124-157">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="d5124-157">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_certificate.png) 

5. <span data-ttu-id="d5124-159">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="d5124-159">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-flatter-files-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d5124-161">Na seção **Configuração do Flatter Files**, clique em **Configurar Flatter Files** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="d5124-161">On the **Flatter Files Configuration** section, click **Configure Flatter Files** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d5124-162">Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="d5124-162">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_configure.png) 

7. <span data-ttu-id="d5124-164">Faça logon no aplicativo Flatter Files como administrador.</span><span class="sxs-lookup"><span data-stu-id="d5124-164">Sign-on to your Flatter Files application as an administrator.</span></span>

8. <span data-ttu-id="d5124-165">Clique em **PAINEL**.</span><span class="sxs-lookup"><span data-stu-id="d5124-165">Click **DASHBOARD**.</span></span> 
   
    ![Configurar Logon Único](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_05.png)  

9. <span data-ttu-id="d5124-167">Clique em **Configurações** e execute as etapas a seguir na guia **Empresa**:</span><span class="sxs-lookup"><span data-stu-id="d5124-167">Click **Settings**, and then perform the following steps on the **Company** tab:</span></span> 
   
    ![Configurar Logon Único](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_06.png)  
    
    <span data-ttu-id="d5124-169">a.</span><span class="sxs-lookup"><span data-stu-id="d5124-169">a.</span></span> <span data-ttu-id="d5124-170">Selecione **Usar SAML 2.0 para Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="d5124-170">Select **Use SAML 2.0 for Authentication**.</span></span>
    
    <span data-ttu-id="d5124-171">b.</span><span class="sxs-lookup"><span data-stu-id="d5124-171">b.</span></span> <span data-ttu-id="d5124-172">Clique em **Configurar SAML**.</span><span class="sxs-lookup"><span data-stu-id="d5124-172">Click **Configure SAML**.</span></span>

8. <span data-ttu-id="d5124-173">No diálogo **Configuração de SAML** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="d5124-173">On the **SAML Configuration** dialog, perform the following steps:</span></span> 
   
    ![Configurar Logon Único](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_08.png)  
   
    <span data-ttu-id="d5124-175">a.</span><span class="sxs-lookup"><span data-stu-id="d5124-175">a.</span></span> <span data-ttu-id="d5124-176">Na caixa de texto **Domínio**, digite seu domínio registrado.</span><span class="sxs-lookup"><span data-stu-id="d5124-176">In the **Domain** textbox, type your registered domain.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="d5124-177">Se não tiver um domínio registrado, entre em contato com a equipe de suporte do Flatter Files pelo email [support@flatterfiles.com](mailto:support@flatterfiles.com).</span><span class="sxs-lookup"><span data-stu-id="d5124-177">If you don't have a registered domain yet, contact your Flatter Files support team via [support@flatterfiles.com](mailto:support@flatterfiles.com).</span></span> 
    
    <span data-ttu-id="d5124-178">b.</span><span class="sxs-lookup"><span data-stu-id="d5124-178">b.</span></span> <span data-ttu-id="d5124-179">Na caixa de texto **URL do Provedor de Identidade**, cole o valor da **URL de Serviço de Logon Único do SAML** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d5124-179">In **Identity Provider URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied form Azure portal.</span></span>
   
    <span data-ttu-id="d5124-180">c.</span><span class="sxs-lookup"><span data-stu-id="d5124-180">c.</span></span>  <span data-ttu-id="d5124-181">Abra seu certificado codificado em Base 64 no bloco de notas, copie o conteúdo dele na área de transferência e cole-o na caixa de texto **Certificado do Provedor de Identidade**.</span><span class="sxs-lookup"><span data-stu-id="d5124-181">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Identity Provider Certificate** textbox.</span></span>

    <span data-ttu-id="d5124-182">d.</span><span class="sxs-lookup"><span data-stu-id="d5124-182">d.</span></span> <span data-ttu-id="d5124-183">Clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="d5124-183">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="d5124-184">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="d5124-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d5124-185">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="d5124-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d5124-186">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d5124-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d5124-187">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d5124-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="d5124-188">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="d5124-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="d5124-190">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="d5124-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d5124-191">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d5124-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d5124-193">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="d5124-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d5124-195">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d5124-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d5124-197">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="d5124-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d5124-199">a.</span><span class="sxs-lookup"><span data-stu-id="d5124-199">a.</span></span> <span data-ttu-id="d5124-200">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="d5124-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d5124-201">b.</span><span class="sxs-lookup"><span data-stu-id="d5124-201">b.</span></span> <span data-ttu-id="d5124-202">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="d5124-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d5124-203">c.</span><span class="sxs-lookup"><span data-stu-id="d5124-203">c.</span></span> <span data-ttu-id="d5124-204">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="d5124-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d5124-205">d.</span><span class="sxs-lookup"><span data-stu-id="d5124-205">d.</span></span> <span data-ttu-id="d5124-206">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d5124-206">Click **Create**.</span></span>
 
### <a name="creating-a-flatter-files-test-user"></a><span data-ttu-id="d5124-207">Criação de um usuário de teste do Flatter Files</span><span class="sxs-lookup"><span data-stu-id="d5124-207">Creating a Flatter Files test user</span></span>

<span data-ttu-id="d5124-208">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no Flatter Files.</span><span class="sxs-lookup"><span data-stu-id="d5124-208">The objective of this section is to create a user called Britta Simon in Flatter Files.</span></span>

<span data-ttu-id="d5124-209">**Para criar um usuário chamado Brenda Fernandes no Flatter Files, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="d5124-209">**To create a user called Britta Simon in Flatter Files, perform the following steps:**</span></span>

1. <span data-ttu-id="d5124-210">Faça logon no site da empresa **Flatter Files** como administrador.</span><span class="sxs-lookup"><span data-stu-id="d5124-210">Sign on to your **Flatter Files** company site as administrator.</span></span>

2. <span data-ttu-id="d5124-211">No painel de navegação à esquerda, clique em **Configurações** e, em seguida, clique na guia **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="d5124-211">In the navigation pane on the left, click **Settings**, and then click the **Users** tab.</span></span>
   
    ![Criar um usuário do Flatter Files](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_09.png)

3. <span data-ttu-id="d5124-213">Clique em **Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="d5124-213">Click **Add User**.</span></span> 

4. <span data-ttu-id="d5124-214">No diálogo **Adicionar Usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="d5124-214">On the **Add User** dialog, perform the following steps:</span></span>
   
    ![Criar um usuário do Flatter Files](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_10.png)

    <span data-ttu-id="d5124-216">a.</span><span class="sxs-lookup"><span data-stu-id="d5124-216">a.</span></span> <span data-ttu-id="d5124-217">Na caixa de texto **Nome**, digite **Brenda**.</span><span class="sxs-lookup"><span data-stu-id="d5124-217">In the **First Name** textbox, type **Britta**.</span></span>
   
    <span data-ttu-id="d5124-218">b.</span><span class="sxs-lookup"><span data-stu-id="d5124-218">b.</span></span> <span data-ttu-id="d5124-219">Na caixa de texto **Sobrenome**, digite **Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="d5124-219">In the **Last Name** textbox, type **Simon**.</span></span> 
   
    <span data-ttu-id="d5124-220">c.</span><span class="sxs-lookup"><span data-stu-id="d5124-220">c.</span></span> <span data-ttu-id="d5124-221">Na caixa de texto **Endereço de Email**, digite o endereço de email de Brenda no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d5124-221">In the **Email Address** textbox, type Britta's email address in the Azure portal.</span></span>
   
    <span data-ttu-id="d5124-222">d.</span><span class="sxs-lookup"><span data-stu-id="d5124-222">d.</span></span> <span data-ttu-id="d5124-223">Clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="d5124-223">Click **Submit**.</span></span>   


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d5124-224">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d5124-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d5124-225">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Flatter Files.</span><span class="sxs-lookup"><span data-stu-id="d5124-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Flatter Files.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="d5124-227">**Para atribuir Brenda Fernandes ao Flatter Files, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="d5124-227">**To assign Britta Simon to Flatter Files, perform the following steps:**</span></span>

1. <span data-ttu-id="d5124-228">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="d5124-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="d5124-230">Na lista de aplicativos, escolha **Flatter Files**.</span><span class="sxs-lookup"><span data-stu-id="d5124-230">In the applications list, select **Flatter Files**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_app.png) 

3. <span data-ttu-id="d5124-232">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="d5124-232">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="d5124-234">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d5124-234">Click **Add** button.</span></span> <span data-ttu-id="d5124-235">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d5124-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="d5124-237">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="d5124-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d5124-238">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d5124-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d5124-239">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d5124-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d5124-240">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="d5124-240">Testing single sign-on</span></span>

<span data-ttu-id="d5124-241">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="d5124-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d5124-242">Quando você clica no bloco Flatter Files no Painel de Acesso, deve fazer logon automaticamente no seu aplicativo Flatter Files.</span><span class="sxs-lookup"><span data-stu-id="d5124-242">When you click the Flatter Files tile in the Access Panel, you should get automatically signed-on to your Flatter Files application.</span></span>
<span data-ttu-id="d5124-243">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d5124-243">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d5124-244">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="d5124-244">Additional resources</span></span>

* [<span data-ttu-id="d5124-245">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="d5124-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d5124-246">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d5124-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_203.png

