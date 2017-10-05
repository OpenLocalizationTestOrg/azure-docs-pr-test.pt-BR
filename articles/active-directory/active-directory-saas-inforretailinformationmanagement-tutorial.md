---
title: "Tutorial: Integração do Azure Active Directory com informações de varejo – gerenciamento de informações | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Infor Retail – Information Management."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 5ff49168-ef81-4169-8e5e-dc86e24dd5e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: 1ab8b7e98324ba4f4ae95775f89df0461058fe4b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-infor-retail--information-management"></a><span data-ttu-id="fcdd5-103">Tutorial: Integração do Azure Active Directory com informações de varejo – gerenciamento de informações</span><span class="sxs-lookup"><span data-stu-id="fcdd5-103">Tutorial: Azure Active Directory integration with Infor Retail – Information Management</span></span>

<span data-ttu-id="fcdd5-104">Neste tutorial, você aprenderá a integrar o Infor Retail – Information Management ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="fcdd5-104">In this tutorial, you learn how to integrate Infor Retail – Information Management with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fcdd5-105">Integrar informações varejo – gerenciamento de informações com o Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="fcdd5-105">Integrating Infor Retail – Information Management with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fcdd5-106">No Azure AD, é possível controlar quem tem acesso ao Infor Retail – Information Management.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-106">You can control in Azure AD who has access to Infor Retail – Information Management.</span></span>
- <span data-ttu-id="fcdd5-107">Você pode permitir que os usuários façam logon automaticamente no Infor Retail – Information Management (Logon Único) com as respectivas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-107">You can enable your users to automatically get signed-on to Infor Retail – Information Management (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="fcdd5-108">Você pode gerenciar suas contas em um único local central – o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="fcdd5-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fcdd5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fcdd5-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fcdd5-110">Prerequisites</span></span>

<span data-ttu-id="fcdd5-111">Para configurar a integração do AD do Azure com informações de varejo – gerenciamento de informações, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="fcdd5-111">To configure Azure AD integration with Infor Retail – Information Management, you need the following items:</span></span>

