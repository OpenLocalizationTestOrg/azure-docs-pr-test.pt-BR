---
title: "Tutorial: Integração do Azure Active Directory ao Velpic SAML | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Velpic SAML."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 5325f3cca00167e6b7b687509ce43435447ad2f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-velpic-saml"></a><span data-ttu-id="63879-103">Tutorial: Integração do Azure Active Directory ao Velpic SAML</span><span class="sxs-lookup"><span data-stu-id="63879-103">Tutorial: Azure Active Directory integration with Velpic SAML</span></span>

<span data-ttu-id="63879-104">Neste tutorial, você aprenderá a integrar o Velpic SAML ao Azure AD (Active Directory).</span><span class="sxs-lookup"><span data-stu-id="63879-104">In this tutorial, you learn how to integrate Velpic SAML with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="63879-105">A integração do Velpic SAML ao Azure AD proporciona os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="63879-105">Integrating Velpic SAML with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="63879-106">No Azure AD, você pode controlar quem tem acesso ao Velpic SAML</span><span class="sxs-lookup"><span data-stu-id="63879-106">You can control in Azure AD who has access to Velpic SAML</span></span>
- <span data-ttu-id="63879-107">Você pode permitir que os usuários façam logon automaticamente no Velpic SAML (Logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="63879-107">You can enable your users to automatically get signed-on to Velpic SAML (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="63879-108">Você pode gerenciar suas contas em um único local - o portal de Gerenciamento do Azure</span><span class="sxs-lookup"><span data-stu-id="63879-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="63879-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="63879-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="63879-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="63879-110">Prerequisites</span></span>

<span data-ttu-id="63879-111">Para configurar a integração do Azure AD ao Velpic SAML, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="63879-111">To configure Azure AD integration with Velpic SAML, you need the following items:</span></span>

- <span data-ttu-id="63879-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="63879-112">An Azure AD subscription</span></span>
- <span data-ttu-id="63879-113">Uma assinatura do Velpic SAML habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="63879-113">A Velpic SAML single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="63879-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="63879-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="63879-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="63879-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="63879-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="63879-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="63879-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="63879-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="63879-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="63879-118">Scenario description</span></span>
<span data-ttu-id="63879-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="63879-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="63879-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="63879-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="63879-121">Adicionando Velpic SAML usando a galeria</span><span class="sxs-lookup"><span data-stu-id="63879-121">Adding Velpic SAML from the gallery</span></span>
2. <span data-ttu-id="63879-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="63879-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-velpic-saml-from-the-gallery"></a><span data-ttu-id="63879-123">Adicionando Velpic SAML usando a galeria</span><span class="sxs-lookup"><span data-stu-id="63879-123">Adding Velpic SAML from the gallery</span></span>
<span data-ttu-id="63879-124">Para configurar a integração do Velpic SAML ao Azure AD, você precisa adicionar o Velpic SAML da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="63879-124">To configure the integration of Velpic SAML into Azure AD, you need to add Velpic SAML from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="63879-125">**Para adicionar o Velpic SAML da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="63879-125">**To add Velpic SAML from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="63879-126">No **[Portal de Gerenciamento do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="63879-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="63879-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="63879-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="63879-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="63879-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="63879-131">Clique em **adicionar** botão na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="63879-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="63879-133">Na caixa de pesquisa, digite **Velpic SAML**.</span><span class="sxs-lookup"><span data-stu-id="63879-133">In the search box, type **Velpic SAML**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_search.png)

5. <span data-ttu-id="63879-135">No painel de resultados, selecione **Velpic SAML** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="63879-135">In the results panel, select **Velpic SAML**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="63879-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="63879-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="63879-138">Nesta seção, você configura e testa o logon único do Azure AD com o Velpic SAML, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="63879-138">In this section, you configure and test Azure AD single sign-on with Velpic SAML based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="63879-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Velpic SAML é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="63879-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Velpic SAML is to a user in Azure AD.</span></span> <span data-ttu-id="63879-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="63879-140">In other words, a link relationship between an Azure AD user and the related user in Velpic SAML needs to be established.</span></span>

<span data-ttu-id="63879-141">Essa relação de vínculo é estabelecida atribuindo o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** no Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="63879-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Velpic SAML.</span></span>

<span data-ttu-id="63879-142">Para configurar e testar o logon único do Azure AD com o Velpic SAML, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="63879-142">To configure and test Azure AD single sign-on with Velpic SAML, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="63879-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="63879-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="63879-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="63879-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="63879-145">**[Criação de um usuário de teste do Velpic SAML](#creating-a-velpic-saml-test-user)** - para ter um equivalente de Brenda Fernandes no Velpic SAML que esteja vinculado à representação dela no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="63879-145">**[Creating a Velpic SAML test user](#creating-a-velpic-saml-test-user)** - to have a counterpart of Britta Simon in Velpic SAML that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="63879-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** - para habilitar Britta Simon a usar o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="63879-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="63879-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="63879-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="63879-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="63879-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="63879-149">Nesta seção, você habilita o logon único do Azure AD no portal de Gerenciamento do Azure e o configura em seu aplicativo Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="63879-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Velpic SAML application.</span></span>

<span data-ttu-id="63879-150">**Para configurar o logon único do Azure AD com o Velpic SAML, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="63879-150">**To configure Azure AD single sign-on with Velpic SAML, perform the following steps:**</span></span>

1. <span data-ttu-id="63879-151">No portal de Gerenciamento do Azure, na página de integração do aplicativo **Velpic SAML**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="63879-151">In the Azure Management portal, on the **Velpic SAML** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o logon único][4]

2. <span data-ttu-id="63879-153">Na caixa de diálogo **Logon único**, como **Modo**, selecione **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="63879-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_samlbase.png)

3. <span data-ttu-id="63879-155">Insira os detalhes na seção **Domínio e URLs do Velpic SAML**</span><span class="sxs-lookup"><span data-stu-id="63879-155">Enter the details in the **Velpic SAML Domain and URLs** section-</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_url.png)

    <span data-ttu-id="63879-157">a.</span><span class="sxs-lookup"><span data-stu-id="63879-157">a.</span></span> <span data-ttu-id="63879-158">Na caixa de texto **URL de Logon**, digite o valor como: `https://<sub-domain>.velpicsaml.net`</span><span class="sxs-lookup"><span data-stu-id="63879-158">In the **Sign-on URL** textbox, type the value as: `https://<sub-domain>.velpicsaml.net`</span></span>

    <span data-ttu-id="63879-159">b.</span><span class="sxs-lookup"><span data-stu-id="63879-159">b.</span></span> <span data-ttu-id="63879-160">Na caixa de texto **Identificador**, cole o valor de **"URL do logon único"** `https://auth.velpic.com/saml/v2/<entity-id>/login`</span><span class="sxs-lookup"><span data-stu-id="63879-160">In the **Identifier** textbox, paste the **‘Single sign on URL’** value `https://auth.velpic.com/saml/v2/<entity-id>/login`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="63879-161">Observe que a URL de Logon será fornecida pela equipe do Velpic SAML e o valor do Identificador estará disponível quando você configurar o Plug-in do SSO no lado do Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="63879-161">Please note that the Sign on URL will be provided by the Velpic SAML team and Identifier value will be available when you configure the SSO Plugin on Velpic SAML side.</span></span> <span data-ttu-id="63879-162">É preciso copiar esse valor na página do aplicativo Velpic SAML e colá-lo aqui.</span><span class="sxs-lookup"><span data-stu-id="63879-162">You need to copy that value from Velpic SAML application  page and paste it here.</span></span>

4. <span data-ttu-id="63879-163">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo XML em seu computador.</span><span class="sxs-lookup"><span data-stu-id="63879-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_certificate.png) 

5. <span data-ttu-id="63879-165">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="63879-165">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="63879-167">Na seção Configuração do Velpic SAML, clique em Configurar o Velpic SAML para abrir a janela Configurar logon.</span><span class="sxs-lookup"><span data-stu-id="63879-167">On the Velpic SAML Configuration section, click Configure Velpic SAML to open Configure sign-on window.</span></span> <span data-ttu-id="63879-168">Copie a ID da Entidade SAML da seção Referência Rápida.</span><span class="sxs-lookup"><span data-stu-id="63879-168">Copy the SAML Entity ID from the Quick Reference section.</span></span>

7. <span data-ttu-id="63879-169">Em uma janela diferente do navegador da Web, faça logon no site do Velpic SAML na sua empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="63879-169">In a different web browser window, log into your Velpic SAML company site as an administrator.</span></span>

8. <span data-ttu-id="63879-170">Clique na guia **Gerenciar** e vá para a seção **Integração**, onde você pode clicar no botão **Plug-ins** para criar novo plug-in para Conectar.</span><span class="sxs-lookup"><span data-stu-id="63879-170">Click on **Manage** tab and go to **Integration** section where you need to click on **Plugins** button to create new plugin for Sign-In.</span></span>

    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_1.png)

