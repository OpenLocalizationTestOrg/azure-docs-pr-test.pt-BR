---
title: "Tutorial: Integração do Azure Active Directory com o Kudos | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Kudos."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 39c47ce6-4944-47ba-8f53-3afa95398034
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 353798fcfd4ad7ce017fc2fddf4110715db3ace2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kudos"></a><span data-ttu-id="0369c-103">Tutorial: Integração do Active Directory do Azure com o Kudos</span><span class="sxs-lookup"><span data-stu-id="0369c-103">Tutorial: Azure Active Directory integration with Kudos</span></span>

<span data-ttu-id="0369c-104">Neste tutorial, você aprenderá a integrar o Kudos ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="0369c-104">In this tutorial, you learn how to integrate Kudos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0369c-105">A integração do Kudos ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="0369c-105">Integrating Kudos with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0369c-106">Você pode controlar no Azure AD quem terá acesso ao Kudos</span><span class="sxs-lookup"><span data-stu-id="0369c-106">You can control in Azure AD who has access to Kudos</span></span>
- <span data-ttu-id="0369c-107">Você pode permitir que seus usuários entrem automaticamente no Kudos (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0369c-107">You can enable your users to automatically get signed-on to Kudos (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0369c-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0369c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0369c-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0369c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0369c-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0369c-110">Prerequisites</span></span>

<span data-ttu-id="0369c-111">Para configurar a integração do Azure AD com o Kudos, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="0369c-111">To configure Azure AD integration with Kudos, you need the following items:</span></span>

- <span data-ttu-id="0369c-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0369c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0369c-113">Uma assinatura habilitada para logon único do Kudos</span><span class="sxs-lookup"><span data-stu-id="0369c-113">A Kudos single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0369c-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="0369c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0369c-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="0369c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0369c-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="0369c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0369c-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0369c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0369c-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="0369c-118">Scenario description</span></span>
<span data-ttu-id="0369c-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="0369c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0369c-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="0369c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0369c-121">Adicionar o Kudos da galeria</span><span class="sxs-lookup"><span data-stu-id="0369c-121">Adding Kudos from the gallery</span></span>
2. <span data-ttu-id="0369c-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0369c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kudos-from-the-gallery"></a><span data-ttu-id="0369c-123">Adicionar o Kudos da galeria</span><span class="sxs-lookup"><span data-stu-id="0369c-123">Adding Kudos from the gallery</span></span>
<span data-ttu-id="0369c-124">Para configurar a integração do Kudos ao Azure AD, você precisará adicionar o Kudos da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="0369c-124">To configure the integration of Kudos into Azure AD, you need to add Kudos from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0369c-125">**Para adicionar o Kudos da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="0369c-125">**To add Kudos from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0369c-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0369c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0369c-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="0369c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0369c-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="0369c-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="0369c-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0369c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="0369c-133">Na caixa de pesquisa, digite **Kudos**.</span><span class="sxs-lookup"><span data-stu-id="0369c-133">In the search box, type **Kudos**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_search.png)

5. <span data-ttu-id="0369c-135">No painel de resultados, selecione **Kudos** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0369c-135">In the results panel, select **Kudos**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0369c-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0369c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0369c-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Kudos, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="0369c-138">In this section, you configure and test Azure AD single sign-on with Kudos based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0369c-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Kudos é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0369c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kudos is to a user in Azure AD.</span></span> <span data-ttu-id="0369c-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Kudos.</span><span class="sxs-lookup"><span data-stu-id="0369c-140">In other words, a link relationship between an Azure AD user and the related user in Kudos needs to be established.</span></span>

<span data-ttu-id="0369c-141">No Kudos, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="0369c-141">In Kudos, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0369c-142">Para configurar e testar o logon único do Azure AD com o Kudos, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="0369c-142">To configure and test Azure AD single sign-on with Kudos, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0369c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="0369c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0369c-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="0369c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0369c-145">**[Criar um usuário de teste do Kudos](#creating-a-kudos-test-user)** – para ter um equivalente de Brenda Fernandes no Kudos que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0369c-145">**[Creating a Kudos test user](#creating-a-kudos-test-user)** - to have a counterpart of Britta Simon in Kudos that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0369c-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="0369c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0369c-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="0369c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0369c-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0369c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0369c-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Kudos.</span><span class="sxs-lookup"><span data-stu-id="0369c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kudos application.</span></span>

<span data-ttu-id="0369c-150">**Para configurar o logon único do Azure AD com o Kudos, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="0369c-150">**To configure Azure AD single sign-on with Kudos, perform the following steps:**</span></span>

1. <span data-ttu-id="0369c-151">No portal do Azure, na página de integração de aplicativos do **Kudos**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="0369c-151">In the Azure portal, on the **Kudos** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="0369c-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="0369c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_samlbase.png)

