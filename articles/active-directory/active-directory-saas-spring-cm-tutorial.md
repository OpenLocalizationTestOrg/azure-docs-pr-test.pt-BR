---
title: "Tutorial: Integração do Azure Active Directory com o SpringCM | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o SpringCM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4a42f797-ac58-4aca-a8e6-53bfe5529083
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: edfd06a06c730597fee4569ca1ce29092b45244a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-springcm"></a><span data-ttu-id="82372-103">Tutorial: Integração do Azure Active Directory com o SpringCM</span><span class="sxs-lookup"><span data-stu-id="82372-103">Tutorial: Azure Active Directory integration with SpringCM</span></span>

<span data-ttu-id="82372-104">Neste tutorial, você aprenderá a integrar o SpringCM ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="82372-104">In this tutorial, you learn how to integrate SpringCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="82372-105">A integração do SpringCM ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="82372-105">Integrating SpringCM with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="82372-106">No Azure AD, é possível controlar quem tem acesso ao SpringCM</span><span class="sxs-lookup"><span data-stu-id="82372-106">You can control in Azure AD who has access to SpringCM</span></span>
- <span data-ttu-id="82372-107">Você pode permitir que os usuários façam logon automaticamente no SpringCM (logon único) com as respectivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="82372-107">You can enable your users to automatically get signed-on to SpringCM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="82372-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="82372-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="82372-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="82372-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82372-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="82372-110">Prerequisites</span></span>

<span data-ttu-id="82372-111">Para configurar a integração do Azure AD ao SpringCM, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="82372-111">To configure Azure AD integration with SpringCM, you need the following items:</span></span>

- <span data-ttu-id="82372-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="82372-112">An Azure AD subscription</span></span>
- <span data-ttu-id="82372-113">Uma assinatura habilitada para logon único do SpringCM</span><span class="sxs-lookup"><span data-stu-id="82372-113">A SpringCM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="82372-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="82372-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="82372-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="82372-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="82372-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="82372-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="82372-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="82372-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="82372-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="82372-118">Scenario description</span></span>
<span data-ttu-id="82372-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="82372-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="82372-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="82372-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="82372-121">Adicionar o SpringCM da galeria</span><span class="sxs-lookup"><span data-stu-id="82372-121">Adding SpringCM from the gallery</span></span>
2. <span data-ttu-id="82372-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="82372-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-springcm-from-the-gallery"></a><span data-ttu-id="82372-123">Adicionar o SpringCM da galeria</span><span class="sxs-lookup"><span data-stu-id="82372-123">Adding SpringCM from the gallery</span></span>
<span data-ttu-id="82372-124">Para configurar a integração do SpringCM ao Azure AD, você precisará adicionar o SpringCM da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="82372-124">To configure the integration of SpringCM into Azure AD, you need to add SpringCM from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="82372-125">**Para adicionar o SpringCM da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="82372-125">**To add SpringCM from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="82372-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="82372-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="82372-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="82372-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="82372-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="82372-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="82372-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="82372-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="82372-133">Na caixa de pesquisa, digite **SpringCM**.</span><span class="sxs-lookup"><span data-stu-id="82372-133">In the search box, type **SpringCM**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_search.png)

5. <span data-ttu-id="82372-135">No painel de resultados, selecione **SpringCM** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="82372-135">In the results panel, select **SpringCM**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="82372-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="82372-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="82372-138">Nesta seção, você configurará e testará o logon único do Azure AD com o SpringCM com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="82372-138">In this section, you configure and test Azure AD single sign-on with SpringCM based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="82372-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do SpringCM é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="82372-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SpringCM is to a user in Azure AD.</span></span> <span data-ttu-id="82372-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no SpringCM.</span><span class="sxs-lookup"><span data-stu-id="82372-140">In other words, a link relationship between an Azure AD user and the related user in SpringCM needs to be established.</span></span>

