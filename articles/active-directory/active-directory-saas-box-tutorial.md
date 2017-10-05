---
title: "Tutorial: integração do Azure Active Directory com o Box | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Box."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5f3517f8-30f2-4be7-9e47-43d702701797
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 2cc2afe8ff3f0063224c94eb0b8135347051b0aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-box"></a><span data-ttu-id="6965e-103">Tutorial: Integração do Active Directory do Azure ao Box</span><span class="sxs-lookup"><span data-stu-id="6965e-103">Tutorial: Azure Active Directory integration with Box</span></span>

<span data-ttu-id="6965e-104">Neste tutorial, você aprenderá a integrar o Box ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="6965e-104">In this tutorial, you learn how to integrate Box with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6965e-105">A integração do Box ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="6965e-105">Integrating Box with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6965e-106">No Azure AD, é possível controlar quem tem acesso ao Box</span><span class="sxs-lookup"><span data-stu-id="6965e-106">You can control in Azure AD who has access to Box</span></span>
- <span data-ttu-id="6965e-107">Você pode permitir que seus usuários façam logon automaticamente no Box (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6965e-107">You can enable your users to automatically get signed-on to Box (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6965e-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6965e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6965e-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6965e-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6965e-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6965e-110">Prerequisites</span></span>

<span data-ttu-id="6965e-111">Para configurar a integração do Azure AD ao Box, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="6965e-111">To configure Azure AD integration with Box, you need the following items:</span></span>

- <span data-ttu-id="6965e-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6965e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6965e-113">Uma assinatura do Box habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="6965e-113">A Box single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6965e-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="6965e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6965e-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="6965e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6965e-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="6965e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6965e-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6965e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6965e-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="6965e-118">Scenario description</span></span>
<span data-ttu-id="6965e-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="6965e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6965e-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="6965e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6965e-121">Adicionar o Box da galeria</span><span class="sxs-lookup"><span data-stu-id="6965e-121">Adding Box from the gallery</span></span>
2. <span data-ttu-id="6965e-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6965e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-box-from-the-gallery"></a><span data-ttu-id="6965e-123">Adicionar o Box da galeria</span><span class="sxs-lookup"><span data-stu-id="6965e-123">Adding Box from the gallery</span></span>
<span data-ttu-id="6965e-124">Para configurar a integração do Box ao Azure AD, você precisa adicionar o Box por meio da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="6965e-124">To configure the integration of Box into Azure AD, you need to add Box from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6965e-125">**Para adicionar o Box por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="6965e-125">**To add Box from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6965e-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6965e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6965e-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="6965e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6965e-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="6965e-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="6965e-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6965e-131">Click **New application** button on the top of the dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="6965e-133">Na caixa de pesquisa, digite **Box**.</span><span class="sxs-lookup"><span data-stu-id="6965e-133">In the search box, type **Box**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-box-tutorial/tutorial_box_search.png)

5. <span data-ttu-id="6965e-135">No painel de resultados, selecione **Box** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6965e-135">In the results panel, select **Box**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-box-tutorial/tutorial_box_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6965e-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6965e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6965e-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Box com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="6965e-138">In this section, you configure and test Azure AD single sign-on with Box based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6965e-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Box é equivalente a um determinado usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6965e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Box is to a user in Azure AD.</span></span> <span data-ttu-id="6965e-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Box.</span><span class="sxs-lookup"><span data-stu-id="6965e-140">In other words, a link relationship between an Azure AD user and the related user in Box needs to be established.</span></span>

<span data-ttu-id="6965e-141">Essa relação de vínculo é estabelecida por meio da atribuição do valor de **nome de usuário** no Azure AD como o valor de **Nome de Usuário** no Box.</span><span class="sxs-lookup"><span data-stu-id="6965e-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Box.</span></span>

<span data-ttu-id="6965e-142">Para configurar e testar o logon único do Azure AD com o Box, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="6965e-142">To configure and test Azure AD single sign-on with Box, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6965e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="6965e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6965e-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="6965e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6965e-145">**[Criação de um usuário de teste do Box](#creating-a-box-test-user)** – para ter um equivalente de Brenda Fernandes no Box que esteja vinculado à sua representação no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6965e-145">**[Creating a Box test user](#creating-a-box-test-user)** - to have a counterpart of Britta Simon in Box that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6965e-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="6965e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6965e-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="6965e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6965e-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6965e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6965e-149">Nesta seção, você habilitará o logon único do Azure AD no portal do Azure e configurará o logon único no aplicativo Box.</span><span class="sxs-lookup"><span data-stu-id="6965e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Box application.</span></span>

<span data-ttu-id="6965e-150">**Para configurar o logon único do Azure AD com o Box, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="6965e-150">**To configure Azure AD single sign-on with Box, perform the following steps:**</span></span>

1. <span data-ttu-id="6965e-151">No portal do Azure, na página de integração de aplicativo do **Box**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="6965e-151">In the Azure portal, on the **Box** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="6965e-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="6965e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-box-tutorial/tutorial_box_samlbase.png)

3. <span data-ttu-id="6965e-155">Na seção **URLs e Domínio do Box**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="6965e-155">On the **Box Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-box-tutorial/tutorial_box_url.png)

    <span data-ttu-id="6965e-157">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<subdomain>.box.com`</span><span class="sxs-lookup"><span data-stu-id="6965e-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.box.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6965e-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="6965e-158">This value is not real.</span></span> <span data-ttu-id="6965e-159">Atualize o valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="6965e-159">Update the value with the actual Sign-on URL.</span></span> <span data-ttu-id="6965e-160">Entre em contato com a [equipe de suporte ao cliente do Box](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) para obter esse valor.</span><span class="sxs-lookup"><span data-stu-id="6965e-160">Contact [Box Client support team](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) to get this value.</span></span> 
 
4. <span data-ttu-id="6965e-161">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo XML em seu computador.</span><span class="sxs-lookup"><span data-stu-id="6965e-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-box-tutorial/tutorial_box_certificate.png) 

5. <span data-ttu-id="6965e-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="6965e-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-box-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6965e-165">Para que o SSO seja configurado para o aplicativo, entre em contato com a [equipe de suporte ao cliente do Box](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) e forneça o arquivo XML baixado.</span><span class="sxs-lookup"><span data-stu-id="6965e-165">To get SSO configured for your application, Contact [Box Client support team](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) and provide them with the downloaded XML file.</span></span>

> [!TIP]
> <span data-ttu-id="6965e-166">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="6965e-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6965e-167">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="6965e-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6965e-168">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6965e-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6965e-169">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6965e-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="6965e-170">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="6965e-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="6965e-172">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="6965e-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6965e-173">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6965e-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-box-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6965e-175">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="6965e-175">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-box-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6965e-177">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6965e-177">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-box-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6965e-179">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="6965e-179">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-box-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6965e-181">a.</span><span class="sxs-lookup"><span data-stu-id="6965e-181">a.</span></span> <span data-ttu-id="6965e-182">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="6965e-182">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6965e-183">b.</span><span class="sxs-lookup"><span data-stu-id="6965e-183">b.</span></span> <span data-ttu-id="6965e-184">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="6965e-184">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6965e-185">c.</span><span class="sxs-lookup"><span data-stu-id="6965e-185">c.</span></span> <span data-ttu-id="6965e-186">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="6965e-186">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6965e-187">d.</span><span class="sxs-lookup"><span data-stu-id="6965e-187">d.</span></span> <span data-ttu-id="6965e-188">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="6965e-188">Click **Create**.</span></span>
 
### <a name="creating-a-box-test-user"></a><span data-ttu-id="6965e-189">Criação de um usuário de teste do Box</span><span class="sxs-lookup"><span data-stu-id="6965e-189">Creating a Box test user</span></span>

<span data-ttu-id="6965e-190">Nesta seção, é criado um usuário chamado Brenda Fernandes no Box.</span><span class="sxs-lookup"><span data-stu-id="6965e-190">In this section, a user called Britta Simon is created in Box.</span></span> <span data-ttu-id="6965e-191">O Box dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="6965e-191">Box supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="6965e-192">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="6965e-192">There is no action item for you in this section.</span></span> <span data-ttu-id="6965e-193">Se um usuário ainda não existir no Box, um novo será criado quando você tentar acessar o Box.</span><span class="sxs-lookup"><span data-stu-id="6965e-193">If a user doesn't already exist in Box, a new one is created when you attempt to access Box.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6965e-194">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6965e-194">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6965e-195">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Box.</span><span class="sxs-lookup"><span data-stu-id="6965e-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Box.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="6965e-197">**Para atribuir Brenda Fernandes ao Box, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="6965e-197">**To assign Britta Simon to Box, perform the following steps:**</span></span>

1. <span data-ttu-id="6965e-198">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="6965e-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="6965e-200">Na lista de aplicativos, selecione o **Box**.</span><span class="sxs-lookup"><span data-stu-id="6965e-200">In the applications list, select **Box**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-box-tutorial/tutorial_box_app.png) 

3. <span data-ttu-id="6965e-202">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="6965e-202">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="6965e-204">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6965e-204">Click **Add** button.</span></span> <span data-ttu-id="6965e-205">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6965e-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="6965e-207">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="6965e-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6965e-208">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6965e-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6965e-209">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6965e-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6965e-210">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="6965e-210">Testing single sign-on</span></span>

<span data-ttu-id="6965e-211">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="6965e-211">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6965e-212">Quando clicar no bloco do Box no Painel de Acesso, você deverá ser levado à página de logon para ser conectado automaticamente ao seu aplicativo Box.</span><span class="sxs-lookup"><span data-stu-id="6965e-212">When you click the Box tile in the Access Panel, you should get login page to get signed-on to your Box application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6965e-213">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="6965e-213">Additional resources</span></span>

* [<span data-ttu-id="6965e-214">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="6965e-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6965e-215">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6965e-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="6965e-216">Configurar Provisionamento de Usuário</span><span class="sxs-lookup"><span data-stu-id="6965e-216">Configure User Provisioning</span></span>](active-directory-saas-box-userprovisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-box-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-box-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-box-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-box-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-box-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-box-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-box-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-box-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-box-tutorial/tutorial_general_203.png

