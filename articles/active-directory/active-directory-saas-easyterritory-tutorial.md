---
title: "Tutorial: Integração do Azure Active Directory ao EasyTerritory | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o EasyTerritory."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d29b362d-e986-4f67-8ff2-e158e49353aa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 46f99496397e2ed39b1d9410453dac7983ced612
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-easyterritory"></a><span data-ttu-id="0711d-103">Tutorial: integração do Azure Active Directory ao EasyTerritory</span><span class="sxs-lookup"><span data-stu-id="0711d-103">Tutorial: Azure Active Directory integration with EasyTerritory</span></span>

<span data-ttu-id="0711d-104">Neste tutorial, você aprenderá como integrar o EasyTerritory ao Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0711d-104">In this tutorial, you learn how to integrate EasyTerritory with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0711d-105">A integração do EasyTerritory ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="0711d-105">Integrating EasyTerritory with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0711d-106">No Azure AD, é possível controlar quem tem acesso ao EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="0711d-106">You can control in Azure AD who has access to EasyTerritory.</span></span>
- <span data-ttu-id="0711d-107">Você pode permitir que os usuários façam logon automaticamente no EasyTerritory (logon único) com as respectivas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0711d-107">You can enable your users to automatically get signed-on to EasyTerritory (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="0711d-108">Você pode gerenciar suas contas em um único local central – o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0711d-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="0711d-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0711d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0711d-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0711d-110">Prerequisites</span></span>

<span data-ttu-id="0711d-111">Para configurar a integração do Azure AD ao EasyTerritory, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="0711d-111">To configure Azure AD integration with EasyTerritory, you need the following items:</span></span>

