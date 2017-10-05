---
title: "Tutorial: integração do Azure Active Directory com o ZPA (Zscaler Private Access) | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o ZPA (Zscaler Private Access)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 83711115-1c4f-4dd7-907b-3da24b37c89e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: 5c598bfa5b6725d21a89df54dbcb3314cc631d80
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-private-access-zpa"></a><span data-ttu-id="594c2-103">Tutorial: integração do Azure Active Directory com o ZPA (Zscaler Private Access)</span><span class="sxs-lookup"><span data-stu-id="594c2-103">Tutorial: Azure Active Directory integration with Zscaler Private Access (ZPA)</span></span>

<span data-ttu-id="594c2-104">Neste tutorial, você aprenderá a integrar o ZPA (Zscaler Private Access) ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="594c2-104">In this tutorial, you learn how to integrate Zscaler Private Access (ZPA) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="594c2-105">A integração do ZPA (Zscaler Private Access) ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="594c2-105">Integrating Zscaler Private Access (ZPA) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="594c2-106">No Azure AD, é possível controlar quem tem acesso ao ZPA (Zscaler Private Access)</span><span class="sxs-lookup"><span data-stu-id="594c2-106">You can control in Azure AD who has access to Zscaler Private Access (ZPA)</span></span>
- <span data-ttu-id="594c2-107">Você pode permitir que seus usuários faça logon automaticamente (logon único) no ZPA (Zscaler Private Access) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="594c2-107">You can enable your users to automatically get signed-on to Zscaler Private Access (ZPA) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="594c2-108">Você pode gerenciar suas contas em um único local - o portal de Gerenciamento do Azure</span><span class="sxs-lookup"><span data-stu-id="594c2-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="594c2-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="594c2-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="594c2-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="594c2-110">Prerequisites</span></span>

<span data-ttu-id="594c2-111">Para configurar a integração do Azure AD ao ZPA (Zscaler Private Access), você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="594c2-111">To configure Azure AD integration with Zscaler Private Access (ZPA), you need the following items:</span></span>

- <span data-ttu-id="594c2-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="594c2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="594c2-113">Uma assinatura com logon único do ZPA (Zscaler Private Access) habilitado</span><span class="sxs-lookup"><span data-stu-id="594c2-113">A Zscaler Private Access (ZPA) single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="594c2-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="594c2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="594c2-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="594c2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="594c2-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="594c2-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="594c2-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="594c2-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="594c2-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="594c2-118">Scenario description</span></span>
<span data-ttu-id="594c2-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="594c2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="594c2-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="594c2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="594c2-121">Adicionando ZPA (Zscaler Private Access) da galeria</span><span class="sxs-lookup"><span data-stu-id="594c2-121">Adding Zscaler Private Access (ZPA) from the gallery</span></span>
2. <span data-ttu-id="594c2-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="594c2-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-zscaler-private-access-zpa-from-the-gallery"></a><span data-ttu-id="594c2-123">Adicionando ZPA (Zscaler Private Access) da galeria</span><span class="sxs-lookup"><span data-stu-id="594c2-123">Adding Zscaler Private Access (ZPA) from the gallery</span></span>
<span data-ttu-id="594c2-124">Para configurar a integração do ZPA (Zscaler Private Access) ao Azure AD, você precisará adicionar o ZPA (Zscaler Private Access) da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="594c2-124">To configure the integration of Zscaler Private Access (ZPA) into Azure AD, you need to add Zscaler Private Access (ZPA) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="594c2-125">**Para adicionar o ZPA (Zscaler Private Access) da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="594c2-125">**To add Zscaler Private Access (ZPA) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="594c2-126">No **[Portal de Gerenciamento do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="594c2-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="594c2-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="594c2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="594c2-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="594c2-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="594c2-131">Clique em **adicionar** botão na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="594c2-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="594c2-133">Na caixa de pesquisa, digite **ZPA (Zscaler Private Access)**.</span><span class="sxs-lookup"><span data-stu-id="594c2-133">In the search box, type **Zscaler Private Access (ZPA)**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_001.png)