- <span data-ttu-id="fcdd5-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="fcdd5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fcdd5-113">Um varejo informações – gerenciamento de informações de logon único assinatura habilitada</span><span class="sxs-lookup"><span data-stu-id="fcdd5-113">An Infor Retail – Information Management single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fcdd5-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fcdd5-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="fcdd5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fcdd5-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fcdd5-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fcdd5-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fcdd5-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="fcdd5-118">Scenario description</span></span>
<span data-ttu-id="fcdd5-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fcdd5-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="fcdd5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fcdd5-121">Adição do Infor Retail – Information Management da galeria</span><span class="sxs-lookup"><span data-stu-id="fcdd5-121">Adding Infor Retail – Information Management from the gallery</span></span>
2. <span data-ttu-id="fcdd5-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="fcdd5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-infor-retail--information-management-from-the-gallery"></a><span data-ttu-id="fcdd5-123">Adição do Infor Retail – Information Management da galeria</span><span class="sxs-lookup"><span data-stu-id="fcdd5-123">Adding Infor Retail – Information Management from the gallery</span></span>
<span data-ttu-id="fcdd5-124">Para configurar a integração de varejo de informações – gerenciamento de informações no AD do Azure, você precisa adicionar informações de varejo – gerenciamento de informações da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-124">To configure the integration of Infor Retail – Information Management into Azure AD, you need to add Infor Retail – Information Management from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fcdd5-125">**Para adicionar informações de varejo – gerenciamento de informações da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="fcdd5-125">**To add Infor Retail – Information Management from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fcdd5-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="fcdd5-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fcdd5-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="fcdd5-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="fcdd5-133">Na caixa de pesquisa, digite **Infor Retail – Information Management**, selecione **Infor Retail – Information Management** no painel de resultados e, em seguida, cique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-133">In the search box, type **Infor Retail – Information Management**, select **Infor Retail – Information Management** from result panel then click **Add** button to add the application.</span></span>

    ![Infor Retail – Information Management na lista de resultados](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="fcdd5-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="fcdd5-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="fcdd5-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Infor Retail – Information Management, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-136">In this section, you configure and test Azure AD single sign-on with Infor Retail – Information Management based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fcdd5-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Infor Retail – Information Management é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Infor Retail – Information Management is to a user in Azure AD.</span></span> <span data-ttu-id="fcdd5-138">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Infor Retail – Information Management.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-138">In other words, a link relationship between an Azure AD user and the related user in Infor Retail – Information Management needs to be established.</span></span>

<span data-ttu-id="fcdd5-139">No Infor Retail – Information Management, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-139">In Infor Retail – Information Management, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="fcdd5-140">Para configurar e testar o logon único do Azure AD com o Infor Retail – Information Management, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="fcdd5-140">To configure and test Azure AD single sign-on with Infor Retail – Information Management, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fcdd5-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fcdd5-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fcdd5-143">**[Criar um usuário de teste do Infor Retail – Information Management](#create-an-infor-retail--information-management-test-user)** – para ter um equivalente de Brenda Fernandes no Infor Retail – Information Management vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-143">**[Create an Infor Retail – Information Management test user](#create-an-infor-retail--information-management-test-user)** - to have a counterpart of Britta Simon in Infor Retail – Information Management that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="fcdd5-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fcdd5-145">**[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="fcdd5-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="fcdd5-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="fcdd5-147">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo Infor Retail – Information Management.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Infor Retail – Information Management application.</span></span>

<span data-ttu-id="fcdd5-148">**Para configurar o logon único do Azure AD com informações de varejo – gerenciamento de informações, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="fcdd5-148">**To configure Azure AD single sign-on with Infor Retail – Information Management, perform the following steps:**</span></span>

1. <span data-ttu-id="fcdd5-149">No Portal do Azure, na página de integração de aplicativos do **Infor Retail – Information Management**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-149">In the Azure portal, on the **Infor Retail – Information Management** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="fcdd5-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_samlbase.png)

3. <span data-ttu-id="fcdd5-153">Na seção **Domínio e URLs do Infor Retail – Information Management**, realize as seguintes etapas se desejar configurar o aplicativo no modo iniciado pelo IdP:</span><span class="sxs-lookup"><span data-stu-id="fcdd5-153">On the **Infor Retail – Information Management Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span></span>

    ![Informações de logon único de Domínio e URLs do Infor Retail – Information Management para IdP](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_url.png)

    <span data-ttu-id="fcdd5-155">a.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-155">a.</span></span> <span data-ttu-id="fcdd5-156">Na caixa de texto **Identificador**, digite uma URL usando os seguintes padrões:</span><span class="sxs-lookup"><span data-stu-id="fcdd5-156">In the **Identifier** textbox, type a URL using the following patterns:</span></span> 
    |   |
    | -- |
    | `https://<company name>.mingle.infor.com` |
    | `http://<company name>.mingledev.infor.com` |

    <span data-ttu-id="fcdd5-157">b.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-157">b.</span></span> <span data-ttu-id="fcdd5-158">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<company name>.mingle.infor.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="fcdd5-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.mingle.infor.com/sp/ACS.saml2`</span></span>

4. <span data-ttu-id="fcdd5-159">Marque **Mostrar configurações avançadas de URL** e realize a seguinte etapa se quiser configurar o aplicativo no modo iniciado pelo **SP**:</span><span class="sxs-lookup"><span data-stu-id="fcdd5-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Informações de logon único de Domínio e URLs do Infor Retail – Information Management para SP](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_url1.png)

    <span data-ttu-id="fcdd5-161">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<company name>.mingle.infor.com/<company code>`</span><span class="sxs-lookup"><span data-stu-id="fcdd5-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.mingle.infor.com/<company code>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="fcdd5-162">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-162">These values are not real.</span></span> <span data-ttu-id="fcdd5-163">Atualize esses valores com o Identificador real, a URL de Resposta e a URL de Entrada.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="fcdd5-164">Contate a [equipe de suporte ao cliente do Infor Retail – Information Management](mailto:innovate@infor.com) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-164">Contact [Infor Retail – Information Management Client support team](mailto:innovate@infor.com) to get these values.</span></span> 

5. <span data-ttu-id="fcdd5-165">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_certificate.png) 

