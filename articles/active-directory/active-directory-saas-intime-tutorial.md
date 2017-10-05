---
title: "Tutorial: Integração do Azure Active Directory ao InTime | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o InTime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d4e2c6e1-ae5d-4d2c-8ffc-1b24534d376a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: jeedes
ms.openlocfilehash: 4bb22c92ad7f6963be6ca15073f7f01da99ba2bb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intime"></a><span data-ttu-id="bde09-103">Tutorial: Integração do Azure Active Directory ao InTime</span><span class="sxs-lookup"><span data-stu-id="bde09-103">Tutorial: Azure Active Directory integration with InTime</span></span>

<span data-ttu-id="bde09-104">Neste tutorial, você aprende a integrar o InTime ao Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bde09-104">In this tutorial, you learn how to integrate InTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bde09-105">A integração do InTime ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="bde09-105">Integrating InTime with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bde09-106">Você pode controlar no Azure AD quem terá acesso ao InTime.</span><span class="sxs-lookup"><span data-stu-id="bde09-106">You can control in Azure AD who has access to InTime.</span></span>
- <span data-ttu-id="bde09-107">Você pode permitir que seus usuários entrem automaticamente no InTime (Logon Único) com suas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bde09-107">You can enable your users to automatically get signed-on to InTime (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="bde09-108">Você pode gerenciar suas contas em um único local central – o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="bde09-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="bde09-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bde09-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bde09-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bde09-110">Prerequisites</span></span>

<span data-ttu-id="bde09-111">Para configurar a integração do Azure AD ao InTime, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="bde09-111">To configure Azure AD integration with InTime, you need the following items:</span></span>

- <span data-ttu-id="bde09-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="bde09-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bde09-113">Uma assinatura habilitada para logon único do InTime</span><span class="sxs-lookup"><span data-stu-id="bde09-113">A InTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bde09-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="bde09-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bde09-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="bde09-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bde09-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="bde09-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bde09-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bde09-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bde09-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="bde09-118">Scenario description</span></span>
<span data-ttu-id="bde09-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="bde09-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bde09-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="bde09-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bde09-121">Adição do InTime a partir da galeria</span><span class="sxs-lookup"><span data-stu-id="bde09-121">Adding InTime from the gallery</span></span>
2. <span data-ttu-id="bde09-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="bde09-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intime-from-the-gallery"></a><span data-ttu-id="bde09-123">Adição do InTime a partir da galeria</span><span class="sxs-lookup"><span data-stu-id="bde09-123">Adding InTime from the gallery</span></span>
<span data-ttu-id="bde09-124">Para configurar a integração do InTime ao Azure AD, você precisa adicionar o InTime por meio da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="bde09-124">To configure the integration of InTime into Azure AD, you need to add InTime from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bde09-125">**Para adicionar o InTime por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="bde09-125">**To add InTime from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bde09-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bde09-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="bde09-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="bde09-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bde09-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="bde09-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="bde09-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bde09-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="bde09-133">Na caixa de pesquisa, digite **InTime**, selecione **InTime** no painel de resultados e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bde09-133">In the search box, type **InTime**, select **InTime** from result panel then click **Add** button to add the application.</span></span>

    ![InTime na lista de resultados](./media/active-directory-saas-intime-tutorial/tutorial_intime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="bde09-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="bde09-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="bde09-136">Nesta seção, você configura e testa o logon único do Azure AD com o InTime, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="bde09-136">In this section, you configure and test Azure AD single sign-on with InTime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bde09-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do InTime é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bde09-137">For single sign-on to work, Azure AD needs to know what the counterpart user in InTime is to a user in Azure AD.</span></span> <span data-ttu-id="bde09-138">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no InTime.</span><span class="sxs-lookup"><span data-stu-id="bde09-138">In other words, a link relationship between an Azure AD user and the related user in InTime needs to be established.</span></span>

<span data-ttu-id="bde09-139">No InTime, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="bde09-139">In InTime, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="bde09-140">Para configurar e testar o logon único do Azure AD com o InTime, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="bde09-140">To configure and test Azure AD single sign-on with InTime, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bde09-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="bde09-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bde09-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="bde09-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bde09-143">**[Criar a partir de um usuário de teste do InTime](#create-a-intime-test-user)** – para ter um equivalente de Brenda Fernandes no InTime vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bde09-143">**[Create a InTime test user](#create-a-intime-test-user)** - to have a counterpart of Britta Simon in InTime that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="bde09-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bde09-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bde09-145">**[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="bde09-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="bde09-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="bde09-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="bde09-147">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo InTime.</span><span class="sxs-lookup"><span data-stu-id="bde09-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your InTime application.</span></span>

<span data-ttu-id="bde09-148">**Para configurar o logon único do Azure AD com o InTime, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="bde09-148">**To configure Azure AD single sign-on with InTime, perform the following steps:**</span></span>

1. <span data-ttu-id="bde09-149">No portal do Azure, na página de integração de aplicativos do **InTime**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="bde09-149">In the Azure portal, on the **InTime** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="bde09-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="bde09-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-intime-tutorial/tutorial_intime_samlbase.png)

3. <span data-ttu-id="bde09-153">Na seção **URLs e Domínio do InTime**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="bde09-153">On the **InTime Domain and URLs** section, perform the following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do InTime](./media/active-directory-saas-intime-tutorial/tutorial_intime_url.png)

    <span data-ttu-id="bde09-155">a.</span><span class="sxs-lookup"><span data-stu-id="bde09-155">a.</span></span> <span data-ttu-id="bde09-156">Na caixa de texto **URL de Logon**, digite a URL: `https://intime6.intimesoft.com/mytime/login/login.xhtml`</span><span class="sxs-lookup"><span data-stu-id="bde09-156">In the **Sign-on URL** textbox, type the URL: `https://intime6.intimesoft.com/mytime/login/login.xhtml`</span></span>

    <span data-ttu-id="bde09-157">b.</span><span class="sxs-lookup"><span data-stu-id="bde09-157">b.</span></span> <span data-ttu-id="bde09-158">Na caixa de texto **Identificador**, digite a URL: `https://auth.intimesoft.com/auth/realms/master`</span><span class="sxs-lookup"><span data-stu-id="bde09-158">In the **Identifier** textbox, type the URL: `https://auth.intimesoft.com/auth/realms/master`</span></span>

