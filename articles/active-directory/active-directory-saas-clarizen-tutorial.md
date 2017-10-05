---
title: "Tutorial: Integração do Azure Active Directory ao Clarizen | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Active Directory do Azure e o Clarizen."
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
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 574c6877bddac8be7d6d541bfabbdc10f6be3101
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clarizen"></a><span data-ttu-id="f26dc-103">Tutorial: integração do Active Directory do Azure ao Clarizen</span><span class="sxs-lookup"><span data-stu-id="f26dc-103">Tutorial: Azure Active Directory integration with Clarizen</span></span>

<span data-ttu-id="f26dc-104">Neste tutorial, você aprenderá a integrar o Azure AD (Azure Active Directory) ao Clarizen.</span><span class="sxs-lookup"><span data-stu-id="f26dc-104">In this tutorial, you learn how to integrate Azure Active Directory (Azure AD) with Clarizen.</span></span> <span data-ttu-id="f26dc-105">Essa integração oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="f26dc-105">This integration gives you the following benefits:</span></span>

- <span data-ttu-id="f26dc-106">No Azure AD, é possível controlar quem tem acesso ao Clarizen.</span><span class="sxs-lookup"><span data-stu-id="f26dc-106">You can control, in Azure AD, who has access to Clarizen.</span></span>
- <span data-ttu-id="f26dc-107">Você pode permitir que seus usuários entrem automaticamente no Clarizen (logon único) com suas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f26dc-107">You can enable your users to be automatically signed in to Clarizen (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="f26dc-108">Você pode gerenciar suas contas em um único local, o portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="f26dc-108">You can manage your accounts in one central location, the Azure portal.</span></span>

<span data-ttu-id="f26dc-109">O cenário deste tutorial consiste em duas tarefas principais:</span><span class="sxs-lookup"><span data-stu-id="f26dc-109">The scenario in this tutorial consists of two main tasks:</span></span>

1. <span data-ttu-id="f26dc-110">Adicione o Clarizen da galeria.</span><span class="sxs-lookup"><span data-stu-id="f26dc-110">Add Clarizen from the gallery.</span></span>
2. <span data-ttu-id="f26dc-111">Configurar e testar logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f26dc-111">Configure and test Azure AD single sign-on.</span></span>

