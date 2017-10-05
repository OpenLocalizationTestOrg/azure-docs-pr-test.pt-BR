---
title: "Tutorial: Integração do Azure Active Directory ao Tangoe Command Premium Mobile| Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Tangoe Command Premium Mobile."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2b0b544c-9c2c-49cd-862b-ec2ee9330126
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 595541e7248a7486e58123927389c552af0e50f7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tangoe-command-premium-mobile"></a><span data-ttu-id="539ab-103">Tutorial: Integração do Azure Active Directory ao Tangoe Command Premium Mobile</span><span class="sxs-lookup"><span data-stu-id="539ab-103">Tutorial: Azure Active Directory integration with Tangoe Command Premium Mobile</span></span>

<span data-ttu-id="539ab-104">Neste tutorial, você aprenderá como integrar o Tangoe Command Premium Mobile ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="539ab-104">In this tutorial, you learn how to integrate Tangoe Command Premium Mobile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="539ab-105">A integração do Tangoe Command Premium Mobile ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="539ab-105">Integrating Tangoe Command Premium Mobile with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="539ab-106">Você pode controlar no Azure AD quem tem acesso ao Tangoe Command Premium Mobile</span><span class="sxs-lookup"><span data-stu-id="539ab-106">You can control in Azure AD who has access to Tangoe Command Premium Mobile</span></span>
- <span data-ttu-id="539ab-107">Você pode habilitar os usuários a entrar automaticamente no Tangoe Command Premium Mobile (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="539ab-107">You can enable your users to automatically get signed-on to Tangoe Command Premium Mobile (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="539ab-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="539ab-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="539ab-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="539ab-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="539ab-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="539ab-110">Prerequisites</span></span>

<span data-ttu-id="539ab-111">Para configurar a integração do Azure AD ao Tangoe Command Premium Mobile, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="539ab-111">To configure Azure AD integration with Tangoe Command Premium Mobile, you need the following items:</span></span>

- <span data-ttu-id="539ab-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="539ab-112">An Azure AD subscription</span></span>
- <span data-ttu-id="539ab-113">Uma assinatura do Tangoe Command Premium Mobile habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="539ab-113">A Tangoe Command Premium Mobile single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="539ab-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="539ab-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="539ab-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="539ab-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="539ab-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="539ab-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="539ab-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="539ab-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="539ab-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="539ab-118">Scenario description</span></span>
<span data-ttu-id="539ab-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="539ab-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="539ab-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="539ab-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="539ab-121">Adicionar o Tangoe Command Premium Mobile da galeria</span><span class="sxs-lookup"><span data-stu-id="539ab-121">Add Tangoe Command Premium Mobile from the gallery</span></span>
2. <span data-ttu-id="539ab-122">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="539ab-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tangoe-command-premium-mobile-from-the-gallery"></a><span data-ttu-id="539ab-123">Adicionar o Tangoe Command Premium Mobile da galeria</span><span class="sxs-lookup"><span data-stu-id="539ab-123">Add Tangoe Command Premium Mobile from the gallery</span></span>
<span data-ttu-id="539ab-124">Para configurar a integração do Tangoe Command Premium Mobile ao Azure AD, você precisará adicionar o Tangoe Command Premium Mobile da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="539ab-124">To configure the integration of Tangoe Command Premium Mobile into Azure AD, you need to add Tangoe Command Premium Mobile from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="539ab-125">**Para adicionar o Tangoe Command Premium Mobile por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="539ab-125">**To add Tangoe Command Premium Mobile from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="539ab-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="539ab-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="539ab-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="539ab-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="539ab-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="539ab-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="539ab-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="539ab-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="539ab-133">Na caixa de pesquisa, digite **Tangoe Command Premium Mobile**, selecione **Tangoe Command Premium Mobile** no painel de resultados e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="539ab-133">In the search box, type **Tangoe Command Premium Mobile**, select **Tangoe Command Premium Mobile** from result panel then click **Add** button to add the application.</span></span>

    ![<span data-ttu-id="539ab-134">Adicionar o Tangoe Command Premium Mobile da galeria</span><span class="sxs-lookup"><span data-stu-id="539ab-134">Add Tangoe Command Premium Mobile from gallery</span></span> ](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="539ab-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="539ab-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="539ab-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Tangoe Command Premium Mobile, com base em uma usuária de teste chamada "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="539ab-136">In this section, you configure and test Azure AD single sign-on with Tangoe Command Premium Mobile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="539ab-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Tangoe Command Premium Mobile é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="539ab-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Tangoe Command Premium Mobile is to a user in Azure AD.</span></span> <span data-ttu-id="539ab-138">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Tangoe Command Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="539ab-138">In other words, a link relationship between an Azure AD user and the related user in Tangoe Command Premium Mobile needs to be established.</span></span>

<span data-ttu-id="539ab-139">No Tangoe Command Premium Mobile, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="539ab-139">In Tangoe Command Premium Mobile, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="539ab-140">Para configurar e testar o logon único do Azure AD com o Tangoe Command Premium Mobile, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="539ab-140">To configure and test Azure AD single sign-on with Tangoe Command Premium Mobile, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="539ab-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="539ab-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="539ab-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="539ab-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="539ab-143">**[Criar um usuário de teste do Tangoe Command Premium Mobile](#create-a-tangoe-command-premium-mobile-test-user)** – para ter um equivalente de Brenda Fernandes no Tangoe Command Premium Mobile vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="539ab-143">**[Create a Tangoe Command Premium Mobile test user](#create-a-tangoe-command-premium-mobile-test-user)** - to have a counterpart of Britta Simon in Tangoe Command Premium Mobile that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="539ab-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="539ab-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="539ab-145">**[Testar o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="539ab-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="539ab-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="539ab-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="539ab-147">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo Tangoe Command Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="539ab-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tangoe Command Premium Mobile application.</span></span>

<span data-ttu-id="539ab-148">**Para configurar o logon único do Azure AD com o Tangoe Command Premium Mobile, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="539ab-148">**To configure Azure AD single sign-on with Tangoe Command Premium Mobile, perform the following steps:**</span></span>

1. <span data-ttu-id="539ab-149">No Portal do Azure, na página de integração de aplicativos do **Tangoe Command Premium Mobile**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="539ab-149">In the Azure portal, on the **Tangoe Command Premium Mobile** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="539ab-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="539ab-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Logon único baseado em SAML](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_samlbase.png)

3. <span data-ttu-id="539ab-153">Na seção **Domínio e URLs do Tangoe Command Premium Mobile**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="539ab-153">On the **Tangoe Command Premium Mobile Domain and URLs** section, perform the following steps:</span></span>

    ![Domínio e URLs do Tangoe Command Premium Mobile](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_url.png)

    <span data-ttu-id="539ab-155">a.</span><span class="sxs-lookup"><span data-stu-id="539ab-155">a.</span></span> <span data-ttu-id="539ab-156">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`</span><span class="sxs-lookup"><span data-stu-id="539ab-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`</span></span>

    <span data-ttu-id="539ab-157">b.</span><span class="sxs-lookup"><span data-stu-id="539ab-157">b.</span></span> <span data-ttu-id="539ab-158">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://sso.tangoe.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="539ab-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://sso.tangoe.com/sp/ACS.saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="539ab-159">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="539ab-159">These values are not real.</span></span> <span data-ttu-id="539ab-160">Atualize esses valores com a URL de Resposta e a URL de Logon reais.</span><span class="sxs-lookup"><span data-stu-id="539ab-160">Update these values with the actual  Reply URL and Sign-On URL.</span></span> <span data-ttu-id="539ab-161">Contate a [equipe de suporte ao cliente do Tangoe Command Premium Mobile](https://www.tangoe.com/contact-2/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="539ab-161">Contact [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) to get these values.</span></span> 

4. <span data-ttu-id="539ab-162">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="539ab-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Seção Certificado de Autenticação SAML](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_certificate.png) 

5. <span data-ttu-id="539ab-164">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="539ab-164">Click **Save** button.</span></span>

    ![Botão Salvar](./media/active-directory-saas-tangoe-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="539ab-166">Na seção **Configuração do Tangoe Command Premium Mobile**, clique em **Configurar o Tangoe Command Premium Mobile** para abrir a janela **Configurar o logon**.</span><span class="sxs-lookup"><span data-stu-id="539ab-166">On the **Tangoe Command Premium Mobile Configuration** section, click **Configure Tangoe Command Premium Mobile** to open **Configure sign-on** window.</span></span> <span data-ttu-id="539ab-167">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="539ab-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Seção Configuração do Tangoe Command Premium Mobile](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_configure.png) 

7. <span data-ttu-id="539ab-169">Para que o SSO seja configurado para seu aplicativo, contate sua [equipe de suporte ao cliente do Tangoe Command Premium Mobile](https://www.tangoe.com/contact-2/) e forneça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="539ab-169">To get SSO configured for your application, contact your [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) and provide the following:</span></span>

   - <span data-ttu-id="539ab-170">O arquivo de metadados baixado</span><span class="sxs-lookup"><span data-stu-id="539ab-170">The downloaded metadata file</span></span>
   - <span data-ttu-id="539ab-171">A **ID da entidade SAML**</span><span class="sxs-lookup"><span data-stu-id="539ab-171">The **SAML Entity ID**</span></span>
   - <span data-ttu-id="539ab-172">A **URL do serviço de logon único SAML**</span><span class="sxs-lookup"><span data-stu-id="539ab-172">The **SAML Single Sign-On Service URL**</span></span>
   - <span data-ttu-id="539ab-173">A **URL de saída**</span><span class="sxs-lookup"><span data-stu-id="539ab-173">The **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="539ab-174">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="539ab-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="539ab-175">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="539ab-175">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="539ab-176">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="539ab-176">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="539ab-177">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="539ab-177">Create an Azure AD test user</span></span>
<span data-ttu-id="539ab-178">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="539ab-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="539ab-180">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="539ab-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="539ab-181">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="539ab-181">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tangoe-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="539ab-183">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="539ab-183">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Usuários e grupos -> Todos os usuários](./media/active-directory-saas-tangoe-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="539ab-185">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="539ab-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Adicionar usuário](./media/active-directory-saas-tangoe-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="539ab-187">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="539ab-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Página da caixa de diálogo do usuário](./media/active-directory-saas-tangoe-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="539ab-189">a.</span><span class="sxs-lookup"><span data-stu-id="539ab-189">a.</span></span> <span data-ttu-id="539ab-190">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="539ab-190">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="539ab-191">b.</span><span class="sxs-lookup"><span data-stu-id="539ab-191">b.</span></span> <span data-ttu-id="539ab-192">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="539ab-192">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="539ab-193">c.</span><span class="sxs-lookup"><span data-stu-id="539ab-193">c.</span></span> <span data-ttu-id="539ab-194">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="539ab-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="539ab-195">d.</span><span class="sxs-lookup"><span data-stu-id="539ab-195">d.</span></span> <span data-ttu-id="539ab-196">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="539ab-196">Click **Create**.</span></span>
 
### <a name="create-a-tangoe-command-premium-mobile-test-user"></a><span data-ttu-id="539ab-197">Criar um usuário de teste do Tangoe Command Premium Mobile</span><span class="sxs-lookup"><span data-stu-id="539ab-197">Create a Tangoe Command Premium Mobile test user</span></span>

<span data-ttu-id="539ab-198">Nesta seção, você criará uma usuária chamada Brenda Fernandes no Tangoe Command Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="539ab-198">In this section, you create a user called Britta Simon in Tangoe Command Premium Mobile.</span></span> 

<span data-ttu-id="539ab-199">O aplicativo Tangoe Command Premium Mobile precisa que todos os usuários sejam provisionados no aplicativo antes de fazer o Logon Único.</span><span class="sxs-lookup"><span data-stu-id="539ab-199">Tangoe Command Premium Mobile application needs all the users to be provisioned in the application before doing Single Sign On.</span></span> <span data-ttu-id="539ab-200">Portanto, trabalhe com [equipe de suporte ao cliente do Tangoe Command Premium Mobile](https://www.tangoe.com/contact-2/) para provisionar todos esses usuários para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="539ab-200">So please work with the [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) to provision all these users into the application.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="539ab-201">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="539ab-201">Assign the Azure AD test user</span></span>

<span data-ttu-id="539ab-202">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Tangoe Command Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="539ab-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tangoe Command Premium Mobile.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="539ab-204">**Para atribuir Brenda Fernandes ao Tangoe Command Premium Mobile, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="539ab-204">**To assign Britta Simon to Tangoe Command Premium Mobile, perform the following steps:**</span></span>

1. <span data-ttu-id="539ab-205">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="539ab-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="539ab-207">Na lista de aplicativos, escolha **Tangoe Command Premium Mobile**.</span><span class="sxs-lookup"><span data-stu-id="539ab-207">In the applications list, select **Tangoe Command Premium Mobile**.</span></span>

    ![Tangoe Command Premium Mobile na lista de aplicativos](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_app.png) 

3. <span data-ttu-id="539ab-209">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="539ab-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="539ab-211">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="539ab-211">Click **Add** button.</span></span> <span data-ttu-id="539ab-212">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="539ab-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="539ab-214">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="539ab-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="539ab-215">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="539ab-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="539ab-216">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="539ab-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="539ab-217">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="539ab-217">Test single sign-on</span></span>

<span data-ttu-id="539ab-218">Nesta seção, você testará sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="539ab-218">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="539ab-219">Ao clicar no bloco Tangoe Command Premium Mobile no Painel de Acesso, você deve ser conectado automaticamente ao aplicativo Tangoe Command Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="539ab-219">When you click the Tangoe Command Premium Mobile tile in the Access Panel, you should get automatically signed-on to your Tangoe Command Premium Mobile application.</span></span> <span data-ttu-id="539ab-220">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="539ab-220">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="539ab-221">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="539ab-221">Additional resources</span></span>

* [<span data-ttu-id="539ab-222">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="539ab-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="539ab-223">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="539ab-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_203.png

