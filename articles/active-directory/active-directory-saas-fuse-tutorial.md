---
title: "Tutorial: integração do Azure Active Directory ao Fuse | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Active Directory do Azure e o Fuse."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 5ef34f58-863a-4b37-875c-e8efa3e18bb3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 9a91e22faced9e126043bebefd85c307dbdf933d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fuse"></a><span data-ttu-id="49512-103">Tutorial: Integração do Active Directory do Azure ao Fuse</span><span class="sxs-lookup"><span data-stu-id="49512-103">Tutorial: Azure Active Directory integration with Fuse</span></span>

<span data-ttu-id="49512-104">Neste tutorial, você aprenderá a integrar o Fuse ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="49512-104">In this tutorial, you learn how to integrate Fuse with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="49512-105">A integração do Fuse ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="49512-105">Integrating Fuse with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="49512-106">No Azure AD, é possível controlar quem tem acesso ao Fuse.</span><span class="sxs-lookup"><span data-stu-id="49512-106">You can control in Azure AD who has access to Fuse.</span></span>
- <span data-ttu-id="49512-107">Você pode permitir que os usuários façam logon automaticamente no Fuse (logon único) com as respectivas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49512-107">You can enable your users to automatically get signed-on to Fuse (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="49512-108">Você pode gerenciar suas contas em um único local central – o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="49512-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="49512-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="49512-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="49512-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="49512-110">Prerequisites</span></span>

<span data-ttu-id="49512-111">Para configurar a integração do Azure AD com o Fuse, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="49512-111">To configure Azure AD integration with Fuse, you need the following items:</span></span>

