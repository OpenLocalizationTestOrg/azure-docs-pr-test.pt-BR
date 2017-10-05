---
title: "Tutorial: integração do Azure Active Directory com o EmpCenter | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o EmpCenter."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a00ecf6e-917a-4284-b998-41506931585e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: aa27175165f4b15477bef4e70ad1c25016db31a2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-empcenter"></a><span data-ttu-id="218de-103">Tutorial: integração do Active Directory do Azure ao EmpCenter</span><span class="sxs-lookup"><span data-stu-id="218de-103">Tutorial: Azure Active Directory integration with EmpCenter</span></span>

<span data-ttu-id="218de-104">Neste tutorial, você aprende a integrar o EmpCenter ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="218de-104">In this tutorial, you learn how to integrate EmpCenter with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="218de-105">A integração do EmpCenter ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="218de-105">Integrating EmpCenter with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="218de-106">No Azure AD, é possível controlar quem tem acesso ao EmpCenter</span><span class="sxs-lookup"><span data-stu-id="218de-106">You can control in Azure AD who has access to EmpCenter</span></span>
- <span data-ttu-id="218de-107">É possível permitir que os usuários se conectem automaticamente ao EmpCenter (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="218de-107">You can enable your users to automatically get signed-on to EmpCenter (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="218de-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="218de-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="218de-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="218de-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="218de-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="218de-110">Prerequisites</span></span>

<span data-ttu-id="218de-111">Para configurar a integração do Azure AD ao EmpCenter, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="218de-111">To configure Azure AD integration with EmpCenter, you need the following items:</span></span>

- <span data-ttu-id="218de-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="218de-112">An Azure AD subscription</span></span>
- <span data-ttu-id="218de-113">Uma assinatura habilitada para logon único do EmpCenter</span><span class="sxs-lookup"><span data-stu-id="218de-113">An EmpCenter single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="218de-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="218de-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="218de-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="218de-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="218de-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="218de-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="218de-117">Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="218de-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="218de-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="218de-118">Scenario description</span></span>
<span data-ttu-id="218de-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="218de-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="218de-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="218de-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="218de-121">Adicionando o EmpCenter por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="218de-121">Adding EmpCenter from the gallery</span></span>
2. <span data-ttu-id="218de-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="218de-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-empcenter-from-the-gallery"></a><span data-ttu-id="218de-123">Adicionando o EmpCenter por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="218de-123">Adding EmpCenter from the gallery</span></span>
<span data-ttu-id="218de-124">Para configurar a integração do EmpCenter ao Azure AD, é necessário adicionar o EmpCenter à lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="218de-124">To configure the integration of EmpCenter into Azure AD, you need to add EmpCenter from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="218de-125">**Para adicionar o EmpCenter por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="218de-125">**To add EmpCenter from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="218de-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="218de-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="218de-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="218de-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="218de-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="218de-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="218de-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="218de-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="218de-133">Na caixa de pesquisa, digite **EmpCenter**.</span><span class="sxs-lookup"><span data-stu-id="218de-133">In the search box, type **EmpCenter**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_search.png)

5. <span data-ttu-id="218de-135">No painel de resultados, selecione **EmpCenter** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="218de-135">In the results panel, select **EmpCenter**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="218de-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="218de-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="218de-138">Nesta seção, você configura e testa o logon único do Azure AD com o EmpCenter, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="218de-138">In this section, you configure and test Azure AD single sign-on with EmpCenter based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="218de-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do EmpCenter é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="218de-139">For single sign-on to work, Azure AD needs to know what the counterpart user in EmpCenter is to a user in Azure AD.</span></span> <span data-ttu-id="218de-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do EmpCenter.</span><span class="sxs-lookup"><span data-stu-id="218de-140">In other words, a link relationship between an Azure AD user and the related user in EmpCenter needs to be established.</span></span>

<span data-ttu-id="218de-141">No EmpCenter, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="218de-141">In EmpCenter, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="218de-142">Para configurar e testar o logon único do Azure AD com o EmpCenter, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="218de-142">To configure and test Azure AD single sign-on with EmpCenter, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="218de-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="218de-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="218de-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="218de-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="218de-145">**[Criando um usuário de teste do EmpCenter](#creating-an-empcenter-test-user)** – para ter um equivalente de Brenda Fernandes no EmpCenter que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="218de-145">**[Creating an EmpCenter test user](#creating-an-empcenter-test-user)** - to have a counterpart of Britta Simon in EmpCenter that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="218de-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="218de-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="218de-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="218de-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="218de-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="218de-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="218de-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo EmpCenter.</span><span class="sxs-lookup"><span data-stu-id="218de-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your EmpCenter application.</span></span>

<span data-ttu-id="218de-150">**Para configurar o logon único do Azure AD com o EmpCenter, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="218de-150">**To configure Azure AD single sign-on with EmpCenter, perform the following steps:**</span></span>

1. <span data-ttu-id="218de-151">No portal do Azure, na página de integração do aplicativo **EmpCenter**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="218de-151">In the Azure portal, on the **EmpCenter** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="218de-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="218de-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_samlbase.png)

3. <span data-ttu-id="218de-155">Na seção **Domínio e URLs do EmpCenter**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="218de-155">On the **EmpCenter Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_url.png)

    <span data-ttu-id="218de-157">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="218de-157">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.EmpCenter.com/<instancename>` |
    | `https://<subdomain>.workforcehosting.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="218de-158">O valor não é real.</span><span class="sxs-lookup"><span data-stu-id="218de-158">The value is not real.</span></span> <span data-ttu-id="218de-159">Atualize o valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="218de-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="218de-160">Contate a [equipe de suporte ao Cliente do EmpCenter](http://www.workforcesoftware.com/services/customer-support/) para obter o valor.</span><span class="sxs-lookup"><span data-stu-id="218de-160">Contact [EmpCenter Client support team](http://www.workforcesoftware.com/services/customer-support/) to get the value.</span></span> 
 