5. <span data-ttu-id="594c2-135">No painel de resultados, selecione **ZPA (Zscaler Private Access)** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="594c2-135">In the results panel, select **Zscaler Private Access (ZPA)**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="594c2-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="594c2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="594c2-138">Nesta seção, você configurará e testará o logon único do Azure AD com o ZPA (Zscaler Private Access), com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="594c2-138">In this section, you configure and test Azure AD single sign-on with Zscaler Private Access (ZPA) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="594c2-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do ZPA (Zscaler Private Access) é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="594c2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler Private Access (ZPA) is to a user in Azure AD.</span></span> <span data-ttu-id="594c2-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do ZPA (Zscaler Private Access).</span><span class="sxs-lookup"><span data-stu-id="594c2-140">In other words, a link relationship between an Azure AD user and the related user in Zscaler Private Access (ZPA) needs to be established.</span></span>

<span data-ttu-id="594c2-141">Essa relação de vínculo é estabelecida atribuindo o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** no ZPA (Zscaler Private Access).</span><span class="sxs-lookup"><span data-stu-id="594c2-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Zscaler Private Access (ZPA).</span></span>

<span data-ttu-id="594c2-142">Para configurar e testar o logon único do Azure AD com o ZPA (Zscaler Private Access), você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="594c2-142">To configure and test Azure AD single sign-on with Zscaler Private Access (ZPA), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="594c2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="594c2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="594c2-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** - para testar logon único do Azure AD com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="594c2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="594c2-145">**[Criando um usuário de teste do ZPA (Zscaler Private Access)](#creating-a-zscaler-private-access-(zpa)-test-user)** – para ter um equivalente de Brenda Fernandes no ZPA (Zscaler Private Access) que esteja vinculado à representação dela no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="594c2-145">**[Creating a Zscaler Private Access (ZPA) test user](#creating-a-zscaler-private-access-(zpa)-test-user)** - to have a counterpart of Britta Simon in Zscaler Private Access (ZPA) that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="594c2-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** - para habilitar Britta Simon a usar o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="594c2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="594c2-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="594c2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="594c2-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="594c2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="594c2-149">Nesta seção, você habilita o logon único do Azure AD no Portal de Gerenciamento do Azure e configura o logon único em seu aplicativo ZPA (Zscaler Private Access).</span><span class="sxs-lookup"><span data-stu-id="594c2-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Zscaler Private Access (ZPA) application.</span></span>

<span data-ttu-id="594c2-150">**Para configurar o logon único do Azure AD com o ZPA (Zscaler Private Access), execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="594c2-150">**To configure Azure AD single sign-on with Zscaler Private Access (ZPA), perform the following steps:**</span></span>

1. <span data-ttu-id="594c2-151">No Portal de Gerenciamento do Azure, na página de integração do aplicativo do **ZPA (Zscaler Private Access)**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="594c2-151">In the Azure Management portal, on the **Zscaler Private Access (ZPA)** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o logon único][4]

2. <span data-ttu-id="594c2-153">Na caixa de diálogo **Logon único**, como **Modo**, selecione **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="594c2-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_300.png)
    
