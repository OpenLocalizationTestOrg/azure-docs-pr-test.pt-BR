---
title: "Tutorial: Integração do Azure Active Directory com o AppBlade | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Active Directory do Azure e o AppBlade."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3360d7aa-6518-4f99-88bd-b7f7258183e8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 7820a70b34b6d25ba81b17c472159d08904335d1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-appblade"></a><span data-ttu-id="809ee-103">Tutorial: Integração do Active Directory do Azure com o AppBlade</span><span class="sxs-lookup"><span data-stu-id="809ee-103">Tutorial: Azure Active Directory integration with AppBlade</span></span>

<span data-ttu-id="809ee-104">Neste tutorial, você aprende a integrar o AppBlade ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="809ee-104">In this tutorial, you learn how to integrate AppBlade with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="809ee-105">A integração do AppBlade ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="809ee-105">Integrating AppBlade with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="809ee-106">É possível controlar no Azure AD quem tem acesso ao AppBlade</span><span class="sxs-lookup"><span data-stu-id="809ee-106">You can control in Azure AD who has access to AppBlade</span></span>
- <span data-ttu-id="809ee-107">É possível permitir que seus usuários façam logon automaticamente no AppBlade (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="809ee-107">You can enable your users to automatically get signed-on to AppBlade (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="809ee-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="809ee-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="809ee-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="809ee-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="809ee-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="809ee-110">Prerequisites</span></span>

<span data-ttu-id="809ee-111">Para configurar a integração do Azure AD com o AppBlade, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="809ee-111">To configure Azure AD integration with AppBlade, you need the following items:</span></span>

- <span data-ttu-id="809ee-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="809ee-112">An Azure AD subscription</span></span>
- <span data-ttu-id="809ee-113">Uma assinatura habilitada para logon único do AppBlade</span><span class="sxs-lookup"><span data-stu-id="809ee-113">An AppBlade single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="809ee-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="809ee-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="809ee-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="809ee-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="809ee-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="809ee-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="809ee-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="809ee-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="809ee-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="809ee-118">Scenario description</span></span>
<span data-ttu-id="809ee-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="809ee-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="809ee-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="809ee-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="809ee-121">Adição do AppBlade da galeria</span><span class="sxs-lookup"><span data-stu-id="809ee-121">Adding AppBlade from the gallery</span></span>
2. <span data-ttu-id="809ee-122">configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="809ee-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-appblade-from-the-gallery"></a><span data-ttu-id="809ee-123">Adição do AppBlade da galeria</span><span class="sxs-lookup"><span data-stu-id="809ee-123">Adding AppBlade from the gallery</span></span>
<span data-ttu-id="809ee-124">Para configurar a integração do AppBlade com o Azure AD, você precisa adicionar o AppBlade à sua lista de aplicativos SaaS gerenciados a partir da galeria.</span><span class="sxs-lookup"><span data-stu-id="809ee-124">To configure the integration of AppBlade into Azure AD, you need to add AppBlade from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="809ee-125">**Para adicionar o AppBlade a partir da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="809ee-125">**To add AppBlade from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="809ee-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="809ee-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="809ee-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="809ee-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="809ee-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="809ee-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="809ee-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="809ee-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="809ee-133">Na caixa de pesquisa, digite **AppBlade**.</span><span class="sxs-lookup"><span data-stu-id="809ee-133">In the search box, type **AppBlade**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_search.png)

5. <span data-ttu-id="809ee-135">No painel de resultados, selecione **AppBlade** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="809ee-135">In the results panel, select **AppBlade**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="809ee-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="809ee-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="809ee-138">Nesta seção, você configura e testa o logon único do Azure AD com o AppBlade, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="809ee-138">In this section, you configure and test Azure AD single sign-on with AppBlade based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="809ee-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do AppBlade é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="809ee-139">For single sign-on to work, Azure AD needs to know what the counterpart user in AppBlade is to a user in Azure AD.</span></span> <span data-ttu-id="809ee-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no AppBlade.</span><span class="sxs-lookup"><span data-stu-id="809ee-140">In other words, a link relationship between an Azure AD user and the related user in AppBlade needs to be established.</span></span>

<span data-ttu-id="809ee-141">No AppBlade, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="809ee-141">In AppBlade, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="809ee-142">Para configurar e testar o logon único do Azure AD com o AppBlade, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="809ee-142">To configure and test Azure AD single sign-on with AppBlade, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="809ee-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="809ee-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="809ee-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="809ee-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="809ee-145">**[Criando um usuário de teste do AppBlade](#creating-an-appblade-test-user)** – para ter um equivalente de Brenda Fernandes no AppBlade que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="809ee-145">**[Creating an AppBlade test user](#creating-an-appblade-test-user)** - to have a counterpart of Britta Simon in AppBlade that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="809ee-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="809ee-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="809ee-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="809ee-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="809ee-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="809ee-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="809ee-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo AppBlade.</span><span class="sxs-lookup"><span data-stu-id="809ee-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AppBlade application.</span></span>

<span data-ttu-id="809ee-150">**Para configurar o logon único do Azure AD com o AppBlade, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="809ee-150">**To configure Azure AD single sign-on with AppBlade, perform the following steps:**</span></span>

1. <span data-ttu-id="809ee-151">No portal do Azure, na página de integração do aplicativo do **AppBlade**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="809ee-151">In the Azure portal, on the **AppBlade** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="809ee-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="809ee-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_samlbase.png)

3. <span data-ttu-id="809ee-155">Na seção **Domínio e URLs do AppBlade**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="809ee-155">On the **AppBlade Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_url.png)

    <span data-ttu-id="809ee-157">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<companyname>.appblade.com/saml/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="809ee-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.appblade.com/saml/<tenantid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="809ee-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="809ee-158">This value is not real.</span></span> <span data-ttu-id="809ee-159">Atualize o valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="809ee-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="809ee-160">Contate a [equipe de suporte ao Cliente do AppBlade](mailto:support@appblade.com) para obter o valor.</span><span class="sxs-lookup"><span data-stu-id="809ee-160">Contact [AppBlade Client support team](mailto:support@appblade.com) to get the value.</span></span> 
 
