---
title: "Tutorial: integração do Azure Active Directory com o Greenhouse | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Greenhouse."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 78ec1766-4f79-4f16-9a66-d5584c4b6151
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: d3aba4aab8ded8749db2bf8197f57a6763008c60
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-greenhouse"></a><span data-ttu-id="b9106-103">Tutorial: integração do Active Directory do Azure ao Greenhouse</span><span class="sxs-lookup"><span data-stu-id="b9106-103">Tutorial: Azure Active Directory integration with Greenhouse</span></span>

<span data-ttu-id="b9106-104">Neste tutorial, você aprende a integrar o Greenhouse ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="b9106-104">In this tutorial, you learn how to integrate Greenhouse with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b9106-105">A integração do Greenhouse ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="b9106-105">Integrating Greenhouse with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b9106-106">No Azure AD, é possível controlar quem tem acesso ao Greenhouse.</span><span class="sxs-lookup"><span data-stu-id="b9106-106">You can control in Azure AD who has access to Greenhouse.</span></span>
- <span data-ttu-id="b9106-107">É possível permitir que os usuários sejam conectados automaticamente no Greenhouse (Logon Único) com suas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9106-107">You can enable your users to automatically get signed-on to Greenhouse (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b9106-108">Você pode gerenciar suas contas em um único local central – o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9106-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="b9106-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b9106-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9106-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b9106-110">Prerequisites</span></span>

<span data-ttu-id="b9106-111">Para configurar a integração do Azure AD ao Greenhouse, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="b9106-111">To configure Azure AD integration with Greenhouse, you need the following items:</span></span>

