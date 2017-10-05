---
title: "Tutorial: Integração do Azure Active Directory com o Lynda.com | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Lynda.com."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f6c92789-8b64-4049-bac9-8cb928398433
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: 84ed2adcc2d49ddbb6bd2e9cc3b93b967ebed063
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lyndacom"></a><span data-ttu-id="7c0a2-103">Tutorial: Integração do Active Directory do Azure com o Lynda.com</span><span class="sxs-lookup"><span data-stu-id="7c0a2-103">Tutorial: Azure Active Directory integration with Lynda.com</span></span>

<span data-ttu-id="7c0a2-104">Neste tutorial, você aprenderá a integrar o Lynda.com ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="7c0a2-104">In this tutorial, you learn how to integrate Lynda.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7c0a2-105">A integração do Lynda.com ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="7c0a2-105">Integrating Lynda.com with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7c0a2-106">Você pode controlar no Azure AD quem tem acesso ao Lynda.com</span><span class="sxs-lookup"><span data-stu-id="7c0a2-106">You can control in Azure AD who has access to Lynda.com</span></span>
- <span data-ttu-id="7c0a2-107">Você pode permitir que usuários façam logon automaticamente no Lynda.com (logon único) com as respectivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7c0a2-107">You can enable your users to automatically get signed-on to Lynda.com (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7c0a2-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7c0a2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7c0a2-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7c0a2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c0a2-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7c0a2-110">Prerequisites</span></span>

<span data-ttu-id="7c0a2-111">Para configurar a integração do Azure AD ao Lynda.com, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="7c0a2-111">To configure Azure AD integration with Lynda.com, you need the following items:</span></span>

- <span data-ttu-id="7c0a2-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7c0a2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7c0a2-113">Uma assinatura do Lynda.com com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="7c0a2-113">A Lynda.com single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7c0a2-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7c0a2-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="7c0a2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7c0a2-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7c0a2-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7c0a2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7c0a2-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="7c0a2-118">Scenario description</span></span>
<span data-ttu-id="7c0a2-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7c0a2-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="7c0a2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7c0a2-121">Adicionar o Lynda.com da Galeria</span><span class="sxs-lookup"><span data-stu-id="7c0a2-121">Adding Lynda.com from the gallery</span></span>
2. <span data-ttu-id="7c0a2-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7c0a2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lyndacom-from-the-gallery"></a><span data-ttu-id="7c0a2-123">Adicionar o Lynda.com da Galeria</span><span class="sxs-lookup"><span data-stu-id="7c0a2-123">Adding Lynda.com from the gallery</span></span>
<span data-ttu-id="7c0a2-124">Para configurar a integração do Lynda.com ao Azure AD, você precisará adicionar o Lynda.com da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-124">To configure the integration of Lynda.com into Azure AD, you need to add Lynda.com from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7c0a2-125">**Para adicionar o Lynda.com da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7c0a2-125">**To add Lynda.com from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7c0a2-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7c0a2-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7c0a2-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="7c0a2-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="7c0a2-133">Na caixa de pesquisa, digite **Lynda.com**.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-133">In the search box, type **Lynda.com**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_search.png)

5. <span data-ttu-id="7c0a2-135">No painel de resultados, selecione **Lynda.com** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-135">In the results panel, select **Lynda.com**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7c0a2-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7c0a2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7c0a2-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Lynda.com, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-138">In this section, you configure and test Azure AD single sign-on with Lynda.com based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7c0a2-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Lynda.com é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lynda.com is to a user in Azure AD.</span></span> <span data-ttu-id="7c0a2-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-140">In other words, a link relationship between an Azure AD user and the related user in Lynda.com needs to be established.</span></span>

<span data-ttu-id="7c0a2-141">Essa relação de vinculação é estabelecida por meio da atribuição do valor de **nome de usuário** no Azure AD como o valor de **Nome de usuário** no Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Lynda.com.</span></span>

<span data-ttu-id="7c0a2-142">Para configurar e testar o logon único do Azure AD com o Lynda.com, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="7c0a2-142">To configure and test Azure AD single sign-on with Lynda.com, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7c0a2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7c0a2-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7c0a2-145">**[Criação de um usuário de teste do Lynda.com](#creating-a-lyndacom-test-user)** – para ter um equivalente de Brenda Fernandes no Lynda.com que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-145">**[Creating a Lynda.com test user](#creating-a-lyndacom-test-user)** - to have a counterpart of Britta Simon in Lynda.com that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7c0a2-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7c0a2-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7c0a2-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7c0a2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7c0a2-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lynda.com application.</span></span>

<span data-ttu-id="7c0a2-150">**Para configurar o logon único do Azure AD com o Lynda.com, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7c0a2-150">**To configure Azure AD single sign-on with Lynda.com, perform the following steps:**</span></span>

1. <span data-ttu-id="7c0a2-151">No portal do Azure, na página de integração de aplicativos do **Lynda.com**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-151">In the Azure portal, on the **Lynda.com** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="7c0a2-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_samlbase.png)