3. <span data-ttu-id="0369c-155">Na seção **URLs e Domínio do Kudos**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="0369c-155">On the **Kudos Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_url.png)

    <span data-ttu-id="0369c-157">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<company>.kudosnow.com`</span><span class="sxs-lookup"><span data-stu-id="0369c-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.kudosnow.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="0369c-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="0369c-158">This value is not real.</span></span> <span data-ttu-id="0369c-159">Atualize esse valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="0369c-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="0369c-160">Para obter esse valor, entre em contato com a [equipe de suporte do cliente Kudos](http://success.kudosnow.com/home).</span><span class="sxs-lookup"><span data-stu-id="0369c-160">Contact [Kudos Client support team](http://success.kudosnow.com/home) to get this value.</span></span> 
 
4. <span data-ttu-id="0369c-161">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="0369c-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_certificate.png) 

5. <span data-ttu-id="0369c-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="0369c-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kudos-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0369c-165">Na seção **Configuração do Kudos**, clique em **Configurar Kudos** para abrir a janela **Configurar Logon**.</span><span class="sxs-lookup"><span data-stu-id="0369c-165">On the **Kudos Configuration** section, click **Configure Kudos** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0369c-166">Copie a **URL do serviço de logon único do SAML e a URL de logoff** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="0369c-166">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_configure.png) 

7. <span data-ttu-id="0369c-168">Em uma janela diferente do navegador da Web, faça logon no site da sua empresa do Kudos como administrador.</span><span class="sxs-lookup"><span data-stu-id="0369c-168">In a different web browser window, log into your Kudos company site as an administrator.</span></span>

8. <span data-ttu-id="0369c-169">No menu na parte superior, clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="0369c-169">In the menu on the top, click **Settings**.</span></span>
   
    <span data-ttu-id="0369c-170">![Configurações](./media/active-directory-saas-kudos-tutorial/ic787806.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="0369c-170">![Settings](./media/active-directory-saas-kudos-tutorial/ic787806.png "Settings")</span></span>

9. <span data-ttu-id="0369c-171">Clique em **Integrações \> SSO**.</span><span class="sxs-lookup"><span data-stu-id="0369c-171">Click **Integrations \> SSO**.</span></span>

10. <span data-ttu-id="0369c-172">Na seção **SSO** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="0369c-172">In the **SSO** section, perform the following steps:</span></span>
   
    <span data-ttu-id="0369c-173">![SSO](./media/active-directory-saas-kudos-tutorial/ic787807.png "SSO")</span><span class="sxs-lookup"><span data-stu-id="0369c-173">![SSO](./media/active-directory-saas-kudos-tutorial/ic787807.png "SSO")</span></span>
   
    <span data-ttu-id="0369c-174">a.</span><span class="sxs-lookup"><span data-stu-id="0369c-174">a.</span></span> <span data-ttu-id="0369c-175">Na caixa de texto **URL de Logon**, cole o valor da **URL do Serviço de Logon Único do SAML** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0369c-175">In **Sign on URL** textbox, paste the value of  **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="0369c-176">b.</span><span class="sxs-lookup"><span data-stu-id="0369c-176">b.</span></span> <span data-ttu-id="0369c-177">Abra seu certificado codificado em Base 64 no bloco de notas, copie o conteúdo dele na área de transferência e cole-o na caixa de texto **Certificado X.509**</span><span class="sxs-lookup"><span data-stu-id="0369c-177">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 certificate** textbox</span></span>
   
    <span data-ttu-id="0369c-178">c.</span><span class="sxs-lookup"><span data-stu-id="0369c-178">c.</span></span> <span data-ttu-id="0369c-179">Em **URL de Logoff**, cole o valor da **URL de Saída** copiado no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0369c-179">In **Logout To URL**, paste the value of  **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="0369c-180">d.</span><span class="sxs-lookup"><span data-stu-id="0369c-180">d.</span></span> <span data-ttu-id="0369c-181">Na caixa de texto **Sua URL do Kudos** , digite o nome de sua empresa.</span><span class="sxs-lookup"><span data-stu-id="0369c-181">In the **Your Kudos URL** textbox, type your company name.</span></span>
   
    <span data-ttu-id="0369c-182">e.</span><span class="sxs-lookup"><span data-stu-id="0369c-182">e.</span></span> <span data-ttu-id="0369c-183">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="0369c-183">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="0369c-184">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="0369c-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0369c-185">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="0369c-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0369c-186">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0369c-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0369c-187">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0369c-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="0369c-188">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="0369c-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="0369c-190">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="0369c-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0369c-191">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0369c-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kudos-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0369c-193">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="0369c-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kudos-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0369c-195">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0369c-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kudos-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0369c-197">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="0369c-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kudos-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0369c-199">a.</span><span class="sxs-lookup"><span data-stu-id="0369c-199">a.</span></span> <span data-ttu-id="0369c-200">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="0369c-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0369c-201">b.</span><span class="sxs-lookup"><span data-stu-id="0369c-201">b.</span></span> <span data-ttu-id="0369c-202">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="0369c-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0369c-203">c.</span><span class="sxs-lookup"><span data-stu-id="0369c-203">c.</span></span> <span data-ttu-id="0369c-204">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="0369c-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0369c-205">d.</span><span class="sxs-lookup"><span data-stu-id="0369c-205">d.</span></span> <span data-ttu-id="0369c-206">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="0369c-206">Click **Create**.</span></span>
 
### <a name="creating-a-kudos-test-user"></a><span data-ttu-id="0369c-207">Criar um usuário de teste do Kudos</span><span class="sxs-lookup"><span data-stu-id="0369c-207">Creating a Kudos test user</span></span>

<span data-ttu-id="0369c-208">Para permitir que os usuários do AD do Azure façam logon no Kudos, eles devem ser provisionados no Kudos.</span><span class="sxs-lookup"><span data-stu-id="0369c-208">In order to enable Azure AD users to log into Kudos, they must be provisioned into Kudos.</span></span> 

<span data-ttu-id="0369c-209">No caso do Kudos, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="0369c-209">In the case of Kudos, provisioning is a manual task.</span></span>

<span data-ttu-id="0369c-210">**Para provisionar uma conta de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="0369c-210">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="0369c-211">Faça logon em seu site de empresa do **Kudos** como administrador.</span><span class="sxs-lookup"><span data-stu-id="0369c-211">Log in to your **Kudos** company site as administrator.</span></span>

2. <span data-ttu-id="0369c-212">No menu na parte superior, clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="0369c-212">In the menu on the top, click **Settings**.</span></span>
   
   <span data-ttu-id="0369c-213">![Configurações](./media/active-directory-saas-kudos-tutorial/ic787806.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="0369c-213">![Settings](./media/active-directory-saas-kudos-tutorial/ic787806.png "Settings")</span></span>

3. <span data-ttu-id="0369c-214">Clique em **Usuário Administrador**.</span><span class="sxs-lookup"><span data-stu-id="0369c-214">Click **User Admin**.</span></span>

4. <span data-ttu-id="0369c-215">Clique na guia **Usuários** e, em seguida, clique em **Adicionar um usuário**.</span><span class="sxs-lookup"><span data-stu-id="0369c-215">Click the **Users** tab, and then click **Add a User**.</span></span>
   
   <span data-ttu-id="0369c-216">![Usuário Administrador](./media/active-directory-saas-kudos-tutorial/ic787809.png "Usuário Administrador")</span><span class="sxs-lookup"><span data-stu-id="0369c-216">![User Admin](./media/active-directory-saas-kudos-tutorial/ic787809.png "User Admin")</span></span>

5. <span data-ttu-id="0369c-217">Na seção **Adicionar um Usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="0369c-217">In the **Add a User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="0369c-218">![Adicionar um Usuário](./media/active-directory-saas-kudos-tutorial/ic787810.png "Adicionar um Usuário")</span><span class="sxs-lookup"><span data-stu-id="0369c-218">![Add a User](./media/active-directory-saas-kudos-tutorial/ic787810.png "Add a User")</span></span>
   
    <span data-ttu-id="0369c-219">a.</span><span class="sxs-lookup"><span data-stu-id="0369c-219">a.</span></span> <span data-ttu-id="0369c-220">Digite o **Nome**, o **Sobrenome** e o **Email** e outros detalhes de uma conta válida do Azure Active Directory que você deseja provisionar nas caixas de texto relacionadas.</span><span class="sxs-lookup"><span data-stu-id="0369c-220">Type the **First Name**, **Last Name**, **Email** and other details of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   
    <span data-ttu-id="0369c-221">b.</span><span class="sxs-lookup"><span data-stu-id="0369c-221">b.</span></span> <span data-ttu-id="0369c-222">Clique em **Criar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="0369c-222">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="0369c-223">É possível usar qualquer outra ferramenta de criação da conta de usuário do Kudos ou APIs fornecidas pelo Kudos para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="0369c-223">You can use any other Kudos user account creation tools or APIs provided by Kudos to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0369c-224">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0369c-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0369c-225">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Kudos.</span><span class="sxs-lookup"><span data-stu-id="0369c-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kudos.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="0369c-227">**Para atribuir Brenda Fernandes ao Kudos, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="0369c-227">**To assign Britta Simon to Kudos, perform the following steps:**</span></span>

1. <span data-ttu-id="0369c-228">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="0369c-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="0369c-230">Na lista de aplicativos, selecione **Kudos**.</span><span class="sxs-lookup"><span data-stu-id="0369c-230">In the applications list, select **Kudos**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_app.png) 

3. <span data-ttu-id="0369c-232">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="0369c-232">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="0369c-234">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="0369c-234">Click **Add** button.</span></span> <span data-ttu-id="0369c-235">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0369c-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="0369c-237">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="0369c-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0369c-238">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0369c-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0369c-239">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0369c-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0369c-240">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="0369c-240">Testing single sign-on</span></span>

<span data-ttu-id="0369c-241">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="0369c-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0369c-242">Ao clicar no bloco Kudos no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo Kudos.</span><span class="sxs-lookup"><span data-stu-id="0369c-242">When you click the Kudos tile in the Access Panel, you should get automatically signed-on to your Kudos application.</span></span> <span data-ttu-id="0369c-243">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0369c-243">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0369c-244">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="0369c-244">Additional resources</span></span>

* [<span data-ttu-id="0369c-245">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="0369c-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0369c-246">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0369c-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_203.png

