---
title: "Tutorial: Integração do Azure Active Directory com o Help Scout | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Help Scout."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0aad9910-0bc1-4394-9f73-267cf39973ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: jeedes
ms.openlocfilehash: 84cee39c28a0f7e6b9878441e504131795673020
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-help-scout"></a><span data-ttu-id="9dfb4-103">Tutorial: integração do Azure Active Directory com o Help Scout</span><span class="sxs-lookup"><span data-stu-id="9dfb4-103">Tutorial: Azure Active Directory integration with Help Scout</span></span>

<span data-ttu-id="9dfb4-104">Neste tutorial, você aprenderá a integrar o Help Scout ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="9dfb4-104">In this tutorial, you learn how to integrate Help Scout with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9dfb4-105">Você obtém os seguintes benefícios ao integrar o Help Scout ao Azure AD:</span><span class="sxs-lookup"><span data-stu-id="9dfb4-105">You get the following benefits from integrating Help Scout with Azure AD:</span></span>

- <span data-ttu-id="9dfb4-106">No Azure AD, é possível controlar quem tem acesso ao Help Scout.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-106">In Azure AD, you can control who has access to Help Scout.</span></span>
- <span data-ttu-id="9dfb4-107">Você pode conectar automaticamente seus usuários ao Help Scout usando o logon único e a conta do Azure AD de um usuário.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-107">You can automatically sign in your users to Help Scout by using single sign-on and a user's Azure AD account.</span></span>
- <span data-ttu-id="9dfb4-108">É possível gerenciar suas contas em uma, um local central e no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-108">You can manage your accounts in one, central location, the Azure portal.</span></span>

