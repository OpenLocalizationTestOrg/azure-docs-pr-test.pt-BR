---
title: "Tutorial: integração do Azure Active Directory ao T&E Express | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o T&E Express."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: B42374E5-2559-4309-8EF2-820BEE7EBB0C
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: jeedes
ms.openlocfilehash: 869e5284c71904fcc817ceee0f39d94fab1bc6f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-te-express"></a><span data-ttu-id="70b78-103">Tutorial: integração do Azure Active Directory com o T&E Express</span><span class="sxs-lookup"><span data-stu-id="70b78-103">Tutorial: Azure Active Directory integration with T&E Express</span></span>

<span data-ttu-id="70b78-104">Neste tutorial, você aprenderá a integrar o T&E Express ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="70b78-104">In this tutorial, you learn how to integrate T&E Express with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="70b78-105">A integração do T&E Express com o Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="70b78-105">Integrating T&E Express with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="70b78-106">No Azure AD, é possível controlar quem tem acesso ao T&E Express</span><span class="sxs-lookup"><span data-stu-id="70b78-106">You can control in Azure AD who has access to T&E Express</span></span>
- <span data-ttu-id="70b78-107">Você pode permitir que os usuários façam logon automaticamente no T&E Express (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="70b78-107">You can enable your users to automatically get signed-on to T&E Express (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="70b78-108">Você pode gerenciar suas contas em um único local - o portal de Gerenciamento do Azure</span><span class="sxs-lookup"><span data-stu-id="70b78-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="70b78-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="70b78-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="70b78-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="70b78-110">Prerequisites</span></span>

<span data-ttu-id="70b78-111">Para configurar a integração do Azure AD com o T&E Express, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="70b78-111">To configure Azure AD integration with T&E Express, you need the following items:</span></span>

- <span data-ttu-id="70b78-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="70b78-112">An Azure AD subscription</span></span>
- <span data-ttu-id="70b78-113">Uma assinatura habilitada para logon único do T&E Express</span><span class="sxs-lookup"><span data-stu-id="70b78-113">A T&E Express single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="70b78-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="70b78-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="70b78-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="70b78-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="70b78-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="70b78-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="70b78-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="70b78-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="70b78-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="70b78-118">Scenario description</span></span>
<span data-ttu-id="70b78-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="70b78-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="70b78-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="70b78-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="70b78-121">Adicionando o T&E Express da galeria</span><span class="sxs-lookup"><span data-stu-id="70b78-121">Adding T&E Express from the gallery</span></span>
2. <span data-ttu-id="70b78-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="70b78-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-te-express-from-the-gallery"></a><span data-ttu-id="70b78-123">Adicionando o T&E Express da galeria</span><span class="sxs-lookup"><span data-stu-id="70b78-123">Adding T&E Express from the gallery</span></span>
<span data-ttu-id="70b78-124">Para configurar a integração do T&E Express com o Azure AD, você precisa adicionar o T&E Express por meio da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="70b78-124">To configure the integration of T&E Express into Azure AD, you need to add T&E Express from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="70b78-125">**Para adicionar o T&E Express da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="70b78-125">**To add T&E Express from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="70b78-126">No **[Portal de Gerenciamento do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="70b78-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="70b78-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="70b78-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="70b78-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="70b78-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="70b78-131">Clique em **adicionar** botão na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="70b78-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="70b78-133">Na caixa de pesquisa, digite **T&E Express**.</span><span class="sxs-lookup"><span data-stu-id="70b78-133">In the search box, type **T&E Express**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_search.png)

5. <span data-ttu-id="70b78-135">No painel de resultados, selecione **T&E Express** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="70b78-135">In the results panel, select **T&E Express**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="70b78-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="70b78-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="70b78-138">Nesta seção, você configurará e testará o logon único do Azure AD com o T&E Express, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="70b78-138">In this section, you configure and test Azure AD single sign-on with T&E Express based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="70b78-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do T&E Express é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70b78-139">For single sign-on to work, Azure AD needs to know what the counterpart user in T&E Express is to a user in Azure AD.</span></span> <span data-ttu-id="70b78-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do T&E Express.</span><span class="sxs-lookup"><span data-stu-id="70b78-140">In other words, a link relationship between an Azure AD user and the related user in T&E Express needs to be established.</span></span>

<span data-ttu-id="70b78-141">Essa relação de vínculo é estabelecida atribuindo o valor do **nome de usuário** no Azure AD ao valor do **Nome de Usuário** no T&E Express.</span><span class="sxs-lookup"><span data-stu-id="70b78-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in T&E Express.</span></span>

<span data-ttu-id="70b78-142">Para configurar e testar o logon único do Azure AD com o T&E Express, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="70b78-142">To configure and test Azure AD single sign-on with T&E Express, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="70b78-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="70b78-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="70b78-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="70b78-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="70b78-145">**[Criando um usuário de teste do T&E Express](#creating-a-te-express-test-user)**: para ter um equivalente a Brenda Fernandes no T&E Express que esteja vinculado à sua representação no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70b78-145">**[Creating a T&E Express test user](#creating-a-te-express-test-user)** - to have a counterpart of Britta Simon in T&E Express that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="70b78-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** - para habilitar Britta Simon a usar o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="70b78-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="70b78-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="70b78-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="70b78-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="70b78-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="70b78-149">Nesta seção, você habilita o logon único do Azure AD no Portal de Gerenciamento do Azure e configura o logon único em seu aplicativo do T&E Express.</span><span class="sxs-lookup"><span data-stu-id="70b78-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your T&E Express application.</span></span>

<span data-ttu-id="70b78-150">**Para configurar o logon único do Azure AD com o T&E Express, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="70b78-150">**To configure Azure AD single sign-on with T&E Express, perform the following steps:**</span></span>

1. <span data-ttu-id="70b78-151">No Portal de Gerenciamento do Azure, na página de integração de aplicativo do **T&E Express**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="70b78-151">In the Azure Management portal, on the **T&E Express** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o logon único][4]

2. <span data-ttu-id="70b78-153">Na caixa de diálogo **Logon único**, como **Modo**, selecione **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="70b78-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurar o logon único](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_samlbase.png)

3. <span data-ttu-id="70b78-155">Na seção **URLs e Domínio do T&E Express**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="70b78-155">On the **T&E Express Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar o logon único](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_url.png)

    <span data-ttu-id="70b78-157">a.</span><span class="sxs-lookup"><span data-stu-id="70b78-157">a.</span></span> <span data-ttu-id="70b78-158">Na caixa de texto **Identificador**, digite o valor como `https://<domain>.tyeexpress.com`</span><span class="sxs-lookup"><span data-stu-id="70b78-158">In the **Identifier** textbox, type the value as: `https://<domain>.tyeexpress.com`</span></span>

    <span data-ttu-id="70b78-159">b.</span><span class="sxs-lookup"><span data-stu-id="70b78-159">b.</span></span> <span data-ttu-id="70b78-160">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`</span><span class="sxs-lookup"><span data-stu-id="70b78-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="70b78-161">Observe que esses não são os valores reais.</span><span class="sxs-lookup"><span data-stu-id="70b78-161">Please note that these are not the real values.</span></span> <span data-ttu-id="70b78-162">Você precisa atualizar esses valores com o Identificador e a URL de Resposta reais.</span><span class="sxs-lookup"><span data-stu-id="70b78-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="70b78-163">Aqui, sugerimos que você use o valor exclusivo de cadeia de caracteres no Identificador.</span><span class="sxs-lookup"><span data-stu-id="70b78-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="70b78-164">Entre em contato com a [Equipe de suporte do T&E Express](http://www.tyeexpress.com/contacto.aspx) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="70b78-164">Contact [T&E Express support team](http://www.tyeexpress.com/contacto.aspx) to get these values.</span></span>

5. <span data-ttu-id="70b78-165">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo XML em seu computador.</span><span class="sxs-lookup"><span data-stu-id="70b78-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_certificate.png) 

6. <span data-ttu-id="70b78-167">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="70b78-167">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="70b78-169">Para configurar o logon único usando o **T&E Express**, faça logon no aplicativo do T&E Express sem logon único com SAML usando credenciais de administrador.</span><span class="sxs-lookup"><span data-stu-id="70b78-169">To configure single sign-on on **T&E Express** side, login to the T&E express application without SAML single sign on using admin credentials.</span></span>

9. <span data-ttu-id="70b78-170">Na guia **Administrador**, clique em **Domínio SAML** para abrir a página de configurações de SAML.</span><span class="sxs-lookup"><span data-stu-id="70b78-170">Under the **Admin** Tab, Click on **SAML domain** to Open the SAML settings page.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tyeexpress-tutorial/tye-SAML.png)

10. <span data-ttu-id="70b78-172">Altere a opção **Ativar** de **Não** para **Sim**.</span><span class="sxs-lookup"><span data-stu-id="70b78-172">Select the **Activar(Activate)** option from **No** to **SI(Yes)**.</span></span> <span data-ttu-id="70b78-173">Na caixa de texto **Metadados do Provedor de Identidade**, cole o XML dos metadados que você baixou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="70b78-173">In the **Identity Provider Metadata** textbox, paste the metadata XML which you have donwloaded from Azure portal.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-tyeexpress-tutorial/tyeAdmin.png)

11. <span data-ttu-id="70b78-175">Clique no botão **Salvar** para salvar as configurações.</span><span class="sxs-lookup"><span data-stu-id="70b78-175">Click on the **Guardar(Save)** button to save the settings.</span></span> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="70b78-176">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="70b78-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="70b78-177">O objetivo desta seção é criar um usuário de teste no Portal de Gerenciamento do Azure chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="70b78-177">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="70b78-179">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="70b78-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="70b78-180">No **portal de Gerenciamento do Azure**, no painel navegação à esquerda, clique em **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="70b78-180">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="70b78-182">Vá para **usuários e grupos** e clique em **todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="70b78-182">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="70b78-184">Na parte superior da caixa de diálogo clique **adicionar** para abrir o **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="70b78-184">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="70b78-186">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="70b78-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="70b78-188">a.</span><span class="sxs-lookup"><span data-stu-id="70b78-188">a.</span></span> <span data-ttu-id="70b78-189">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="70b78-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="70b78-190">b.</span><span class="sxs-lookup"><span data-stu-id="70b78-190">b.</span></span> <span data-ttu-id="70b78-191">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="70b78-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="70b78-192">c.</span><span class="sxs-lookup"><span data-stu-id="70b78-192">c.</span></span> <span data-ttu-id="70b78-193">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="70b78-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="70b78-194">d.</span><span class="sxs-lookup"><span data-stu-id="70b78-194">d.</span></span> <span data-ttu-id="70b78-195">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="70b78-195">Click **Create**.</span></span>
 
### <a name="creating-a-te-express-test-user"></a><span data-ttu-id="70b78-196">Criar um usuário de teste do T&E Express</span><span class="sxs-lookup"><span data-stu-id="70b78-196">Creating a T&E Express test user</span></span>

<span data-ttu-id="70b78-197">A fim de permitir que os usuários do Azure AD façam logon no T&E Express, eles devem ser provisionados no T&E Express.</span><span class="sxs-lookup"><span data-stu-id="70b78-197">In order to enable Azure AD users to log into T&E Express, they must be provisioned into T&E Express.</span></span>  
<span data-ttu-id="70b78-198">No caso do T&E Express, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="70b78-198">In case of T&E Express, provisioning is a manual task.</span></span>

<span data-ttu-id="70b78-199">**Para provisionar contas de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="70b78-199">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="70b78-200">Faça logon no site da empresa do T&E Express como administrador.</span><span class="sxs-lookup"><span data-stu-id="70b78-200">Log in to your T&E Express company site as an administrator.</span></span>

2. <span data-ttu-id="70b78-201">Na guia Administrador, clique em Usuários para abrir a página mestra de Usuários.</span><span class="sxs-lookup"><span data-stu-id="70b78-201">Under Admin tag, click on Users to open the Users master page.</span></span>

    ![Adicionar Funcionário](./media/active-directory-saas-tyeexpress-tutorial/tye-adminusers.png)

3. <span data-ttu-id="70b78-203">Na página inicial, clique em **+** para adicionar os usuários.</span><span class="sxs-lookup"><span data-stu-id="70b78-203">On the home page, click on **+** to add the users.</span></span>

    ![Adicionar Funcionário](./media/active-directory-saas-tyeexpress-tutorial/tye-usershome.png)

4. <span data-ttu-id="70b78-205">Insira todos os detalhes obrigatórios conforme solicitado no formulário e clique no botão Salvar para salvar os detalhes.</span><span class="sxs-lookup"><span data-stu-id="70b78-205">Enter all the mandatory details as asked in the form and click the save button to save the details.</span></span>

    ![Adicionar Funcionário](./media/active-directory-saas-tyeexpress-tutorial/tye-usersadd.png)

    ![Adicionar Funcionário](./media/active-directory-saas-tyeexpress-tutorial/tye-userssave.png)


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="70b78-208">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="70b78-208">Assigning the Azure AD test user</span></span>

<span data-ttu-id="70b78-209">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao T&E Express.</span><span class="sxs-lookup"><span data-stu-id="70b78-209">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to T&E Express.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="70b78-211">**Para atribuir Brenda Fernandes ao T&E Express, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="70b78-211">**To assign Britta Simon to T&E Express, perform the following steps:**</span></span>

1. <span data-ttu-id="70b78-212">No portal de gerenciamento do Azure, abra a exibição de aplicativos e, em seguida, navegue até o modo de exibição de diretório e vá para **aplicativos empresariais** e clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="70b78-212">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="70b78-214">Na lista de aplicativos, selecione **T&E Express**.</span><span class="sxs-lookup"><span data-stu-id="70b78-214">In the applications list, select **T&E Express**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_app.png) 

3. <span data-ttu-id="70b78-216">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="70b78-216">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="70b78-218">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="70b78-218">Click **Add** button.</span></span> <span data-ttu-id="70b78-219">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="70b78-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="70b78-221">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="70b78-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="70b78-222">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="70b78-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="70b78-223">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="70b78-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="70b78-224">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="70b78-224">Testing single sign-on</span></span>

<span data-ttu-id="70b78-225">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="70b78-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="70b78-226">Quando clicar no bloco T&E Express no Painel de Acesso, você deve ser conectado automaticamente ao seu aplicativo T&E Express.</span><span class="sxs-lookup"><span data-stu-id="70b78-226">When you click the T&E Express tile in the Access Panel, you should get automatically signed-on to your T&E Express application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="70b78-227">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="70b78-227">Additional resources</span></span>

* [<span data-ttu-id="70b78-228">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="70b78-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="70b78-229">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="70b78-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_203.png