9. <span data-ttu-id="63879-172">Clique no botão **"Adicionar plug-in"**.</span><span class="sxs-lookup"><span data-stu-id="63879-172">Click on the **‘Add plugin’** button.</span></span>
    
    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_2.png)

10. <span data-ttu-id="63879-174">Clique no bloco **SAML** na página Adicionar Plug-in.</span><span class="sxs-lookup"><span data-stu-id="63879-174">Click on the **SAML** tile in the Add Plugin page.</span></span>
    
    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_3.png)

11. <span data-ttu-id="63879-176">Insira o nome do novo plug-in SAML e clique no botão **"Adicionar"**.</span><span class="sxs-lookup"><span data-stu-id="63879-176">Enter the name of the new SAML plugin and click the **‘Add’** button.</span></span>

    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_4.png)

12. <span data-ttu-id="63879-178">Insira os detalhes da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="63879-178">Enter the details as follows:</span></span>

    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_5.png)

    <span data-ttu-id="63879-180">a.</span><span class="sxs-lookup"><span data-stu-id="63879-180">a.</span></span> <span data-ttu-id="63879-181">Na caixa de texto **Nome**, digite o nome do plug-in SAML.</span><span class="sxs-lookup"><span data-stu-id="63879-181">In the **Name** textbox, type the name of SAML plugin.</span></span>

    <span data-ttu-id="63879-182">b.</span><span class="sxs-lookup"><span data-stu-id="63879-182">b.</span></span> <span data-ttu-id="63879-183">Na caixa de texto **URL do Emissor**, cole a **ID da Entidade SAML** que copiou da janela **Configurar logon** no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="63879-183">In the **Issuer URL** textbox, paste the **SAML Entity ID** you copied from the **Configure sign-on** window of the Azure portal.</span></span>

    <span data-ttu-id="63879-184">c.</span><span class="sxs-lookup"><span data-stu-id="63879-184">c.</span></span> <span data-ttu-id="63879-185">Em **Configuração dos Metadados do Provedor**, faça upload do arquivo XML de Metadados que você baixou no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="63879-185">In the **Provider Metadata Config** upload the Metadata XML file which you downloaded from Azure portal.</span></span>

    <span data-ttu-id="63879-186">d.</span><span class="sxs-lookup"><span data-stu-id="63879-186">d.</span></span> <span data-ttu-id="63879-187">Você também pode optar por habilitar o SAML apenas durante o provisionamento, habilitando a caixa de seleção **"Criar automaticamente novos usuários"**.</span><span class="sxs-lookup"><span data-stu-id="63879-187">You can also choose to enable SAML just in time provisioning by enabling the **‘Auto create new users’** checkbox.</span></span> <span data-ttu-id="63879-188">Se um usuário não existir no Velpic e esse sinalizador não estiver habilitado, o logon no Azure falhará.</span><span class="sxs-lookup"><span data-stu-id="63879-188">If a user doesn’t exist in Velpic and this flag is not enabled, the login from Azure will fail.</span></span> <span data-ttu-id="63879-189">Se o sinalizador estiver habilitado, o usuário será provisionado automaticamente no Velpic no momento do logon.</span><span class="sxs-lookup"><span data-stu-id="63879-189">If the flag is enabled the user will automatically be provisioned into Velpic at the time of login.</span></span> 

    <span data-ttu-id="63879-190">e.</span><span class="sxs-lookup"><span data-stu-id="63879-190">e.</span></span> <span data-ttu-id="63879-191">Copie a **URL de logon único** da caixa de texto e cole-a no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="63879-191">Copy the **Single sign on URL** from the text box and paste it in the Azure portal.</span></span>
    
    <span data-ttu-id="63879-192">f.</span><span class="sxs-lookup"><span data-stu-id="63879-192">f.</span></span> <span data-ttu-id="63879-193">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="63879-193">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="63879-194">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="63879-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="63879-195">O objetivo desta seção é criar um usuário de teste no Portal de Gerenciamento do Azure chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="63879-195">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="63879-197">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="63879-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="63879-198">No **portal de Gerenciamento do Azure**, no painel navegação à esquerda, clique em **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="63879-198">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="63879-200">Vá para **usuários e grupos** e clique em **todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="63879-200">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="63879-202">Na parte superior da caixa de diálogo clique **adicionar** para abrir o **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="63879-202">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="63879-204">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="63879-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="63879-206">a.</span><span class="sxs-lookup"><span data-stu-id="63879-206">a.</span></span> <span data-ttu-id="63879-207">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="63879-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="63879-208">b.</span><span class="sxs-lookup"><span data-stu-id="63879-208">b.</span></span> <span data-ttu-id="63879-209">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="63879-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="63879-210">c.</span><span class="sxs-lookup"><span data-stu-id="63879-210">c.</span></span> <span data-ttu-id="63879-211">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="63879-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="63879-212">d.</span><span class="sxs-lookup"><span data-stu-id="63879-212">d.</span></span> <span data-ttu-id="63879-213">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="63879-213">Click **Create**.</span></span>
 