<span data-ttu-id="9dfb4-109">Para saber mais sobre a integração de aplicativos de SaaS (software como serviço) ao Azure AD, confira [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9dfb4-109">To learn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9dfb4-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9dfb4-110">Prerequisites</span></span>

<span data-ttu-id="9dfb4-111">Para configurar a integração do Azure AD ao Help Scout, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="9dfb4-111">To set up Azure AD integration with Help Scout, you need the following items:</span></span>

- <span data-ttu-id="9dfb4-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9dfb4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9dfb4-113">Uma assinatura do Help Scout, com o logon único ativado</span><span class="sxs-lookup"><span data-stu-id="9dfb4-113">A Help Scout subscription, with single sign-on turned on</span></span> 

> [!NOTE]
> <span data-ttu-id="9dfb4-114">Em caso de testar as etapas deste tutorial, recomendamos não testá-las em um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-114">If you test the steps in this tutorial, we recommend that you don't test them in a production environment.</span></span>

<span data-ttu-id="9dfb4-115">Recomendações para testar as etapas deste tutorial:</span><span class="sxs-lookup"><span data-stu-id="9dfb4-115">Recommendations for testing the steps in this tutorial:</span></span>

- <span data-ttu-id="9dfb4-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-116">Do not use your production environment, unless it's necessary.</span></span>
- <span data-ttu-id="9dfb4-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9dfb4-117">If you don't have an Azure AD trial environment, you can [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9dfb4-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="9dfb4-118">Scenario description</span></span>
<span data-ttu-id="9dfb4-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="9dfb4-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="9dfb4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9dfb4-121">Adicionar o Help Scout da galeria.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-121">Add Help Scout from the gallery.</span></span>
2. <span data-ttu-id="9dfb4-122">Configurar e testar o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-122">Set up and test Azure AD single sign-on.</span></span>

## <a name="add-help-scout-from-the-gallery"></a><span data-ttu-id="9dfb4-123">Adicionar o Help Scout da galeria</span><span class="sxs-lookup"><span data-stu-id="9dfb4-123">Add Help Scout from the gallery</span></span>
<span data-ttu-id="9dfb4-124">Para configurar a integração do Help Scout ao Azure AD, na galeria, adicione o Help Scout à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-124">To set up the integration of Help Scout with Azure AD, in the gallery, add Help Scout to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9dfb4-125">Para adicionar o Help Scout da galeria:</span><span class="sxs-lookup"><span data-stu-id="9dfb4-125">To add Help Scout from the gallery:</span></span>

1. <span data-ttu-id="9dfb4-126">No [portal do Azure](https://portal.azure.com), no menu esquerdo, selecione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-126">In the [Azure portal](https://portal.azure.com), in the left menu, select **Azure Active Directory**.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="9dfb4-128">Selecione **Aplicativos empresariais** e, em seguida, selecione **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![A página de aplicativos empresariais][2]
    
3. <span data-ttu-id="9dfb4-130">Para adicionar um novo aplicativo, selecione **Novo aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-130">To add a new application, select **New application**.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="9dfb4-132">Na caixa de pesquisa, insira **Help Scout**.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-132">In the search box, enter **Help Scout**.</span></span> <span data-ttu-id="9dfb4-133">Nos resultados da pesquisa, selecione **Help Scout** e **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-133">In the search results, select **Help Scout**, and then select **Add**.</span></span>

    ![Help Scout na lista de resultados](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_addfromgallery.png)

## <a name="set-up-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9dfb4-135">Configurar e testar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9dfb4-135">Set up and test Azure AD single sign-on</span></span>

<span data-ttu-id="9dfb4-136">Nesta seção, você vai configurar e testar o logon único do Azure AD com o Help Scout, com base em uma usuária de teste chamada *Brenda Fernandes*.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-136">In this section, you set up and test Azure AD single sign-on with Help Scout based on a test user named *Britta Simon*.</span></span>

<span data-ttu-id="9dfb4-137">Para que o logon único funcione, o Azure AD precisa conhecer o usuário equivalente do Azure AD no Help Scout.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-137">For single sign-on to work, Azure AD needs to know the Azure AD counterpart user in Help Scout.</span></span> <span data-ttu-id="9dfb4-138">É necessário estabelecer uma relação de vinculação entre um usuário do Azure AD e o usuário relacionado no Help Scout.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-138">A link relationship between an Azure AD user and the related user in Help Scout must be established.</span></span>

<span data-ttu-id="9dfb4-139">Para estabelecer a relação de vinculação, no Help Scout, para **Nome de usuário**, atribua o valor de **nome de usuário** no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-139">To establish the link relationship, in Help Scout, for **Username**, assign the value of the **user name** in Azure AD.</span></span>

<span data-ttu-id="9dfb4-140">Para configurar e testar o logon único do Azure AD com o Help Scout, conclua as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="9dfb4-140">To configure and test Azure AD single sign-on with Help Scout, complete the following tasks:</span></span>

1. <span data-ttu-id="9dfb4-141">[Configurar o logon único do Azure AD](#set-up-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="9dfb4-141">[Set up Azure AD single sign-on](#set-up-azure-ad-single-sign-on).</span></span> <span data-ttu-id="9dfb4-142">Configura um usuário para usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-142">Sets up a user to use this feature.</span></span>
2. <span data-ttu-id="9dfb4-143">[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="9dfb4-143">[Create an Azure AD test user](#create-an-azure-ad-test-user).</span></span> <span data-ttu-id="9dfb4-144">Testa o logon único do Azure AD com a usuária Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-144">Tests Azure AD single sign-on with the user Britta Simon.</span></span>
3. <span data-ttu-id="9dfb4-145">[Criar um usuário de teste do Help Scout](#create-a-help-scout-test-user).</span><span class="sxs-lookup"><span data-stu-id="9dfb4-145">[Create a Help Scout test user](#create-a-help-scout-test-user).</span></span> <span data-ttu-id="9dfb4-146">Cria um equivalente de Brenda Fernandes no Help Scout que é vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-146">Creates a counterpart of Britta Simon in Help Scout that is linked to the Azure AD representation of the user.</span></span>
4. <span data-ttu-id="9dfb4-147">[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="9dfb4-147">[Assign the Azure AD test user](#assign-the-azure-ad-test-user).</span></span> <span data-ttu-id="9dfb4-148">Configura Brenda Fernandes para usar o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-148">Sets up Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9dfb4-149">[Testar o logon único](#test-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="9dfb4-149">[Test single sign-on](#test-single-sign-on).</span></span> <span data-ttu-id="9dfb4-150">Verifica se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-150">Verifies that the configuration works.</span></span>

### <a name="set-up-azure-ad-single-sign-on"></a><span data-ttu-id="9dfb4-151">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9dfb4-151">Set up Azure AD single sign-on</span></span>

<span data-ttu-id="9dfb4-152">Nesta seção, você configura o logon único do Azure AD no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-152">In this section, you set up Azure AD single sign-on in the Azure portal.</span></span> <span data-ttu-id="9dfb4-153">Em seguida, define o logon único no aplicativo Help Scout.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-153">Then, you set up single sign-on in your Help Scout application.</span></span>

<span data-ttu-id="9dfb4-154">Para configurar o logon único do Azure AD com o Help Scout:</span><span class="sxs-lookup"><span data-stu-id="9dfb4-154">To set up Azure AD single sign-on with Help Scout:</span></span>

1. <span data-ttu-id="9dfb4-155">No portal do Azure, na página de integração do aplicativo **Help Scout**, selecione **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-155">In the Azure portal, on the **Help Scout** application integration page, select **Single sign-on**.</span></span>
 
    ![Link Configurar logon único][4]

2. <span data-ttu-id="9dfb4-157">Na página **Logon único**, para **Modo**, selecione **Logon com base em SAML**.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-157">On the **Single sign-on** page, for **Mode**, select **SAML-based Sign-on**.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_samlbase.png)

3. <span data-ttu-id="9dfb4-159">Em **Domínio e URLs do Help Scout**, se quiser configurar o aplicativo no modo iniciado por IDP, concluas as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="9dfb4-159">Under **Help Scout Domain and URLs**, if you want to set up the application in IDP-initiated mode, complete the following steps:</span></span>

    1. <span data-ttu-id="9dfb4-160">Na caixa **Identificador**, digite uma URL com o seguinte padrão: `urn:auth0:helpscout:<instancename>`</span><span class="sxs-lookup"><span data-stu-id="9dfb4-160">In the **Identifier** box, enter a URL that has the following pattern: `urn:auth0:helpscout:<instancename>`</span></span>

    2. <span data-ttu-id="9dfb4-161">Na caixa **URL de Resposta**, digite uma URL com o seguinte padrão: `https://helpscout.auth0.com/login/callback?connection=<instancename>`</span><span class="sxs-lookup"><span data-stu-id="9dfb4-161">In the **Reply URL** box, enter a URL that has the following pattern: `https://helpscout.auth0.com/login/callback?connection=<instancename>`</span></span>

    ![Informações de logon único de Domínio e URLs do Help Scout](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url.png)

4. <span data-ttu-id="9dfb4-163">Se você quiser configurar o aplicativo no modo iniciado pelo SP, marque a caixa de seleção **Mostrar configurações avançadas de URL** e siga este procedimento:</span><span class="sxs-lookup"><span data-stu-id="9dfb4-163">If you want to set up the application in SP-initiated mode, select the **Show advanced URL settings** check box, and then do the following:</span></span>

    * <span data-ttu-id="9dfb4-164">Na caixa **URL de Entrada**, digite uma URL com o seguinte formato: `https://secure.helpscout.net/members/login/`</span><span class="sxs-lookup"><span data-stu-id="9dfb4-164">In the **Sign on URL** box, enter a URL that has the following format: `https://secure.helpscout.net/members/login/`</span></span>

    ![Informações de logon único de Domínio e URLs do Help Scout](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url1.png)
 
    > [!NOTE] 
    > <span data-ttu-id="9dfb4-166">Os valores nessas URLs são apenas para demonstração.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-166">The values in these URLs are for demonstration only.</span></span> <span data-ttu-id="9dfb4-167">Atualize os valores com as verdadeiras URL de identificador e URL de resposta.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-167">Update the values with the actual identifier URL and reply URL.</span></span> <span data-ttu-id="9dfb4-168">Para obter esses valores, entre em contato com a [equipe de suporte do Help Scout](mailto:help@helpscout.com).</span><span class="sxs-lookup"><span data-stu-id="9dfb4-168">To get these values, contact [Help Scout support team](mailto:help@helpscout.com).</span></span> 

5. <span data-ttu-id="9dfb4-169">Em **Certificado de Autenticação SAML**, selecione **XML de Metadados** e salve o arquivo de metadados no computador.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-169">Under **SAML Signing Certificate**, select **Metadata XML**, and then save the metadata file on your computer.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_certificate.png) 

6. <span data-ttu-id="9dfb4-171">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-171">Select **Save**.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-helpscout-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="9dfb4-173">Para configurar o logon único no lado do Help Scout, envie o arquivo XML de metadados baixado para a [equipe de suporte do Help Scout](mailto:help@helpscout.com).</span><span class="sxs-lookup"><span data-stu-id="9dfb4-173">To set up single sign-on on the Help Scout side, send the downloaded metadata XML file to the [Help Scout support team](mailto:help@helpscout.com).</span></span> <span data-ttu-id="9dfb4-174">A equipe de suporte do Help Scout aplica essa configuração para que a conexão de logon único do SAML seja definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-174">The Help Scout support team applies this setting so that the SAML single sign-on connection is set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="9dfb4-175">É possível ler uma versão concisa dessas instruções no [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="9dfb4-175">You can read a concise version of these instructions in the [Azure portal](https://portal.azure.com), while you are setting up your app!</span></span> <span data-ttu-id="9dfb4-176">Depois de adicionar o aplicativo selecionando **Active Directory** > **Aplicativos Empresariais**, selecione a guia **Logon Único**. Você pode acessar a documentação inserida na seção **Configuração**, na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-176">After you add the app by selecting **Active Directory** > **Enterprise Applications**, select the **Single Sign-On** tab. You can access the embedded documentation in the **Configuration** section, at the bottom of the page.</span></span> <span data-ttu-id="9dfb4-177">Para saber mais, confira a [documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="9dfb4-177">For more information, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9dfb4-178">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9dfb4-178">Create an Azure AD test user</span></span>

<span data-ttu-id="9dfb4-179">Nesta seção, no portal do Azure, você criará uma usuária de teste chamada Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-179">In this section, in the Azure portal, you create a test user named Britta Simon.</span></span>

![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="9dfb4-181">Para criar um usuário de teste no Azure AD:</span><span class="sxs-lookup"><span data-stu-id="9dfb4-181">To create a test user in Azure AD:</span></span>

1. <span data-ttu-id="9dfb4-182">No portal do Azure, no menu esquerdo, selecione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-182">In the Azure portal, in the left menu, select **Azure Active Directory**.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-helpscout-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="9dfb4-184">Para exibir a lista de usuários, selecione **Usuários e grupos** e, em seguida, selecione **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-184">To display the list of users, select **Users and groups**, and then select **All users**.</span></span>

    ![Selecionar Usuários e grupos e depois Todos os usuários](./media/active-directory-saas-helpscout-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="9dfb4-186">Para abrir a caixa de diálogo **Usuário**, na parte superior da página **Todos os Usuários**, selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-186">To open the **User** dialog box, at the top of the **All Users** page, select **Add**.</span></span>

    ![O botão Adicionar](./media/active-directory-saas-helpscout-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="9dfb4-188">Na caixa de diálogo **Usuário**, conclua as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="9dfb4-188">In the **User** dialog box, complete the following steps:</span></span>

    1. <span data-ttu-id="9dfb4-189">Na caixa **Nome**, insira **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-189">In the **Name** box, enter **BrittaSimon**.</span></span>

    2. <span data-ttu-id="9dfb4-190">Na caixa **Nome de usuário**, insira o endereço de email da usuária Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-190">In the **User name** box, enter the email address of user Britta Simon.</span></span>

    3. <span data-ttu-id="9dfb4-191">Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    4. <span data-ttu-id="9dfb4-192">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-192">Select **Create**.</span></span>

        ![A caixa de diálogo Usuário](./media/active-directory-saas-helpscout-tutorial/create_aaduser_04.png)

 
### <a name="create-a-help-scout-test-user"></a><span data-ttu-id="9dfb4-194">Criar um usuário de teste do Help Scout</span><span class="sxs-lookup"><span data-stu-id="9dfb4-194">Create a Help Scout test user</span></span>

<span data-ttu-id="9dfb4-195">O objeto desta seção é criar um usuário chamado Brenda Fernandes no Help Scout.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-195">The object of this section is to create a user named Britta Simon in Help Scout.</span></span> <span data-ttu-id="9dfb4-196">O Help Scout dá suporte ao provisionamento JIT (Just-In-Time), que é ativado por padrão.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-196">Help Scout supports just-in-time (JIT) provisioning, which is turned on by default.</span></span>

<span data-ttu-id="9dfb4-197">Nesta seção, não há ação nem tarefa a ser executada.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-197">In this section, there's no action or task to complete.</span></span> <span data-ttu-id="9dfb4-198">Se um usuário ainda não existir no Help Scout, um novo será criado quando você tentar acessar o Help Scout.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-198">If a user doesn't already exist in Help Scout, a new one is created when you attempt to access Help Scout.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="9dfb4-199">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9dfb4-199">Assign the Azure AD test user</span></span>

<span data-ttu-id="9dfb4-200">Nesta seção, você permitirá que a usuária Brenda Fernandes use o logon único do Azure AD concedendo acesso de conta de usuário ao Help Scout.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-200">In this section, you allow the user Britta Simon to use Azure AD single sign-on by granting the user account access to Help Scout.</span></span>

![Atribuir a função de usuário][200] 

<span data-ttu-id="9dfb4-202">Para atribuir Brenda Fernandes ao Help Scout:</span><span class="sxs-lookup"><span data-stu-id="9dfb4-202">To assign Britta Simon to Help Scout:</span></span>

1. <span data-ttu-id="9dfb4-203">No portal do Azure, abra a exibição de aplicativos e vá para a exibição de diretório.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-203">In the Azure portal, open the applications view, and then go to the directory view.</span></span> <span data-ttu-id="9dfb4-204">Selecione **Aplicativos empresariais** e, em seguida, selecione **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-204">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="9dfb4-206">Na lista de aplicativos, selecione **Help Scout**.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-206">In the applications list, select **Help Scout**.</span></span>

    ![O link do Help Scout na lista de Aplicativos](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_app.png)  

3. <span data-ttu-id="9dfb4-208">No menu esquerdo, selecione **Usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-208">In the left menu, select **Users and groups**.</span></span>

    ![O link Usuários e grupos][202]

4. <span data-ttu-id="9dfb4-210">Selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-210">Select **Add**.</span></span> <span data-ttu-id="9dfb4-211">Na página **Adicionar Atribuição**, selecione **Usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-211">Then, on the **Add Assignment** page, select **Users and groups**.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="9dfb4-213">Na página **Usuários e grupos**, na lista de usuários, selecione **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-213">On the **Users and groups** page, in the list of users, select **Britta Simon**.</span></span>

6. <span data-ttu-id="9dfb4-214">Na página **Usuários e grupos**, selecione **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-214">On the **Users and groups** page, select **Select**.</span></span>

7. <span data-ttu-id="9dfb4-215">Na página **Adicionar Atribuição**, selecione **Atribuir**.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-215">On the **Add Assignment** page, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9dfb4-216">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="9dfb4-216">Test single sign-on</span></span>

<span data-ttu-id="9dfb4-217">Nesta seção, você testará sua configuração de logon único do Azure AD usando o painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-217">In this section, you test your Azure AD single sign-on configuration by using the access panel.</span></span>

<span data-ttu-id="9dfb4-218">Ao selecionar o bloco Help Scout no painel de acesso, você deverá ser conectado automaticamente ao aplicativo Help Scout.</span><span class="sxs-lookup"><span data-stu-id="9dfb4-218">When you select the Help Scout tile in the access panel, you should be automatically signed in to your Help Scout application.</span></span>

<span data-ttu-id="9dfb4-219">Para saber mais sobre o painel de acesso, veja [Introdução ao painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9dfb4-219">For more information about the access panel, see [Introduction to the access panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9dfb4-220">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="9dfb4-220">Additional resources</span></span>

* [<span data-ttu-id="9dfb4-221">Lista de tutoriais sobre como integrar aplicativos SaaS ao Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="9dfb4-221">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9dfb4-222">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9dfb4-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_203.png

