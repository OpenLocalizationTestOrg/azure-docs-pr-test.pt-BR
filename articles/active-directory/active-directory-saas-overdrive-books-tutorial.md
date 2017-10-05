---
title: "Tutorial: Integração do Azure Active Directory com o Overdrive | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Overdrive."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e68cede7-1130-4813-bd55-22a9a6fc6bf5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 515dd397c46df7c8c82afab9b50051e34db69d7a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-overdrive"></a><span data-ttu-id="9b4ac-103">Tutorial: Integração do Azure Active Directory com o Overdrive</span><span class="sxs-lookup"><span data-stu-id="9b4ac-103">Tutorial: Azure Active Directory integration with Overdrive</span></span> 

<span data-ttu-id="9b4ac-104">Neste tutorial, você aprende a integrar o Overdrive ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="9b4ac-104">In this tutorial, you learn how to integrate Overdrive with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9b4ac-105">A integração do Overdrive ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="9b4ac-105">Integrating Overdrive with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9b4ac-106">Você pode controlar no Azure AD quem tem acesso ao Overdrive</span><span class="sxs-lookup"><span data-stu-id="9b4ac-106">You can control in Azure AD who has access to Overdrive</span></span> 
- <span data-ttu-id="9b4ac-107">Você pode permitir que seus usuários façam logon automaticamente no Overdrive (logon único) com as contas do Azure AD deles</span><span class="sxs-lookup"><span data-stu-id="9b4ac-107">You can enable your users to automatically get signed-on to Overdrive (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9b4ac-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9b4ac-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9b4ac-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9b4ac-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b4ac-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9b4ac-110">Prerequisites</span></span>

<span data-ttu-id="9b4ac-111">Para configurar a integração do Azure AD com o Overdrive, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="9b4ac-111">To configure Azure AD integration with Overdrive, you need the following items:</span></span>

- <span data-ttu-id="9b4ac-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9b4ac-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9b4ac-113">Uma assinatura habilitada para logon único do Overdrive</span><span class="sxs-lookup"><span data-stu-id="9b4ac-113">An Overdrive single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9b4ac-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9b4ac-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="9b4ac-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9b4ac-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9b4ac-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9b4ac-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9b4ac-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="9b4ac-118">Scenario description</span></span>
<span data-ttu-id="9b4ac-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9b4ac-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="9b4ac-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9b4ac-121">Adicionar o Overdrive da galeria</span><span class="sxs-lookup"><span data-stu-id="9b4ac-121">Adding Overdrive from the gallery</span></span>
2. <span data-ttu-id="9b4ac-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9b4ac-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-overdrive-from-the-gallery"></a><span data-ttu-id="9b4ac-123">Adicionar o Overdrive da galeria</span><span class="sxs-lookup"><span data-stu-id="9b4ac-123">Adding Overdrive from the gallery</span></span>
<span data-ttu-id="9b4ac-124">Para configurar a integração do Overdrive ao Azure AD, você precisa adicionar o Overdrive na galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-124">To configure the integration of Overdrive into Azure AD, you need to add Overdrive from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9b4ac-125">**Para adicionar o Overdrive por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="9b4ac-125">**To add Overdrive from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9b4ac-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9b4ac-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9b4ac-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="9b4ac-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="9b4ac-133">Na caixa de pesquisa, digite **Overdrive**.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-133">In the search box, type **Overdrive**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_search.png)

5. <span data-ttu-id="9b4ac-135">No painel de resultados, selecione **Overdrive** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-135">In the results panel, select **Overdrive**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9b4ac-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9b4ac-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9b4ac-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Overdrive com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-138">In this section, you configure and test Azure AD single sign-on with Overdrive based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9b4ac-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Overdrive é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Overdrive is to a user in Azure AD.</span></span> <span data-ttu-id="9b4ac-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Overdrive.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-140">In other words, a link relationship between an Azure AD user and the related user in Overdrive needs to be established.</span></span>

<span data-ttu-id="9b4ac-141">No Overdrive, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-141">In Overdrive, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9b4ac-142">Para configurar e testar o logon único do Azure AD com o Overdrive, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="9b4ac-142">To configure and test Azure AD single sign-on with Overdrive, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9b4ac-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9b4ac-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9b4ac-145">**[Criação de um usuário de teste do Overdrive](#creating-an-overdrive-test-user)** – para ter um equivalente de Brenda Fernandes no Overdrive que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-145">**[Creating an Overdrive test user](#creating-an-overdrive-test-user)** - to have a counterpart of Britta Simon in Overdrive that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9b4ac-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9b4ac-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9b4ac-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b4ac-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9b4ac-149">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único em seu aplicativo Overdrive.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Overdrive  application.</span></span>

<span data-ttu-id="9b4ac-150">**Para configurar o logon único do Azure AD com o Overdrive, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="9b4ac-150">**To configure Azure AD single sign-on with Overdrive, perform the following steps:**</span></span>

1. <span data-ttu-id="9b4ac-151">No Portal do Azure, na página de integração de aplicativos do **Overdrive**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-151">In the Azure portal, on the **Overdrive** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="9b4ac-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_samlbase.png)