4. <span data-ttu-id="218de-161">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="218de-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_certificate.png) 

5. <span data-ttu-id="218de-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="218de-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="218de-165">Para configurar o logon único no lado do **EmpCenter**, é necessário enviar o **XML de Metadados** baixado para a [equipe de suporte do EmpCenter](http://www.workforcesoftware.com/services/customer-support/).</span><span class="sxs-lookup"><span data-stu-id="218de-165">To configure single sign-on on **EmpCenter** side, you need to send the downloaded **Metadata XML** to [EmpCenter support team](http://www.workforcesoftware.com/services/customer-support/).</span></span> <span data-ttu-id="218de-166">Eles definem essa configuração para ter a conexão de SSO de SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="218de-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="218de-167">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="218de-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="218de-168">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="218de-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="218de-169">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="218de-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="218de-170">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="218de-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="218de-171">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="218de-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="218de-173">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="218de-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="218de-174">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="218de-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-EmpCenter-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="218de-176">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="218de-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-EmpCenter-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="218de-178">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="218de-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-EmpCenter-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="218de-180">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="218de-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-EmpCenter-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="218de-182">a.</span><span class="sxs-lookup"><span data-stu-id="218de-182">a.</span></span> <span data-ttu-id="218de-183">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="218de-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="218de-184">b.</span><span class="sxs-lookup"><span data-stu-id="218de-184">b.</span></span> <span data-ttu-id="218de-185">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="218de-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="218de-186">c.</span><span class="sxs-lookup"><span data-stu-id="218de-186">c.</span></span> <span data-ttu-id="218de-187">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="218de-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="218de-188">d.</span><span class="sxs-lookup"><span data-stu-id="218de-188">d.</span></span> <span data-ttu-id="218de-189">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="218de-189">Click **Create**.</span></span>
 
### <a name="creating-an-empcenter-test-user"></a><span data-ttu-id="218de-190">Criando um usuário de teste do EmpCenter</span><span class="sxs-lookup"><span data-stu-id="218de-190">Creating an EmpCenter test user</span></span>

<span data-ttu-id="218de-191">Para permitir que os usuários do Azure AD façam logon no EmpCenter, eles devem ser provisionados no EmpCenter.</span><span class="sxs-lookup"><span data-stu-id="218de-191">In order to enable Azure AD users to log in to EmpCenter, they must be provisioned into EmpCenter.</span></span> <span data-ttu-id="218de-192">No caso do EmpCenter, as contas de usuário precisam ser criadas pela [equipe de suporte do EmpCenter](http://www.workforcesoftware.com/services/customer-support/).</span><span class="sxs-lookup"><span data-stu-id="218de-192">In the case of EmpCenter, the user accounts need to be created by your [EmpCenter support team](http://www.workforcesoftware.com/services/customer-support/).</span></span>

> [!NOTE]
> <span data-ttu-id="218de-193">Você pode usar qualquer outra ferramenta de criação da conta de usuário do EmpCenter ou as APIs fornecidas pelo EmpCenter para provisionar as contas de usuário do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="218de-193">You can use any other EmpCenter user account creation tools or APIs provided by EmpCenter to provision Azure Active Directory user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="218de-194">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="218de-194">Assigning the Azure AD test user</span></span>

<span data-ttu-id="218de-195">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao EmpCenter.</span><span class="sxs-lookup"><span data-stu-id="218de-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to EmpCenter.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="218de-197">**Para atribuir Brenda Fernandes ao EmpCenter, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="218de-197">**To assign Britta Simon to EmpCenter, perform the following steps:**</span></span>

1. <span data-ttu-id="218de-198">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="218de-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="218de-200">Na lista de aplicativos, selecione **EmpCenter**.</span><span class="sxs-lookup"><span data-stu-id="218de-200">In the applications list, select **EmpCenter**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_app.png) 

3. <span data-ttu-id="218de-202">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="218de-202">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="218de-204">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="218de-204">Click **Add** button.</span></span> <span data-ttu-id="218de-205">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="218de-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="218de-207">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="218de-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="218de-208">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="218de-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="218de-209">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="218de-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="218de-210">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="218de-210">Testing single sign-on</span></span>


<span data-ttu-id="218de-211">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="218de-211">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="218de-212">Quando você clicar no bloco do EmpCenter no Painel de Acesso, deverá ser conectado automaticamente ao aplicativo EmpCenter.</span><span class="sxs-lookup"><span data-stu-id="218de-212">When you click the EmpCenter tile in the Access Panel, you should get automatically signed-on to your EmpCenter application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="218de-213">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="218de-213">Additional resources</span></span>

* [<span data-ttu-id="218de-214">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="218de-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="218de-215">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="218de-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_203.png