4. <span data-ttu-id="bde09-159">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="bde09-159">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-intime-tutorial/tutorial_intime_certificate.png) 

5. <span data-ttu-id="bde09-161">Seu aplicativo InTime espera as declarações do SAML em um formato específico, o que exige que você adicione mapeamentos de atributo personalizados de acordo com a sua configuração de atributos de token SAML.</span><span class="sxs-lookup"><span data-stu-id="bde09-161">Your InTime application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="bde09-162">A captura de tela a seguir mostra um exemplo disso.</span><span class="sxs-lookup"><span data-stu-id="bde09-162">The following screenshot shows an example for this.</span></span> <span data-ttu-id="bde09-163">O valor padrão do **Identificador de usuário** é **user.userprincipalname**, mas o InTime espera que isso seja mapeado com o endereço de email do usuário.</span><span class="sxs-lookup"><span data-stu-id="bde09-163">The default value of **User Identifier** is **user.userprincipalname** but InTime expects this to be mapped with the user's email address.</span></span> <span data-ttu-id="bde09-164">Para que você possa usar o atributo **user.mail** na lista ou usar o valor do atributo apropriado com base na configuração da sua organização</span><span class="sxs-lookup"><span data-stu-id="bde09-164">For that you can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration</span></span> 

    ![Configurar Atributo](./media/active-directory-saas-intime-tutorial/tutorial_intime_attribute.png)

6. <span data-ttu-id="bde09-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="bde09-166">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-intime-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="bde09-168">Na seção **Configuração do InTime**, clique em **Configurar o InTime** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="bde09-168">On the **InTime Configuration** section, click **Configure InTime** to open **Configure sign-on** window.</span></span> <span data-ttu-id="bde09-169">Copie a **URL de Saída e a URL do Serviço de Logon Único SAML** da **seção Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="bde09-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuração do InTime](./media/active-directory-saas-intime-tutorial/tutorial_intime_configure.png) 

8. <span data-ttu-id="bde09-171">Para configurar o logon único no lado do **InTime**, é necessário enviar o **XML de metadados**, a **URL de Saída e a URL do Serviço de Logon Único SAML** baixados para a [Equipe de suporte do InTime](mailto:hdollard@intimesoft.com).</span><span class="sxs-lookup"><span data-stu-id="bde09-171">To configure single sign-on on **InTime** side, you need to send the downloaded **Metadata XML**, **Sign-Out URL, and SAML Single Sign-On Service URL** to [InTime support team](mailto:hdollard@intimesoft.com).</span></span> <span data-ttu-id="bde09-172">Eles definem essa configuração para ter a conexão de SSO de SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="bde09-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="bde09-173">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="bde09-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bde09-174">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="bde09-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bde09-175">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bde09-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="bde09-176">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="bde09-176">Create an Azure AD test user</span></span>

