---
title: "Tutorial: Integração do Azure Active Directory ao Nexonia | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Nexonia."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a93b771a-9bc3-444a-bdc0-457f8bb7e780
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/1/2017
ms.author: jeedes
ms.openlocfilehash: 1370fa64c2ddc25d3121c567ceea4828b1e50921
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-nexonia"></a><span data-ttu-id="a564e-103">Tutorial: Integração do Azure Active Directory ao Nexonia</span><span class="sxs-lookup"><span data-stu-id="a564e-103">Tutorial: Azure Active Directory integration with Nexonia</span></span>

<span data-ttu-id="a564e-104">Neste tutorial, você aprenderá a integrar o Nexonia ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="a564e-104">In this tutorial, you learn how to integrate Nexonia with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a564e-105">A integração do Nexonia ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="a564e-105">Integrating Nexonia with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a564e-106">No Azure AD, você pode controlar quem tem acesso ao Nexonia</span><span class="sxs-lookup"><span data-stu-id="a564e-106">You can control in Azure AD who has access to Nexonia</span></span>
- <span data-ttu-id="a564e-107">Você pode permitir que seus usuários faça logon automaticamente no Nexonia (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a564e-107">You can enable your users to automatically get signed-on to Nexonia (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a564e-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a564e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a564e-109">Se você quiser saber mais detalhes sobre a integração de aplicativos SaaS com o Azure AD, consulte.</span><span class="sxs-lookup"><span data-stu-id="a564e-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="a564e-110">[O que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a564e-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a564e-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a564e-111">Prerequisites</span></span>

<span data-ttu-id="a564e-112">Para configurar a integração do Azure AD ao Nexonia, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="a564e-112">To configure Azure AD integration with Nexonia, you need the following items:</span></span>

- <span data-ttu-id="a564e-113">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a564e-113">An Azure AD subscription</span></span>
- <span data-ttu-id="a564e-114">Uma assinatura do Nexonia habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="a564e-114">A Nexonia single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a564e-115">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="a564e-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a564e-116">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="a564e-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a564e-117">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="a564e-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a564e-118">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a564e-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a564e-119">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="a564e-119">Scenario description</span></span>
<span data-ttu-id="a564e-120">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="a564e-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a564e-121">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="a564e-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a564e-122">Adicionar Nexonia da galeria</span><span class="sxs-lookup"><span data-stu-id="a564e-122">Adding Nexonia from the gallery</span></span>
2. <span data-ttu-id="a564e-123">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a564e-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-nexonia-from-the-gallery"></a><span data-ttu-id="a564e-124">Adicionar Nexonia da galeria</span><span class="sxs-lookup"><span data-stu-id="a564e-124">Adding Nexonia from the gallery</span></span>
<span data-ttu-id="a564e-125">Para configurar a integração do Nexonia ao Azure AD, você precisará adicionar o Nexonia da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="a564e-125">To configure the integration of Nexonia into Azure AD, you need to add Nexonia from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a564e-126">**Para adicionar o Nexonia da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a564e-126">**To add Nexonia from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a564e-127">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a564e-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a564e-129">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="a564e-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a564e-130">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a564e-130">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="a564e-132">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a564e-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="a564e-134">Na caixa de pesquisa, digite **Nexonia**.</span><span class="sxs-lookup"><span data-stu-id="a564e-134">In the search box, type **Nexonia**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_search.png)

5. <span data-ttu-id="a564e-136">No painel de resultados, selecione **Nexonia** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a564e-136">In the results panel, select **Nexonia**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a564e-138">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a564e-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a564e-139">Nesta seção, você configurará e testará o logon único do Azure AD com o Nexonia, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="a564e-139">In this section, you configure and test Azure AD single sign-on with Nexonia based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a564e-140">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Nexonia é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a564e-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Nexonia is to a user in Azure AD.</span></span> <span data-ttu-id="a564e-141">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Nexonia.</span><span class="sxs-lookup"><span data-stu-id="a564e-141">In other words, a link relationship between an Azure AD user and the related user in Nexonia needs to be established.</span></span>

<span data-ttu-id="a564e-142">No Nexonia, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="a564e-142">In Nexonia, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a564e-143">Para configurar e testar o logon único do Azure AD com o Nexonia, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="a564e-143">To configure and test Azure AD single sign-on with Nexonia, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a564e-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="a564e-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a564e-145">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="a564e-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a564e-146">**[Criar um usuário de teste do Nexonia](#creating-a-nexonia-test-user)** – para ter um equivalente de Brenda Fernandes no Nexonia que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a564e-146">**[Creating a Nexonia test user](#creating-a-nexonia-test-user)** - to have a counterpart of Britta Simon in Nexonia that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a564e-147">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="a564e-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a564e-148">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="a564e-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a564e-149">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a564e-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a564e-150">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único em seu aplicativo Nexonia.</span><span class="sxs-lookup"><span data-stu-id="a564e-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Nexonia application.</span></span>

>[!Note]
><span data-ttu-id="a564e-151">Se você tiver problemas na integração, consulte este [link](https://docs.microsoft.com/azure/active-directory/application-sign-in-problem-federated-sso-gallery?WT.mc_id=UI_AAD_Enterprise_Apps_SupportOrTroubleshooting) para um guia de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="a564e-151">If you have issues in the integration then refer this [link](https://docs.microsoft.com/azure/active-directory/application-sign-in-problem-federated-sso-gallery?WT.mc_id=UI_AAD_Enterprise_Apps_SupportOrTroubleshooting) for troubleshooting guide.</span></span> <span data-ttu-id="a564e-152">Se você ainda não encontrou a solução, acione a solicitação de suporte do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a564e-152">If you still have not found the solution, then raise the support request from Azure portal.</span></span>

<span data-ttu-id="a564e-153">**Para configurar o logon único do Azure AD com o Nexonia, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a564e-153">**To configure Azure AD single sign-on with Nexonia, perform the following steps:**</span></span>

1. <span data-ttu-id="a564e-154">No Portal do Azure, na página de integração de aplicativos do **Nexonia**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="a564e-154">In the Azure portal, on the **Nexonia** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="a564e-156">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="a564e-156">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_samlbase.png)

3. <span data-ttu-id="a564e-158">Na seção **URLs e Domínio do Nexonia**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="a564e-158">On the **Nexonia Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_url.png)

    <span data-ttu-id="a564e-160">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://system.nexonia.com/assistant/saml.do?orgCode=<organizationcode>`</span><span class="sxs-lookup"><span data-stu-id="a564e-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://system.nexonia.com/assistant/saml.do?orgCode=<organizationcode>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a564e-161">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="a564e-161">This value is not real.</span></span> <span data-ttu-id="a564e-162">Atualize esse valor com a URL de Resposta real.</span><span class="sxs-lookup"><span data-stu-id="a564e-162">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="a564e-163">Para obter esse valor, entre em contato com a [equipe de suporte do Nexonia](https://nexonia.zendesk.com/hc/requests/new).</span><span class="sxs-lookup"><span data-stu-id="a564e-163">Contact [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) to get this value.</span></span> 


4. <span data-ttu-id="a564e-164">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="a564e-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_certificate.png) 

5. <span data-ttu-id="a564e-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="a564e-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-nexonia-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a564e-168">Na seção **Configuração do Nexonia**, clique em **Configurar o Nexonia** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="a564e-168">On the **Nexonia Configuration** section, click **Configure Nexonia** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a564e-169">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="a564e-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_configure.png) 

7. <span data-ttu-id="a564e-171">Para que o SSO seja configurado para seu aplicativo, entre em contato com a [equipe de suporte do Nexonia](https://nexonia.zendesk.com/hc/requests/new) e forneça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="a564e-171">To get SSO configured for your application, contact [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) and provide them with the following:</span></span>

    <span data-ttu-id="a564e-172">• O **certificado**</span><span class="sxs-lookup"><span data-stu-id="a564e-172">• The downloaded **certificate**</span></span>

    <span data-ttu-id="a564e-173">• A **ID da entidade SAML**</span><span class="sxs-lookup"><span data-stu-id="a564e-173">• The **SAML Entity ID**</span></span>

    <span data-ttu-id="a564e-174">• A **URL do Serviço de Logon Único SAML**</span><span class="sxs-lookup"><span data-stu-id="a564e-174">• The **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="a564e-175">• A **URL de Saída**</span><span class="sxs-lookup"><span data-stu-id="a564e-175">• The **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="a564e-176">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="a564e-176">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a564e-177">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="a564e-177">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a564e-178">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a564e-178">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a564e-179">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a564e-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="a564e-180">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="a564e-180">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="a564e-182">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a564e-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a564e-183">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a564e-183">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-nexonia-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a564e-185">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="a564e-185">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-nexonia-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a564e-187">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a564e-187">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-nexonia-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a564e-189">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="a564e-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-nexonia-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a564e-191">a.</span><span class="sxs-lookup"><span data-stu-id="a564e-191">a.</span></span> <span data-ttu-id="a564e-192">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="a564e-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a564e-193">b.</span><span class="sxs-lookup"><span data-stu-id="a564e-193">b.</span></span> <span data-ttu-id="a564e-194">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="a564e-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a564e-195">c.</span><span class="sxs-lookup"><span data-stu-id="a564e-195">c.</span></span> <span data-ttu-id="a564e-196">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="a564e-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a564e-197">d.</span><span class="sxs-lookup"><span data-stu-id="a564e-197">d.</span></span> <span data-ttu-id="a564e-198">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a564e-198">Click **Create**.</span></span>
 
### <a name="creating-a-nexonia-test-user"></a><span data-ttu-id="a564e-199">Criar um usuário de teste do Nexonia</span><span class="sxs-lookup"><span data-stu-id="a564e-199">Creating a Nexonia test user</span></span>

<span data-ttu-id="a564e-200">Nesta seção, você criará um usuário chamado Brenda Fernandes no Nexonia.</span><span class="sxs-lookup"><span data-stu-id="a564e-200">In this section, you create a user called Britta Simon in Nexonia.</span></span> <span data-ttu-id="a564e-201">Trabalhe com a [equipe de suporte do Nexonia](https://nexonia.zendesk.com/hc/requests/new) para adicionar os usuários na plataforma do Nexonia.</span><span class="sxs-lookup"><span data-stu-id="a564e-201">Work with [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) to add the users in the Nexonia platform.</span></span> <span data-ttu-id="a564e-202">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="a564e-202">Users must be created and activated before you use single sign-on.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a564e-203">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a564e-203">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a564e-204">Nesta seção, ao conceder acesso ao Nexonia a Brenda Fernandes, você permitirá que ela use o logon único do Azure.</span><span class="sxs-lookup"><span data-stu-id="a564e-204">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Nexonia.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="a564e-206">**Para atribuir Brenda Fernandes ao Nexonia, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a564e-206">**To assign Britta Simon to Nexonia, perform the following steps:**</span></span>

1. <span data-ttu-id="a564e-207">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a564e-207">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="a564e-209">Na lista de aplicativos, selecione **Nexonia**.</span><span class="sxs-lookup"><span data-stu-id="a564e-209">In the applications list, select **Nexonia**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_app.png) 

3. <span data-ttu-id="a564e-211">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="a564e-211">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="a564e-213">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a564e-213">Click **Add** button.</span></span> <span data-ttu-id="a564e-214">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a564e-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="a564e-216">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="a564e-216">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a564e-217">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a564e-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a564e-218">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a564e-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a564e-219">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="a564e-219">Testing single sign-on</span></span>

<span data-ttu-id="a564e-220">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="a564e-220">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a564e-221">Ao clicar no bloco Nexonia no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo Nexonia.</span><span class="sxs-lookup"><span data-stu-id="a564e-221">When you click the Nexonia tile in the Access Panel, you should get automatically signed-on to your Nexonia application.</span></span>
<span data-ttu-id="a564e-222">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="a564e-222">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a564e-223">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="a564e-223">Additional resources</span></span>

* [<span data-ttu-id="a564e-224">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="a564e-224">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a564e-225">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a564e-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_203.png

