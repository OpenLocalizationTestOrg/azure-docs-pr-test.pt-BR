---
title: "Tutorial: integração do Azure Active Directory ao Citrix GoToMeeting | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Citrix GoToMeeting."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7d7897f6-b88e-4dd5-8f3a-e612337b1413
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: c1ac144c4fa43312ec26fce03cd0ee1bfcf73d4b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-gotomeeting"></a><span data-ttu-id="23927-103">Tutorial: integração do Active Directory do Azure ao Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="23927-103">Tutorial: Azure Active Directory integration with Citrix GoToMeeting</span></span>

<span data-ttu-id="23927-104">Nesse tutorial, você aprenderá a integrar o Citrix GoToMeeting ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="23927-104">In this tutorial, you learn how to integrate Citrix GoToMeeting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="23927-105">A integração do Citrix GoToMeeting ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="23927-105">Integrating Citrix GoToMeeting with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="23927-106">Você pode controlar, no Azure AD, quem tem acesso ao Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="23927-106">You can control in Azure AD who has access to Citrix GoToMeeting</span></span>
- <span data-ttu-id="23927-107">Você pode habilitar seus usuários a fazerem logon automaticamente no Citrix GoToMeeting (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="23927-107">You can enable your users to automatically get signed-on to Citrix GoToMeeting (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="23927-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="23927-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="23927-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="23927-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="23927-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="23927-110">Prerequisites</span></span>

<span data-ttu-id="23927-111">Para configurar a integração do Azure AD ao Citrix GoToMeeting, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="23927-111">To configure Azure AD integration with Citrix GoToMeeting, you need the following items:</span></span>

- <span data-ttu-id="23927-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="23927-112">An Azure AD subscription</span></span>
- <span data-ttu-id="23927-113">Uma assinatura do Citrix GoToMeeting habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="23927-113">A Citrix GoToMeeting single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="23927-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="23927-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="23927-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="23927-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="23927-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="23927-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="23927-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="23927-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="23927-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="23927-118">Scenario description</span></span>
<span data-ttu-id="23927-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="23927-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="23927-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="23927-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="23927-121">Adicionar o Citrix GoToMeeting da galeria</span><span class="sxs-lookup"><span data-stu-id="23927-121">Adding Citrix GoToMeeting from the gallery</span></span>
2. <span data-ttu-id="23927-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="23927-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-citrix-gotomeeting-from-the-gallery"></a><span data-ttu-id="23927-123">Adicionar o Citrix GoToMeeting da galeria</span><span class="sxs-lookup"><span data-stu-id="23927-123">Adding Citrix GoToMeeting from the gallery</span></span>
<span data-ttu-id="23927-124">Para configurar a integração do Citrix GoToMeeting ao Azure AD, você precisa adicionar o Citrix GoToMeeting, por meio da galeria, à sua lista de aplicativos de SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="23927-124">To configure the integration of Citrix GoToMeeting into Azure AD, you need to add Citrix GoToMeeting from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="23927-125">**Para adicionar o Citrix GoToMeeting da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="23927-125">**To add Citrix GoToMeeting from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="23927-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="23927-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="23927-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="23927-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="23927-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="23927-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="23927-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="23927-131">Click **New application** button on the top of the dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="23927-133">Na caixa de pesquisa, digite **Citrix GoToMeeting**.</span><span class="sxs-lookup"><span data-stu-id="23927-133">In the search box, type **Citrix GoToMeeting**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_search.png)

5. <span data-ttu-id="23927-135">No painel de resultados, selecione **Citrix GoToMeeting** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="23927-135">In the results panel, select **Citrix GoToMeeting**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="23927-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="23927-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="23927-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Citrix GoToMeeting com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="23927-138">In this section, you configure and test Azure AD single sign-on with Citrix GoToMeeting based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="23927-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Citrix GoToMeeting é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="23927-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Citrix GoToMeeting is to a user in Azure AD.</span></span> <span data-ttu-id="23927-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="23927-140">In other words, a link relationship between an Azure AD user and the related user in Citrix GoToMeeting needs to be established.</span></span>

<span data-ttu-id="23927-141">Essa relação de vínculo é estabelecida atribuindo o valor de **nome de usuário** no Azure AD ao valor de **Nome de usuário** no Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="23927-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Citrix GoToMeeting.</span></span>

<span data-ttu-id="23927-142">Para configurar e testar o logon único do Azure AD com o Citrix GoToMeeting, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="23927-142">To configure and test Azure AD single sign-on with Citrix GoToMeeting, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="23927-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="23927-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="23927-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="23927-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="23927-145">**[Criação de um usuário de teste do Citrix GoToMeeting](#creating-a-citrix-gotomeeting-test-user)** – para ter um equivalente de Brenda Fernandes no Citrix GoToMeeting que esteja vinculado à sua representação no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="23927-145">**[Creating a Citrix GoToMeeting test user](#creating-a-citrix-gotomeeting-test-user)** - to have a counterpart of Britta Simon in Citrix GoToMeeting that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="23927-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="23927-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="23927-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="23927-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="23927-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="23927-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="23927-149">Nesta seção, você habilitará o logon único do Azure AD no portal do Azure e configurará o logon único no aplicativo Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="23927-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Citrix GoToMeeting application.</span></span>

<span data-ttu-id="23927-150">**Para configurar o logon único do Azure AD com o Citrix GoToMeeting, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="23927-150">**To configure Azure AD single sign-on with Citrix GoToMeeting, perform the following steps:**</span></span>

1. <span data-ttu-id="23927-151">No portal do Azure, na página de integração de aplicativo do **Citrix GoToMeeting**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="23927-151">In the Azure portal, on the **Citrix GoToMeeting** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="23927-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="23927-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_samlbase.png)

3. <span data-ttu-id="23927-155">Na seção **URLs e Domínio do Citrix GoToMeeting** não é necessário executar nenhuma etapa.</span><span class="sxs-lookup"><span data-stu-id="23927-155">On the **Citrix GoToMeeting Domain and URLs** section, no need to perform any steps.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_url.png)


3. <span data-ttu-id="23927-157">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="23927-157">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_certificate.png) 

