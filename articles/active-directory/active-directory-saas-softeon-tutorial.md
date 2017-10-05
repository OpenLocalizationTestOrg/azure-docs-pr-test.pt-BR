---
title: "Tutorial: integração do Azure Active Directory ao Softeon WMS | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Softeon WMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 07c5de0d-90aa-43b3-b24e-0cc334b2f9b0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: jeedes
ms.openlocfilehash: 87714bbcb317395563033d2f0ebc60aaa0ff0e10
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-softeon-wms"></a><span data-ttu-id="38fbf-103">Tutorial: integração do Azure Active Directory com o Softeon WMS</span><span class="sxs-lookup"><span data-stu-id="38fbf-103">Tutorial: Azure Active Directory integration with Softeon WMS</span></span>

<span data-ttu-id="38fbf-104">Neste tutorial, você aprenderá a integrar o Softeon WMS ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="38fbf-104">In this tutorial, you learn how to integrate Softeon WMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="38fbf-105">A integração do Softeon WMS ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="38fbf-105">Integrating Softeon WMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="38fbf-106">No Azure AD, é possível controlar quem tem acesso ao Softeon WMS</span><span class="sxs-lookup"><span data-stu-id="38fbf-106">You can control in Azure AD who has access to Softeon WMS</span></span>
- <span data-ttu-id="38fbf-107">Você pode permitir que seus usuários entrem automaticamente no Softeon WMS (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="38fbf-107">You can enable your users to automatically get signed-on to Softeon WMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="38fbf-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="38fbf-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="38fbf-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="38fbf-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38fbf-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="38fbf-110">Prerequisites</span></span>

<span data-ttu-id="38fbf-111">Para configurar a integração do Azure AD ao Softeon WMS, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="38fbf-111">To configure Azure AD integration with Softeon WMS, you need the following items:</span></span>

- <span data-ttu-id="38fbf-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="38fbf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="38fbf-113">Uma assinatura habilitada para logon único do Softeon WMS</span><span class="sxs-lookup"><span data-stu-id="38fbf-113">A Softeon WMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="38fbf-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="38fbf-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="38fbf-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="38fbf-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="38fbf-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="38fbf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="38fbf-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="38fbf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="38fbf-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="38fbf-118">Scenario description</span></span>
<span data-ttu-id="38fbf-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="38fbf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="38fbf-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="38fbf-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="38fbf-121">Adicionando o Softeon WMS da galeria</span><span class="sxs-lookup"><span data-stu-id="38fbf-121">Adding Softeon WMS from the gallery</span></span>
2. <span data-ttu-id="38fbf-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="38fbf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-softeon-wms-from-the-gallery"></a><span data-ttu-id="38fbf-123">Adicionando o Softeon WMS da galeria</span><span class="sxs-lookup"><span data-stu-id="38fbf-123">Adding Softeon WMS from the gallery</span></span>
<span data-ttu-id="38fbf-124">Para configurar a integração do Softeon WMS ao Azure AD, você precisará adicionar o Softeon WMS da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="38fbf-124">To configure the integration of Softeon WMS into Azure AD, you need to add Softeon WMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="38fbf-125">**Para adicionar o Softeon WMS da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="38fbf-125">**To add Softeon WMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="38fbf-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="38fbf-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="38fbf-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="38fbf-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="38fbf-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="38fbf-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="38fbf-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="38fbf-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="38fbf-133">Na caixa de pesquisa, digite **Softeon WMS**.</span><span class="sxs-lookup"><span data-stu-id="38fbf-133">In the search box, type **Softeon WMS**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-softeon-tutorial/tutorial_softeon_search.png)

5. <span data-ttu-id="38fbf-135">No painel de resultados, selecione **Softeon WMS** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="38fbf-135">In the results panel, select **Softeon WMS**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-softeon-tutorial/tutorial_softeon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="38fbf-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="38fbf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="38fbf-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Softeon WMS, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="38fbf-138">In this section, you configure and test Azure AD single sign-on with Softeon WMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="38fbf-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Softeon WMS é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="38fbf-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Softeon WMS is to a user in Azure AD.</span></span> <span data-ttu-id="38fbf-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Softeon WMS.</span><span class="sxs-lookup"><span data-stu-id="38fbf-140">In other words, a link relationship between an Azure AD user and the related user in Softeon WMS needs to be established.</span></span>