### <a name="creating-a-velpic-saml-test-user"></a><span data-ttu-id="63879-214">Criando um usuário de teste no Velpic SAML</span><span class="sxs-lookup"><span data-stu-id="63879-214">Creating a Velpic SAML test user</span></span>

<span data-ttu-id="63879-215">Normalmente, esta etapa não é necessária, pois o aplicativo dá suporte ao provisionamento de usuário na hora certa.</span><span class="sxs-lookup"><span data-stu-id="63879-215">This step is usually not required as the application supports just in time user provisioning.</span></span> <span data-ttu-id="63879-216">Se o provisionamento automático de usuário não estiver habilitado, a criação manual do usuário poderá ser feita como descrito abaixo.</span><span class="sxs-lookup"><span data-stu-id="63879-216">If the automatic user provisioning is not enabled then manual user creation can be done as described below.</span></span>

<span data-ttu-id="63879-217">Entre no site da empresa do seu Velpic SAML como um administrador e execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="63879-217">Log into your Velpic SAML company site as an administrator and perform following steps:</span></span>
    
1. <span data-ttu-id="63879-218">Clique na guia Gerenciar, vá para a seção Usuários e clique no botão Novo para adicionar usuários.</span><span class="sxs-lookup"><span data-stu-id="63879-218">Click on Manage tab and go to Users section, then click on New button to add users.</span></span>

    ![adicionar usuário](./media/active-directory-saas-velpicsaml-tutorial/velpic_7.png)

