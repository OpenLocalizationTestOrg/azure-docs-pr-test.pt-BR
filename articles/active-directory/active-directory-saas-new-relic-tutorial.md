---
title: "Tutorial: Integração do Azure Active Directory ao New Relic | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o New Relic."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3186b9a8-f4d8-45e2-ad82-6275f95e7aa6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: 605e85c23a849f70fcc0237361d7a891f716ca3a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-new-relic"></a><span data-ttu-id="245b3-103">Tutorial: Integração do Active Directory do Azure com o New Relic</span><span class="sxs-lookup"><span data-stu-id="245b3-103">Tutorial: Azure Active Directory integration with New Relic</span></span>

<span data-ttu-id="245b3-104">Neste tutorial, você aprenderá a integrar o New Relic ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="245b3-104">In this tutorial, you learn how to integrate New Relic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="245b3-105">A integração do New Relic ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="245b3-105">Integrating New Relic with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="245b3-106">No Azure AD, é possível controlar quem tem acesso ao New Relic</span><span class="sxs-lookup"><span data-stu-id="245b3-106">You can control in Azure AD who has access to New Relic</span></span>
- <span data-ttu-id="245b3-107">Você pode permitir que seus usuários façam logon automaticamente no New Relic (logon único) com as contas do Azure AD deles</span><span class="sxs-lookup"><span data-stu-id="245b3-107">You can enable your users to automatically get signed-on to New Relic (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="245b3-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="245b3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="245b3-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="245b3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="245b3-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="245b3-110">Prerequisites</span></span>

<span data-ttu-id="245b3-111">Para configurar a integração do Azure AD com o New Relic, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="245b3-111">To configure Azure AD integration with New Relic, you need the following items:</span></span>

- <span data-ttu-id="245b3-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="245b3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="245b3-113">Uma assinatura habilitada para logon único do New Relic</span><span class="sxs-lookup"><span data-stu-id="245b3-113">A New Relic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="245b3-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="245b3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="245b3-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="245b3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="245b3-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="245b3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="245b3-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="245b3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="245b3-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="245b3-118">Scenario description</span></span>
<span data-ttu-id="245b3-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="245b3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="245b3-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="245b3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="245b3-121">Adicionar o New Relic da Galeria</span><span class="sxs-lookup"><span data-stu-id="245b3-121">Adding New Relic from the gallery</span></span>
2. <span data-ttu-id="245b3-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="245b3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-new-relic-from-the-gallery"></a><span data-ttu-id="245b3-123">Adicionar o New Relic da Galeria</span><span class="sxs-lookup"><span data-stu-id="245b3-123">Adding New Relic from the gallery</span></span>
<span data-ttu-id="245b3-124">Para configurar a integração do New Relic ao Azure AD, você precisará adicionar o New Relic da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="245b3-124">To configure the integration of New Relic into Azure AD, you need to add New Relic from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="245b3-125">**Para adicionar o do New Relic da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="245b3-125">**To add New Relic from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="245b3-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="245b3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="245b3-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="245b3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="245b3-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="245b3-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="245b3-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="245b3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="245b3-133">Na caixa de pesquisa, digite **New Relic**.</span><span class="sxs-lookup"><span data-stu-id="245b3-133">In the search box, type **New Relic**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_search.png)

5. <span data-ttu-id="245b3-135">No painel de resultados, selecione **New Relic** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="245b3-135">In the results panel, select **New Relic**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="245b3-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="245b3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="245b3-138">Nesta seção, você configurará e testará o logon único do Azure AD com o New Relic, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="245b3-138">In this section, you configure and test Azure AD single sign-on with New Relic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="245b3-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do New Relic é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="245b3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in New Relic is to a user in Azure AD.</span></span> <span data-ttu-id="245b3-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no New Relic.</span><span class="sxs-lookup"><span data-stu-id="245b3-140">In other words, a link relationship between an Azure AD user and the related user in New Relic needs to be established.</span></span>

