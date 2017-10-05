---
title: "Tutorial: Integração do Azure Active Directory com o RealtimeBoard | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o RealtimeBoard."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: a37fc1c0-4bae-4173-989b-00de53a0076f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: jeedes
ms.openlocfilehash: d3ba8cb1f7e1d4332f7912848e8b6902d9acf909
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-realtimeboard"></a><span data-ttu-id="8cad6-103">Tutorial: Integração do Azure Active Directory com o RealtimeBoard</span><span class="sxs-lookup"><span data-stu-id="8cad6-103">Tutorial: Azure Active Directory integration with RealtimeBoard</span></span>

<span data-ttu-id="8cad6-104">Neste tutorial, você aprende a integrar o RealtimeBoard ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="8cad6-104">In this tutorial, you learn how to integrate RealtimeBoard with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8cad6-105">A integração do RealtimeBoard ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="8cad6-105">Integrating RealtimeBoard with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8cad6-106">No Azure AD, é possível controlar quem tem acesso ao RealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="8cad6-106">You can control in Azure AD who has access to RealtimeBoard.</span></span>
- <span data-ttu-id="8cad6-107">Você pode permitir que os usuários façam logon automaticamente no RealtimeBoard (Logon Único) com suas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8cad6-107">You can enable your users to automatically get signed-on to RealtimeBoard (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="8cad6-108">Você pode gerenciar suas contas em um único local central – o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8cad6-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="8cad6-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8cad6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8cad6-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8cad6-110">Prerequisites</span></span>

<span data-ttu-id="8cad6-111">Para configurar a integração do Azure AD com o RealtimeBoard, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="8cad6-111">To configure Azure AD integration with RealtimeBoard, you need the following items:</span></span>

- <span data-ttu-id="8cad6-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8cad6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8cad6-113">Uma assinatura habilitada para logon único do RealtimeBoard</span><span class="sxs-lookup"><span data-stu-id="8cad6-113">A RealtimeBoard single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8cad6-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="8cad6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8cad6-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="8cad6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8cad6-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="8cad6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8cad6-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8cad6-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8cad6-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="8cad6-118">Scenario description</span></span>
<span data-ttu-id="8cad6-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="8cad6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8cad6-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="8cad6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8cad6-121">Adicionando RealtimeBoard pela galeria</span><span class="sxs-lookup"><span data-stu-id="8cad6-121">Adding RealtimeBoard from the gallery</span></span>
2. <span data-ttu-id="8cad6-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8cad6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-realtimeboard-from-the-gallery"></a><span data-ttu-id="8cad6-123">Adicionando RealtimeBoard pela galeria</span><span class="sxs-lookup"><span data-stu-id="8cad6-123">Adding RealtimeBoard from the gallery</span></span>
<span data-ttu-id="8cad6-124">Para configurar a integração de RealtimeBoard ao Azure AD, você precisa adicionar RealtimeBoard por meio da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="8cad6-124">To configure the integration of RealtimeBoard into Azure AD, you need to add RealtimeBoard from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8cad6-125">**Para adicionar o RealtimeBoard pela galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="8cad6-125">**To add RealtimeBoard from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8cad6-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8cad6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="8cad6-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="8cad6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8cad6-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="8cad6-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="8cad6-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8cad6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="8cad6-133">Na caixa de pesquisa, digite **RealtimeBoard**, selecione **RealtimeBoard** no painel de resultados e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8cad6-133">In the search box, type **RealtimeBoard**, select **RealtimeBoard** from result panel then click **Add** button to add the application.</span></span>

    ![RealtimeBoard na lista de resultados](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8cad6-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="8cad6-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="8cad6-136">Nesta seção, você vai configurar e testar o logon único do Azure AD com o RealtimeBoard com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="8cad6-136">In this section, you configure and test Azure AD single sign-on with RealtimeBoard based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8cad6-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do RealtimeBoard é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8cad6-137">For single sign-on to work, Azure AD needs to know what the counterpart user in RealtimeBoard is to a user in Azure AD.</span></span> <span data-ttu-id="8cad6-138">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado em RealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="8cad6-138">In other words, a link relationship between an Azure AD user and the related user in RealtimeBoard needs to be established.</span></span>

<span data-ttu-id="8cad6-139">No RealtimeBoard, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="8cad6-139">In RealtimeBoard, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8cad6-140">Para configurar e testar o logon único do Azure AD com o RealtimeBoard, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="8cad6-140">To configure and test Azure AD single sign-on with RealtimeBoard, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8cad6-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="8cad6-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8cad6-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="8cad6-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8cad6-143">**[Criar um usuário de teste do RealtimeBoard](#create-a-realtimeboard-test-user)** – para ter um equivalente de Brenda Fernandes no RealtimeBoard que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8cad6-143">**[Create a RealtimeBoard test user](#create-a-realtimeboard-test-user)** - to have a counterpart of Britta Simon in RealtimeBoard that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8cad6-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8cad6-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8cad6-145">**[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="8cad6-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8cad6-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="8cad6-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="8cad6-147">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo RealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="8cad6-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RealtimeBoard application.</span></span>

<span data-ttu-id="8cad6-148">**Para configurar o logon único do Azure AD com o RealtimeBoard, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="8cad6-148">**To configure Azure AD single sign-on with RealtimeBoard, perform the following steps:**</span></span>

1. <span data-ttu-id="8cad6-149">No portal do Azure, na página de integração de aplicativos do **RealtimeBoard**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="8cad6-149">In the Azure portal, on the **RealtimeBoard** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="8cad6-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="8cad6-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_samlbase.png)

3. <span data-ttu-id="8cad6-153">Na seção **Domínio e URLs do RealtimeBoard**, se você desejar configurar o aplicativo em modo iniciado pelo **IDP**:</span><span class="sxs-lookup"><span data-stu-id="8cad6-153">On the **RealtimeBoard Domain and URLs** section, if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Informações de logon único em Domínio e URLs do RealtimeBoard](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_url.png)

    <span data-ttu-id="8cad6-155">Na caixa de texto **Identificador**, digite uma URL como: `https://realtimeboard.com/`</span><span class="sxs-lookup"><span data-stu-id="8cad6-155">In the **Identifier** textbox, type a URL as: `https://realtimeboard.com/`</span></span>