3. <span data-ttu-id="9b4ac-155">Na seção **URLs e Domínio do Overdrive**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="9b4ac-155">On the **Overdrive Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_url.png)

    <span data-ttu-id="9b4ac-157">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `http://<subdomain>.libraryreserve.com`</span><span class="sxs-lookup"><span data-stu-id="9b4ac-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://<subdomain>.libraryreserve.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9b4ac-158">O valor não é real.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-158">The value is not real.</span></span> <span data-ttu-id="9b4ac-159">Atualize o valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="9b4ac-160">Entre em contato com a [equipe de suporte ao cliente do Overdrive](https://help.overdrive.com/) para obter o valor.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-160">Contact [Overdrive Client support team](https://help.overdrive.com/) to get the value.</span></span> 
 
4. <span data-ttu-id="9b4ac-161">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_certificate.png) 

5. <span data-ttu-id="9b4ac-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="9b4ac-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9b4ac-165">Para configurar o logon único no lado do **Overdrive**, é necessário enviar o **XML de Metadados** baixado para a [equipe de suporte do Overdrive](https://help.overdrive.com/).</span><span class="sxs-lookup"><span data-stu-id="9b4ac-165">To configure single sign-on on **Overdrive** side, you need to send the downloaded **Metadata XML** to [Overdrive support team](https://help.overdrive.com/).</span></span> <span data-ttu-id="9b4ac-166">Eles definem essa configuração para ter a conexão de SSO do SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="9b4ac-167">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="9b4ac-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9b4ac-168">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9b4ac-169">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9b4ac-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9b4ac-170">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9b4ac-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="9b4ac-171">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="9b4ac-173">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="9b4ac-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9b4ac-174">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-overdrive-books-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9b4ac-176">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-overdrive-books-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9b4ac-178">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-overdrive-books-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9b4ac-180">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="9b4ac-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-overdrive-books-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9b4ac-182">a.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-182">a.</span></span> <span data-ttu-id="9b4ac-183">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9b4ac-184">b.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-184">b.</span></span> <span data-ttu-id="9b4ac-185">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9b4ac-186">c.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-186">c.</span></span> <span data-ttu-id="9b4ac-187">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9b4ac-188">d.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-188">d.</span></span> <span data-ttu-id="9b4ac-189">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-189">Click **Create**.</span></span>
 
### <a name="creating-an-overdrive-test-user"></a><span data-ttu-id="9b4ac-190">Criação de um usuário de teste do Overdrive</span><span class="sxs-lookup"><span data-stu-id="9b4ac-190">Creating an Overdrive test user</span></span>

<span data-ttu-id="9b4ac-191">Não há nenhum item de ação para a configuração de provisionamento de usuário para o OverDrive.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-191">There is no action item for you to configure user provisioning to OverDrive.</span></span>  

<span data-ttu-id="9b4ac-192">Quando um usuário atribuído tentar fazer logon no OverDrive, uma conta do OverDrive será automaticamente criada, se necessário.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-192">When an assigned user tries to log in to OverDrive, an OverDrive account is automatically created if necessary.</span></span>

>[!NOTE]
><span data-ttu-id="9b4ac-193">É possível usar qualquer outra ferramenta de criação da conta de usuário do OverDrive ou as APIs fornecidas pelo OverDrive para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-193">You can use any other OverDrive user account creation tools or APIs provided by OverDrive to provision AAD user accounts.</span></span>
>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9b4ac-194">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9b4ac-194">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9b4ac-195">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo acesso ao Overdrive.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Overdrive.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="9b4ac-197">**Para atribuir Brenda Fernandes ao Overdrive, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="9b4ac-197">**To assign Britta Simon to Overdrive, perform the following steps:**</span></span>

1. <span data-ttu-id="9b4ac-198">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="9b4ac-200">Na lista de aplicativos, selecione **Overdrive**.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-200">In the applications list, select **Overdrive**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_app.png) 

3. <span data-ttu-id="9b4ac-202">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-202">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="9b4ac-204">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-204">Click **Add** button.</span></span> <span data-ttu-id="9b4ac-205">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="9b4ac-207">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9b4ac-208">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9b4ac-209">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9b4ac-210">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="9b4ac-210">Testing single sign-on</span></span>

<span data-ttu-id="9b4ac-211">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-211">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9b4ac-212">Ao clicar no bloco do Overdrive no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo Overdrive.</span><span class="sxs-lookup"><span data-stu-id="9b4ac-212">When you click the Overdrive tile in the Access Panel, you should get automatically signed-on to your Overdrive application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9b4ac-213">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="9b4ac-213">Additional resources</span></span>

* [<span data-ttu-id="9b4ac-214">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="9b4ac-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9b4ac-215">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9b4ac-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_203.png