6. <span data-ttu-id="fcdd5-167">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="fcdd5-167">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="fcdd5-169">Para configurar o logon único no lado do **Infor Retail – Information Management**, você precisa enviar o **XML de Metadados** baixado para [a equipe de suporte do Infor Retail – Information Management](mailto:innovate@infor.com).</span><span class="sxs-lookup"><span data-stu-id="fcdd5-169">To configure single sign-on on **Infor Retail – Information Management** side, you need to send the downloaded **Metadata XML** to [Infor Retail – Information Management support team](mailto:innovate@infor.com).</span></span> <span data-ttu-id="fcdd5-170">Eles definem essa configuração para ter a conexão de SSO de SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="fcdd5-171">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="fcdd5-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="fcdd5-172">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="fcdd5-173">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fcdd5-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="fcdd5-174">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="fcdd5-174">Create an Azure AD test user</span></span>

<span data-ttu-id="fcdd5-175">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="fcdd5-177">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="fcdd5-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fcdd5-178">No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-inforretailinformationmanagement-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="fcdd5-180">Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-inforretailinformationmanagement-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="fcdd5-182">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![O botão Adicionar](./media/active-directory-saas-inforretailinformationmanagement-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="fcdd5-184">Na caixa de diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="fcdd5-184">In the **User** dialog box, perform the following steps:</span></span>

    ![A caixa de diálogo Usuário](./media/active-directory-saas-inforretailinformationmanagement-tutorial/create_aaduser_04.png)

    <span data-ttu-id="fcdd5-186">a.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-186">a.</span></span> <span data-ttu-id="fcdd5-187">Na caixa **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-187">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fcdd5-188">b.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-188">b.</span></span> <span data-ttu-id="fcdd5-189">Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-189">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="fcdd5-190">c.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-190">c.</span></span> <span data-ttu-id="fcdd5-191">Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="fcdd5-192">d.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-192">d.</span></span> <span data-ttu-id="fcdd5-193">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-193">Click **Create**.</span></span>
 
### <a name="create-an-infor-retail--information-management-test-user"></a><span data-ttu-id="fcdd5-194">Criar um usuário de teste do Infor Retail – Information Management</span><span class="sxs-lookup"><span data-stu-id="fcdd5-194">Create an Infor Retail – Information Management test user</span></span>

<span data-ttu-id="fcdd5-195">Nesta seção, você deve criar um usuário chamado Britta Simon no varejo de informações – gerenciamento de informações.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-195">In this section, you create a user called Britta Simon in Infor Retail – Information Management.</span></span> <span data-ttu-id="fcdd5-196">Trabalhe com [informações varejo – a equipe de suporte de gerenciamento de informações](mailto:innovate@infor.com) para adicionar os usuários no varejo de informações – plataforma de gerenciamento de informações.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-196">Please work with [Infor Retail – Information Management support team](mailto:innovate@infor.com) to add the users in the Infor Retail – Information Management platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="fcdd5-197">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="fcdd5-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="fcdd5-198">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Infor Retail – Information Management.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Infor Retail – Information Management.</span></span>

![Atribuir a função de usuário][200] 

<span data-ttu-id="fcdd5-200">**Para atribuir Britta Simon comercial de informações – gerenciamento de informações, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="fcdd5-200">**To assign Britta Simon to Infor Retail – Information Management, perform the following steps:**</span></span>

1. <span data-ttu-id="fcdd5-201">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="fcdd5-203">Na lista de aplicativos, selecione **informações varejo – gerenciamento de informação**.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-203">In the applications list, select **Infor Retail – Information Management**.</span></span>

    ![O link do Infor Retail – Information Management na lista de Aplicativos](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_app.png)  

3. <span data-ttu-id="fcdd5-205">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-205">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202]

4. <span data-ttu-id="fcdd5-207">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-207">Click **Add** button.</span></span> <span data-ttu-id="fcdd5-208">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="fcdd5-210">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="fcdd5-211">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fcdd5-212">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="fcdd5-213">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="fcdd5-213">Test single sign-on</span></span>

<span data-ttu-id="fcdd5-214">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="fcdd5-215">Quando você clica em varejo informações – bloco de gerenciamento de informações no painel de acesso, você deve obter logon automaticamente no seu comercial de informações – aplicativo de gerenciamento de informações.</span><span class="sxs-lookup"><span data-stu-id="fcdd5-215">When you click the Infor Retail – Information Management tile in the Access Panel, you should get automatically signed-on to your Infor Retail – Information Management application.</span></span>
<span data-ttu-id="fcdd5-216">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fcdd5-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="fcdd5-217">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="fcdd5-217">Additional resources</span></span>

* [<span data-ttu-id="fcdd5-218">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="fcdd5-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fcdd5-219">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fcdd5-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_203.png