<span data-ttu-id="bde09-177">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="bde09-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="bde09-179">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="bde09-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bde09-180">No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bde09-180">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-intime-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="bde09-182">Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="bde09-182">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-intime-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="bde09-184">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.</span><span class="sxs-lookup"><span data-stu-id="bde09-184">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![O botão Adicionar](./media/active-directory-saas-intime-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="bde09-186">Na caixa de diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="bde09-186">In the **User** dialog box, perform the following steps:</span></span>

    ![A caixa de diálogo Usuário](./media/active-directory-saas-intime-tutorial/create_aaduser_04.png)

    <span data-ttu-id="bde09-188">a.</span><span class="sxs-lookup"><span data-stu-id="bde09-188">a.</span></span> <span data-ttu-id="bde09-189">Na caixa **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="bde09-189">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bde09-190">b.</span><span class="sxs-lookup"><span data-stu-id="bde09-190">b.</span></span> <span data-ttu-id="bde09-191">Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="bde09-191">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="bde09-192">c.</span><span class="sxs-lookup"><span data-stu-id="bde09-192">c.</span></span> <span data-ttu-id="bde09-193">Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.</span><span class="sxs-lookup"><span data-stu-id="bde09-193">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="bde09-194">d.</span><span class="sxs-lookup"><span data-stu-id="bde09-194">d.</span></span> <span data-ttu-id="bde09-195">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="bde09-195">Click **Create**.</span></span>
 
### <a name="create-a-intime-test-user"></a><span data-ttu-id="bde09-196">Criar um usuário de teste do InTime</span><span class="sxs-lookup"><span data-stu-id="bde09-196">Create a InTime test user</span></span>

<span data-ttu-id="bde09-197">Nesta seção, você cria um usuário chamado Brenda Fernandes no InTime.</span><span class="sxs-lookup"><span data-stu-id="bde09-197">In this section, you create a user called Britta Simon in InTime.</span></span> <span data-ttu-id="bde09-198">Trabalhe com a [equipe de suporte do InTime](mailto:hdollard@intimesoft.com) para adicionar os usuários na plataforma do InTime.</span><span class="sxs-lookup"><span data-stu-id="bde09-198">Work with [InTime support team](mailto:hdollard@intimesoft.com) to add the users in the InTime platform.</span></span> <span data-ttu-id="bde09-199">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="bde09-199">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="bde09-200">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="bde09-200">Assign the Azure AD test user</span></span>

<span data-ttu-id="bde09-201">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao InTime.</span><span class="sxs-lookup"><span data-stu-id="bde09-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to InTime.</span></span>

![Atribuir a função de usuário][200] 

<span data-ttu-id="bde09-203">**Para atribuir Brenda Fernandes ao InTime, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="bde09-203">**To assign Britta Simon to InTime, perform the following steps:**</span></span>

1. <span data-ttu-id="bde09-204">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="bde09-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="bde09-206">Na lista de aplicativos, selecione **InTime**.</span><span class="sxs-lookup"><span data-stu-id="bde09-206">In the applications list, select **InTime**.</span></span>

    ![O link do InTime na lista de Aplicativos](./media/active-directory-saas-intime-tutorial/tutorial_intime_app.png)  

3. <span data-ttu-id="bde09-208">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="bde09-208">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202]

4. <span data-ttu-id="bde09-210">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="bde09-210">Click **Add** button.</span></span> <span data-ttu-id="bde09-211">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bde09-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="bde09-213">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="bde09-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="bde09-214">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bde09-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bde09-215">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bde09-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="bde09-216">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="bde09-216">Test single sign-on</span></span>

<span data-ttu-id="bde09-217">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="bde09-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="bde09-218">Ao clicar no bloco InTime no Painel de Acesso, você deve acessar a página de logon do aplicativo InTime.</span><span class="sxs-lookup"><span data-stu-id="bde09-218">When you click the InTime tile in the Access Panel, you should get the login page of your InTime application.</span></span> <span data-ttu-id="bde09-219">Clique no botão **Login**, uma série de IdPs serão exibidos em uma lista de botões.</span><span class="sxs-lookup"><span data-stu-id="bde09-219">Click the **Login** button, then a series of IdPs will be displayed on a list of buttons.</span></span> <span data-ttu-id="bde09-220">Clique no **nome IDP** determinado pela [equipe de suporte do InTime](mailto:hdollard@intimesoft.com) para fazer logon no seu aplicativo InTime.</span><span class="sxs-lookup"><span data-stu-id="bde09-220">click **IDP name** given by [InTime support team](mailto:hdollard@intimesoft.com) to login into your InTime application.</span></span> <span data-ttu-id="bde09-221">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bde09-221">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="bde09-222">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="bde09-222">Additional resources</span></span>

* [<span data-ttu-id="bde09-223">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="bde09-223">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bde09-224">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bde09-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-intime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intime-tutorial/tutorial_general_203.png