4. <span data-ttu-id="8cad6-156">Marque **Mostrar configurações avançadas de URL**, se quiser configurar o aplicativo no modo iniciado em **SP**:</span><span class="sxs-lookup"><span data-stu-id="8cad6-156">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_url2.png)

    <span data-ttu-id="8cad6-158">Na caixa de texto **URL de Logon**, digite uma URL como: `https://realtimeboard.com/sso/saml`</span><span class="sxs-lookup"><span data-stu-id="8cad6-158">In the **Sign-on URL** textbox, type a URL as: `https://realtimeboard.com/sso/saml`</span></span>

5. <span data-ttu-id="8cad6-159">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="8cad6-159">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_certificate.png) 

6. <span data-ttu-id="8cad6-161">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="8cad6-161">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="8cad6-163">Para configurar o logon único no lado do **RealtimeBoard**, é necessário enviar o **XML de metadados** baixado para a [equipe de suporte do RealtimeBoard](mailto:support@realtimeboard.com).</span><span class="sxs-lookup"><span data-stu-id="8cad6-163">To configure single sign-on on **RealtimeBoard** side, you need to send the downloaded **Metadata XML** to [RealtimeBoard support team](mailto:support@realtimeboard.com).</span></span> <span data-ttu-id="8cad6-164">Eles definem essa configuração para ter a conexão de SSO de SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="8cad6-164">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="8cad6-165">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="8cad6-165">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8cad6-166">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="8cad6-166">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8cad6-167">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8cad6-167">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8cad6-168">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="8cad6-168">Create an Azure AD test user</span></span>