<span data-ttu-id="245b3-141">No New Relic, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="245b3-141">In New Relic, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="245b3-142">Para configurar e testar o logon único do Azure AD com o New Relic, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="245b3-142">To configure and test Azure AD single sign-on with New Relic, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="245b3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="245b3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="245b3-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="245b3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="245b3-145">**[Criar um usuário de teste do New Relic](#creating-a-new-relic-test-user)** – para ter um equivalente de Brenda Fernandes no New Relic que esteja vinculado à representação desse usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="245b3-145">**[Creating a New Relic test user](#creating-a-new-relic-test-user)** - to have a counterpart of Britta Simon in New Relic that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="245b3-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="245b3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="245b3-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="245b3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="245b3-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="245b3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="245b3-149">Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único no aplicativo New Relic.</span><span class="sxs-lookup"><span data-stu-id="245b3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your New Relic application.</span></span>

<span data-ttu-id="245b3-150">**Para configurar o logon único do Azure AD com o New Relic, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="245b3-150">**To configure Azure AD single sign-on with New Relic, perform the following steps:**</span></span>

1. <span data-ttu-id="245b3-151">No Portal do Azure, na página de integração de aplicativos do **New Relic**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="245b3-151">In the Azure portal, on the **New Relic** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="245b3-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="245b3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_samlbase.png)