3. <span data-ttu-id="594c2-155">Na seção **URLs e Domínio do ZPA (Zscaler Private Access)**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="594c2-155">On the **Zscaler Private Access (ZPA) Domain and URLs** section, perform the following steps:</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_01.png)

    <span data-ttu-id="594c2-157">a.</span><span class="sxs-lookup"><span data-stu-id="594c2-157">a.</span></span> <span data-ttu-id="594c2-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://samlsp.private.zscaler.com/auth/login?domain=<your-domain-name>`</span><span class="sxs-lookup"><span data-stu-id="594c2-158">In the **Sign On URL** textbox, type a URL using the following pattern: `https://samlsp.private.zscaler.com/auth/login?domain=<your-domain-name>`</span></span>

    <span data-ttu-id="594c2-159">b.</span><span class="sxs-lookup"><span data-stu-id="594c2-159">b.</span></span> <span data-ttu-id="594c2-160">Na caixa de texto **Identificador**, digite: `https://samlsp.private.zscaler.com/auth/metadata`</span><span class="sxs-lookup"><span data-stu-id="594c2-160">In the **Identifier** textbox, type: `https://samlsp.private.zscaler.com/auth/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="594c2-161">Observe que esses não são os valores reais.</span><span class="sxs-lookup"><span data-stu-id="594c2-161">Please note that these are not the real values.</span></span> <span data-ttu-id="594c2-162">É necessário atualizar esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="594c2-162">You have to update these values with the actual Sign On URL and Identifier.</span></span> <span data-ttu-id="594c2-163">Aqui, sugerimos que você use o valor exclusivo de URL no Identificador.</span><span class="sxs-lookup"><span data-stu-id="594c2-163">Here we suggest you to use the unique value of URL in the Identifier.</span></span> <span data-ttu-id="594c2-164">Entre em contato com [equipe de suporte do ZPA (Zscaler Private Access)](https://help.zscaler.com/zpa-submit-ticket) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="594c2-164">Contact [Zscaler Private Access (ZPA) support team](https://help.zscaler.com/zpa-submit-ticket) to get these values.</span></span>

4. <span data-ttu-id="594c2-165">Sobre o **certificado de autenticação SAML** seção, clique em **criar novo certificado**.</span><span class="sxs-lookup"><span data-stu-id="594c2-165">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_400.png)   

5. <span data-ttu-id="594c2-167">Na caixa de diálogo **Criar um Novo Certificado**, clique no ícone de calendário e selecione uma **data de expiração**.</span><span class="sxs-lookup"><span data-stu-id="594c2-167">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="594c2-168">Em seguida, clique no botão **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="594c2-168">Then click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_500.png)

6. <span data-ttu-id="594c2-170">Na seção **Certificado de Autenticação SAML**, selecione **Ativar o novo certificado** e clique no botão **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="594c2-170">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_02.png)

7. <span data-ttu-id="594c2-172">Na janela pop-up **Certificado de substituição**, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="594c2-172">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_600.png)

8. <span data-ttu-id="594c2-174">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="594c2-174">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_03.png) 

9. <span data-ttu-id="594c2-176">Em uma janela diferente do navegador da Web, faça logon no site ZPA (Zscaler Private Access) da sua empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="594c2-176">In a different web browser window, log into your Zscaler Private Access (ZPA) company site as an administrator.</span></span>

10. <span data-ttu-id="594c2-177">Navegue até **Administrador** e, em seguida, clique em **Configuração de IdP**.</span><span class="sxs-lookup"><span data-stu-id="594c2-177">Navigate to **Administrator** and then click **Idp Configuration**.</span></span>

    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_04.png)

11. <span data-ttu-id="594c2-179">Na seção **Configuração IdP**, clique em **Adicionar Nova Configuração de IdP**.</span><span class="sxs-lookup"><span data-stu-id="594c2-179">In the **Idp Configuration** section, click **Add New IDP Configuration**.</span></span>

    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_05.png)

12. <span data-ttu-id="594c2-181">Na seção **Nova Configuração de IdP**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="594c2-181">In the **New IDP Configuration** section, perform the following steps:</span></span>

    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_06.png)

    <span data-ttu-id="594c2-183">a.</span><span class="sxs-lookup"><span data-stu-id="594c2-183">a.</span></span> <span data-ttu-id="594c2-184">Clique em **Selecionar Arquivo** e carregue o arquivo de metadados baixado.</span><span class="sxs-lookup"><span data-stu-id="594c2-184">Click **Select File** and upload your downloaded metadata file.</span></span>

    <span data-ttu-id="594c2-185">b.</span><span class="sxs-lookup"><span data-stu-id="594c2-185">b.</span></span> <span data-ttu-id="594c2-186">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="594c2-186">Click **Save** button.</span></span>
    


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="594c2-187">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="594c2-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="594c2-188">O objetivo desta seção é criar um usuário de teste no Portal de Gerenciamento do Azure chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="594c2-188">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="594c2-190">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="594c2-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="594c2-191">No **portal de Gerenciamento do Azure**, no painel navegação à esquerda, clique em **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="594c2-191">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="594c2-193">Vá para **usuários e grupos** e clique em **todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="594c2-193">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="594c2-195">Na parte superior da caixa de diálogo clique **adicionar** para abrir o **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="594c2-195">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="594c2-197">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="594c2-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="594c2-199">a.</span><span class="sxs-lookup"><span data-stu-id="594c2-199">a.</span></span> <span data-ttu-id="594c2-200">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="594c2-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="594c2-201">b.</span><span class="sxs-lookup"><span data-stu-id="594c2-201">b.</span></span> <span data-ttu-id="594c2-202">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="594c2-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="594c2-203">c.</span><span class="sxs-lookup"><span data-stu-id="594c2-203">c.</span></span> <span data-ttu-id="594c2-204">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="594c2-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="594c2-205">d.</span><span class="sxs-lookup"><span data-stu-id="594c2-205">d.</span></span> <span data-ttu-id="594c2-206">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="594c2-206">Click **Create**.</span></span> 



### <a name="creating-a-zscaler-private-access-zpa-test-user"></a><span data-ttu-id="594c2-207">Criar um usuário de teste do ZPA (Zscaler Private Access)</span><span class="sxs-lookup"><span data-stu-id="594c2-207">Creating a Zscaler Private Access (ZPA) test user</span></span>

<span data-ttu-id="594c2-208">Nesta seção, você deve criar uma usuária chamada Brenda Fernandes no ZPA (Zscaler Private Access).</span><span class="sxs-lookup"><span data-stu-id="594c2-208">In this section, you create a user called Britta Simon in Zscaler Private Access (ZPA).</span></span> <span data-ttu-id="594c2-209">Trabalhe com [equipe de suporte do ZPA (Zscaler Private Access)](https://help.zscaler.com/zpa-submit-ticket) para adicionar os usuários na plataforma ZPA (Zscaler Private Access).</span><span class="sxs-lookup"><span data-stu-id="594c2-209">Please work with [Zscaler Private Access (ZPA) support team](https://help.zscaler.com/zpa-submit-ticket) to add the users in the Zscaler Private Access (ZPA) platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="594c2-210">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="594c2-210">Assigning the Azure AD test user</span></span>

<span data-ttu-id="594c2-211">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao ZPA (Zscaler Private Access).</span><span class="sxs-lookup"><span data-stu-id="594c2-211">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Zscaler Private Access (ZPA).</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="594c2-213">**Para atribuir Brenda Fernandes ao ZPA (Zscaler Private Access), execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="594c2-213">**To assign Britta Simon to Zscaler Private Access (ZPA), perform the following steps:**</span></span>

1. <span data-ttu-id="594c2-214">No portal de gerenciamento do Azure, abra a exibição de aplicativos e, em seguida, navegue até o modo de exibição de diretório e vá para **aplicativos empresariais** e clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="594c2-214">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="594c2-216">Na lista de aplicativos, selecione **ZPA (Zscaler Private Access)**.</span><span class="sxs-lookup"><span data-stu-id="594c2-216">In the applications list, select **Zscaler Private Access (ZPA)**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_50.png) 

3. <span data-ttu-id="594c2-218">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="594c2-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="594c2-220">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="594c2-220">Click **Add** button.</span></span> <span data-ttu-id="594c2-221">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="594c2-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="594c2-223">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="594c2-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="594c2-224">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="594c2-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="594c2-225">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="594c2-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="594c2-226">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="594c2-226">Testing single sign-on</span></span>

<span data-ttu-id="594c2-227">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="594c2-227">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="594c2-228">Ao clicar no bloco do ZPA (Zscaler Private Access) no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo do ZPA (Zscaler Private Access).</span><span class="sxs-lookup"><span data-stu-id="594c2-228">When you click the Zscaler Private Access (ZPA) tile in the Access Panel, you should get automatically signed-on to your Zscaler Private Access (ZPA) application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="594c2-229">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="594c2-229">Additional resources</span></span>

* [<span data-ttu-id="594c2-230">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="594c2-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="594c2-231">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="594c2-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_203.png