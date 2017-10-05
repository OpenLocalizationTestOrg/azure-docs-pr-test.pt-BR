---
title: "Tutorial: Integração do Azure Active Directory com o Workrite | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Active Directory do Azure e o Workrite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2a5c2956-a011-4d5c-877b-80679b6587b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 4358c4c621634c17cbbd7fa1c72f12746b8e4a2a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workrite"></a><span data-ttu-id="3c224-103">Tutorial: Integração do Active Directory do Azure com o Workrite</span><span class="sxs-lookup"><span data-stu-id="3c224-103">Tutorial: Azure Active Directory integration with Workrite</span></span>

<span data-ttu-id="3c224-104">Neste tutorial, você aprenderá a integrar o Workrite ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="3c224-104">In this tutorial, you learn how to integrate Workrite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3c224-105">A integração do Workrite ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="3c224-105">Integrating Workrite with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3c224-106">No Azure AD, é possível controlar quem tem acesso ao Workrite.</span><span class="sxs-lookup"><span data-stu-id="3c224-106">You can control in Azure AD who has access to Workrite.</span></span>
- <span data-ttu-id="3c224-107">É possível permitir que seus usuários entrem automaticamente no Workrite (Logon Único) com suas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3c224-107">You can enable your users to automatically get signed-on to Workrite (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="3c224-108">Você pode gerenciar suas contas em um único local central – o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3c224-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="3c224-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3c224-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3c224-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3c224-110">Prerequisites</span></span>

<span data-ttu-id="3c224-111">Para configurar a integração do AD do Azure ao Workrite, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="3c224-111">To configure Azure AD integration with Workrite, you need the following items:</span></span>

- <span data-ttu-id="3c224-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3c224-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3c224-113">Uma assinatura do Workrite habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="3c224-113">A Workrite single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3c224-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="3c224-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3c224-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="3c224-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3c224-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="3c224-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3c224-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3c224-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3c224-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="3c224-118">Scenario description</span></span>
<span data-ttu-id="3c224-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="3c224-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3c224-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="3c224-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3c224-121">Adicionar o Workrite a partir da galeria</span><span class="sxs-lookup"><span data-stu-id="3c224-121">Adding Workrite from the gallery</span></span>
2. <span data-ttu-id="3c224-122">configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3c224-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workrite-from-the-gallery"></a><span data-ttu-id="3c224-123">Adicionar o Workrite a partir da galeria</span><span class="sxs-lookup"><span data-stu-id="3c224-123">Adding Workrite from the gallery</span></span>
<span data-ttu-id="3c224-124">Para configurar a integração do Workrite ao AD do Azure, você precisa adicionar o Workrite a partir da galeria à sua lista de aplicativos de SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="3c224-124">To configure the integration of Workrite into Azure AD, you need to add Workrite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3c224-125">**Para adicionar o Workrite a partir da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3c224-125">**To add Workrite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3c224-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3c224-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="3c224-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="3c224-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3c224-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3c224-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="3c224-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3c224-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="3c224-133">Na caixa de pesquisa, digite **Workrite**, selecione **Workrite** no painel de resultados e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3c224-133">In the search box, type **Workrite**, select **Workrite** from result panel then click **Add** button to add the application.</span></span>

    ![Workrite na lista de resultados](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3c224-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3c224-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="3c224-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Workrite com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="3c224-136">In this section, you configure and test Azure AD single sign-on with Workrite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3c224-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Workrite é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3c224-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Workrite is to a user in Azure AD.</span></span> <span data-ttu-id="3c224-138">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do AD do Azure e o usuário relacionado no Workrite.</span><span class="sxs-lookup"><span data-stu-id="3c224-138">In other words, a link relationship between an Azure AD user and the related user in Workrite needs to be established.</span></span>

<span data-ttu-id="3c224-139">No Workrite, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="3c224-139">In Workrite, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3c224-140">Para configurar e testar o logon único do AD do Azure com o Workrite, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="3c224-140">To configure and test Azure AD single sign-on with Workrite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3c224-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="3c224-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3c224-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="3c224-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3c224-143">**[Criar um usuário de teste do Workrite](#create-a-workrite-test-user)** – para ter um equivalente de Brenda Fernandes no Workrite que esteja vinculado à representação de usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3c224-143">**[Create a Workrite test user](#create-a-workrite-test-user)** - to have a counterpart of Britta Simon in Workrite that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3c224-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3c224-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3c224-145">**[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="3c224-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="3c224-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3c224-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="3c224-147">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo Workrite.</span><span class="sxs-lookup"><span data-stu-id="3c224-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workrite application.</span></span>

<span data-ttu-id="3c224-148">**Para configurar o logon único do AD do Azure com o Workrite, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3c224-148">**To configure Azure AD single sign-on with Workrite, perform the following steps:**</span></span>

1. <span data-ttu-id="3c224-149">No Portal do Azure, na página de integração de aplicativos do **Workrite**, clique em **Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="3c224-149">In the Azure portal, on the **Workrite** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="3c224-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="3c224-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_samlbase.png)

3. <span data-ttu-id="3c224-153">Na seção **URLs e Domínio do Workrite**, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="3c224-153">On the **Workrite Domain and URLs** section, perform the following steps:</span></span>

    ![Informações de logon único de URLs e Domínio do Workrite](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_url.png)

    <span data-ttu-id="3c224-155">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://app.workrite.co.uk/securelogin/samlgateway.aspx?id=<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="3c224-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.workrite.co.uk/securelogin/samlgateway.aspx?id=<uniqueid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3c224-156">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="3c224-156">This value is not real.</span></span> <span data-ttu-id="3c224-157">Atualize esse valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="3c224-157">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="3c224-158">Contate a [equipe de suporte ao cliente do Workrite](mailto:support@workrite.co.uk) para obter esse valor.</span><span class="sxs-lookup"><span data-stu-id="3c224-158">Contact [Workrite Client support team](mailto:support@workrite.co.uk) to get this value.</span></span>

4. <span data-ttu-id="3c224-159">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="3c224-159">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_certificate.png) 