- <span data-ttu-id="49512-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="49512-112">An Azure AD subscription</span></span>
- <span data-ttu-id="49512-113">Uma assinatura do Fuse habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="49512-113">A Fuse single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="49512-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="49512-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="49512-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="49512-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="49512-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="49512-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="49512-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="49512-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="49512-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="49512-118">Scenario description</span></span>
<span data-ttu-id="49512-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="49512-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="49512-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="49512-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="49512-121">Adicionar o Fuse da galeria</span><span class="sxs-lookup"><span data-stu-id="49512-121">Add Fuse from the gallery</span></span>
2. <span data-ttu-id="49512-122">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="49512-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-fuse-from-the-gallery"></a><span data-ttu-id="49512-123">Adicionar o Fuse da galeria</span><span class="sxs-lookup"><span data-stu-id="49512-123">Add Fuse from the gallery</span></span>
<span data-ttu-id="49512-124">Para configurar a integração do Fuse com o Azure AD, você precisará adicionar o Fuse à sua lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="49512-124">To configure the integration of Fuse into Azure AD, you need to add Fuse from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="49512-125">**Para adicionar o Fuse por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="49512-125">**To add Fuse from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="49512-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="49512-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="49512-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="49512-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="49512-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="49512-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="49512-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="49512-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="49512-133">Na caixa de pesquisa, digite **Fuse**, selecione **Fuse** no painel de resultados e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="49512-133">In the search box, type **Fuse**, select **Fuse** from result panel then click **Add** button to add the application.</span></span>

    ![Fuse na lista de resultados](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="49512-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="49512-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="49512-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Fuse, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="49512-136">In this section, you configure and test Azure AD single sign-on with Fuse based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="49512-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Fuse é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49512-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Fuse is to a user in Azure AD.</span></span> <span data-ttu-id="49512-138">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Fuse.</span><span class="sxs-lookup"><span data-stu-id="49512-138">In other words, a link relationship between an Azure AD user and the related user in Fuse needs to be established.</span></span>

<span data-ttu-id="49512-139">No Fuse, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="49512-139">In Fuse, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="49512-140">Para configurar e testar o logon único do Azure AD com o Fuse, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="49512-140">To configure and test Azure AD single sign-on with Fuse, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="49512-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="49512-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="49512-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="49512-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="49512-143">**[Criar de um usuário de teste do Fuse](#create-a-fuse-test-user)** – para ter um equivalente de Brenda Fernandes no Fuse vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49512-143">**[Create a Fuse test user](#create-a-fuse-test-user)** - to have a counterpart of Britta Simon in Fuse that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="49512-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49512-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="49512-145">**[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="49512-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="49512-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="49512-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="49512-147">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo Fuse.</span><span class="sxs-lookup"><span data-stu-id="49512-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Fuse application.</span></span>

<span data-ttu-id="49512-148">**Para configurar o logon único do Azure AD com o Fuse, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="49512-148">**To configure Azure AD single sign-on with Fuse, perform the following steps:**</span></span>

1. <span data-ttu-id="49512-149">No Portal do Azure, na página de integração de aplicativos do **Fuse**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="49512-149">In the Azure portal, on the **Fuse** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="49512-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="49512-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_samlbase.png)

3. <span data-ttu-id="49512-153">Na seção **URLs e Domínio do Fuse**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="49512-153">On the **Fuse Domain and URLs** section, perform the following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do fusível](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_url.png)
    
    <span data-ttu-id="49512-155">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<tenant name>.fusion-universal.com/`</span><span class="sxs-lookup"><span data-stu-id="49512-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant name>.fusion-universal.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="49512-156">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="49512-156">This value is not real.</span></span> <span data-ttu-id="49512-157">Atualize esse valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="49512-157">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="49512-158">Contate a [equipe de suporte ao cliente do Fuse](mailto:support@fusion-universal.com) para obter esse valor.</span><span class="sxs-lookup"><span data-stu-id="49512-158">Contact [Fuse Client support team](mailto:support@fusion-universal.com) to get this value.</span></span> 
 
4. <span data-ttu-id="49512-159">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Bruto)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="49512-159">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_certificate.png) 

5. <span data-ttu-id="49512-161">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="49512-161">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-fuse-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="49512-163">No **configuração fusível** seção, clique em **configurar fusível** para abrir **logon** janela.</span><span class="sxs-lookup"><span data-stu-id="49512-163">On the **Fuse Configuration** section, click **Configure Fuse** to open **Configure sign-on** window.</span></span> <span data-ttu-id="49512-164">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="49512-164">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuração do Fuse](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_configure.png) 

7. <span data-ttu-id="49512-166">Para que o SSO seja configurado para seu aplicativo, entre em contato com a [equipe de suporte do Fuse](mailto:support@fusion-universal.com) e forneça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="49512-166">To get SSO configured for your application, contact [Fuse support team](mailto:support@fusion-universal.com) and provide them with the following:</span></span>

    * <span data-ttu-id="49512-167">O **arquivo de certificado (bruto)** baixado</span><span class="sxs-lookup"><span data-stu-id="49512-167">The downloaded **Certificate (Raw) file**</span></span>
    * <span data-ttu-id="49512-168">A **URL do serviço de logon único SAML**</span><span class="sxs-lookup"><span data-stu-id="49512-168">The **SAML Single Sign-On Service URL**</span></span>
    * <span data-ttu-id="49512-169">A **ID da entidade SAML**</span><span class="sxs-lookup"><span data-stu-id="49512-169">The **SAML Entity ID**</span></span>
    * <span data-ttu-id="49512-170">A **URL de saída**</span><span class="sxs-lookup"><span data-stu-id="49512-170">The **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="49512-171">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="49512-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="49512-172">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="49512-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="49512-173">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="49512-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="49512-174">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="49512-174">Create an Azure AD test user</span></span>

<span data-ttu-id="49512-175">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="49512-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="49512-177">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="49512-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="49512-178">No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="49512-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-fuse-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="49512-180">Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="49512-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-fuse-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="49512-182">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.</span><span class="sxs-lookup"><span data-stu-id="49512-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![O botão Adicionar](./media/active-directory-saas-fuse-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="49512-184">Na caixa de diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="49512-184">In the **User** dialog box, perform the following steps:</span></span>

    ![A caixa de diálogo Usuário](./media/active-directory-saas-fuse-tutorial/create_aaduser_04.png)

    <span data-ttu-id="49512-186">a.</span><span class="sxs-lookup"><span data-stu-id="49512-186">a.</span></span> <span data-ttu-id="49512-187">Na caixa **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="49512-187">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="49512-188">b.</span><span class="sxs-lookup"><span data-stu-id="49512-188">b.</span></span> <span data-ttu-id="49512-189">Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="49512-189">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="49512-190">c.</span><span class="sxs-lookup"><span data-stu-id="49512-190">c.</span></span> <span data-ttu-id="49512-191">Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.</span><span class="sxs-lookup"><span data-stu-id="49512-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="49512-192">d.</span><span class="sxs-lookup"><span data-stu-id="49512-192">d.</span></span> <span data-ttu-id="49512-193">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="49512-193">Click **Create**.</span></span>
 
### <a name="create-a-fuse-test-user"></a><span data-ttu-id="49512-194">Criar um usuário de teste do Fuse</span><span class="sxs-lookup"><span data-stu-id="49512-194">Create a Fuse test user</span></span>

<span data-ttu-id="49512-195">Nesta seção, você criará uma usuária chamada Brenda Fernandes no Fuse.</span><span class="sxs-lookup"><span data-stu-id="49512-195">In this section, you create a user called Britta Simon in Fuse.</span></span> <span data-ttu-id="49512-196">Trabalhe com a [equipe de suporte do Fuse](mailto:support@fusion-universal.com) para adicionar os usuários na plataforma do Fuse.</span><span class="sxs-lookup"><span data-stu-id="49512-196">Please work with [Fuse support team](mailto:support@fusion-universal.com) to add the users in the Fuse platform.</span></span>


### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="49512-197">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="49512-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="49512-198">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Fuse.</span><span class="sxs-lookup"><span data-stu-id="49512-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Fuse.</span></span>

![Atribuir a função de usuário][200] 

<span data-ttu-id="49512-200">**Para atribuir Brenda Fernandes ao Fuse, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="49512-200">**To assign Britta Simon to Fuse, perform the following steps:**</span></span>

1. <span data-ttu-id="49512-201">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="49512-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="49512-203">Na lista de aplicativos, escolha **Fuse**.</span><span class="sxs-lookup"><span data-stu-id="49512-203">In the applications list, select **Fuse**.</span></span>

    ![O link do Fuse na lista de Aplicativos](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_app.png)  

3. <span data-ttu-id="49512-205">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="49512-205">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202]

4. <span data-ttu-id="49512-207">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="49512-207">Click **Add** button.</span></span> <span data-ttu-id="49512-208">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="49512-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="49512-210">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="49512-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="49512-211">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="49512-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="49512-212">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="49512-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="49512-213">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="49512-213">Test single sign-on</span></span>

<span data-ttu-id="49512-214">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="49512-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="49512-215">Ao clicar no bloco do Fuse no Painel de Acesso, você deverá ser conectado automaticamente a seu aplicativo do Fuse.</span><span class="sxs-lookup"><span data-stu-id="49512-215">When you click the Fuse tile in the Access Panel, you should get automatically signed-on to your Fuse application.</span></span>
<span data-ttu-id="49512-216">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="49512-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="49512-217">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="49512-217">Additional resources</span></span>

* [<span data-ttu-id="49512-218">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="49512-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="49512-219">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="49512-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_203.png

