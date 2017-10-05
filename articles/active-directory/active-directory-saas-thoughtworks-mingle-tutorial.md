---
title: "Tutorial: Integração do Azure Active Directory com o Thoughtworks Mingle | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Thoughtworks Mingle."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 69d859d9-b7f7-4c42-bc8c-8036138be586
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 268ae5affb88a718f68c08daa94fe7aba4a99c11
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thoughtworks-mingle"></a><span data-ttu-id="75ee8-103">Tutorial: Integração do Active Directory do Azure com o Thoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="75ee8-103">Tutorial: Azure Active Directory integration with Thoughtworks Mingle</span></span>

<span data-ttu-id="75ee8-104">Neste tutorial, você aprenderá a integrar o Thoughtworks Mingle ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="75ee8-104">In this tutorial, you learn how to integrate Thoughtworks Mingle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="75ee8-105">A integração do Thoughtworks Mingle ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="75ee8-105">Integrating Thoughtworks Mingle with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="75ee8-106">No Azure AD, é possível controlar quem tem acesso ao Thoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="75ee8-106">You can control in Azure AD who has access to Thoughtworks Mingle</span></span>
- <span data-ttu-id="75ee8-107">Você pode permitir que os usuários façam logon automaticamente no Thoughtworks Mingle (Logon Único) com as respectivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="75ee8-107">You can enable your users to automatically get signed-on to Thoughtworks Mingle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="75ee8-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="75ee8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="75ee8-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="75ee8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="75ee8-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="75ee8-110">Prerequisites</span></span>

<span data-ttu-id="75ee8-111">Para configurar a integração do Azure AD ao Thoughtworks Mingle, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="75ee8-111">To configure Azure AD integration with Thoughtworks Mingle, you need the following items:</span></span>