- <span data-ttu-id="0711d-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0711d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0711d-113">Uma assinatura do EasyTerritory habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="0711d-113">A EasyTerritory single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0711d-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="0711d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0711d-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="0711d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0711d-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="0711d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0711d-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0711d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0711d-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="0711d-118">Scenario description</span></span>
<span data-ttu-id="0711d-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="0711d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0711d-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="0711d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0711d-121">Adicionar o EasyTerritory da galeria</span><span class="sxs-lookup"><span data-stu-id="0711d-121">Adding EasyTerritory from the gallery</span></span>
2. <span data-ttu-id="0711d-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0711d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-easyterritory-from-the-gallery"></a><span data-ttu-id="0711d-123">Adicionar o EasyTerritory da galeria</span><span class="sxs-lookup"><span data-stu-id="0711d-123">Adding EasyTerritory from the gallery</span></span>
<span data-ttu-id="0711d-124">Para configurar a integração do EasyTerritory ao Azure AD, você precisa adicionar o EasyTerritory da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="0711d-124">To configure the integration of EasyTerritory into Azure AD, you need to add EasyTerritory from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0711d-125">**Para adicionar o EasyTerritory da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="0711d-125">**To add EasyTerritory from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0711d-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0711d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="0711d-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="0711d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0711d-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="0711d-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="0711d-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0711d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="0711d-133">Na caixa de pesquisa, digite **EasyTerritory**, selecione **EasyTerritory** no painel de resultados e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0711d-133">In the search box, type **EasyTerritory**, select **EasyTerritory** from result panel then click **Add** button to add the application.</span></span>

    ![EasyTerritory na lista de resultados](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0711d-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0711d-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="0711d-136">Nesta seção, você configurará e testará o logon único do Azure AD com o EasyTerritory, com base em um usuário de teste chamado “Britta Simon”.</span><span class="sxs-lookup"><span data-stu-id="0711d-136">In this section, you configure and test Azure AD single sign-on with EasyTerritory based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0711d-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do EasyTerritory é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0711d-137">For single sign-on to work, Azure AD needs to know what the counterpart user in EasyTerritory is to a user in Azure AD.</span></span> <span data-ttu-id="0711d-138">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="0711d-138">In other words, a link relationship between an Azure AD user and the related user in EasyTerritory needs to be established.</span></span>

<span data-ttu-id="0711d-139">No EasyTerritory, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="0711d-139">In EasyTerritory, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0711d-140">Para configurar e testar o logon único do Azure AD com o EasyTerritory, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="0711d-140">To configure and test Azure AD single sign-on with EasyTerritory, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0711d-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="0711d-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0711d-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="0711d-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0711d-143">**[Criar de um usuário de teste do EasyTerritory](#create-a-easyterritory-test-user)** – para ter um equivalente de Brenda Fernandes no EasyTerritory vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0711d-143">**[Create a EasyTerritory test user](#create-a-easyterritory-test-user)** - to have a counterpart of Britta Simon in EasyTerritory that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0711d-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0711d-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0711d-145">**[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="0711d-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="0711d-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0711d-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="0711d-147">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="0711d-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your EasyTerritory application.</span></span>

<span data-ttu-id="0711d-148">**Para configurar o logon único do Azure AD com o EasyTerritory, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="0711d-148">**To configure Azure AD single sign-on with EasyTerritory, perform the following steps:**</span></span>

1. <span data-ttu-id="0711d-149">No Portal do Azure, na página de integração de aplicativos do **EasyTerritory**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="0711d-149">In the Azure portal, on the **EasyTerritory** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="0711d-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="0711d-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_samlbase.png)

3. <span data-ttu-id="0711d-153">Na seção **Domínio e URLs do EasyTerritory**, realize as seguintes etapas se desejar configurar o aplicativo no modo iniciado pelo IdP:</span><span class="sxs-lookup"><span data-stu-id="0711d-153">On the **EasyTerritory Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span></span>

    ![Informações de logon único de Domínio e URLs do EasyTerritory](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_url.png)

    <span data-ttu-id="0711d-155">a.</span><span class="sxs-lookup"><span data-stu-id="0711d-155">a.</span></span> <span data-ttu-id="0711d-156">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://apps.easyterritory.com/<tenant id>/dev/`</span><span class="sxs-lookup"><span data-stu-id="0711d-156">In the **Identifier** textbox, type a URL using the following pattern: `https://apps.easyterritory.com/<tenant id>/dev/`</span></span>

    <span data-ttu-id="0711d-157">b.</span><span class="sxs-lookup"><span data-stu-id="0711d-157">b.</span></span> <span data-ttu-id="0711d-158">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://apps.easyterritory.com/<tenant id>/dev/authservices/acs`</span><span class="sxs-lookup"><span data-stu-id="0711d-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://apps.easyterritory.com/<tenant id>/dev/authservices/acs`</span></span>

4. <span data-ttu-id="0711d-159">Marque **Mostrar configurações avançadas de URL** e realize a seguinte etapa se quiser configurar o aplicativo no modo iniciado pelo **SP**:</span><span class="sxs-lookup"><span data-stu-id="0711d-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Informações de logon único de Domínio e URLs do EasyTerritory](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_url1.png)

    <span data-ttu-id="0711d-161">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<company name>.easyterritory.com/`</span><span class="sxs-lookup"><span data-stu-id="0711d-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.easyterritory.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="0711d-162">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="0711d-162">These values are not real.</span></span> <span data-ttu-id="0711d-163">Atualize esses valores com o Identificador real, a URL de Resposta e a URL de Entrada.</span><span class="sxs-lookup"><span data-stu-id="0711d-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="0711d-164">Contate a [equipe de suporte ao cliente do EasyTerritory](mailto:sales@easyterritory.com) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="0711d-164">Contact [EasyTerritory Client support team](mailto:sales@easyterritory.com) to get these values.</span></span> 

5. <span data-ttu-id="0711d-165">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="0711d-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_certificate.png) 

6. <span data-ttu-id="0711d-167">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="0711d-167">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-easyterritory-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="0711d-169">Para configurar o logon único no lado do **EasyTerritory**, é necessário enviar o **XML de metadados** baixado para a [equipe de suporte do EasyTerritory](mailto:sales@easyterritory.com).</span><span class="sxs-lookup"><span data-stu-id="0711d-169">To configure single sign-on on **EasyTerritory** side, you need to send the downloaded **Metadata XML** to [EasyTerritory support team](mailto:sales@easyterritory.com).</span></span> <span data-ttu-id="0711d-170">Eles definem essa configuração para ter a conexão de SSO de SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="0711d-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="0711d-171">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="0711d-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0711d-172">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="0711d-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0711d-173">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0711d-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0711d-174">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0711d-174">Create an Azure AD test user</span></span>

<span data-ttu-id="0711d-175">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="0711d-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="0711d-177">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="0711d-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0711d-178">No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0711d-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-easyterritory-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="0711d-180">Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="0711d-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-easyterritory-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="0711d-182">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.</span><span class="sxs-lookup"><span data-stu-id="0711d-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![O botão Adicionar](./media/active-directory-saas-easyterritory-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="0711d-184">Na caixa de diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="0711d-184">In the **User** dialog box, perform the following steps:</span></span>

    ![A caixa de diálogo Usuário](./media/active-directory-saas-easyterritory-tutorial/create_aaduser_04.png)

    <span data-ttu-id="0711d-186">a.</span><span class="sxs-lookup"><span data-stu-id="0711d-186">a.</span></span> <span data-ttu-id="0711d-187">Na caixa **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="0711d-187">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0711d-188">b.</span><span class="sxs-lookup"><span data-stu-id="0711d-188">b.</span></span> <span data-ttu-id="0711d-189">Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="0711d-189">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="0711d-190">c.</span><span class="sxs-lookup"><span data-stu-id="0711d-190">c.</span></span> <span data-ttu-id="0711d-191">Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.</span><span class="sxs-lookup"><span data-stu-id="0711d-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="0711d-192">d.</span><span class="sxs-lookup"><span data-stu-id="0711d-192">d.</span></span> <span data-ttu-id="0711d-193">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="0711d-193">Click **Create**.</span></span>
 
### <a name="create-a-easyterritory-test-user"></a><span data-ttu-id="0711d-194">Criar um usuário de teste do EasyTerritory</span><span class="sxs-lookup"><span data-stu-id="0711d-194">Create a EasyTerritory test user</span></span>

<span data-ttu-id="0711d-195">Nesta seção, você criará uma usuária chamada Britta Simon no EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="0711d-195">In this section, you create a user called Britta Simon in EasyTerritory.</span></span> <span data-ttu-id="0711d-196">Trabalhe com a [equipe de suporte do EasyTerritory](mailto:sales@easyterritory.com) para adicionar os usuários na plataforma do EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="0711d-196">Please work with [EasyTerritory support team](mailto:sales@easyterritory.com) to add the users in the EasyTerritory platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="0711d-197">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0711d-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="0711d-198">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="0711d-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to EasyTerritory.</span></span>

![Atribuir a função de usuário][200] 

<span data-ttu-id="0711d-200">**Para atribuir Britta Simon ao EasyTerritory, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="0711d-200">**To assign Britta Simon to EasyTerritory, perform the following steps:**</span></span>

1. <span data-ttu-id="0711d-201">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="0711d-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="0711d-203">Na lista de aplicativos, escolha **EasyTerritory**.</span><span class="sxs-lookup"><span data-stu-id="0711d-203">In the applications list, select **EasyTerritory**.</span></span>

    ![O link do EasyTerritory na lista de Aplicativos](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_app.png)  

3. <span data-ttu-id="0711d-205">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="0711d-205">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202]

4. <span data-ttu-id="0711d-207">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="0711d-207">Click **Add** button.</span></span> <span data-ttu-id="0711d-208">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0711d-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="0711d-210">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="0711d-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0711d-211">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0711d-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0711d-212">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0711d-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="0711d-213">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="0711d-213">Test single sign-on</span></span>

<span data-ttu-id="0711d-214">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="0711d-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0711d-215">Ao clicar no bloco EasyTerritory no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="0711d-215">When you click the EasyTerritory tile in the Access Panel, you should get automatically signed-on to your EasyTerritory application.</span></span>
<span data-ttu-id="0711d-216">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0711d-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0711d-217">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="0711d-217">Additional resources</span></span>

* [<span data-ttu-id="0711d-218">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="0711d-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0711d-219">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0711d-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)




<!--Image references-->

[1]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_203.png