<span data-ttu-id="38fbf-141">No Softeon WMS, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="38fbf-141">In Softeon WMS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="38fbf-142">Para configurar e testar o logon único do Azure AD com o Softeon WMS, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="38fbf-142">To configure and test Azure AD single sign-on with Softeon WMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="38fbf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="38fbf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="38fbf-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="38fbf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="38fbf-145">**[Criação um usuário de teste do Softeon WMS](#creating-a-softeon-wms-test-user)** – para ter um equivalente de Brenda Fernandes no Softeon WMS que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="38fbf-145">**[Creating a Softeon WMS test user](#creating-a-softeon-wms-test-user)** - to have a counterpart of Britta Simon in Softeon WMS that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="38fbf-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="38fbf-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="38fbf-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="38fbf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="38fbf-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="38fbf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="38fbf-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Softeon WMS.</span><span class="sxs-lookup"><span data-stu-id="38fbf-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Softeon WMS application.</span></span>

<span data-ttu-id="38fbf-150">**Para configurar o logon único do Azure AD com o Softeon WMS, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="38fbf-150">**To configure Azure AD single sign-on with Softeon WMS, perform the following steps:**</span></span>

1. <span data-ttu-id="38fbf-151">No portal do Azure, na página de integração de aplicativos do **Softeon WMS**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="38fbf-151">In the Azure portal, on the **Softeon WMS** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="38fbf-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="38fbf-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-softeon-tutorial/tutorial_softeon_samlbase.png)

3. <span data-ttu-id="38fbf-155">Na seção **URLs e Domínio do Softeon WMS**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="38fbf-155">On the **Softeon WMS Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-softeon-tutorial/tutorial_softeon_url.png)

    <span data-ttu-id="38fbf-157">a.</span><span class="sxs-lookup"><span data-stu-id="38fbf-157">a.</span></span> <span data-ttu-id="38fbf-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<companyname>.softeon.com/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="38fbf-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.softeon.com/<instancename>`</span></span>

    <span data-ttu-id="38fbf-159">b.</span><span class="sxs-lookup"><span data-stu-id="38fbf-159">b.</span></span> <span data-ttu-id="38fbf-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<companyname>.softeon.com/sp`</span><span class="sxs-lookup"><span data-stu-id="38fbf-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.softeon.com/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="38fbf-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="38fbf-161">These values are not real.</span></span> <span data-ttu-id="38fbf-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="38fbf-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="38fbf-163">Contate a [equipe de suporte do cliente Softeon WMS](mailto:contact@softeon.com) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="38fbf-163">Contact [Softeon WMS Client support team](mailto:contact@softeon.com) to get these values.</span></span> 
 
4. <span data-ttu-id="38fbf-164">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="38fbf-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-softeon-tutorial/tutorial_softeon_certificate.png) 

5. <span data-ttu-id="38fbf-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="38fbf-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-softeon-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="38fbf-168">Na seção **Configuração do Softeon WMS**, clique em **Configurar Softeon WMS** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="38fbf-168">On the **Softeon WMS Configuration** section, click **Configure Softeon WMS** to open **Configure sign-on** window.</span></span> <span data-ttu-id="38fbf-169">Copie a **ID da Entidade SAML e a URL do Serviço de Logon Único do SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="38fbf-169">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-softeon-tutorial/tutorial_softeon_configure.png) 