- <span data-ttu-id="75ee8-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="75ee8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="75ee8-113">Uma assinatura do Thoughtworks Mingle habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="75ee8-113">A Thoughtworks Mingle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="75ee8-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="75ee8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="75ee8-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="75ee8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="75ee8-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="75ee8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="75ee8-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="75ee8-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="75ee8-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="75ee8-118">Scenario description</span></span>
<span data-ttu-id="75ee8-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="75ee8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="75ee8-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="75ee8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="75ee8-121">Adicionar o Thoughtworks Mingle da galeria</span><span class="sxs-lookup"><span data-stu-id="75ee8-121">Adding Thoughtworks Mingle from the gallery</span></span>
2. <span data-ttu-id="75ee8-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="75ee8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thoughtworks-mingle-from-the-gallery"></a><span data-ttu-id="75ee8-123">Adicionar o Thoughtworks Mingle da galeria</span><span class="sxs-lookup"><span data-stu-id="75ee8-123">Adding Thoughtworks Mingle from the gallery</span></span>
<span data-ttu-id="75ee8-124">Para configurar a integração do Thoughtworks Mingle ao Azure AD, você precisa adicionar o Thoughtworks Mingle da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="75ee8-124">To configure the integration of Thoughtworks Mingle into Azure AD, you need to add Thoughtworks Mingle from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="75ee8-125">**Para adicionar o Thoughtworks Mingle da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="75ee8-125">**To add Thoughtworks Mingle from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="75ee8-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="75ee8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="75ee8-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="75ee8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="75ee8-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="75ee8-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="75ee8-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="75ee8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="75ee8-133">Na caixa de pesquisa, digite **Thoughtworks Mingle**, selecione **Thoughtworks Mingle** no painel de resultados e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="75ee8-133">In the search box, type **Thoughtworks Mingle**, select **Thoughtworks Mingle** from result panel then click **Add** button to add the application.</span></span>

    ![ThoughtWorks Mingle na lista de resultados](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="75ee8-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="75ee8-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="75ee8-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Thoughtworks Mingle, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="75ee8-136">In this section, you configure and test Azure AD single sign-on with Thoughtworks Mingle based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="75ee8-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Thoughtworks Mingle é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="75ee8-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Thoughtworks Mingle is to a user in Azure AD.</span></span> <span data-ttu-id="75ee8-138">Em outras palavras, é necessário estabelecer uma relação de vinculação entre um usuário do Azure AD e o usuário relacionado do Thoughtworks Mingle.</span><span class="sxs-lookup"><span data-stu-id="75ee8-138">In other words, a link relationship between an Azure AD user and the related user in Thoughtworks Mingle needs to be established.</span></span>

<span data-ttu-id="75ee8-139">No Thoughtworks Mingle, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="75ee8-139">In Thoughtworks Mingle, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="75ee8-140">Para configurar e testar o logon único do Azure AD com o Thoughtworks Mingle, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="75ee8-140">To configure and test Azure AD single sign-on with Thoughtworks Mingle, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="75ee8-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="75ee8-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="75ee8-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="75ee8-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="75ee8-143">**[Criar um usuário de teste do Workrite](#create-a-thoughtworks-mingle-test-user)** – para ter um equivalente de Brenda Fernandes no Thoughtworks Mingle vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="75ee8-143">**[Create a Thoughtworks Mingle test user](#create-a-thoughtworks-mingle-test-user)** - to have a counterpart of Britta Simon in Thoughtworks Mingle that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="75ee8-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="75ee8-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="75ee8-145">**[Testar o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="75ee8-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="75ee8-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="75ee8-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="75ee8-147">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo Thoughtworks Mingle.</span><span class="sxs-lookup"><span data-stu-id="75ee8-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Thoughtworks Mingle application.</span></span>

<span data-ttu-id="75ee8-148">**Para configurar o logon único do Azure AD com o Thoughtworks Mingle, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="75ee8-148">**To configure Azure AD single sign-on with Thoughtworks Mingle, perform the following steps:**</span></span>

1. <span data-ttu-id="75ee8-149">No Portal do Azure, na página de integração de aplicativos do **Thoughtworks Mingle**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="75ee8-149">In the Azure portal, on the **Thoughtworks Mingle** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="75ee8-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="75ee8-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_samlbase.png)

3. <span data-ttu-id="75ee8-153">Na seção **Domínio e URLs do Thoughtworks Mingle**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="75ee8-153">On the **Thoughtworks Mingle Domain and URLs** section, perform the following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do Thoughtworks Mingle](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_url.png)

    <span data-ttu-id="75ee8-155">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<companyname>.mingle.thoughtworks.com`</span><span class="sxs-lookup"><span data-stu-id="75ee8-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.mingle.thoughtworks.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="75ee8-156">O valor não é real.</span><span class="sxs-lookup"><span data-stu-id="75ee8-156">The value is not real.</span></span> <span data-ttu-id="75ee8-157">Atualize o valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="75ee8-157">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="75ee8-158">Contate a [equipe de suporte ao cliente do Thoughtworks Mingle](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support) para obter o valor.</span><span class="sxs-lookup"><span data-stu-id="75ee8-158">Contact [Thoughtworks Mingle Client support team](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support) to get the value.</span></span> 
 
4. <span data-ttu-id="75ee8-159">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="75ee8-159">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_certificate.png) 

5. <span data-ttu-id="75ee8-161">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="75ee8-161">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="75ee8-163">Faça logon em seu site de empresa do **Thoughtworks Mingle** como administrador.</span><span class="sxs-lookup"><span data-stu-id="75ee8-163">Log in to your **Thoughtworks Mingle** company site as administrator.</span></span>

7. <span data-ttu-id="75ee8-164">Clique na guia **Administrador** e em **Config. de SSO**.</span><span class="sxs-lookup"><span data-stu-id="75ee8-164">Click the **Admin** tab, and then, click **SSO Config**.</span></span>
   
    <span data-ttu-id="75ee8-165">![Guia Administrador](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "Configuração de SSO")</span><span class="sxs-lookup"><span data-stu-id="75ee8-165">![Admin tab](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "SSO Config")</span></span>

8. <span data-ttu-id="75ee8-166">Na seção **Config. de SSO** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="75ee8-166">In the **SSO Config** section, perform the following steps:</span></span>
   
    <span data-ttu-id="75ee8-167">![Configuração de SSO](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "Configuração de SSO")</span><span class="sxs-lookup"><span data-stu-id="75ee8-167">![SSO Config](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "SSO Config")</span></span>
    
    <span data-ttu-id="75ee8-168">a.</span><span class="sxs-lookup"><span data-stu-id="75ee8-168">a.</span></span> <span data-ttu-id="75ee8-169">Para carregar o arquivo de metadados, clique em **Escolher arquivo**.</span><span class="sxs-lookup"><span data-stu-id="75ee8-169">To upload the metadata file, click **Choose file**.</span></span> 

    <span data-ttu-id="75ee8-170">b.</span><span class="sxs-lookup"><span data-stu-id="75ee8-170">b.</span></span> <span data-ttu-id="75ee8-171">Clique em **Salvar Alterações**.</span><span class="sxs-lookup"><span data-stu-id="75ee8-171">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="75ee8-172">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="75ee8-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="75ee8-173">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="75ee8-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="75ee8-174">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="75ee8-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="75ee8-175">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="75ee8-175">Create an Azure AD test user</span></span>
<span data-ttu-id="75ee8-176">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="75ee8-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="75ee8-178">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="75ee8-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="75ee8-179">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="75ee8-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="75ee8-181">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="75ee8-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="75ee8-183">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="75ee8-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![O botão Adicionar](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="75ee8-185">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="75ee8-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![A caixa de diálogo Usuário](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="75ee8-187">a.</span><span class="sxs-lookup"><span data-stu-id="75ee8-187">a.</span></span> <span data-ttu-id="75ee8-188">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="75ee8-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="75ee8-189">b.</span><span class="sxs-lookup"><span data-stu-id="75ee8-189">b.</span></span> <span data-ttu-id="75ee8-190">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="75ee8-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="75ee8-191">c.</span><span class="sxs-lookup"><span data-stu-id="75ee8-191">c.</span></span> <span data-ttu-id="75ee8-192">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="75ee8-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="75ee8-193">d.</span><span class="sxs-lookup"><span data-stu-id="75ee8-193">d.</span></span> <span data-ttu-id="75ee8-194">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="75ee8-194">Click **Create**.</span></span>
 
### <a name="create-a-thoughtworks-mingle-test-user"></a><span data-ttu-id="75ee8-195">Criar um usuário de teste do Thoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="75ee8-195">Create a Thoughtworks Mingle test user</span></span>

<span data-ttu-id="75ee8-196">Para usuários do Azure AD conseguirem entrar, eles devem ser provisionados para o aplicativo Thoughtworks Mingle usando seus nomes de usuário do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="75ee8-196">For Azure AD users to be able to sign in, they must be provisioned to the Thoughtworks Mingle application using their Azure Active Directory user names.</span></span> <span data-ttu-id="75ee8-197">No caso do Thoughtworks Mingle, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="75ee8-197">In the case of Thoughtworks Mingle, provisioning is a manual task.</span></span>

<span data-ttu-id="75ee8-198">**Para configurar o provisionamento de usuários, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="75ee8-198">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="75ee8-199">Faça logon em seu site de empresa Thoughtworks Mingle como um administrador.</span><span class="sxs-lookup"><span data-stu-id="75ee8-199">Log in to your Thoughtworks Mingle company site as administrator.</span></span>

2. <span data-ttu-id="75ee8-200">Clique em **Perfil**.</span><span class="sxs-lookup"><span data-stu-id="75ee8-200">Click **Profile**.</span></span>
   
    <span data-ttu-id="75ee8-201">![Seu primeiro projeto](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "Seu primeiro projeto")</span><span class="sxs-lookup"><span data-stu-id="75ee8-201">![Your First Project](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "Your First Project")</span></span>

3. <span data-ttu-id="75ee8-202">Clique na guia **Administrador** e em **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="75ee8-202">Click the **Admin** tab, and then click **Users**.</span></span>
   
    <span data-ttu-id="75ee8-203">![Usuários](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="75ee8-203">![Users](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "Users")</span></span>

4. <span data-ttu-id="75ee8-204">Clique em **Novo Usuário**.</span><span class="sxs-lookup"><span data-stu-id="75ee8-204">Click **New User**.</span></span>
   
    <span data-ttu-id="75ee8-205">![Novo Usuário](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "Novo Usuário")</span><span class="sxs-lookup"><span data-stu-id="75ee8-205">![New User](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "New User")</span></span>

5. <span data-ttu-id="75ee8-206">Na página do diálogo **Novo Usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="75ee8-206">On the **New User** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="75ee8-207">![Caixa de diálogo Novo Usuário](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "Novo Usuário")</span><span class="sxs-lookup"><span data-stu-id="75ee8-207">![New User dialog](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "New User")</span></span>  
 
    <span data-ttu-id="75ee8-208">a.</span><span class="sxs-lookup"><span data-stu-id="75ee8-208">a.</span></span> <span data-ttu-id="75ee8-209">Digite o **Nome de entrada**, **Nome de exibição**, **Escolher senha** e **Confirmar senha** de uma conta válida do Azure AD que você deseja provisionar nas caixas de texto relacionadas.</span><span class="sxs-lookup"><span data-stu-id="75ee8-209">Type the **Sign-in name**, **Display name**, **Choose password**, **Confirm password** of a valid Azure AD account you want to provision into the related textboxes.</span></span> 

    <span data-ttu-id="75ee8-210">b.</span><span class="sxs-lookup"><span data-stu-id="75ee8-210">b.</span></span> <span data-ttu-id="75ee8-211">Para **Tipo de usuário**, selecione **Usuário completo**.</span><span class="sxs-lookup"><span data-stu-id="75ee8-211">As **User type**, select **Full user**.</span></span>

    <span data-ttu-id="75ee8-212">c.</span><span class="sxs-lookup"><span data-stu-id="75ee8-212">c.</span></span> <span data-ttu-id="75ee8-213">Clique em **Criar este Perfil**.</span><span class="sxs-lookup"><span data-stu-id="75ee8-213">Click **Create This Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="75ee8-214">É possível usar qualquer outra ferramenta de criação da conta de usuário do Thoughtworks Mingle ou as APIs fornecidas pelo Thoughtworks Mingle para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="75ee8-214">You can use any other Thoughtworks Mingle user account creation tools or APIs provided by Thoughtworks Mingle to provision AAD user accounts.</span></span>
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="75ee8-215">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="75ee8-215">Assign the Azure AD test user</span></span>

<span data-ttu-id="75ee8-216">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Thoughtworks Mingle.</span><span class="sxs-lookup"><span data-stu-id="75ee8-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Thoughtworks Mingle.</span></span>

![Atribuir a função de usuário][200] 

<span data-ttu-id="75ee8-218">**Para atribuir Brenda Fernandes ao Thoughtworks Mingle, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="75ee8-218">**To assign Britta Simon to Thoughtworks Mingle, perform the following steps:**</span></span>

1. <span data-ttu-id="75ee8-219">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="75ee8-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="75ee8-221">Na lista de aplicativos, selecione **Thoughtworks Mingle**.</span><span class="sxs-lookup"><span data-stu-id="75ee8-221">In the applications list, select **Thoughtworks Mingle**.</span></span>

    ![O link do Thoughtworks Mingle na lista de Aplicativos](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_app.png) 

3. <span data-ttu-id="75ee8-223">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="75ee8-223">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202] 

4. <span data-ttu-id="75ee8-225">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="75ee8-225">Click **Add** button.</span></span> <span data-ttu-id="75ee8-226">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="75ee8-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="75ee8-228">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="75ee8-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="75ee8-229">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="75ee8-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="75ee8-230">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="75ee8-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="75ee8-231">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="75ee8-231">Test single sign-on</span></span>

<span data-ttu-id="75ee8-232">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="75ee8-232">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="75ee8-233">Ao clicar no bloco do Thoughtworks Mingle no Painel de Acesso, você deverá ser conectado automaticamente ao aplicativo Thoughtworks Mingle.</span><span class="sxs-lookup"><span data-stu-id="75ee8-233">When you click the Thoughtworks Mingle tile in the Access Panel, you should get automatically signed-on to your Thoughtworks Mingle application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="75ee8-234">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="75ee8-234">Additional resources</span></span>

* [<span data-ttu-id="75ee8-235">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="75ee8-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="75ee8-236">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="75ee8-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_203.png