3. <span data-ttu-id="7c0a2-155">Na seção **Domínio e URLs do Lynda.com**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7c0a2-155">On the **Lynda.com Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_url.png)

    <span data-ttu-id="7c0a2-157">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<subdomain>.lynda.com/Shibboleth.sso/InCommon?providerId=<url>&target=<url> `</span><span class="sxs-lookup"><span data-stu-id="7c0a2-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.lynda.com/Shibboleth.sso/InCommon?providerId=<url>&target=<url> `</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7c0a2-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-158">This value is not real.</span></span> <span data-ttu-id="7c0a2-159">Atualize esse valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="7c0a2-160">Contate a [equipe de suporte do Cliente Lynda.com](https://www.linkedin.com/help/lynda/ask) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-160">Contact [Lynda.com Client support team](https://www.linkedin.com/help/lynda/ask) to get these values.</span></span> 
 
4. <span data-ttu-id="7c0a2-161">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo XML em seu computador.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_certificate.png) 

5. <span data-ttu-id="7c0a2-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="7c0a2-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lynda-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7c0a2-165">Para configurar o logon único no lado do **Lynda.com**, é necessário enviar o **XML de metadados** baixado para a [equipe de suporte do Lynda.com](https://www.linkedin.com/help/lynda/ask).</span><span class="sxs-lookup"><span data-stu-id="7c0a2-165">To configure single sign-on on **Lynda.com** side, you need to send the downloaded **Metadata XML** [Lynda.com support](https://www.linkedin.com/help/lynda/ask).</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7c0a2-166">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7c0a2-166">Creating an Azure AD test user</span></span>
<span data-ttu-id="7c0a2-167">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-167">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="7c0a2-169">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7c0a2-169">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7c0a2-170">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-170">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lynda-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7c0a2-172">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-172">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lynda-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7c0a2-174">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-174">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lynda-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7c0a2-176">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7c0a2-176">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lynda-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7c0a2-178">a.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-178">a.</span></span> <span data-ttu-id="7c0a2-179">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-179">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7c0a2-180">b.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-180">b.</span></span> <span data-ttu-id="7c0a2-181">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-181">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7c0a2-182">c.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-182">c.</span></span> <span data-ttu-id="7c0a2-183">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-183">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7c0a2-184">d.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-184">d.</span></span> <span data-ttu-id="7c0a2-185">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-185">Click **Create**.</span></span>
 
### <a name="creating-a-lyndacom-test-user"></a><span data-ttu-id="7c0a2-186">Criar um usuário de teste do Lynda.com</span><span class="sxs-lookup"><span data-stu-id="7c0a2-186">Creating a Lynda.com test user</span></span>

<span data-ttu-id="7c0a2-187">Não há nenhum item de ação para a configuração de provisionamento de usuário para o Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-187">There is no action item for you to configure user provisioning to Lynda.com.</span></span>  
<span data-ttu-id="7c0a2-188">Quando um usuário atribuído tenta fazer logon no Lynda.com usando o painel de acesso, o Lynda.com verifica se o usuário existe.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-188">When an assigned user tries to log in to Lynda.com using the access panel, Lynda.com checks whether the user exists.</span></span>  

<span data-ttu-id="7c0a2-189">Se não houver conta de usuário ainda, ela é criada automaticamente pelo Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-189">If there is no user account available yet, it is automatically created by Lynda.com.</span></span>

>[!NOTE]
><span data-ttu-id="7c0a2-190">É possível usar qualquer outra ferramenta de criação da conta de usuário do Lynda.com ou APIs fornecidas pelo Lynda.com para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-190">You can use any other Lynda.com user account creation tools or APIs provided by Lynda.com to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7c0a2-191">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7c0a2-191">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7c0a2-192">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-192">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lynda.com.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="7c0a2-194">**Para atribuir Brenda Fernandes ao Lynda.com, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7c0a2-194">**To assign Britta Simon to Lynda.com, perform the following steps:**</span></span>

1. <span data-ttu-id="7c0a2-195">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="7c0a2-197">Na lista de aplicativos, selecione **Lynda.com**.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-197">In the applications list, select **Lynda.com**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_app.png) 

3. <span data-ttu-id="7c0a2-199">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-199">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="7c0a2-201">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-201">Click **Add** button.</span></span> <span data-ttu-id="7c0a2-202">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="7c0a2-204">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7c0a2-205">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-205">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7c0a2-206">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7c0a2-207">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="7c0a2-207">Testing single sign-on</span></span>

<span data-ttu-id="7c0a2-208">Se você quiser testar suas configurações de logon único, abra o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="7c0a2-208">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="7c0a2-209">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7c0a2-209">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7c0a2-210">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="7c0a2-210">Additional resources</span></span>

* [<span data-ttu-id="7c0a2-211">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="7c0a2-211">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7c0a2-212">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7c0a2-212">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_203.png