2. <span data-ttu-id="63879-220">Na página da caixa de diálogo **"Criar Novo Usuário"**, execute as etapas que se seguem.</span><span class="sxs-lookup"><span data-stu-id="63879-220">On the **“Create New User”** dialog page, perform the following steps.</span></span>

    ![usuário](./media/active-directory-saas-velpicsaml-tutorial/velpic_8.png)
    
    <span data-ttu-id="63879-222">a.</span><span class="sxs-lookup"><span data-stu-id="63879-222">a.</span></span> <span data-ttu-id="63879-223">Na caixa de texto **Nome**, digite o nome de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="63879-223">In the **First Name** textbox, type the first name of Britta Simon.</span></span>

    <span data-ttu-id="63879-224">b.</span><span class="sxs-lookup"><span data-stu-id="63879-224">b.</span></span> <span data-ttu-id="63879-225">Na caixa de texto **Sobrenome**, digite o sobrenome de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="63879-225">In the **Last Name** textbox, type the last name of Britta Simon.</span></span>

    <span data-ttu-id="63879-226">c.</span><span class="sxs-lookup"><span data-stu-id="63879-226">c.</span></span> <span data-ttu-id="63879-227">Na caixa de texto **Nome de Usuário**, digite o nome de usuário de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="63879-227">In the **User Name** textbox, type the user name of Britta Simon.</span></span>

    <span data-ttu-id="63879-228">d.</span><span class="sxs-lookup"><span data-stu-id="63879-228">d.</span></span> <span data-ttu-id="63879-229">Na caixa de texto **Email**, digite o endereço de email da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="63879-229">In the **Email** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="63879-230">e.</span><span class="sxs-lookup"><span data-stu-id="63879-230">e.</span></span> <span data-ttu-id="63879-231">O restante das informações é opcional, você pode preenchê-las se necessário.</span><span class="sxs-lookup"><span data-stu-id="63879-231">Rest of the information is optional, you can fill it if needed.</span></span>
    
    <span data-ttu-id="63879-232">f.</span><span class="sxs-lookup"><span data-stu-id="63879-232">f.</span></span> <span data-ttu-id="63879-233">Clique em **SALVAR**.</span><span class="sxs-lookup"><span data-stu-id="63879-233">Click **SAVE**.</span></span>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="63879-234">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="63879-234">Assigning the Azure AD test user</span></span>