<span data-ttu-id="f26dc-112">Para conhecer mais detalhadamente a integração de aplicativos de SaaS (software como serviço) ao Azure AD, consulte [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f26dc-112">If you want more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f26dc-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f26dc-113">Prerequisites</span></span>
<span data-ttu-id="f26dc-114">Para configurar a integração do Azure AD ao Clarizen, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="f26dc-114">To configure Azure AD integration with Clarizen, you need the following items:</span></span>

- <span data-ttu-id="f26dc-115">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f26dc-115">An Azure AD subscription</span></span>
- <span data-ttu-id="f26dc-116">Uma assinatura de Clarizen está habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="f26dc-116">A Clarizen subscription that's enabled for single sign-on</span></span>

<span data-ttu-id="f26dc-117">Para testar as etapas neste tutorial, siga estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="f26dc-117">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="f26dc-118">Teste o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="f26dc-118">Test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f26dc-119">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="f26dc-119">Don't use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="f26dc-120">Se não tiver um ambiente de teste do Azure AD, você poderá [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f26dc-120">If you don't have an Azure AD test environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="add-clarizen-from-the-gallery"></a><span data-ttu-id="f26dc-121">Adicionar o Clarizen da galeria</span><span class="sxs-lookup"><span data-stu-id="f26dc-121">Add Clarizen from the gallery</span></span>
<span data-ttu-id="f26dc-122">Para configurar a integração do Clarizen ao Azure AD, adicione o Clarizen da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="f26dc-122">To configure the integration of Clarizen into Azure AD, add Clarizen from the gallery to your list of managed SaaS apps.</span></span>

1. <span data-ttu-id="f26dc-123">No [portal do Azure](https://portal.azure.com), no painel esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f26dc-123">In the [Azure portal](https://portal.azure.com), in the left pane, click the **Azure Active Directory** icon.</span></span>

    ![Ícone do Azure Active Directory][1]

2. <span data-ttu-id="f26dc-125">Clique em **Aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="f26dc-125">Click **Enterprise applications**.</span></span> <span data-ttu-id="f26dc-126">Em seguida, clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f26dc-126">Then click **All applications**.</span></span>

    ![Clicar em "Aplicativos corporativos" e em "Todos os aplicativos"][2]

3. <span data-ttu-id="f26dc-128">Clique no botão **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f26dc-128">Click the **Add** button at the top of the dialog box.</span></span>

    ![O botão “Adicionar”][3]

4. <span data-ttu-id="f26dc-130">Na caixa de pesquisa, digite **Clarizen**.</span><span class="sxs-lookup"><span data-stu-id="f26dc-130">In the search box, type **Clarizen**.</span></span>

    ![Digitar "Clarizen" na caixa de pesquisa](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_000.png)

5. <span data-ttu-id="f26dc-132">No painel de resultados, selecione **Clarizen** e clique em **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f26dc-132">In the results pane, select **Clarizen**, and then click **Add** to add the application.</span></span>

    ![Selecionar o Clarizen no painel de resultados](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_0001.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f26dc-134">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f26dc-134">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="f26dc-135">Nas seções a seguir, você configurará e testará o logon único do Azure AD com o Clarizen, com base no usuário de teste Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="f26dc-135">In the following sections, you configure and test Azure AD single sign-on with Clarizen based on the test user Britta Simon.</span></span>

<span data-ttu-id="f26dc-136">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Clarizen é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f26dc-136">For single sign-on to work, Azure AD needs to know what the counterpart user in Clarizen is to a user in Azure AD.</span></span> <span data-ttu-id="f26dc-137">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Clarizen.</span><span class="sxs-lookup"><span data-stu-id="f26dc-137">In other words, a link relationship between an Azure AD user and the related user in Clarizen needs to be established.</span></span> <span data-ttu-id="f26dc-138">Você estabelece essa relação de vínculo atribuindo o valor de **nome de usuário** no Azure AD como o valor de **Nome de usuário** no Clarizen.</span><span class="sxs-lookup"><span data-stu-id="f26dc-138">You establish this link relationship by assigning the value of **user name** in Azure AD as the value of **Username** in Clarizen.</span></span>

<span data-ttu-id="f26dc-139">Para configurar e testar o logon único do Azure AD com o Clarizen, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="f26dc-139">To configure and test Azure AD single sign-on with Clarizen, complete the following building blocks:</span></span>

1. <span data-ttu-id="f26dc-140">**[Configure o logon único do Azure AD](#configure-azure-ad-single-sign-on)** para permitir que seus usuários usem esse recurso.</span><span class="sxs-lookup"><span data-stu-id="f26dc-140">**[Configure Azure AD single sign-on](#configure-azure-ad-single-sign-on)** to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f26dc-141">**[Crie um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="f26dc-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f26dc-142">**[Criar um usuário de teste do Clarizen](#create-a-clarizen-test-user)**: para ter um equivalente de Brenda Fernandes no Clarizen que esteja vinculado à representação dela no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f26dc-142">**[Create a Clarizen test user](#create-a-clarizen-test-user)** to have a counterpart of Britta Simon in Clarizen that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="f26dc-143">**[Atribua o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f26dc-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f26dc-144">**[Teste o logon único](#test-single-sign-on)** para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="f26dc-144">**[Test single sign-on](#test-single-sign-on)** to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f26dc-145">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f26dc-145">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="f26dc-146">Habilite o logon único do Azure AD no portal do Azure e configura o logon único em seu aplicativo Clarizen.</span><span class="sxs-lookup"><span data-stu-id="f26dc-146">Enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Clarizen application.</span></span>

1. <span data-ttu-id="f26dc-147">No portal do Azure, na página de integração do aplicativo **Clarizen**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="f26dc-147">In the Azure portal, on the **Clarizen** application integration page, click **Single sign-on**.</span></span>

    ![Clicar em "Logon único"][4]

2. <span data-ttu-id="f26dc-149">Na caixa de diálogo **Logon único**, como **Modo**, selecione **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="f26dc-149">In the **Single sign-on** dialog box, for **Mode**, select **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Selecionar "Logon único baseado em SAML"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_01.png)

3. <span data-ttu-id="f26dc-151">Na seção **URLs e Domínio do Clarizen**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f26dc-151">In the **Clarizen Domain and URLs** section, perform the following steps:</span></span>

    ![Caixas de URL de resposta e o identificador](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_02.png)

    <span data-ttu-id="f26dc-153">a.</span><span class="sxs-lookup"><span data-stu-id="f26dc-153">a.</span></span> <span data-ttu-id="f26dc-154">Na caixa **Identificador**, digite o valor como: **Clarizen**</span><span class="sxs-lookup"><span data-stu-id="f26dc-154">In the **Identifier** box, type the value as: **Clarizen**</span></span>

    <span data-ttu-id="f26dc-155">b.</span><span class="sxs-lookup"><span data-stu-id="f26dc-155">b.</span></span> <span data-ttu-id="f26dc-156">Na caixa **URL de Resposta**, digite uma URL usando o seguinte padrão: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span><span class="sxs-lookup"><span data-stu-id="f26dc-156">In the **Reply URL** box, type a URL by using the following pattern: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span></span>

    > [!NOTE]
    > <span data-ttu-id="f26dc-157">Esses não são os valores reais.</span><span class="sxs-lookup"><span data-stu-id="f26dc-157">These are not the real values.</span></span> <span data-ttu-id="f26dc-158">Você precisa usar o identificador real e a URL de resposta.</span><span class="sxs-lookup"><span data-stu-id="f26dc-158">You have to use the actual identifier and reply URL.</span></span> <span data-ttu-id="f26dc-159">Aqui, sugerimos que você use o valor exclusivo de uma cadeia de caracteres como o identificador.</span><span class="sxs-lookup"><span data-stu-id="f26dc-159">Here we suggest that you use the unique value of a string as the identifier.</span></span> <span data-ttu-id="f26dc-160">Para obter os valores reais, entre em contato com a [equipe de suporte do Clarizen](https://success.clarizen.com/hc/en-us/requests/new).</span><span class="sxs-lookup"><span data-stu-id="f26dc-160">To get the actual values, contact the [Clarizen support team](https://success.clarizen.com/hc/en-us/requests/new).</span></span>

4. <span data-ttu-id="f26dc-161">Sobre o **certificado de autenticação SAML** seção, clique em **criar novo certificado**.</span><span class="sxs-lookup"><span data-stu-id="f26dc-161">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Clicar em "Criar novo certificado"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_03.png)  

5. <span data-ttu-id="f26dc-163">Na caixa de diálogo **Criar um Novo Certificado**, clique no ícone de calendário e selecione uma data de expiração.</span><span class="sxs-lookup"><span data-stu-id="f26dc-163">In the **Create New Certificate** dialog box, click the calendar icon and select an expiry date.</span></span> <span data-ttu-id="f26dc-164">Em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="f26dc-164">Then click **Save**.</span></span>

    ![Selecionar e salvar uma data de expiração](./media/active-directory-saas-clarizen-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="f26dc-166">Na seção **Certificado de Autenticação SAML**, selecione **Ativar o novo certificado** e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="f26dc-166">In the **SAML Signing Certificate** section, select **Make new certificate active**, and then click **Save**.</span></span>

    ![Marcar a caixa de seleção para ativar o novo certificado](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_04.png)

7. <span data-ttu-id="f26dc-168">Na caixa de diálogo **Certificado de substituição**, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="f26dc-168">In the **Rollover certificate** dialog box, click **OK**.</span></span>

    ![Clicar em "OK" para confirmar que você deseja ativar o certificado](./media/active-directory-saas-clarizen-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="f26dc-170">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="f26dc-170">In the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Clicar em "Certificado (Base64)" para iniciar o download](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_05.png)

9. <span data-ttu-id="f26dc-172">Na seção **Configuração do Clarizen**, clique em **Configurar o Clarizen** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="f26dc-172">In the **Clarizen Configuration** section, click **Configure Clarizen** to open the **Configure sign-on** window.</span></span>

    ![Clicar em "Configurar Clarizen"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_06.png)

    ![Janela "Configurar o logon", incluindo URLs e arquivos](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_07.png)

10. <span data-ttu-id="f26dc-175">Em outra janela do navegador da Web, entre em seu site de empresa do Clarizen como administrador.</span><span class="sxs-lookup"><span data-stu-id="f26dc-175">In a different web browser window, sign in to your Clarizen company site as an administrator.</span></span>

11. <span data-ttu-id="f26dc-176">Clique no nome de usuário e em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="f26dc-176">Click your username, and then click **Settings**.</span></span>

    <span data-ttu-id="f26dc-177">![Clicar em "Configurações" em seu nome de usuário](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="f26dc-177">![Clicking "Settings" under your username](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "Settings")</span></span>

12. <span data-ttu-id="f26dc-178">Clique na guia **Configurações Globais**.</span><span class="sxs-lookup"><span data-stu-id="f26dc-178">Click the **Global Settings** tab.</span></span> <span data-ttu-id="f26dc-179">Em seguida, próximo a **Autenticação Federada**, clique em **editar**.</span><span class="sxs-lookup"><span data-stu-id="f26dc-179">Then, next to **Federated Authentication**, click **edit**.</span></span>

    <span data-ttu-id="f26dc-180">![Guia "Configurações Globais"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "Configurações Globais")</span><span class="sxs-lookup"><span data-stu-id="f26dc-180">!["Global Settings" tab](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "Global Settings")</span></span>

13. <span data-ttu-id="f26dc-181">Na caixa de diálogo **Autenticação Federada**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f26dc-181">In the **Federated Authentication** dialog box, perform the following steps:</span></span>

    <span data-ttu-id="f26dc-182">![Caixa de diálogo "Autenticação Federada"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Autenticação Federada")</span><span class="sxs-lookup"><span data-stu-id="f26dc-182">!["Federated Authentication" dialog box](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Federated Authentication")</span></span>

    <span data-ttu-id="f26dc-183">a.</span><span class="sxs-lookup"><span data-stu-id="f26dc-183">a.</span></span> <span data-ttu-id="f26dc-184">Selecione **Habilitar Autenticação Federada**.</span><span class="sxs-lookup"><span data-stu-id="f26dc-184">Select **Enable Federated Authentication**.</span></span>

    <span data-ttu-id="f26dc-185">b.</span><span class="sxs-lookup"><span data-stu-id="f26dc-185">b.</span></span> <span data-ttu-id="f26dc-186">Clique em **Carregar** para carregar o certificado baixado.</span><span class="sxs-lookup"><span data-stu-id="f26dc-186">Click **Upload** to upload your downloaded certificate.</span></span>

    <span data-ttu-id="f26dc-187">c.</span><span class="sxs-lookup"><span data-stu-id="f26dc-187">c.</span></span> <span data-ttu-id="f26dc-188">Na caixa de texto **URL de Entrada**, insira o valor da **URL de Serviço de Logon Único SAML** do assistente de configuração de aplicativo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f26dc-188">In the **Sign-in URL** box, enter the value of **SAML Single Sign-On Service URL** from the Azure AD application configuration window.</span></span>

    <span data-ttu-id="f26dc-189">d.</span><span class="sxs-lookup"><span data-stu-id="f26dc-189">d.</span></span> <span data-ttu-id="f26dc-190">Na caixa de texto **URL de Saída**, insira o valor da **URL de Saída** do assistente de configuração de aplicativo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f26dc-190">In the **Sign-out URL** box, enter the value of **Sign-Out URL** from the Azure AD application configuration window.</span></span>

    <span data-ttu-id="f26dc-191">e.</span><span class="sxs-lookup"><span data-stu-id="f26dc-191">e.</span></span> <span data-ttu-id="f26dc-192">Selecione **Usar POST**.</span><span class="sxs-lookup"><span data-stu-id="f26dc-192">Select **Use POST**.</span></span>

    <span data-ttu-id="f26dc-193">f.</span><span class="sxs-lookup"><span data-stu-id="f26dc-193">f.</span></span> <span data-ttu-id="f26dc-194">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="f26dc-194">Click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f26dc-195">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f26dc-195">Create an Azure AD test user</span></span>
<span data-ttu-id="f26dc-196">No portal do Azure, crie um usuário de teste chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="f26dc-196">In the Azure portal, create a test user called Britta Simon.</span></span>

![Nome e endereço de email do usuário de teste do Azure AD][100]

1. <span data-ttu-id="f26dc-198">No portal do Azure, no painel esquerdo, clique no ícone do **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f26dc-198">In the Azure portal, in the left pane, click the **Azure Active Directory** icon.</span></span>

    ![Ícone do Azure Active Directory](./media/active-directory-saas-clarizen-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="f26dc-200">Clique em **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="f26dc-200">Click **Users and groups**, and then click **All users** to display the list of users.</span></span>

    ![Clicar em "Usuários e grupos" e "Todos os usuários"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="f26dc-202">Na parte superior da caixa de diálogo, clique em **Adicionar** para abrir a caixa de diálogo **Usuário**.</span><span class="sxs-lookup"><span data-stu-id="f26dc-202">At the top of the dialog box, click **Add** to open the **User** dialog box.</span></span>

    ![O botão “Adicionar”](./media/active-directory-saas-clarizen-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="f26dc-204">Na caixa de diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f26dc-204">In the **User** dialog box, perform the following steps:</span></span>

    ![Caixa de diálogo "Usuário" com o nome, p endereço de email e a senha preenchidos](./media/active-directory-saas-clarizen-tutorial/create_aaduser_04.png)

    <span data-ttu-id="f26dc-206">a.</span><span class="sxs-lookup"><span data-stu-id="f26dc-206">a.</span></span> <span data-ttu-id="f26dc-207">Na caixa **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="f26dc-207">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f26dc-208">b.</span><span class="sxs-lookup"><span data-stu-id="f26dc-208">b.</span></span> <span data-ttu-id="f26dc-209">Na caixa **Nome de usuário**, digite o endereço de email da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="f26dc-209">In the **User name** box, type the email address of the Britta Simon account.</span></span>

    <span data-ttu-id="f26dc-210">c.</span><span class="sxs-lookup"><span data-stu-id="f26dc-210">c.</span></span> <span data-ttu-id="f26dc-211">Selecione **Mostrar Senha** e anote o valor de **Senha**.</span><span class="sxs-lookup"><span data-stu-id="f26dc-211">Select **Show Password** and write down the value of **Password**.</span></span>

    <span data-ttu-id="f26dc-212">d.</span><span class="sxs-lookup"><span data-stu-id="f26dc-212">d.</span></span> <span data-ttu-id="f26dc-213">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f26dc-213">Click **Create**.</span></span>

### <a name="create-a-clarizen-test-user"></a><span data-ttu-id="f26dc-214">Criar um usuário de teste do Clarizen</span><span class="sxs-lookup"><span data-stu-id="f26dc-214">Create a Clarizen test user</span></span>
<span data-ttu-id="f26dc-215">Para permitir que os usuários do Azure AD entrem no Clarizen, você deverá provisionar contas de usuário.</span><span class="sxs-lookup"><span data-stu-id="f26dc-215">To enable Azure AD users to sign in to Clarizen, you must provision user accounts.</span></span> <span data-ttu-id="f26dc-216">No caso do Clarizen, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="f26dc-216">In the case of Clarizen, provisioning is a manual task.</span></span>

1. <span data-ttu-id="f26dc-217">Entre em seu site de empresa do Clarizen como administrador.</span><span class="sxs-lookup"><span data-stu-id="f26dc-217">Sign in to your Clarizen company site as an administrator.</span></span>

2. <span data-ttu-id="f26dc-218">Clique em **Pessoas**.</span><span class="sxs-lookup"><span data-stu-id="f26dc-218">Click **People**.</span></span>

    <span data-ttu-id="f26dc-219">![Clicar em "Pessoas"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "Pessoas")</span><span class="sxs-lookup"><span data-stu-id="f26dc-219">![Clicking "People"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="f26dc-220">Clique em **Convidar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="f26dc-220">Click **Invite User**.</span></span>

    <span data-ttu-id="f26dc-221">![Botão "Convidar Usuário"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "Convidar Usuários")</span><span class="sxs-lookup"><span data-stu-id="f26dc-221">!["Invite User" button](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="f26dc-222">Na página **Convidar Pessoas**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f26dc-222">In the **Invite People** dialog box, perform the following steps:</span></span>

    <span data-ttu-id="f26dc-223">![Caixa de diálogo "Convidar Pessoas"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "Convidar Pessoas")</span><span class="sxs-lookup"><span data-stu-id="f26dc-223">!["Invite People" dialog box](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="f26dc-224">a.</span><span class="sxs-lookup"><span data-stu-id="f26dc-224">a.</span></span> <span data-ttu-id="f26dc-225">Na caixa **Email**, digite o endereço de email da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="f26dc-225">In the **Email** box, type the email address of the Britta Simon account.</span></span>

    <span data-ttu-id="f26dc-226">b.</span><span class="sxs-lookup"><span data-stu-id="f26dc-226">b.</span></span> <span data-ttu-id="f26dc-227">Clique em **Convidar**.</span><span class="sxs-lookup"><span data-stu-id="f26dc-227">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f26dc-228">O titular da conta do Active Directory do Azure receberá um email e seguirá um link para confirmar a conta antes que ela se torne ativa.</span><span class="sxs-lookup"><span data-stu-id="f26dc-228">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="f26dc-229">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f26dc-229">Assign the Azure AD test user</span></span>
<span data-ttu-id="f26dc-230">Permita que Brenda Fernandes use o logon único do Azure concedendo a ela acesso ao Clarizen.</span><span class="sxs-lookup"><span data-stu-id="f26dc-230">Enable Britta Simon to use Azure single sign-on by granting her access to Clarizen.</span></span>

![Usuário de teste atribuído][200]

1. <span data-ttu-id="f26dc-232">No portal do Azure, abra a exibição de aplicativos, navegue até a exibição de diretório, clique em **Aplicativos empresariais** e então clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f26dc-232">In the Azure portal, open the applications view, browse to the directory view, click **Enterprise applications**, and then click **All applications**.</span></span>

    ![Clicar em "Aplicativos corporativos" e em "Todos os aplicativos"][201]

2. <span data-ttu-id="f26dc-234">Na lista de aplicativos, selecione **Clarizen**.</span><span class="sxs-lookup"><span data-stu-id="f26dc-234">In the applications list, select **Clarizen**.</span></span>

    ![Selecionar Clarizen na lista](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_50.png)

3. <span data-ttu-id="f26dc-236">No painel esquerdo, clique em **Usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="f26dc-236">In the left pane, click **Users and groups**.</span></span>

    ![Clicar em “Usuário e grupos”][202]

4. <span data-ttu-id="f26dc-238">Clique no botão **Adicionar** .</span><span class="sxs-lookup"><span data-stu-id="f26dc-238">Click the **Add** button.</span></span> <span data-ttu-id="f26dc-239">Em seguida, na caixa de diálogo **Adicionar Atribuição**, selecione **Usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="f26dc-239">Then, in the **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![O botão "Adicionar" e a caixa de diálogo "Adicionar Atribuição"][203]

5. <span data-ttu-id="f26dc-241">Na caixa de diálogo **Usuários e grupos**, selecione **Brenda Fernandes** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="f26dc-241">In the **Users and groups** dialog box, select **Britta Simon** in the list of users.</span></span>

6. <span data-ttu-id="f26dc-242">Na caixa de diálogo **Usuários e grupos**, clique no botão **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="f26dc-242">In the **Users and groups** dialog box, click the **Select** button.</span></span>

7. <span data-ttu-id="f26dc-243">Na caixa de diálogo **Adicionar Atribuição**, clique no botão **Atribuir**.</span><span class="sxs-lookup"><span data-stu-id="f26dc-243">In the **Add Assignment** dialog box, click the **Assign** button.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="f26dc-244">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="f26dc-244">Test single sign-on</span></span>
<span data-ttu-id="f26dc-245">Teste sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="f26dc-245">Test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="f26dc-246">Ao clicar no bloco do Clarizen no Painel de Acesso, você deve ser conectado automaticamente ao aplicativo do Clarizen.</span><span class="sxs-lookup"><span data-stu-id="f26dc-246">When you click the Clarizen tile in the Access Panel, you should be automatically signed in to your Clarizen application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f26dc-247">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="f26dc-247">Additional resources</span></span>

* [<span data-ttu-id="f26dc-248">Lista de tutoriais sobre como integrar aplicativos SaaS ao Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="f26dc-248">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f26dc-249">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f26dc-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_203.png