5. <span data-ttu-id="3c224-161">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="3c224-161">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-workrite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3c224-163">Na seção **Configuração do Workrite**, clique em **Configurar o Workrite** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="3c224-163">On the **Workrite Configuration** section, click **Configure Workrite** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3c224-164">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="3c224-164">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuração do Workrite](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_configure.png) 

7. <span data-ttu-id="3c224-166">Para configurar o logon único no lado do **Workrite**, é necessário enviar o **Certificado (Base64), a URL de Saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** baixados para a [equipe de suporte do Workrite](mailto:support@workrite.co.uk).</span><span class="sxs-lookup"><span data-stu-id="3c224-166">To configure single sign-on on **Workrite** side, you need to send the downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Workrite support team](mailto:support@workrite.co.uk).</span></span>

> [!TIP]
> <span data-ttu-id="3c224-167">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="3c224-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3c224-168">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="3c224-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3c224-169">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3c224-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3c224-170">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3c224-170">Create an Azure AD test user</span></span>

<span data-ttu-id="3c224-171">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="3c224-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="3c224-173">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3c224-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3c224-174">No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3c224-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-workrite-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="3c224-176">Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="3c224-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-workrite-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="3c224-178">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.</span><span class="sxs-lookup"><span data-stu-id="3c224-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![O botão Adicionar](./media/active-directory-saas-workrite-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="3c224-180">Na caixa de diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3c224-180">In the **User** dialog box, perform the following steps:</span></span>

    ![A caixa de diálogo Usuário](./media/active-directory-saas-workrite-tutorial/create_aaduser_04.png)

    <span data-ttu-id="3c224-182">a.</span><span class="sxs-lookup"><span data-stu-id="3c224-182">a.</span></span> <span data-ttu-id="3c224-183">Na caixa **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="3c224-183">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3c224-184">b.</span><span class="sxs-lookup"><span data-stu-id="3c224-184">b.</span></span> <span data-ttu-id="3c224-185">Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="3c224-185">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="3c224-186">c.</span><span class="sxs-lookup"><span data-stu-id="3c224-186">c.</span></span> <span data-ttu-id="3c224-187">Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.</span><span class="sxs-lookup"><span data-stu-id="3c224-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="3c224-188">d.</span><span class="sxs-lookup"><span data-stu-id="3c224-188">d.</span></span> <span data-ttu-id="3c224-189">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3c224-189">Click **Create**.</span></span>
 
### <a name="create-a-workrite-test-user"></a><span data-ttu-id="3c224-190">Criar um usuário de teste do Workrite</span><span class="sxs-lookup"><span data-stu-id="3c224-190">Create a Workrite test user</span></span>

<span data-ttu-id="3c224-191">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no Workrite.</span><span class="sxs-lookup"><span data-stu-id="3c224-191">The objective of this section is to create a user called Britta Simon in Workrite.</span></span>

<span data-ttu-id="3c224-192">**Para criar um usuário chamado Brenda Fernandes no Workrite, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3c224-192">**To create a user called Britta Simon in Workrite, perform the following steps:**</span></span>

1. <span data-ttu-id="3c224-193">Faça logon no site da empresa workrite como administrador.</span><span class="sxs-lookup"><span data-stu-id="3c224-193">Sign on to your workrite company site as administrator.</span></span>

2. <span data-ttu-id="3c224-194">No painel de navegação, clique em **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="3c224-194">In the navigation pane, click **Admin**.</span></span>
   
    ![Controle de administração][400]

3. <span data-ttu-id="3c224-196">Vá para Links Rápidos e clique em **Criar um usuário**.</span><span class="sxs-lookup"><span data-stu-id="3c224-196">Go to Quick Links, and then click **Create a User**.</span></span>
   
    ![Seção Criar usuário][401]

4. <span data-ttu-id="3c224-198">No diálogo **Criar Usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3c224-198">On the **Create User** dialog, perform the following steps:</span></span>
   
    ![Caixa de diálogo Criar usuário][402]
    
    <span data-ttu-id="3c224-200">a.</span><span class="sxs-lookup"><span data-stu-id="3c224-200">a.</span></span> <span data-ttu-id="3c224-201">Na caixa de texto **Email**, digite o endereço de email do usuário, como Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="3c224-201">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="3c224-202">b.</span><span class="sxs-lookup"><span data-stu-id="3c224-202">b.</span></span> <span data-ttu-id="3c224-203">Na caixa de texto **Nome**, digite o nome do usuário como Brenda.</span><span class="sxs-lookup"><span data-stu-id="3c224-203">In the **First Name** textbox, type the firstname of user like Britta.</span></span>

    <span data-ttu-id="3c224-204">c.</span><span class="sxs-lookup"><span data-stu-id="3c224-204">c.</span></span> <span data-ttu-id="3c224-205">Na caixa de texto **Sobrenome**, digite o sobrenome do usuário como Fernandes.</span><span class="sxs-lookup"><span data-stu-id="3c224-205">In the **Surname** textbox, type the surname of user like Simon.</span></span>
    
    <span data-ttu-id="3c224-206">d.</span><span class="sxs-lookup"><span data-stu-id="3c224-206">d.</span></span> <span data-ttu-id="3c224-207">Selecione **Administrador Cliente** como **Escolher Função**.</span><span class="sxs-lookup"><span data-stu-id="3c224-207">Select **Client Administrator** as **Choose Role**.</span></span>
    
    <span data-ttu-id="3c224-208">e.</span><span class="sxs-lookup"><span data-stu-id="3c224-208">e.</span></span> <span data-ttu-id="3c224-209">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="3c224-209">Click **Save**.</span></span>   

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="3c224-210">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3c224-210">Assign the Azure AD test user</span></span>

<span data-ttu-id="3c224-211">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo acesso ao Workrite.</span><span class="sxs-lookup"><span data-stu-id="3c224-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workrite.</span></span>

![Atribuir a função de usuário][200] 

<span data-ttu-id="3c224-213">**Para atribuir Brenda Fernandes ao Workrite, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3c224-213">**To assign Britta Simon to Workrite, perform the following steps:**</span></span>

1. <span data-ttu-id="3c224-214">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3c224-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="3c224-216">Na lista de aplicativos, selecione **Workrite**.</span><span class="sxs-lookup"><span data-stu-id="3c224-216">In the applications list, select **Workrite**.</span></span>

    ![O link do Workrite na lista Aplicativos](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_app.png)  

3. <span data-ttu-id="3c224-218">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="3c224-218">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202]

4. <span data-ttu-id="3c224-220">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="3c224-220">Click **Add** button.</span></span> <span data-ttu-id="3c224-221">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3c224-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="3c224-223">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="3c224-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3c224-224">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3c224-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3c224-225">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3c224-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="3c224-226">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="3c224-226">Test single sign-on</span></span>

<span data-ttu-id="3c224-227">O objetivo desta seção é testar sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="3c224-227">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="3c224-228">Quando você clica no bloco Workrite no Painel de Acesso, deve fazer logon automaticamente no seu aplicativo Workrite.</span><span class="sxs-lookup"><span data-stu-id="3c224-228">When you click the Workrite tile in the Access Panel, you should get automatically signed-on to your Workrite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3c224-229">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="3c224-229">Additional resources</span></span>

* [<span data-ttu-id="3c224-230">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="3c224-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3c224-231">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3c224-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_203.png
[400]: ./media/active-directory-saas-workrite-tutorial/tutorial_workrite_400.png
[401]: ./media/active-directory-saas-workrite-tutorial/tutorial_workrite_401.png
[402]: ./media/active-directory-saas-workrite-tutorial/tutorial_workrite_402.png

