---
title: "Tutorial: Integração do Azure Active Directory ao Bime | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Bime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bdcf0729-c880-4c95-b739-0f6345b17dd8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 8f46ff1265d302ab114747b4b45227e58718166b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bime"></a><span data-ttu-id="44744-103">Tutorial: Integração do Azure Active Directory ao Bime</span><span class="sxs-lookup"><span data-stu-id="44744-103">Tutorial: Azure Active Directory integration with Bime</span></span>

<span data-ttu-id="44744-104">Neste tutorial, você aprenderá a integrar o Bime ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="44744-104">In this tutorial, you learn how to integrate Bime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="44744-105">A integração do Bime ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="44744-105">Integrating Bime with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="44744-106">Você pode controlar no Azure AD quem terá acesso ao Bime</span><span class="sxs-lookup"><span data-stu-id="44744-106">You can control in Azure AD who has access to Bime</span></span>
- <span data-ttu-id="44744-107">Você pode permitir que seus usuários façam logon automaticamente no Bime (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="44744-107">You can enable your users to automatically get signed-on to Bime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="44744-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="44744-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="44744-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="44744-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44744-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="44744-110">Prerequisites</span></span>

<span data-ttu-id="44744-111">Para configurar a integração do Azure AD ao Bime, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="44744-111">To configure Azure AD integration with Bime, you need the following items:</span></span>

- <span data-ttu-id="44744-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="44744-112">An Azure AD subscription</span></span>
- <span data-ttu-id="44744-113">Uma assinatura do Bime habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="44744-113">A Bime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="44744-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="44744-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="44744-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="44744-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="44744-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="44744-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="44744-117">Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="44744-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="44744-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="44744-118">Scenario description</span></span>
<span data-ttu-id="44744-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="44744-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="44744-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="44744-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="44744-121">Adicionar o Bime da galeria</span><span class="sxs-lookup"><span data-stu-id="44744-121">Adding Bime from the gallery</span></span>
2. <span data-ttu-id="44744-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="44744-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bime-from-the-gallery"></a><span data-ttu-id="44744-123">Adicionar o Bime da galeria</span><span class="sxs-lookup"><span data-stu-id="44744-123">Adding Bime from the gallery</span></span>
<span data-ttu-id="44744-124">Para configurar a integração do Bime ao Azure AD, você precisará adicionar o Bime à sua lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="44744-124">To configure the integration of Bime into Azure AD, you need to add Bime from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="44744-125">**Para adicionar o Bime por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="44744-125">**To add Bime from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="44744-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="44744-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="44744-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="44744-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="44744-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="44744-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="44744-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="44744-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="44744-133">Na caixa de pesquisa, digite **Bime**.</span><span class="sxs-lookup"><span data-stu-id="44744-133">In the search box, type **Bime**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bime-tutorial/tutorial_bime_search.png)

5. <span data-ttu-id="44744-135">No painel de resultados, selecione **Bime** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="44744-135">In the results panel, select **Bime**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bime-tutorial/tutorial_bime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="44744-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="44744-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="44744-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Bime com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="44744-138">In this section, you configure and test Azure AD single sign-on with Bime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="44744-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Bime é equivalente a um determinado usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="44744-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Bime is to a user in Azure AD.</span></span> <span data-ttu-id="44744-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Bime.</span><span class="sxs-lookup"><span data-stu-id="44744-140">In other words, a link relationship between an Azure AD user and the related user in Bime needs to be established.</span></span>

<span data-ttu-id="44744-141">No Bime, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="44744-141">In Bime, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="44744-142">Para configurar e testar o logon único do Azure AD com o Bime, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="44744-142">To configure and test Azure AD single sign-on with Bime, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="44744-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="44744-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="44744-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="44744-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="44744-145">**[Criação de um usuário de teste do Bime](#creating-a-bime-test-user)** – para ter um equivalente de Brenda Fernandes no Bime que esteja vinculado à sua representação no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="44744-145">**[Creating a Bime test user](#creating-a-bime-test-user)** - to have a counterpart of Britta Simon in Bime that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="44744-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="44744-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="44744-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="44744-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="44744-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="44744-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="44744-149">Nesta seção, você habilitará o logon único do Azure AD no portal do Azure e configurará o logon único no aplicativo Bime.</span><span class="sxs-lookup"><span data-stu-id="44744-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bime application.</span></span>

<span data-ttu-id="44744-150">**Para configurar o logon único do Azure AD com o Bime, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="44744-150">**To configure Azure AD single sign-on with Bime, perform the following steps:**</span></span>

1. <span data-ttu-id="44744-151">No portal do Azure, na página de integração de aplicativo do **Bime**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="44744-151">In the Azure portal, on the **Bime** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="44744-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="44744-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-bime-tutorial/tutorial_bime_samlbase.png)

