---
title: "Tutorial: Integração do Azure Active Directory ao TigerText Secure Messenger | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o TigerText Secure Messenger."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 03f1e128-5bcb-4e49-b6a3-fe22eedc6d5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: e101e5fc84b032b66dd0636bab8bff128791f77c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tigertext-secure-messenger"></a><span data-ttu-id="81a20-103">Tutorial: Integração do Azure Active Directory ao TigerText Secure Messenger</span><span class="sxs-lookup"><span data-stu-id="81a20-103">Tutorial: Azure Active Directory integration with TigerText Secure Messenger</span></span>

<span data-ttu-id="81a20-104">Neste tutorial, você aprenderá a integrar o TigerText Secure Messenger ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="81a20-104">In this tutorial, you learn how to integrate TigerText Secure Messenger with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="81a20-105">A integração do TigerText Secure Messenger ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="81a20-105">Integrating TigerText Secure Messenger with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="81a20-106">No Azure AD, é possível controlar quem tem acesso ao TigerText Secure Messenger</span><span class="sxs-lookup"><span data-stu-id="81a20-106">You can control in Azure AD who has access to TigerText Secure Messenger</span></span>
- <span data-ttu-id="81a20-107">Você pode permitir que os usuários façam logon automaticamente no TigerText Secure Messenger (Logon Único) com as respectivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="81a20-107">You can enable your users to automatically get signed-on to TigerText Secure Messenger (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="81a20-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="81a20-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="81a20-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="81a20-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81a20-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="81a20-110">Prerequisites</span></span>

<span data-ttu-id="81a20-111">Para configurar a integração do Azure AD ao TigerText Secure Messenger, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="81a20-111">To configure Azure AD integration with TigerText Secure Messenger, you need the following items:</span></span>

- <span data-ttu-id="81a20-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="81a20-112">An Azure AD subscription</span></span>
- <span data-ttu-id="81a20-113">Uma assinatura do TigerText Secure Messenger habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="81a20-113">A TigerText Secure Messenger single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="81a20-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="81a20-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="81a20-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="81a20-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="81a20-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="81a20-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="81a20-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="81a20-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="81a20-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="81a20-118">Scenario description</span></span>
<span data-ttu-id="81a20-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="81a20-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="81a20-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="81a20-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="81a20-121">Adicionar o TigerText Secure Messenger da galeria</span><span class="sxs-lookup"><span data-stu-id="81a20-121">Add TigerText Secure Messenger from the gallery</span></span>
2. <span data-ttu-id="81a20-122">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="81a20-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tigertext-secure-messenger-from-the-gallery"></a><span data-ttu-id="81a20-123">Adicionar o TigerText Secure Messenger da galeria</span><span class="sxs-lookup"><span data-stu-id="81a20-123">Add TigerText Secure Messenger from the gallery</span></span>
<span data-ttu-id="81a20-124">Para configurar a integração do TigerText Secure Messenger ao Azure AD, você precisa adicionar o TigerText Secure Messenger da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="81a20-124">To configure the integration of TigerText Secure Messenger into Azure AD, you need to add TigerText Secure Messenger from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="81a20-125">**Para adicionar o TigerText Secure Messenger da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="81a20-125">**To add TigerText Secure Messenger from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="81a20-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="81a20-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="81a20-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="81a20-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="81a20-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="81a20-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="81a20-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="81a20-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="81a20-133">Na caixa de pesquisa, digite **TigerText Secure Messenger**, selecione **TigerText Secure Messenger** no painel de resultados e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="81a20-133">In the search box, type **TigerText Secure Messenger**, select **TigerText Secure Messenger** from result panel then click **Add** button to add the application.</span></span>

    ![Adicionar da galeria](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="81a20-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="81a20-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="81a20-136">Nesta seção, você vai configurar e testar o logon único do Azure AD com o TigerText Secure Messenger, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="81a20-136">In this section, you configure and test Azure AD single sign-on with TigerText Secure Messenger based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="81a20-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do TigerText Secure Messenger é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81a20-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TigerText Secure Messenger is to a user in Azure AD.</span></span> <span data-ttu-id="81a20-138">Em outras palavras, é necessário estabelecer uma relação de vinculação entre um usuário do Azure AD e o usuário relacionado do TigerText Secure Messenger.</span><span class="sxs-lookup"><span data-stu-id="81a20-138">In other words, a link relationship between an Azure AD user and the related user in TigerText Secure Messenger needs to be established.</span></span>

<span data-ttu-id="81a20-139">No TigerText Secure Messenger, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="81a20-139">In TigerText Secure Messenger, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="81a20-140">Para configurar e testar o logon único do Azure AD com o TigerText Secure Messenger, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="81a20-140">To configure and test Azure AD single sign-on with TigerText Secure Messenger, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="81a20-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="81a20-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="81a20-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="81a20-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="81a20-143">**[Criar um usuário de teste do TigerText Secure Messenger](#create-a-tigertext-secure-messenger-test-user)** – para ter um equivalente de Brenda Fernandes no TigerText Secure Messenger vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81a20-143">**[Create a TigerText Secure Messenger test user](#create-a-tigertext-secure-messenger-test-user)** - to have a counterpart of Britta Simon in TigerText Secure Messenger that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="81a20-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81a20-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="81a20-145">**[Testar o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="81a20-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="81a20-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="81a20-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="81a20-147">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo TigerText Secure Messenger.</span><span class="sxs-lookup"><span data-stu-id="81a20-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TigerText Secure Messenger application.</span></span>

<span data-ttu-id="81a20-148">**Para configurar o logon único do Azure AD com o TigerText Secure Messenger, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="81a20-148">**To configure Azure AD single sign-on with TigerText Secure Messenger, perform the following steps:**</span></span>

1. <span data-ttu-id="81a20-149">No Portal do Azure, na página de integração de aplicativos do **TigerText Secure Messenger**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="81a20-149">In the Azure portal, on the **TigerText Secure Messenger** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="81a20-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="81a20-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Logon único baseado em SAML](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_samlbase.png)

3. <span data-ttu-id="81a20-153">Na seção **Domínio e URLs do TigerText Secure Messenger**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="81a20-153">On the **TigerText Secure Messenger Domain and URLs** section, perform the following steps:</span></span>

    ![Seção Domínio e URLs do TigerText Secure Messenger](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_url.png)

    <span data-ttu-id="81a20-155">a.</span><span class="sxs-lookup"><span data-stu-id="81a20-155">a.</span></span> <span data-ttu-id="81a20-156">Na caixa de texto **URL de Logon**, digite uma URL como: `https://home.tigertext.com`</span><span class="sxs-lookup"><span data-stu-id="81a20-156">In the **Sign-on URL** textbox, type URL as: `https://home.tigertext.com`</span></span>

    <span data-ttu-id="81a20-157">b.</span><span class="sxs-lookup"><span data-stu-id="81a20-157">b.</span></span> <span data-ttu-id="81a20-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://saml-lb.tigertext.me/v1/organization/<instance Id>`</span><span class="sxs-lookup"><span data-stu-id="81a20-158">In the **Identifier** textbox, type a URL using the following pattern: `https://saml-lb.tigertext.me/v1/organization/<instance Id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="81a20-159">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="81a20-159">This value is not real.</span></span> <span data-ttu-id="81a20-160">Atualize esse valor com o Identificador real.</span><span class="sxs-lookup"><span data-stu-id="81a20-160">Update this value with the actual Identifier.</span></span> <span data-ttu-id="81a20-161">Contate a [equipe de suporte ao cliente do TigerText Secure Messenger](mailTo:prosupport@tigertext.com) para obter esse valor.</span><span class="sxs-lookup"><span data-stu-id="81a20-161">Contact [TigerText Secure Messenger Client support team](mailTo:prosupport@tigertext.com) to get this value.</span></span> 
 
4. <span data-ttu-id="81a20-162">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="81a20-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Seção Certificado de Autenticação SAML](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_certificate.png) 

5. <span data-ttu-id="81a20-164">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="81a20-164">Click **Save** button.</span></span>

    ![Botão Salvar](./media/active-directory-saas-tigertext-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="81a20-166">Para que o logon único seja configurado para o aplicativo, entre em contato com a [equipe de suporte do TigerText Secure Messenger](mailTo:prosupport@tigertext.com) e forneça os **metadados baixados**.</span><span class="sxs-lookup"><span data-stu-id="81a20-166">To get single sign-on configured for your application, contact [TigerText Secure Messenger support team](mailTo:prosupport@tigertext.com) and provide them the **Downloaded metadata**.</span></span>

> [!TIP]
> <span data-ttu-id="81a20-167">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="81a20-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="81a20-168">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="81a20-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="81a20-169">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="81a20-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="81a20-170">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="81a20-170">Create an Azure AD test user</span></span>
<span data-ttu-id="81a20-171">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="81a20-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="81a20-173">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="81a20-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="81a20-174">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="81a20-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tigertext-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="81a20-176">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="81a20-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Usuários e grupos->Todos os usuários](./media/active-directory-saas-tigertext-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="81a20-178">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="81a20-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Botão Adicionar](./media/active-directory-saas-tigertext-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="81a20-180">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="81a20-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Diálogo do usuário](./media/active-directory-saas-tigertext-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="81a20-182">a.</span><span class="sxs-lookup"><span data-stu-id="81a20-182">a.</span></span> <span data-ttu-id="81a20-183">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="81a20-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="81a20-184">b.</span><span class="sxs-lookup"><span data-stu-id="81a20-184">b.</span></span> <span data-ttu-id="81a20-185">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="81a20-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="81a20-186">c.</span><span class="sxs-lookup"><span data-stu-id="81a20-186">c.</span></span> <span data-ttu-id="81a20-187">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="81a20-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="81a20-188">d.</span><span class="sxs-lookup"><span data-stu-id="81a20-188">d.</span></span> <span data-ttu-id="81a20-189">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="81a20-189">Click **Create**.</span></span>
 
### <a name="create-a-tigertext-secure-messenger-test-user"></a><span data-ttu-id="81a20-190">Criar um usuário de teste do TigerText Secure Messenger</span><span class="sxs-lookup"><span data-stu-id="81a20-190">Create a TigerText Secure Messenger test user</span></span>

<span data-ttu-id="81a20-191">Nesta seção, você criará um usuário chamado Brenda Fernandes no TigerText.</span><span class="sxs-lookup"><span data-stu-id="81a20-191">In this section, you create a user called Britta Simon in TigerText.</span></span> <span data-ttu-id="81a20-192">Contate a [equipe de suporte ao cliente do TigerText Secure Messenger](mailTo:prosupport@tigertext.com) para adicionar os usuários na plataforma TigerText.</span><span class="sxs-lookup"><span data-stu-id="81a20-192">Please reach out to [TigerText Secure Messenger Client support team](mailTo:prosupport@tigertext.com) to add the users in the TigerText platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="81a20-193">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="81a20-193">Assign the Azure AD test user</span></span>

<span data-ttu-id="81a20-194">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao TigerText Secure Messenger.</span><span class="sxs-lookup"><span data-stu-id="81a20-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TigerText Secure Messenger.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="81a20-196">**Para atribuir Brenda Fernandes ao TigerText Secure Messenger, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="81a20-196">**To assign Britta Simon to TigerText Secure Messenger, perform the following steps:**</span></span>

1. <span data-ttu-id="81a20-197">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="81a20-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="81a20-199">Na lista de aplicativos, selecione **TigerText Secure Messenger**.</span><span class="sxs-lookup"><span data-stu-id="81a20-199">In the applications list, select **TigerText Secure Messenger**.</span></span>

    ![TigerText Secure Messenger na lista de aplicativos](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_app.png) 

3. <span data-ttu-id="81a20-201">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="81a20-201">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="81a20-203">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="81a20-203">Click **Add** button.</span></span> <span data-ttu-id="81a20-204">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="81a20-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="81a20-206">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="81a20-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="81a20-207">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="81a20-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="81a20-208">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="81a20-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="81a20-209">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="81a20-209">Test single sign-on</span></span>

<span data-ttu-id="81a20-210">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="81a20-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="81a20-211">Quando clicar no bloco TigerText no Painel de Acesso, você deverá ser conectado automaticamente ao aplicativo TigerText.</span><span class="sxs-lookup"><span data-stu-id="81a20-211">When you click the TigerText tile in the Access Panel, you should get automatically signed-on to your TigerText application.</span></span> <span data-ttu-id="81a20-212">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="81a20-212">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="81a20-213">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="81a20-213">Additional resources</span></span>

* [<span data-ttu-id="81a20-214">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="81a20-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="81a20-215">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="81a20-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_203.png