4. <span data-ttu-id="23927-159">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="23927-159">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_400.png)
    
5. <span data-ttu-id="23927-161">Na seção "Configuração de SAML do Citrix GoToMeeting", clique em "Configurar SAML do Citrix GoToMeeting" para abrir a janela "Configurar logon".</span><span class="sxs-lookup"><span data-stu-id="23927-161">On the Citrix GoToMeeting SAML Configuration section, click Configure Citrix GoToMeeting SAML to open Configure sign-on window.</span></span> <span data-ttu-id="23927-162">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="23927-162">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

6. <span data-ttu-id="23927-163">Em uma janela de navegador diferente, faça logon no seu [Citrix Organization Center](https://account.citrixonline.com/organization/administration/).</span><span class="sxs-lookup"><span data-stu-id="23927-163">In a different browser window, log in to your [Citrix Organization Center](https://account.citrixonline.com/organization/administration/).</span></span>

7. <span data-ttu-id="23927-164">Clique na guia **Provedor de Identidade** e execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="23927-164">Click the **Identity Provider** tab, and then perform the following steps:</span></span>  
   
    <span data-ttu-id="23927-165">![Instalação do SAML](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "Instalação do SAML")</span><span class="sxs-lookup"><span data-stu-id="23927-165">![SAML setup](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "SAML setup")</span></span>
   
    <span data-ttu-id="23927-166">a.</span><span class="sxs-lookup"><span data-stu-id="23927-166">a.</span></span> <span data-ttu-id="23927-167">Selecione **Manual**</span><span class="sxs-lookup"><span data-stu-id="23927-167">Select **Manual**</span></span>

    <span data-ttu-id="23927-168">b.</span><span class="sxs-lookup"><span data-stu-id="23927-168">b.</span></span> <span data-ttu-id="23927-169">No portal do Azure, na página de diálogo **Configurar logon único no Citrix GoToMeeting**, copie o valor da **URL do Serviço de Logon Único SAML** e cole-o na caixa de texto **URL da página de entrada**.</span><span class="sxs-lookup"><span data-stu-id="23927-169">In the Azure portal, on the **Configure single sign-on at Citrix GoToMeeting** dialog page, copy the **SAML Single Sign-On Service URL** value, and then paste it into the **Sign-in page URL** textbox.</span></span> 

    <span data-ttu-id="23927-170">c.</span><span class="sxs-lookup"><span data-stu-id="23927-170">c.</span></span> <span data-ttu-id="23927-171">No portal do Azure, na página de diálogo **Configurar logon único no Citrix GoToMeeting**, copie o valor da **URL de Saída** e cole-o na caixa de texto **URL da página de saída**.</span><span class="sxs-lookup"><span data-stu-id="23927-171">In the Azure portal, on the **Configure single sign-on at Citrix GoToMeeting** dialog page, copy the **Sign-Out URL** value, and then paste it into the **Sign-out page URL** textbox.</span></span>

    <span data-ttu-id="23927-172">d.</span><span class="sxs-lookup"><span data-stu-id="23927-172">d.</span></span> <span data-ttu-id="23927-173">No portal do Azure, na página de diálogo **Configurar logon único no Citrix GoToMeeting**, copie o valor da **ID da Entidade SAML** e cole-o na caixa de texto **ID da Entidade do Provedor de Identidade**.</span><span class="sxs-lookup"><span data-stu-id="23927-173">In the Azure portal, on the **Configure single sign-on at Citrix GoToMeeting** dialog page, copy the **SAML Entity ID** value, and then paste it into the **Identity Provider Entity ID** textbox.</span></span>

    <span data-ttu-id="23927-174">e.</span><span class="sxs-lookup"><span data-stu-id="23927-174">e.</span></span> <span data-ttu-id="23927-175">Clique em **Carregar Certificado**para carregar o certificado que você baixou.</span><span class="sxs-lookup"><span data-stu-id="23927-175">To upload your downloaded certificate, click **Upload Certificate**.</span></span>

    <span data-ttu-id="23927-176">f.</span><span class="sxs-lookup"><span data-stu-id="23927-176">f.</span></span> <span data-ttu-id="23927-177">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="23927-177">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="23927-178">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="23927-178">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="23927-179">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="23927-179">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="23927-180">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="23927-180">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="23927-181">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="23927-181">Creating an Azure AD test user</span></span>
<span data-ttu-id="23927-182">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="23927-182">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="23927-184">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="23927-184">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="23927-185">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="23927-185">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="23927-187">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="23927-187">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="23927-189">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="23927-189">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="23927-191">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="23927-191">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="23927-193">a.</span><span class="sxs-lookup"><span data-stu-id="23927-193">a.</span></span> <span data-ttu-id="23927-194">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="23927-194">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="23927-195">b.</span><span class="sxs-lookup"><span data-stu-id="23927-195">b.</span></span> <span data-ttu-id="23927-196">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="23927-196">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="23927-197">c.</span><span class="sxs-lookup"><span data-stu-id="23927-197">c.</span></span> <span data-ttu-id="23927-198">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="23927-198">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="23927-199">d.</span><span class="sxs-lookup"><span data-stu-id="23927-199">d.</span></span> <span data-ttu-id="23927-200">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="23927-200">Click **Create**.</span></span>
 
### <a name="creating-a-citrix-gotomeeting-test-user"></a><span data-ttu-id="23927-201">Criando um usuário de teste do Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="23927-201">Creating a Citrix GoToMeeting test user</span></span>

<span data-ttu-id="23927-202">Nesta seção, é criado um usuário chamado Brenda Fernandes no Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="23927-202">In this section, a user called Britta Simon is created in Citrix GoToMeeting.</span></span> <span data-ttu-id="23927-203">O Citrix GoToMeeting dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="23927-203">Citrix GoToMeeting supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="23927-204">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="23927-204">There is no action item for you in this section.</span></span> <span data-ttu-id="23927-205">Se um usuário ainda não existir no Citrix GoToMeeting, um novo será criado quando você tentar acessar o Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="23927-205">If a user doesn't already exist in Citrix GoToMeeting, a new one is created when you attempt to access Citrix GoToMeeting.</span></span>

>[!Note]
><span data-ttu-id="23927-206">Se você precisar criar um usuário manualmente, entre em contato com a [Equipe de suporte do Citrix GoToMeeting](https://care.citrixonline.com/gotomeeting)</span><span class="sxs-lookup"><span data-stu-id="23927-206">If you need to create a user manually, Contact [Citrix GoToMeeting support team](https://care.citrixonline.com/gotomeeting)</span></span> 


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="23927-207">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="23927-207">Assigning the Azure AD test user</span></span>

<span data-ttu-id="23927-208">Nesta seção, você habilitará Brenda Fernandes a usar o logon único do Azure concedendo a ela acesso ao Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="23927-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Citrix GoToMeeting.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="23927-210">**Para atribuir Brenda Fernandes ao Citrix GoToMeeting, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="23927-210">**To assign Britta Simon to Citrix GoToMeeting, perform the following steps:**</span></span>

1. <span data-ttu-id="23927-211">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="23927-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="23927-213">Na lista de aplicativos, selecione **Citrix GoToMeeting**.</span><span class="sxs-lookup"><span data-stu-id="23927-213">In the applications list, select **Citrix GoToMeeting**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_app.png) 

3. <span data-ttu-id="23927-215">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="23927-215">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="23927-217">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="23927-217">Click **Add** button.</span></span> <span data-ttu-id="23927-218">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="23927-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="23927-220">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="23927-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="23927-221">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="23927-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="23927-222">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="23927-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="23927-223">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="23927-223">Testing single sign-on</span></span>

<span data-ttu-id="23927-224">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="23927-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="23927-225">Se você quiser testar suas configurações de logon único, abra o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="23927-225">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="23927-226">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="23927-226">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="23927-227">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="23927-227">Additional resources</span></span>

* [<span data-ttu-id="23927-228">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="23927-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="23927-229">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="23927-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="23927-230">Configurar Provisionamento de Usuário</span><span class="sxs-lookup"><span data-stu-id="23927-230">Configure User Provisioning</span></span>](active-directory-saas-citrixgotomeeting-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_203.png