3. <span data-ttu-id="44744-155">Na seção **URLs e Domínio do Bime**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="44744-155">On the **Bime Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bime-tutorial/tutorial_bime_url.png)

    <span data-ttu-id="44744-157">a.</span><span class="sxs-lookup"><span data-stu-id="44744-157">a.</span></span> <span data-ttu-id="44744-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<tenant-name>.Bimeapp.com`</span><span class="sxs-lookup"><span data-stu-id="44744-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.Bimeapp.com`</span></span>

    <span data-ttu-id="44744-159">b.</span><span class="sxs-lookup"><span data-stu-id="44744-159">b.</span></span> <span data-ttu-id="44744-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<tenant-name>.Bimeapp.com`</span><span class="sxs-lookup"><span data-stu-id="44744-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant-name>.Bimeapp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="44744-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="44744-161">These values are not real.</span></span> <span data-ttu-id="44744-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="44744-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="44744-163">Entre em contato com a [equipe de suporte ao cliente do Bime](https://bime.zendesk.com/hc/categories/202604307-Support-tech-notes-and-tips-) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="44744-163">Contact [Bime Client support team](https://bime.zendesk.com/hc/categories/202604307-Support-tech-notes-and-tips-) to get these values.</span></span> 
 
4. <span data-ttu-id="44744-164">Na seção **Certificado de Autenticação SAML**, copie o valor da **IMPRESSÃO DIGITAL** do certificado.</span><span class="sxs-lookup"><span data-stu-id="44744-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value from the certificate.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bime-tutorial/tutorial_bime_certificate.png) 

5. <span data-ttu-id="44744-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="44744-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bime-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="44744-168">Na seção **Configuração do Bime**, clique em **Configurar Bime** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="44744-168">On the **Bime Configuration** section, click **Configure Bime** to open **Configure sign-on** window.</span></span> <span data-ttu-id="44744-169">Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="44744-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bime-tutorial/tutorial_bime_configure.png) 

7. <span data-ttu-id="44744-171">Em outra janela do navegador da Web, faça logon em seu site de empresa Bime como um administrador.</span><span class="sxs-lookup"><span data-stu-id="44744-171">In a different web browser window, log into your Bime company site as an administrator.</span></span>

8. <span data-ttu-id="44744-172">Na barra de ferramentas, clique em **Administrador** e em **Conta**.</span><span class="sxs-lookup"><span data-stu-id="44744-172">In the toolbar, click **Admin**, and then **Account**.</span></span>
   
    <span data-ttu-id="44744-173">![Admin](./media/active-directory-saas-bime-tutorial/ic775558.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="44744-173">![Admin](./media/active-directory-saas-bime-tutorial/ic775558.png "Admin")</span></span>

9. <span data-ttu-id="44744-174">Na página de configuração da conta, execute as seguintes etapas: </span><span class="sxs-lookup"><span data-stu-id="44744-174">On the account configuration page, perform the following steps:</span></span>
   
    <span data-ttu-id="44744-175">![Configurar Logon Único](./media/active-directory-saas-bime-tutorial/ic775559.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="44744-175">![Configure Single Sign-On](./media/active-directory-saas-bime-tutorial/ic775559.png "Configure Single Sign-On")</span></span>
   
    <span data-ttu-id="44744-176">a.</span><span class="sxs-lookup"><span data-stu-id="44744-176">a.</span></span> <span data-ttu-id="44744-177">Selecione **Habilitar autenticação SAML**.</span><span class="sxs-lookup"><span data-stu-id="44744-177">Select **Enable SAML authentication**.</span></span>

    <span data-ttu-id="44744-178">b.</span><span class="sxs-lookup"><span data-stu-id="44744-178">b.</span></span> <span data-ttu-id="44744-179">Na caixa de texto **URL de Acesso Remoto**, cole o valor da **URL de Serviço de Logon Único SAML** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="44744-179">In the **Remote Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="44744-180">c.</span><span class="sxs-lookup"><span data-stu-id="44744-180">c.</span></span>  <span data-ttu-id="44744-181">Cole o valor da **Impressão digital** do portal do Azure na caixa de texto **Impressão digital do certificado**.</span><span class="sxs-lookup"><span data-stu-id="44744-181">Paste the **Thumbprint** value from Azure portal into the **Certificate Fingerprint** textbox.</span></span>       
   
    <span data-ttu-id="44744-182">d.</span><span class="sxs-lookup"><span data-stu-id="44744-182">d.</span></span> <span data-ttu-id="44744-183">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="44744-183">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="44744-184">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="44744-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="44744-185">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="44744-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="44744-186">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="44744-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="44744-187">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="44744-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="44744-188">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="44744-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="44744-190">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="44744-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="44744-191">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="44744-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="44744-193">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="44744-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="44744-195">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="44744-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="44744-197">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="44744-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="44744-199">a.</span><span class="sxs-lookup"><span data-stu-id="44744-199">a.</span></span> <span data-ttu-id="44744-200">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="44744-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="44744-201">b.</span><span class="sxs-lookup"><span data-stu-id="44744-201">b.</span></span> <span data-ttu-id="44744-202">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="44744-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="44744-203">c.</span><span class="sxs-lookup"><span data-stu-id="44744-203">c.</span></span> <span data-ttu-id="44744-204">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="44744-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="44744-205">d.</span><span class="sxs-lookup"><span data-stu-id="44744-205">d.</span></span> <span data-ttu-id="44744-206">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="44744-206">Click **Create**.</span></span>
 
### <a name="creating-a-bime-test-user"></a><span data-ttu-id="44744-207">Criação de um usuário de teste do Bime</span><span class="sxs-lookup"><span data-stu-id="44744-207">Creating a Bime test user</span></span>

<span data-ttu-id="44744-208">Para que possam fazer logon no Bime, os usuários do Azure AD deverão ser provisionados nele.</span><span class="sxs-lookup"><span data-stu-id="44744-208">In order to enable Azure AD users to log in to Bime, they must be provisioned into Bime.</span></span> <span data-ttu-id="44744-209">No caso do Bime, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="44744-209">In the case of Bime, provisioning is a manual task.</span></span>

<span data-ttu-id="44744-210">**Para configurar o provisionamento de usuários, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="44744-210">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="44744-211">Faça logon em seu locatário do **Bime** .</span><span class="sxs-lookup"><span data-stu-id="44744-211">Log in to your **Bime** tenant.</span></span>

2. <span data-ttu-id="44744-212">Na barra de ferramentas, clique em **Administrador** e em **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="44744-212">In the toolbar, click **Admin**, and then **Users**.</span></span>
   
    <span data-ttu-id="44744-213">![Admin](./media/active-directory-saas-bime-tutorial/ic775561.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="44744-213">![Admin](./media/active-directory-saas-bime-tutorial/ic775561.png "Admin")</span></span>

3. <span data-ttu-id="44744-214">Na **Lista de Usuários**, clique em **Adicionar Novo Usuário** (“+”).</span><span class="sxs-lookup"><span data-stu-id="44744-214">In the **Users List**, click **Add New User** (“+”).</span></span>
   
    <span data-ttu-id="44744-215">![Usuários](./media/active-directory-saas-bime-tutorial/ic775562.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="44744-215">![Users](./media/active-directory-saas-bime-tutorial/ic775562.png "Users")</span></span>

4. <span data-ttu-id="44744-216">Na página do diálogo **Detalhes do Usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="44744-216">On the **User Details** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="44744-217">![Detalhes do Usuário](./media/active-directory-saas-bime-tutorial/ic775563.png "Detalhes do Usuário")</span><span class="sxs-lookup"><span data-stu-id="44744-217">![User Details](./media/active-directory-saas-bime-tutorial/ic775563.png "User Details")</span></span>
   
    <span data-ttu-id="44744-218">a.</span><span class="sxs-lookup"><span data-stu-id="44744-218">a.</span></span> <span data-ttu-id="44744-219">Na caixa de texto **Nome**, digite o nome do usuário, como **Brenda**.</span><span class="sxs-lookup"><span data-stu-id="44744-219">In the **First name** textbox, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="44744-220">b.</span><span class="sxs-lookup"><span data-stu-id="44744-220">b.</span></span> <span data-ttu-id="44744-221">Na caixa de texto **Sobrenome**, digite o sobrenome do usuário como **Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="44744-221">In the **Last name** textbox, enter the last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="44744-222">c.</span><span class="sxs-lookup"><span data-stu-id="44744-222">c.</span></span> <span data-ttu-id="44744-223">Na caixa de texto **Email**, insira o email do usuário, como **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="44744-223">In the **Email** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="44744-224">d.</span><span class="sxs-lookup"><span data-stu-id="44744-224">d.</span></span> <span data-ttu-id="44744-225">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="44744-225">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="44744-226">É possível usar qualquer outra ferramenta de criação da conta de usuário do Bime ou as APIs fornecidas pelo Bime para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="44744-226">You can use any other Bime user account creation tools or APIs provided by Bime to provision AAD user accounts.</span></span>
>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="44744-227">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="44744-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="44744-228">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Bime.</span><span class="sxs-lookup"><span data-stu-id="44744-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Bime.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="44744-230">**Para atribuir Brenda Fernandes ao Bime, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="44744-230">**To assign Britta Simon to Bime, perform the following steps:**</span></span>

1. <span data-ttu-id="44744-231">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="44744-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="44744-233">Na lista de aplicativos, selecione o **Bime**.</span><span class="sxs-lookup"><span data-stu-id="44744-233">In the applications list, select **Bime**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bime-tutorial/tutorial_bime_app.png) 

3. <span data-ttu-id="44744-235">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="44744-235">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="44744-237">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="44744-237">Click **Add** button.</span></span> <span data-ttu-id="44744-238">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="44744-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="44744-240">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="44744-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="44744-241">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="44744-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="44744-242">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="44744-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="44744-243">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="44744-243">Testing single sign-on</span></span>

<span data-ttu-id="44744-244">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="44744-244">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="44744-245">Ao clicar no bloco do Bime no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo Bime.</span><span class="sxs-lookup"><span data-stu-id="44744-245">When you click the Bime tile in the Access Panel, you should get automatically signed-on to your Bime application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="44744-246">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="44744-246">Additional resources</span></span>

* [<span data-ttu-id="44744-247">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="44744-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="44744-248">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="44744-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bime-tutorial/tutorial_general_203.png