7. <span data-ttu-id="38fbf-171">Para configurar o logon único no lado do **Softeon WMS**, é necessário enviar o **Certificado (Base64) baixado, a URL do Serviço de Logon Único do SAML e a ID da Entidade do SAML** para a [equipe de suporte do Softeon WMS](mailto:contact@softeon.com).</span><span class="sxs-lookup"><span data-stu-id="38fbf-171">To configure single sign-on on **Softeon WMS** side, you need to send the downloaded **Certificate (Base64), SAML Entity ID, and SAML Single Sign-On Service URL** to [Softeon WMS support team](mailto:contact@softeon.com).</span></span> <span data-ttu-id="38fbf-172">Eles definem essa configuração para ter a conexão de SSO do SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="38fbf-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="38fbf-173">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="38fbf-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="38fbf-174">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="38fbf-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="38fbf-175">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="38fbf-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="38fbf-176">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="38fbf-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="38fbf-177">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="38fbf-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="38fbf-179">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="38fbf-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="38fbf-180">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="38fbf-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-softeon-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="38fbf-182">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="38fbf-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-softeon-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="38fbf-184">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="38fbf-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-softeon-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="38fbf-186">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="38fbf-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-softeon-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="38fbf-188">a.</span><span class="sxs-lookup"><span data-stu-id="38fbf-188">a.</span></span> <span data-ttu-id="38fbf-189">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="38fbf-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="38fbf-190">b.</span><span class="sxs-lookup"><span data-stu-id="38fbf-190">b.</span></span> <span data-ttu-id="38fbf-191">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="38fbf-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="38fbf-192">c.</span><span class="sxs-lookup"><span data-stu-id="38fbf-192">c.</span></span> <span data-ttu-id="38fbf-193">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="38fbf-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="38fbf-194">d.</span><span class="sxs-lookup"><span data-stu-id="38fbf-194">d.</span></span> <span data-ttu-id="38fbf-195">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="38fbf-195">Click **Create**.</span></span>
 
### <a name="creating-a-softeon-wms-test-user"></a><span data-ttu-id="38fbf-196">Criar um usuário de teste do Softeon WMS</span><span class="sxs-lookup"><span data-stu-id="38fbf-196">Creating a Softeon WMS test user</span></span>

<span data-ttu-id="38fbf-197">O aplicativo dá suporte ao provisionamento de usuário Just-In-Time e, após a autenticação, os usuários são criados no aplicativo automaticamente.</span><span class="sxs-lookup"><span data-stu-id="38fbf-197">Application supports Just in time user provisioning and after authentication users are created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="38fbf-198">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="38fbf-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="38fbf-199">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Softeon WMS.</span><span class="sxs-lookup"><span data-stu-id="38fbf-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Softeon WMS.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="38fbf-201">**Para atribuir Brenda Fernandes ao Softeon WMS, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="38fbf-201">**To assign Britta Simon to Softeon WMS, perform the following steps:**</span></span>

1. <span data-ttu-id="38fbf-202">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="38fbf-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="38fbf-204">Na lista de aplicativos, selecione **Softeon WMS**.</span><span class="sxs-lookup"><span data-stu-id="38fbf-204">In the applications list, select **Softeon WMS**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-softeon-tutorial/tutorial_softeon_app.png) 

3. <span data-ttu-id="38fbf-206">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="38fbf-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="38fbf-208">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="38fbf-208">Click **Add** button.</span></span> <span data-ttu-id="38fbf-209">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="38fbf-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="38fbf-211">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="38fbf-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="38fbf-212">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="38fbf-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="38fbf-213">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="38fbf-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="38fbf-214">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="38fbf-214">Testing single sign-on</span></span>

<span data-ttu-id="38fbf-215">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="38fbf-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="38fbf-216">Ao clicar no bloco Softeon WMS no Painel de Acesso, você deve acessar a página de logon do aplicativo Softeon WMS.</span><span class="sxs-lookup"><span data-stu-id="38fbf-216">When you click the Softeon WMS tile in the Access Panel, you should get login page of Softeon WMS application.</span></span>
<span data-ttu-id="38fbf-217">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="38fbf-217">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="38fbf-218">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="38fbf-218">Additional resources</span></span>

* [<span data-ttu-id="38fbf-219">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="38fbf-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="38fbf-220">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="38fbf-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-softeon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-softeon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-softeon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-softeon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-softeon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-softeon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-softeon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-softeon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-softeon-tutorial/tutorial_general_203.png