<span data-ttu-id="82372-141">No SpringCM, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="82372-141">In SpringCM, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="82372-142">Para configurar e testar o logon único do Azure AD com o SpringCM, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="82372-142">To configure and test Azure AD single sign-on with SpringCM, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="82372-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="82372-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="82372-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="82372-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="82372-145">**[Criar de um usuário de teste do SpringCM](#creating-a-springcm-test-user)** – para ter um equivalente de Brenda Fernandes no SpringCM que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="82372-145">**[Creating a SpringCM test user](#creating-a-springcm-test-user)** - to have a counterpart of Britta Simon in SpringCM that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="82372-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="82372-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="82372-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="82372-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="82372-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="82372-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="82372-149">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo SpringCM.</span><span class="sxs-lookup"><span data-stu-id="82372-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SpringCM application.</span></span>

<span data-ttu-id="82372-150">**Para configurar o logon único do Azure AD com o SpringCM, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="82372-150">**To configure Azure AD single sign-on with SpringCM, perform the following steps:**</span></span>

1. <span data-ttu-id="82372-151">No Portal do Azure, na página de integração de aplicativos do **SpringCM**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="82372-151">In the Azure portal, on the **SpringCM** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="82372-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="82372-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_samlbase.png)

3. <span data-ttu-id="82372-155">Na seção **Domínio e URLs do SpringCM**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="82372-155">On the **SpringCM Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_url.png)

    <span data-ttu-id="82372-157">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`</span><span class="sxs-lookup"><span data-stu-id="82372-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="82372-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="82372-158">This value is not real.</span></span> <span data-ttu-id="82372-159">Atualize esse valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="82372-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="82372-160">Contate a [equipe de suporte ao cliente do SpringCM](https://knowledge.springcm.com/support) para obter esse valor.</span><span class="sxs-lookup"><span data-stu-id="82372-160">Contact [SpringCM Client support team](https://knowledge.springcm.com/support) to get this value.</span></span> 
 
4. <span data-ttu-id="82372-161">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Bruto)** e, em seguida, salve o arquivo de certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="82372-161">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_certificate.png) 

5. <span data-ttu-id="82372-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="82372-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-spring-cm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="82372-165">Na seção **Configuração do SpringCM**, clique em **Configurar o SpringCM** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="82372-165">On the **SpringCM Configuration** section, click **Configure SpringCM** to open **Configure sign-on** window.</span></span> <span data-ttu-id="82372-166">Copie a **ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="82372-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_configure.png)   

7. <span data-ttu-id="82372-168">Em outra janela do navegador da Web, entre em seu site de empresa do **SpringCM** como administrador.</span><span class="sxs-lookup"><span data-stu-id="82372-168">In a different web browser window, sign on to your **SpringCM** company site as administrator.</span></span>

8. <span data-ttu-id="82372-169">No menu na parte superior, clique em **IR PARA**, clique em **Preferências** e, na seção **Preferências da Conta**, clique em **SSO do SAML**.</span><span class="sxs-lookup"><span data-stu-id="82372-169">In the menu on the top, click **GO TO**, click **Preferences**, and then, in the **Account Preferences** section, click **SAML SSO**.</span></span>
   
    <span data-ttu-id="82372-170">![SSO do SAML](./media/active-directory-saas-spring-cm-tutorial/ic797051.png "SSO do SAML")</span><span class="sxs-lookup"><span data-stu-id="82372-170">![SAML SSO](./media/active-directory-saas-spring-cm-tutorial/ic797051.png "SAML SSO")</span></span>

9. <span data-ttu-id="82372-171">Na seção Configuração do Provedor de Identidade, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="82372-171">In the Identity Provider Configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="82372-172">![Configuração do Provedor de Identidade](./media/active-directory-saas-spring-cm-tutorial/ic797052.png "Configuração do Provedor de Identidade")</span><span class="sxs-lookup"><span data-stu-id="82372-172">![Identity Provider Configuration](./media/active-directory-saas-spring-cm-tutorial/ic797052.png "Identity Provider Configuration")</span></span>
    
    <span data-ttu-id="82372-173">a.</span><span class="sxs-lookup"><span data-stu-id="82372-173">a.</span></span> <span data-ttu-id="82372-174">Para carregar seu certificado baixado do Azure Active Directory, clique em **Selecionar Certificado do Emissor** ou **Alterar Certificado do Emissor**.</span><span class="sxs-lookup"><span data-stu-id="82372-174">To upload your downloaded Azure Active Directory certificate, click **Select Issuer Certificate** or **Change Issuer Certificate**.</span></span>
    
    <span data-ttu-id="82372-175">b.</span><span class="sxs-lookup"><span data-stu-id="82372-175">b.</span></span> <span data-ttu-id="82372-176">Cole o valor de **ID de Entidade do SAML** copiado no Portal do Azure na caixa de texto **Emissor**.</span><span class="sxs-lookup"><span data-stu-id="82372-176">Paste **SAML Entity ID** value, which you have copied from Azure portal into the **Issuer** textbox.</span></span>
    
    <span data-ttu-id="82372-177">c.</span><span class="sxs-lookup"><span data-stu-id="82372-177">c.</span></span> <span data-ttu-id="82372-178">Cole o valor da **URL do Serviço de Logon Único SAML** copiado do Portal do Azure na caixa de texto **Ponto de Extremidade Iniciado do Provedor de Serviço (SP)**.</span><span class="sxs-lookup"><span data-stu-id="82372-178">Paste **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **Service Provider (SP) Initiated Endpoint** textbox.</span></span>
            
    <span data-ttu-id="82372-179">d.</span><span class="sxs-lookup"><span data-stu-id="82372-179">d.</span></span> <span data-ttu-id="82372-180">Selecione **SAML Habilitado** como **Habilitar**.</span><span class="sxs-lookup"><span data-stu-id="82372-180">Select **SAML Enabled** as **Enable**.</span></span>

    <span data-ttu-id="82372-181">e.</span><span class="sxs-lookup"><span data-stu-id="82372-181">e.</span></span> <span data-ttu-id="82372-182">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="82372-182">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="82372-183">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="82372-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="82372-184">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="82372-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="82372-185">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="82372-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="82372-186">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="82372-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="82372-187">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="82372-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="82372-189">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="82372-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="82372-190">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="82372-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="82372-192">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="82372-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="82372-194">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="82372-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="82372-196">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="82372-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="82372-198">a.</span><span class="sxs-lookup"><span data-stu-id="82372-198">a.</span></span> <span data-ttu-id="82372-199">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="82372-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="82372-200">b.</span><span class="sxs-lookup"><span data-stu-id="82372-200">b.</span></span> <span data-ttu-id="82372-201">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="82372-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="82372-202">c.</span><span class="sxs-lookup"><span data-stu-id="82372-202">c.</span></span> <span data-ttu-id="82372-203">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="82372-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="82372-204">d.</span><span class="sxs-lookup"><span data-stu-id="82372-204">d.</span></span> <span data-ttu-id="82372-205">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="82372-205">Click **Create**.</span></span>
 
### <a name="creating-a-springcm-test-user"></a><span data-ttu-id="82372-206">Criar um usuário de teste do SpringCM</span><span class="sxs-lookup"><span data-stu-id="82372-206">Creating a SpringCM test user</span></span>

<span data-ttu-id="82372-207">Para permitir que os usuários do Azure Active Directory façam logon no SpringCM, eles deverão ser provisionados no SpringCM.</span><span class="sxs-lookup"><span data-stu-id="82372-207">To enable Azure Active Directory users to log in to SpringCM, they must be provisioned into SpringCM.</span></span> <span data-ttu-id="82372-208">No caso do SpringCM, o provisionamento será uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="82372-208">In the case of SpringCM, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="82372-209">Para obter mais informações, veja [Criar e editar um usuário do SpringCM](http://knowledge.springcm.com/create-and-edit-a-springcm-user).</span><span class="sxs-lookup"><span data-stu-id="82372-209">For more information, see [Create and Edit a SpringCM User](http://knowledge.springcm.com/create-and-edit-a-springcm-user).</span></span> 

<span data-ttu-id="82372-210">**Para provisionar uma conta de usuário no SpringCM, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="82372-210">**To provision a user account to SpringCM, perform the following steps:**</span></span>

1. <span data-ttu-id="82372-211">Faça logon em seu site de empresa do **SpringCM** como administrador.</span><span class="sxs-lookup"><span data-stu-id="82372-211">Log in to your **SpringCM** company site as administrator.</span></span>

2. <span data-ttu-id="82372-212">Clique em **IR PARA** e depois em **CATÁLOGO DE ENDEREÇOS**.</span><span class="sxs-lookup"><span data-stu-id="82372-212">Click **GOTO**, and then click **ADDRESS BOOK**.</span></span>
   
    <span data-ttu-id="82372-213">![Criar usuário](./media/active-directory-saas-spring-cm-tutorial/ic797054.png "Criar usuário")</span><span class="sxs-lookup"><span data-stu-id="82372-213">![Create User](./media/active-directory-saas-spring-cm-tutorial/ic797054.png "Create User")</span></span>

3. <span data-ttu-id="82372-214">Clique em **Criar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="82372-214">Click **Create User**.</span></span>

4. <span data-ttu-id="82372-215">Selecione uma **Função de Usuário**.</span><span class="sxs-lookup"><span data-stu-id="82372-215">Select a **User Role**.</span></span>

5. <span data-ttu-id="82372-216">Selecione **Enviar Email de Ativação**.</span><span class="sxs-lookup"><span data-stu-id="82372-216">Select **Send Activation Email**.</span></span>

6. <span data-ttu-id="82372-217">Digite o nome, o sobrenome e o endereço de email de uma conta de usuário válida do Azure Active Directory que você deseja provisionar nas caixas de texto relacionadas.</span><span class="sxs-lookup"><span data-stu-id="82372-217">Type the first name, last name, and email address of a valid Azure Active Directory user account you want to provision into the related textboxes.</span></span>

7. <span data-ttu-id="82372-218">Adicione o usuário a um **Grupo de segurança**.</span><span class="sxs-lookup"><span data-stu-id="82372-218">Add the user to a **Security group**.</span></span>

8. <span data-ttu-id="82372-219">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="82372-219">Click **Save**.</span></span>

  >[!NOTE]
  ><span data-ttu-id="82372-220">É possível usar qualquer outra ferramenta de criação da conta de usuário do SpringCM ou as APIs fornecidas pelo SpringCM para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="82372-220">You can use any other SpringCM user account creation tools or APIs provided by SpringCM to provision AAD user accounts.</span></span>  
  > 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="82372-221">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="82372-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="82372-222">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao SpringCM.</span><span class="sxs-lookup"><span data-stu-id="82372-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SpringCM.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="82372-224">**Para atribuir Brenda Fernandes ao SpringCM, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="82372-224">**To assign Britta Simon to SpringCM, perform the following steps:**</span></span>

1. <span data-ttu-id="82372-225">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="82372-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="82372-227">Na lista de aplicativos, selecione **SpringCM**.</span><span class="sxs-lookup"><span data-stu-id="82372-227">In the applications list, select **SpringCM**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_app.png) 

3. <span data-ttu-id="82372-229">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="82372-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="82372-231">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="82372-231">Click **Add** button.</span></span> <span data-ttu-id="82372-232">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="82372-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="82372-234">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="82372-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="82372-235">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="82372-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="82372-236">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="82372-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="82372-237">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="82372-237">Testing single sign-on</span></span>

<span data-ttu-id="82372-238">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="82372-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
 
<span data-ttu-id="82372-239">Ao clicar no bloco do SpringCM no Painel de Acesso, você deverá ser conectado automaticamente ao aplicativo SpringCM.</span><span class="sxs-lookup"><span data-stu-id="82372-239">When you click the SpringCM tile in the Access Panel, you should get automatically signed-on to your SpringCM application.</span></span>

<span data-ttu-id="82372-240">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="82372-240">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="82372-241">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="82372-241">Additional resources</span></span>

* [<span data-ttu-id="82372-242">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="82372-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="82372-243">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="82372-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_203.png