4. <span data-ttu-id="809ee-161">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="809ee-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_certificate.png) 

5. <span data-ttu-id="809ee-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="809ee-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-appblade-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="809ee-165">Para configurar o logon único no lado do **AppBlade**, é necessário enviar o **XML de Metadados** baixado para a [equipe de suporte do AppBlade](mailto:support@appblade.com).</span><span class="sxs-lookup"><span data-stu-id="809ee-165">To configure single sign-on on **AppBlade** side, you need to send the downloaded **Metadata XML** to [AppBlade support team](mailto:support@appblade.com).</span></span> <span data-ttu-id="809ee-166">Além disso, solicite a eles que configurem a **URL do Emissor de SSO** como `https://appblade.com/saml`.</span><span class="sxs-lookup"><span data-stu-id="809ee-166">Also, please ask them to configure the **SSO Issuer URL** as `https://appblade.com/saml`.</span></span> <span data-ttu-id="809ee-167">Essa configuração é necessária para que o logon único funcione.</span><span class="sxs-lookup"><span data-stu-id="809ee-167">This setting is required for single sign-on to work.</span></span>


> [!TIP]
> <span data-ttu-id="809ee-168">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="809ee-168">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="809ee-169">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="809ee-169">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="809ee-170">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="809ee-170">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="809ee-171">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="809ee-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="809ee-172">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="809ee-172">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="809ee-174">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="809ee-174">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="809ee-175">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="809ee-175">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-appblade-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="809ee-177">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="809ee-177">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-appblade-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="809ee-179">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="809ee-179">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-appblade-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="809ee-181">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="809ee-181">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-appblade-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="809ee-183">a.</span><span class="sxs-lookup"><span data-stu-id="809ee-183">a.</span></span> <span data-ttu-id="809ee-184">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="809ee-184">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="809ee-185">b.</span><span class="sxs-lookup"><span data-stu-id="809ee-185">b.</span></span> <span data-ttu-id="809ee-186">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="809ee-186">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="809ee-187">c.</span><span class="sxs-lookup"><span data-stu-id="809ee-187">c.</span></span> <span data-ttu-id="809ee-188">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="809ee-188">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="809ee-189">d.</span><span class="sxs-lookup"><span data-stu-id="809ee-189">d.</span></span> <span data-ttu-id="809ee-190">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="809ee-190">Click **Create**.</span></span>
 