- <span data-ttu-id="b9106-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b9106-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b9106-113">Uma assinatura do Greenhouse habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="b9106-113">A Greenhouse single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b9106-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="b9106-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b9106-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="b9106-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b9106-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="b9106-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b9106-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b9106-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b9106-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="b9106-118">Scenario description</span></span>
<span data-ttu-id="b9106-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="b9106-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b9106-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="b9106-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b9106-121">Adicionando o Greenhouse por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="b9106-121">Adding Greenhouse from the gallery</span></span>
2. <span data-ttu-id="b9106-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b9106-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-greenhouse-from-the-gallery"></a><span data-ttu-id="b9106-123">Adicionando o Greenhouse por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="b9106-123">Adding Greenhouse from the gallery</span></span>
<span data-ttu-id="b9106-124">Para configurar a integração do Greenhouse ao Azure AD, é necessário adicionar o Greenhouse à lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="b9106-124">To configure the integration of Greenhouse into Azure AD, you need to add Greenhouse from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b9106-125">**Para adicionar o Greenhouse por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="b9106-125">**To add Greenhouse from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b9106-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b9106-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="b9106-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="b9106-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b9106-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="b9106-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="b9106-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b9106-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="b9106-133">Na caixa de pesquisa, digite **Greenhouse**, selecione **Greenhouse** no painel de resultados e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b9106-133">In the search box, type **Greenhouse**, select **Greenhouse** from result panel then click **Add** button to add the application.</span></span>

    ![Greenhouse na lista de resultados](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b9106-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9106-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b9106-136">Nesta seção, você configura e testa o logon único do Azure AD com o Greenhouse, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="b9106-136">In this section, you configure and test Azure AD single sign-on with Greenhouse based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b9106-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Greenhouse é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9106-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Greenhouse is to a user in Azure AD.</span></span> <span data-ttu-id="b9106-138">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Greenhouse.</span><span class="sxs-lookup"><span data-stu-id="b9106-138">In other words, a link relationship between an Azure AD user and the related user in Greenhouse needs to be established.</span></span>

<span data-ttu-id="b9106-139">No Greenhouse, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="b9106-139">In Greenhouse, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b9106-140">Para configurar e testar o logon único do Azure AD com o Greenhouse, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="b9106-140">To configure and test Azure AD single sign-on with Greenhouse, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b9106-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="b9106-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b9106-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="b9106-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b9106-143">**[Criar um usuário de teste do Greenhouse](#create-a-greenhouse-test-user)** – para ter um equivalente de Brenda Fernandes no Greenhouse que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9106-143">**[Create a Greenhouse test user](#create-a-greenhouse-test-user)** - to have a counterpart of Britta Simon in Greenhouse that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b9106-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9106-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b9106-145">**[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="b9106-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b9106-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9106-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b9106-147">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Greenhouse.</span><span class="sxs-lookup"><span data-stu-id="b9106-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Greenhouse application.</span></span>

<span data-ttu-id="b9106-148">**Para configurar o logon único do Azure AD com o Greenhouse, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="b9106-148">**To configure Azure AD single sign-on with Greenhouse, perform the following steps:**</span></span>

1. <span data-ttu-id="b9106-149">No portal do Azure, na página de integração do aplicativo **Greenhouse**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="b9106-149">In the Azure portal, on the **Greenhouse** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="b9106-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="b9106-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_samlbase.png)

3. <span data-ttu-id="b9106-153">Na seção **Domínio e URLs do Greenhouse**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="b9106-153">On the **Greenhouse Domain and URLs** section, perform the following steps:</span></span>

    ![Informações de logon único em Domínio e URLs do Greenhouse](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_url.png)

    <span data-ttu-id="b9106-155">a.</span><span class="sxs-lookup"><span data-stu-id="b9106-155">a.</span></span> <span data-ttu-id="b9106-156">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<companyname>.greenhouse.io`</span><span class="sxs-lookup"><span data-stu-id="b9106-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.greenhouse.io`</span></span>

    <span data-ttu-id="b9106-157">b.</span><span class="sxs-lookup"><span data-stu-id="b9106-157">b.</span></span> <span data-ttu-id="b9106-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<companyname>.greenhouse.io`</span><span class="sxs-lookup"><span data-stu-id="b9106-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.greenhouse.io`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b9106-159">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="b9106-159">These values are not real.</span></span> <span data-ttu-id="b9106-160">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="b9106-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b9106-161">Contate a [equipe de suporte ao Cliente do Greenhouse](https://www.greenhouse.io/contact) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="b9106-161">Contact [Greenhouse Client support team](https://www.greenhouse.io/contact) to get these values.</span></span> 
 


4. <span data-ttu-id="b9106-162">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="b9106-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_certificate.png) 

5. <span data-ttu-id="b9106-164">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="b9106-164">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-greenhouse-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b9106-166">Para configurar o logon único no lado do **Greenhouse**, é necessário enviar o **XML de Metadados** baixado para a [equipe de suporte do Greenhouse](http://www.greenhouse.io/contact).</span><span class="sxs-lookup"><span data-stu-id="b9106-166">To configure single sign-on on **Greenhouse** side, you need to send the downloaded **Metadata XML** to [Greenhouse support team](http://www.greenhouse.io/contact).</span></span>

> [!TIP]
> <span data-ttu-id="b9106-167">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="b9106-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b9106-168">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="b9106-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b9106-169">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b9106-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b9106-170">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9106-170">Create an Azure AD test user</span></span>

<span data-ttu-id="b9106-171">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="b9106-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="b9106-173">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="b9106-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b9106-174">No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b9106-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="b9106-176">Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="b9106-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="b9106-178">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.</span><span class="sxs-lookup"><span data-stu-id="b9106-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![O botão Adicionar](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="b9106-180">Na caixa de diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="b9106-180">In the **User** dialog box, perform the following steps:</span></span>

    ![A caixa de diálogo Usuário](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_04.png)

    <span data-ttu-id="b9106-182">a.</span><span class="sxs-lookup"><span data-stu-id="b9106-182">a.</span></span> <span data-ttu-id="b9106-183">Na caixa **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="b9106-183">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b9106-184">b.</span><span class="sxs-lookup"><span data-stu-id="b9106-184">b.</span></span> <span data-ttu-id="b9106-185">Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="b9106-185">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="b9106-186">c.</span><span class="sxs-lookup"><span data-stu-id="b9106-186">c.</span></span> <span data-ttu-id="b9106-187">Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.</span><span class="sxs-lookup"><span data-stu-id="b9106-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="b9106-188">d.</span><span class="sxs-lookup"><span data-stu-id="b9106-188">d.</span></span> <span data-ttu-id="b9106-189">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b9106-189">Click **Create**.</span></span>
 
### <a name="create-a-greenhouse-test-user"></a><span data-ttu-id="b9106-190">Criar um usuário de teste do Greenhouse</span><span class="sxs-lookup"><span data-stu-id="b9106-190">Create a Greenhouse test user</span></span>

<span data-ttu-id="b9106-191">Para permitir que os usuários do Azure AD façam logon no Greenhouse, eles devem ser provisionados no Greenhouse.</span><span class="sxs-lookup"><span data-stu-id="b9106-191">In order to enable Azure AD users to log into Greenhouse, they must be provisioned into Greenhouse.</span></span> <span data-ttu-id="b9106-192">No caso do Greenhouse, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="b9106-192">In the case of Greenhouse, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="b9106-193">É possível usar qualquer outra ferramenta de criação da conta de usuário do Greenhouse ou as APIs fornecidas pelo Greenhouse para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="b9106-193">You can use any other Greenhouse user account creation tools or APIs provided by Greenhouse to provision AAD user accounts.</span></span> 

<span data-ttu-id="b9106-194">**Para provisionar contas de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="b9106-194">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="b9106-195">Faça logon em seu site de empresa do **Greenhouse** como administrador.</span><span class="sxs-lookup"><span data-stu-id="b9106-195">Log in to your **Greenhouse** company site as an administrator.</span></span>

2. <span data-ttu-id="b9106-196">No menu na parte superior, clique em **Configurar**, em seguida, clique em **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="b9106-196">In the menu on the top, click **Configure**, and then click **Users**.</span></span>
   
   <span data-ttu-id="b9106-197">![Usuários](./media/active-directory-saas-greenhouse-tutorial/ic790791.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="b9106-197">![Users](./media/active-directory-saas-greenhouse-tutorial/ic790791.png "Users")</span></span>

3. <span data-ttu-id="b9106-198">Clique em **Novos Usuários**.</span><span class="sxs-lookup"><span data-stu-id="b9106-198">Click **New Users**.</span></span>
   
   <span data-ttu-id="b9106-199">![Novo Usuário](./media/active-directory-saas-greenhouse-tutorial/ic790792.png "Novo Usuário")</span><span class="sxs-lookup"><span data-stu-id="b9106-199">![New User](./media/active-directory-saas-greenhouse-tutorial/ic790792.png "New User")</span></span>

4. <span data-ttu-id="b9106-200">Na seção **Adicionar Novo Usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="b9106-200">In the **Add New User** section, perform the following steps:</span></span>
   
   <span data-ttu-id="b9106-201">![Adicionar Novo Usuário](./media/active-directory-saas-greenhouse-tutorial/ic790793.png "Adicionar Novo Usuário")</span><span class="sxs-lookup"><span data-stu-id="b9106-201">![Add New User](./media/active-directory-saas-greenhouse-tutorial/ic790793.png "Add New User")</span></span>

   <span data-ttu-id="b9106-202">a.</span><span class="sxs-lookup"><span data-stu-id="b9106-202">a.</span></span> <span data-ttu-id="b9106-203">Na caixa de texto **Inserir email de usuários** , digite o endereço de email de uma conta válida do Active Directory do Azure que você deseja provisionar.</span><span class="sxs-lookup"><span data-stu-id="b9106-203">In the **Enter user emails** textbox, type the email address of a valid Azure Active Directory account you want to provision.</span></span>

   <span data-ttu-id="b9106-204">b.</span><span class="sxs-lookup"><span data-stu-id="b9106-204">b.</span></span> <span data-ttu-id="b9106-205">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="b9106-205">Click **Save**.</span></span>    
   
      >[!NOTE]
      ><span data-ttu-id="b9106-206">O titular da conta do Active Directory do Azure recebe um email com um link para confirmar a conta antes que ela se torne ativa.</span><span class="sxs-lookup"><span data-stu-id="b9106-206">The Azure Active Directory account holders will receive an email including a link to confirm the account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="b9106-207">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9106-207">Assign the Azure AD test user</span></span>

<span data-ttu-id="b9106-208">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Greenhouse.</span><span class="sxs-lookup"><span data-stu-id="b9106-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Greenhouse.</span></span>

![Atribuir a função de usuário][200] 

<span data-ttu-id="b9106-210">**Para atribuir Brenda Fernandes ao Greenhouse, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="b9106-210">**To assign Britta Simon to Greenhouse, perform the following steps:**</span></span>

1. <span data-ttu-id="b9106-211">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="b9106-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="b9106-213">Na lista de aplicativos, selecione **Greenhouse**.</span><span class="sxs-lookup"><span data-stu-id="b9106-213">In the applications list, select **Greenhouse**.</span></span>

    ![O link do Greenhouse na lista de Aplicativos](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_app.png)  

3. <span data-ttu-id="b9106-215">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="b9106-215">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202]

4. <span data-ttu-id="b9106-217">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="b9106-217">Click **Add** button.</span></span> <span data-ttu-id="b9106-218">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b9106-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="b9106-220">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="b9106-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b9106-221">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b9106-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b9106-222">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b9106-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b9106-223">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="b9106-223">Test single sign-on</span></span>

<span data-ttu-id="b9106-224">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="b9106-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b9106-225">Quando você clicar no bloco do Greenhouse no Painel de Acesso, deverá ser conectado automaticamente ao aplicativo Greenhouse.</span><span class="sxs-lookup"><span data-stu-id="b9106-225">When you click the Greenhouse tile in the Access Panel, you should get automatically signed-on to your Greenhouse application.</span></span>
<span data-ttu-id="b9106-226">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b9106-226">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b9106-227">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="b9106-227">Additional resources</span></span>

* [<span data-ttu-id="b9106-228">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="b9106-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b9106-229">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b9106-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_203.png