3. <span data-ttu-id="245b3-155">Na seção **URLs e Domínio do New Relic**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="245b3-155">On the **New Relic Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_url.png)

    <span data-ttu-id="245b3-157">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<subdomain>.newrelic.com`</span><span class="sxs-lookup"><span data-stu-id="245b3-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.newrelic.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="245b3-158">O valor não é real.</span><span class="sxs-lookup"><span data-stu-id="245b3-158">The value is not real.</span></span> <span data-ttu-id="245b3-159">Atualize o valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="245b3-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="245b3-160">Contate a [equipe de suporte ao Cliente do New Relic](https://support.newrelic.com/) para obter o valor.</span><span class="sxs-lookup"><span data-stu-id="245b3-160">Contact [New Relic Client support team](https://support.newrelic.com/) to get the value.</span></span> 
 
4. <span data-ttu-id="245b3-161">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="245b3-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_certificate.png) 

5. <span data-ttu-id="245b3-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="245b3-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-new-relic-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="245b3-165">Na seção **Configuração do New Relic**, clique em **Configurar o New Relic** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="245b3-165">On the **New Relic Configuration** section, click **Configure New Relic** to open **Configure sign-on** window.</span></span> <span data-ttu-id="245b3-166">Copie a **URL de Saída e a URL do Serviço de Logon Único SAML** da **seção Referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="245b3-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_configure.png) 

7. <span data-ttu-id="245b3-168">Em outra janela do navegador da Web, entre em seu site de empresa do **New Relic** como administrador.</span><span class="sxs-lookup"><span data-stu-id="245b3-168">In a different web browser window, sign on to your **New Relic** company site as administrator.</span></span>

8. <span data-ttu-id="245b3-169">No menu na parte superior, clique em **Configurações de Conta**.</span><span class="sxs-lookup"><span data-stu-id="245b3-169">In the menu on the top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="245b3-170">![Configurações de Conta](./media/active-directory-saas-new-relic-tutorial/ic797036.png "Configurações de Conta")</span><span class="sxs-lookup"><span data-stu-id="245b3-170">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797036.png "Account Settings")</span></span>

9. <span data-ttu-id="245b3-171">Clique na guia **Segurança e autenticação** e na guia **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="245b3-171">Click the **Security and authentication** tab, and then click the **Single sign on** tab.</span></span>
   
    <span data-ttu-id="245b3-172">![Logon Único](./media/active-directory-saas-new-relic-tutorial/ic797037.png "Logon Único")</span><span class="sxs-lookup"><span data-stu-id="245b3-172">![Single Sign-On](./media/active-directory-saas-new-relic-tutorial/ic797037.png "Single Sign-On")</span></span>

10. <span data-ttu-id="245b3-173">Na página da caixa de diálogo SAML, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="245b3-173">On the SAML dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="245b3-174">![SAML](./media/active-directory-saas-new-relic-tutorial/ic797038.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="245b3-174">![SAML](./media/active-directory-saas-new-relic-tutorial/ic797038.png "SAML")</span></span>
   
   <span data-ttu-id="245b3-175">a.</span><span class="sxs-lookup"><span data-stu-id="245b3-175">a.</span></span> <span data-ttu-id="245b3-176">Clique em **Escolher Arquivo** para carregar seu certificado baixado do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="245b3-176">Click **Choose File** to upload your downloaded Azure Active Directory certificate.</span></span>

   <span data-ttu-id="245b3-177">b.</span><span class="sxs-lookup"><span data-stu-id="245b3-177">b.</span></span> <span data-ttu-id="245b3-178">Na caixa de texto **URL de Acesso Remoto**, cole o valor da **URL de Serviço de Logon Único do SAML** copiado do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="245b3-178">In the **Remote login URL** textbox,  paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="245b3-179">c.</span><span class="sxs-lookup"><span data-stu-id="245b3-179">c.</span></span> <span data-ttu-id="245b3-180">Na caixa de texto **URL de chegada de Logoff**, cole o valor da **URL de Saída** copiado do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="245b3-180">In the **Logout landing URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

   <span data-ttu-id="245b3-181">d.</span><span class="sxs-lookup"><span data-stu-id="245b3-181">d.</span></span> <span data-ttu-id="245b3-182">Clique em **Salvar minhas alterações**.</span><span class="sxs-lookup"><span data-stu-id="245b3-182">Click **Save my changes**.</span></span>

> [!TIP]
> <span data-ttu-id="245b3-183">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="245b3-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="245b3-184">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="245b3-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="245b3-185">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="245b3-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="245b3-186">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="245b3-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="245b3-187">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="245b3-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="245b3-189">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="245b3-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="245b3-190">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="245b3-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-new-relic-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="245b3-192">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="245b3-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-new-relic-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="245b3-194">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="245b3-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-new-relic-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="245b3-196">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="245b3-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-new-relic-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="245b3-198">a.</span><span class="sxs-lookup"><span data-stu-id="245b3-198">a.</span></span> <span data-ttu-id="245b3-199">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="245b3-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="245b3-200">b.</span><span class="sxs-lookup"><span data-stu-id="245b3-200">b.</span></span> <span data-ttu-id="245b3-201">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="245b3-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="245b3-202">c.</span><span class="sxs-lookup"><span data-stu-id="245b3-202">c.</span></span> <span data-ttu-id="245b3-203">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="245b3-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="245b3-204">d.</span><span class="sxs-lookup"><span data-stu-id="245b3-204">d.</span></span> <span data-ttu-id="245b3-205">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="245b3-205">Click **Create**.</span></span>
 
### <a name="creating-a-new-relic-test-user"></a><span data-ttu-id="245b3-206">Criar um usuário de teste do New Relic</span><span class="sxs-lookup"><span data-stu-id="245b3-206">Creating a New Relic test user</span></span>

<span data-ttu-id="245b3-207">Para permitir que os usuários do Azure Active Directory façam logon no New Relic, eles deverão ser provisionados no New Relic.</span><span class="sxs-lookup"><span data-stu-id="245b3-207">In order to enable Azure Active Directory users to log in to New Relic, they must be provisioned into New Relic.</span></span> <span data-ttu-id="245b3-208">No caso do New Relic, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="245b3-208">In the case of New Relic, provisioning is a manual task.</span></span>

<span data-ttu-id="245b3-209">**Para provisionar uma conta de usuário no New Relic, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="245b3-209">**To provision a user account to New Relic, perform the following steps:**</span></span>

1. <span data-ttu-id="245b3-210">Faça logon em seu site de empresa do **New Relic** como administrador.</span><span class="sxs-lookup"><span data-stu-id="245b3-210">Log in to your **New Relic** company site as administrator.</span></span>

2. <span data-ttu-id="245b3-211">No menu na parte superior, clique em **Configurações de Conta**.</span><span class="sxs-lookup"><span data-stu-id="245b3-211">In the menu on the top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="245b3-212">![Configurações de Conta](./media/active-directory-saas-new-relic-tutorial/ic797040.png "Configurações de Conta")</span><span class="sxs-lookup"><span data-stu-id="245b3-212">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797040.png "Account Settings")</span></span>

3. <span data-ttu-id="245b3-213">No painel **Conta** no lado esquerdo, clique em **Resumo** e em **Adicionar usuário**.</span><span class="sxs-lookup"><span data-stu-id="245b3-213">In the **Account** pane on the left side, click **Summary**, and then click **Add user**.</span></span>
   
    <span data-ttu-id="245b3-214">![Configurações de Conta](./media/active-directory-saas-new-relic-tutorial/ic797041.png "Configurações de Conta")</span><span class="sxs-lookup"><span data-stu-id="245b3-214">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797041.png "Account Settings")</span></span>

4. <span data-ttu-id="245b3-215">No diálogo **Usuários ativos** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="245b3-215">On the **Active users** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="245b3-216">![Usuários ativos](./media/active-directory-saas-new-relic-tutorial/ic797042.png "Usuários ativos")</span><span class="sxs-lookup"><span data-stu-id="245b3-216">![Active Users](./media/active-directory-saas-new-relic-tutorial/ic797042.png "Active Users")</span></span>
   
    <span data-ttu-id="245b3-217">a.</span><span class="sxs-lookup"><span data-stu-id="245b3-217">a.</span></span> <span data-ttu-id="245b3-218">Na caixa de texto **Email** , digite o endereço de email de um usuário válido do Active Directory do Azure que você deseja provisionar.</span><span class="sxs-lookup"><span data-stu-id="245b3-218">In the **Email** textbox, type the email address of a valid Azure Active Directory user you want to provision.</span></span>

    <span data-ttu-id="245b3-219">b.</span><span class="sxs-lookup"><span data-stu-id="245b3-219">b.</span></span> <span data-ttu-id="245b3-220">Como **Função**, selecione **Usuário**.</span><span class="sxs-lookup"><span data-stu-id="245b3-220">As **Role** select **User**.</span></span>

    <span data-ttu-id="245b3-221">c.</span><span class="sxs-lookup"><span data-stu-id="245b3-221">c.</span></span> <span data-ttu-id="245b3-222">Clique em **Adicionar este usuário**.</span><span class="sxs-lookup"><span data-stu-id="245b3-222">Click **Add this user**.</span></span>

>[!NOTE]
><span data-ttu-id="245b3-223">É possível usar qualquer outra ferramenta de criação da conta de usuário do New Relic ou as APIs fornecidas pelo New Relic para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="245b3-223">You can use any other New Relic user account creation tools or APIs provided by New Relic to provision AAD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="245b3-224">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="245b3-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="245b3-225">Nesta seção, você concederá a Brenda Fernandes acesso ao New Relic para que ela fique habilitada a usar o logon único do Azure.</span><span class="sxs-lookup"><span data-stu-id="245b3-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to New Relic.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="245b3-227">**Para atribuir Brenda Fernandes ao New Relic, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="245b3-227">**To assign Britta Simon to New Relic, perform the following steps:**</span></span>

1. <span data-ttu-id="245b3-228">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="245b3-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="245b3-230">Na lista de aplicativos, selecione **New Relic**.</span><span class="sxs-lookup"><span data-stu-id="245b3-230">In the applications list, select **New Relic**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_app.png) 

3. <span data-ttu-id="245b3-232">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="245b3-232">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="245b3-234">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="245b3-234">Click **Add** button.</span></span> <span data-ttu-id="245b3-235">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="245b3-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="245b3-237">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="245b3-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="245b3-238">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="245b3-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="245b3-239">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="245b3-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="245b3-240">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="245b3-240">Testing single sign-on</span></span>

<span data-ttu-id="245b3-241">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="245b3-241">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="245b3-242">Quando você clicar no bloco New Relic no Painel de Acesso, você deverá ser automaticamente conectado ao seu aplicativo New Relic.</span><span class="sxs-lookup"><span data-stu-id="245b3-242">When you click the New Relic tile in the Access Panel, you should get automatically signed-on to your New Relic application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="245b3-243">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="245b3-243">Additional resources</span></span>

* [<span data-ttu-id="245b3-244">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="245b3-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="245b3-245">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="245b3-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_203.png