### <a name="creating-an-appblade-test-user"></a><span data-ttu-id="809ee-191">Criando um usuário de teste do AppBlade</span><span class="sxs-lookup"><span data-stu-id="809ee-191">Creating an AppBlade test user</span></span>

<span data-ttu-id="809ee-192">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no AppBlade.</span><span class="sxs-lookup"><span data-stu-id="809ee-192">The objective of this section is to create a user called Britta Simon in AppBlade.</span></span> <span data-ttu-id="809ee-193">O AppBlade dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="809ee-193">AppBlade supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="809ee-194">**Verifique se o nome de domínio está configurado no AppBlade para o provisionamento de usuário. Depois disso, somente o provisionamento de usuário Just-In-Time funciona.**</span><span class="sxs-lookup"><span data-stu-id="809ee-194">**Make sure that your domain name is configured with AppBlade for user provisioning. After that only the just-in-time user provisioning works.**</span></span>

<span data-ttu-id="809ee-195">Se o usuário tiver um endereço de email que termina com o domínio configurado pelo AppBlade para sua conta, o usuário unirá automaticamente na conta como membro, com o nível de permissão especificado por você, que pode ser “Básico” (um usuário básico que só pode instalar aplicativos), “Membro da Equipe” (um usuário que pode carregar novas versões do aplicativo e gerenciar projetos) ou “Administrador” (privilégios totais de administrador na conta).</span><span class="sxs-lookup"><span data-stu-id="809ee-195">If the user has an email address ending with the domain configured by AppBlade for your account, then the user will automatically join the account as a member with the permission level you specify, which is one of "Basic" (a basic user who can only install applications), "Team Member" (a user who can upload new app versions and manage projects), or "Administrator" (full admin privileges to the account).</span></span> <span data-ttu-id="809ee-196">O normal seria escolher Básico e promover os usuários manualmente por meio de um logon de administrador (o AppBlade precisa configurar antecipadamente um logon de administração baseado em email ou promover um usuário em nome do cliente após o logon).</span><span class="sxs-lookup"><span data-stu-id="809ee-196">Normally one would choose Basic and then promote users manually via an Admin login (AppBlade needs to configure either an email-based admin login in advance or promote a user on behalf of the customer after login).</span></span>

<span data-ttu-id="809ee-197">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="809ee-197">There is no action item for you in this section.</span></span> <span data-ttu-id="809ee-198">Um novo usuário será criado durante uma tentativa de acessar o AppBlade, caso ele ainda não exista.</span><span class="sxs-lookup"><span data-stu-id="809ee-198">A new user is created during an attempt to access AppBlade if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="809ee-199">Se precisar criar um usuário manualmente, será necessário contatar a [equipe de suporte do AppBlade](mailto:support@appblade.com).</span><span class="sxs-lookup"><span data-stu-id="809ee-199">If you need to create a user manually, you need to contact the [AppBlade support team](mailto:support@appblade.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="809ee-200">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="809ee-200">Assigning the Azure AD test user</span></span>

<span data-ttu-id="809ee-201">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao AppBlade.</span><span class="sxs-lookup"><span data-stu-id="809ee-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AppBlade.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="809ee-203">**Para atribuir Brenda Fernandes ao AppBlade, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="809ee-203">**To assign Britta Simon to AppBlade, perform the following steps:**</span></span>

1. <span data-ttu-id="809ee-204">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="809ee-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="809ee-206">Na lista de aplicativos, escolha **AppBlade**.</span><span class="sxs-lookup"><span data-stu-id="809ee-206">In the applications list, select **AppBlade**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_app.png) 

3. <span data-ttu-id="809ee-208">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="809ee-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="809ee-210">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="809ee-210">Click **Add** button.</span></span> <span data-ttu-id="809ee-211">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="809ee-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="809ee-213">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="809ee-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="809ee-214">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="809ee-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="809ee-215">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="809ee-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="809ee-216">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="809ee-216">Testing single sign-on</span></span>

<span data-ttu-id="809ee-217">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="809ee-217">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="809ee-218">Ao clicar no bloco do AppBlade no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo do AppBlade.</span><span class="sxs-lookup"><span data-stu-id="809ee-218">When you click the AppBlade tile in the Access Panel, you should get automatically signed-on to your AppBlade application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="809ee-219">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="809ee-219">Additional resources</span></span>

* [<span data-ttu-id="809ee-220">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="809ee-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="809ee-221">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="809ee-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_203.png