<span data-ttu-id="63879-235">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure, concedendo a ela acesso ao Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="63879-235">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Velpic SAML.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="63879-237">**Para atribuir Brenda Fernandes ao Velpic SAML, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="63879-237">**To assign Britta Simon to Velpic SAML, perform the following steps:**</span></span>

1. <span data-ttu-id="63879-238">No portal de gerenciamento do Azure, abra a exibição de aplicativos e, em seguida, navegue até o modo de exibição de diretório e vá para **aplicativos empresariais** e clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="63879-238">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="63879-240">Na lista de aplicativos, selecione **Velpic SAML**.</span><span class="sxs-lookup"><span data-stu-id="63879-240">In the applications list, select **Velpic SAML**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_app.png) 

3. <span data-ttu-id="63879-242">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="63879-242">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="63879-244">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="63879-244">Click **Add** button.</span></span> <span data-ttu-id="63879-245">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="63879-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="63879-247">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="63879-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="63879-248">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="63879-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="63879-249">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="63879-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="63879-250">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="63879-250">Testing single sign-on</span></span>

<span data-ttu-id="63879-251">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="63879-251">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

1. <span data-ttu-id="63879-252">Ao clicar no bloco Velpic SAML no Painel de Acesso, você deve acessar a página de logon do aplicativo Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="63879-252">When you click the Velpic SAML tile in the Access Panel, you should get login page of Velpic SAML application.</span></span> <span data-ttu-id="63879-253">Você deve ver o botão **"Fazer logon com Azure AD"** na página de entrada.</span><span class="sxs-lookup"><span data-stu-id="63879-253">You should see the **‘Log In With Azure AD’** button on the sign in page.</span></span>

    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_6.png)

2. <span data-ttu-id="63879-255">Clique no botão **"Fazer logon com Azure AD"** para entrar no Velpic usando sua conta do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="63879-255">Click on the **‘Log In With Azure AD’** button to log in to Velpic using your Azure AD account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="63879-256">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="63879-256">Additional resources</span></span>

* [<span data-ttu-id="63879-257">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="63879-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="63879-258">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="63879-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_203.png