<span data-ttu-id="8cad6-169">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="8cad6-169">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="8cad6-171">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="8cad6-171">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8cad6-172">No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8cad6-172">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-realtimeboard-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="8cad6-174">Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="8cad6-174">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-realtimeboard-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="8cad6-176">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.</span><span class="sxs-lookup"><span data-stu-id="8cad6-176">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![O botão Adicionar](./media/active-directory-saas-realtimeboard-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="8cad6-178">Na caixa de diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="8cad6-178">In the **User** dialog box, perform the following steps:</span></span>

    ![A caixa de diálogo Usuário](./media/active-directory-saas-realtimeboard-tutorial/create_aaduser_04.png)

    <span data-ttu-id="8cad6-180">a.</span><span class="sxs-lookup"><span data-stu-id="8cad6-180">a.</span></span> <span data-ttu-id="8cad6-181">Na caixa **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="8cad6-181">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8cad6-182">b.</span><span class="sxs-lookup"><span data-stu-id="8cad6-182">b.</span></span> <span data-ttu-id="8cad6-183">Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="8cad6-183">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="8cad6-184">c.</span><span class="sxs-lookup"><span data-stu-id="8cad6-184">c.</span></span> <span data-ttu-id="8cad6-185">Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.</span><span class="sxs-lookup"><span data-stu-id="8cad6-185">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="8cad6-186">d.</span><span class="sxs-lookup"><span data-stu-id="8cad6-186">d.</span></span> <span data-ttu-id="8cad6-187">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="8cad6-187">Click **Create**.</span></span>
 
### <a name="create-a-realtimeboard-test-user"></a><span data-ttu-id="8cad6-188">Criar um usuário de teste do RealtimeBoard</span><span class="sxs-lookup"><span data-stu-id="8cad6-188">Create a RealtimeBoard test user</span></span>

<span data-ttu-id="8cad6-189">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no RealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="8cad6-189">The objective of this section is to create a user called Britta Simon in RealtimeBoard.</span></span> <span data-ttu-id="8cad6-190">O RealtimeBoard dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="8cad6-190">RealtimeBoard supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="8cad6-191">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="8cad6-191">There is no action item for you in this section.</span></span> <span data-ttu-id="8cad6-192">Se um usuário ainda não existir no RealtimeBoard, um novo será criado quando você tentar acessar o RealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="8cad6-192">If a user doesn't already exist in RealtimeBoard, a new one is created when you attempt to access RealtimeBoard.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="8cad6-193">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="8cad6-193">Assign the Azure AD test user</span></span>

<span data-ttu-id="8cad6-194">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao RealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="8cad6-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RealtimeBoard.</span></span>

![Atribuir a função de usuário][200] 

<span data-ttu-id="8cad6-196">**Para atribuir Brenda Fernandes ao RealtimeBoard, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="8cad6-196">**To assign Britta Simon to RealtimeBoard, perform the following steps:**</span></span>

1. <span data-ttu-id="8cad6-197">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="8cad6-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="8cad6-199">Na lista de aplicativos, escolha **RealtimeBoard**.</span><span class="sxs-lookup"><span data-stu-id="8cad6-199">In the applications list, select **RealtimeBoard**.</span></span>

    ![O link do RealtimeBoard na lista de aplicativos](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_app.png)  

3. <span data-ttu-id="8cad6-201">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="8cad6-201">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202]

4. <span data-ttu-id="8cad6-203">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="8cad6-203">Click **Add** button.</span></span> <span data-ttu-id="8cad6-204">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8cad6-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="8cad6-206">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="8cad6-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8cad6-207">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8cad6-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8cad6-208">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8cad6-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="8cad6-209">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="8cad6-209">Test single sign-on</span></span>

<span data-ttu-id="8cad6-210">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="8cad6-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8cad6-211">Ao clicar no bloco do RealtimeBoard no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo do RealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="8cad6-211">When you click the RealtimeBoard tile in the Access Panel, you should get automatically signed-on to your RealtimeBoard application.</span></span>
<span data-ttu-id="8cad6-212">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8cad6-212">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8cad6-213">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="8cad6-213">Additional resources</span></span>

* [<span data-ttu-id="8cad6-214">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="8cad6-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8cad6-215">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8cad6-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_203.png

