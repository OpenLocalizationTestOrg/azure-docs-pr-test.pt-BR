---
title: "Tutorial: Integração do Azure Active Directory ao Bonusly | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Bonusly."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 29fea32a-fa20-47b2-9e24-26feb47b0ae6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 29a88b2efdb9f0f33f7933bc654a5a0fdf589c5a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bonusly"></a><span data-ttu-id="00ca2-103">Tutorial: integração do Azure Active Directory ao Bonusly</span><span class="sxs-lookup"><span data-stu-id="00ca2-103">Tutorial: Azure Active Directory integration with Bonusly</span></span>

<span data-ttu-id="00ca2-104">Neste tutorial, você aprenderá a integrar o Bonusly ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="00ca2-104">In this tutorial, you learn how to integrate Bonusly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="00ca2-105">A integração do Bonusly ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="00ca2-105">Integrating Bonusly with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="00ca2-106">No Azure AD, é possível controlar quem tem acesso ao Bonusly</span><span class="sxs-lookup"><span data-stu-id="00ca2-106">You can control in Azure AD who has access to Bonusly</span></span>
- <span data-ttu-id="00ca2-107">Você pode permitir que seus usuários façam logon automaticamente no Bonusly (Logon único) com as contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="00ca2-107">You can enable your users to automatically get signed-on to Bonusly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="00ca2-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="00ca2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="00ca2-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="00ca2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00ca2-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="00ca2-110">Prerequisites</span></span>

<span data-ttu-id="00ca2-111">Para configurar a integração do Azure AD ao Bonusly, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="00ca2-111">To configure Azure AD integration with Bonusly, you need the following items:</span></span>

- <span data-ttu-id="00ca2-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="00ca2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="00ca2-113">Uma assinatura do Bonusly habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="00ca2-113">A Bonusly single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="00ca2-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="00ca2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="00ca2-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="00ca2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="00ca2-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="00ca2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="00ca2-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="00ca2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="00ca2-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="00ca2-118">Scenario description</span></span>
<span data-ttu-id="00ca2-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="00ca2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="00ca2-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="00ca2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="00ca2-121">Adicionando o Bonusly da galeria</span><span class="sxs-lookup"><span data-stu-id="00ca2-121">Adding Bonusly from the gallery</span></span>
2. <span data-ttu-id="00ca2-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="00ca2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bonusly-from-the-gallery"></a><span data-ttu-id="00ca2-123">Adicionando o Bonusly da galeria</span><span class="sxs-lookup"><span data-stu-id="00ca2-123">Adding Bonusly from the gallery</span></span>
<span data-ttu-id="00ca2-124">Para configurar a integração do Bonusly ao Azure AD, você precisa adicionar o Bonusly da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="00ca2-124">To configure the integration of Bonusly into Azure AD, you need to add Bonusly from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="00ca2-125">**Para adicionar o Bonusly da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="00ca2-125">**To add Bonusly from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="00ca2-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="00ca2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="00ca2-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="00ca2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="00ca2-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="00ca2-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="00ca2-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="00ca2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="00ca2-133">Na caixa de pesquisa, digite **Bonusly**, selecione **Bonusly** no painel de resultados e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="00ca2-133">In the search box, type **Bonusly**, select **Bonusly** from result panel then click **Add** button to add the application.</span></span>

    ![Bonusly na lista de resultados](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="00ca2-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="00ca2-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="00ca2-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Bonusly, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="00ca2-136">In this section, you configure and test Azure AD single sign-on with Bonusly based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="00ca2-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Bonusly é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="00ca2-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Bonusly is to a user in Azure AD.</span></span> <span data-ttu-id="00ca2-138">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Bonusly.</span><span class="sxs-lookup"><span data-stu-id="00ca2-138">In other words, a link relationship between an Azure AD user and the related user in Bonusly needs to be established.</span></span>

<span data-ttu-id="00ca2-139">No Bonusly, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="00ca2-139">In Bonusly, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="00ca2-140">Para configurar e testar o logon único do Azure AD com o Bonusly, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="00ca2-140">To configure and test Azure AD single sign-on with Bonusly, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="00ca2-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="00ca2-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="00ca2-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="00ca2-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="00ca2-143">**[Criar um usuário de teste do Bonusly](#create-a-bonusly-test-user)** – para ter um equivalente de Brenda Fernandes no Bonusly vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="00ca2-143">**[Create a Bonusly test user](#create-a-bonusly-test-user)** - to have a counterpart of Britta Simon in Bonusly that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="00ca2-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="00ca2-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="00ca2-145">**[Testar o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="00ca2-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="00ca2-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="00ca2-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="00ca2-147">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo Bonusly.</span><span class="sxs-lookup"><span data-stu-id="00ca2-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bonusly application.</span></span>

<span data-ttu-id="00ca2-148">**Para configurar o logon único do Azure AD com o Bonusly, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="00ca2-148">**To configure Azure AD single sign-on with Bonusly, perform the following steps:**</span></span>

1. <span data-ttu-id="00ca2-149">No Portal do Azure, na página de integração de aplicativos do **Bonusly**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="00ca2-149">In the Azure portal, on the **Bonusly** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="00ca2-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="00ca2-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_samlbase.png)

3. <span data-ttu-id="00ca2-153">Na seção **Domínio e URLs do Bonusly**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="00ca2-153">On the **Bonusly Domain and URLs** section, perform the following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do Bonusly](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_url.png)

    <span data-ttu-id="00ca2-155">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://Bonus.ly/saml/<tenant-name>`</span><span class="sxs-lookup"><span data-stu-id="00ca2-155">In the **Reply URL** textbox, type a URL using the following pattern: `https://Bonus.ly/saml/<tenant-name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="00ca2-156">O valor não é real.</span><span class="sxs-lookup"><span data-stu-id="00ca2-156">The value is not real.</span></span> <span data-ttu-id="00ca2-157">Atualize o valor com a URL de Resposta real.</span><span class="sxs-lookup"><span data-stu-id="00ca2-157">Update the value with the actual Reply URL.</span></span> <span data-ttu-id="00ca2-158">Contate a [equipe de suporte do Bonusly](https://Bonusly/contact) para obter o valor.</span><span class="sxs-lookup"><span data-stu-id="00ca2-158">Contact [Bonusly support team](https://Bonusly/contact) to get the value.</span></span>
 
4. <span data-ttu-id="00ca2-159">Na seção **Certificado de Autenticação SAML**, copie o valor da **IMPRESSÃO DIGITAL** do certificado.</span><span class="sxs-lookup"><span data-stu-id="00ca2-159">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value from the certificate.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_certificate.png) 

5. <span data-ttu-id="00ca2-161">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="00ca2-161">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-bonus-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="00ca2-163">Na seção **Configuração do Bonusly**, clique em **Configurar o Bonusly** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="00ca2-163">On the **Bonusly Configuration** section, click **Configure Bonusly** to open **Configure sign-on** window.</span></span> <span data-ttu-id="00ca2-164">Copie a **ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="00ca2-164">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuração do Bonusly](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_configure.png) 

7. <span data-ttu-id="00ca2-166">Em outra janela do navegador, faça logon no seu locatário do **Bonusly**.</span><span class="sxs-lookup"><span data-stu-id="00ca2-166">In a different browser window, log in to your **Bonusly** tenant.</span></span>

8. <span data-ttu-id="00ca2-167">Na barra de ferramentas na parte superior, clique em **Configurações** e selecione **Integrações e aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="00ca2-167">In the toolbar on the top, click **Settings**, and then select **Integrations and apps**.</span></span>
   
    <span data-ttu-id="00ca2-168">![Seção Social Bonusly](./media/active-directory-saas-bonus-tutorial/ic773686.png "Bonusly")</span><span class="sxs-lookup"><span data-stu-id="00ca2-168">![Bonusly Social Section](./media/active-directory-saas-bonus-tutorial/ic773686.png "Bonusly")</span></span>
9. <span data-ttu-id="00ca2-169">Em **Logon Único**, selecione **SAML**.</span><span class="sxs-lookup"><span data-stu-id="00ca2-169">Under **Single Sign-On**, select **SAML**.</span></span>

10. <span data-ttu-id="00ca2-170">Na página do diálogo **SAML** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="00ca2-170">On the **SAML** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="00ca2-171">![Página de Diálogo Saml do Bonusly](./media/active-directory-saas-bonus-tutorial/ic773687.png "Bonusly")</span><span class="sxs-lookup"><span data-stu-id="00ca2-171">![Bonusly Saml Dialog page](./media/active-directory-saas-bonus-tutorial/ic773687.png "Bonusly")</span></span>
   
    <span data-ttu-id="00ca2-172">a.</span><span class="sxs-lookup"><span data-stu-id="00ca2-172">a.</span></span> <span data-ttu-id="00ca2-173">Na caixa de texto **URL de destino do SSO de IdP**, cole o valor da **URL do Serviço de Logon Único SAML** copiado do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="00ca2-173">In the **IdP SSO target URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="00ca2-174">b.</span><span class="sxs-lookup"><span data-stu-id="00ca2-174">b.</span></span> <span data-ttu-id="00ca2-175">Na caixa de texto **Emissor IdP**, cole o valor da **ID de Entidade do SAML** que você copiou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="00ca2-175">In the **IdP Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="00ca2-176">c.</span><span class="sxs-lookup"><span data-stu-id="00ca2-176">c.</span></span> <span data-ttu-id="00ca2-177">Na caixa de texto **URL de Logon do IdP**, cole o valor da **URL do Serviço de Logon Único SAML** copiado do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="00ca2-177">In the **IdP Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="00ca2-178">d.</span><span class="sxs-lookup"><span data-stu-id="00ca2-178">d.</span></span> <span data-ttu-id="00ca2-179">Cole o valor da **Impressão digital** copiado do Portal do Azure na caixa de texto **Impressão Digital do Certificado**.</span><span class="sxs-lookup"><span data-stu-id="00ca2-179">Paste the **Thumbprint** value copied from Azure portal into the **Cert Fingerprint** textbox.</span></span>
   
11. <span data-ttu-id="00ca2-180">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="00ca2-180">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="00ca2-181">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="00ca2-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="00ca2-182">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="00ca2-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="00ca2-183">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="00ca2-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="00ca2-184">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="00ca2-184">Create an Azure AD test user</span></span>
<span data-ttu-id="00ca2-185">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="00ca2-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="00ca2-187">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="00ca2-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="00ca2-188">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="00ca2-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-bonus-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="00ca2-190">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="00ca2-190">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-bonus-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="00ca2-192">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="00ca2-192">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![O botão Adicionar](./media/active-directory-saas-bonus-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="00ca2-194">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="00ca2-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![A caixa de diálogo Usuário](./media/active-directory-saas-bonus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="00ca2-196">a.</span><span class="sxs-lookup"><span data-stu-id="00ca2-196">a.</span></span> <span data-ttu-id="00ca2-197">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="00ca2-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="00ca2-198">b.</span><span class="sxs-lookup"><span data-stu-id="00ca2-198">b.</span></span> <span data-ttu-id="00ca2-199">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="00ca2-199">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="00ca2-200">c.</span><span class="sxs-lookup"><span data-stu-id="00ca2-200">c.</span></span> <span data-ttu-id="00ca2-201">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="00ca2-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="00ca2-202">d.</span><span class="sxs-lookup"><span data-stu-id="00ca2-202">d.</span></span> <span data-ttu-id="00ca2-203">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="00ca2-203">Click **Create**.</span></span>
 
### <a name="create-a-bonusly-test-user"></a><span data-ttu-id="00ca2-204">Criar um usuário de teste do Bonusly</span><span class="sxs-lookup"><span data-stu-id="00ca2-204">Create a Bonusly test user</span></span>

<span data-ttu-id="00ca2-205">Para permitir que os usuários do Azure AD façam logon no Bonusly, eles devem estar provisionados no Bonusly.</span><span class="sxs-lookup"><span data-stu-id="00ca2-205">In order to enable Azure AD users to log in to Bonusly, they must be provisioned into Bonusly.</span></span> <span data-ttu-id="00ca2-206">No caso do Bonusly, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="00ca2-206">In the case of Bonusly, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="00ca2-207">É possível usar qualquer outra ferramenta de criação da conta de usuário do Bonusly ou as APIs fornecidas pelo Bonusly para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="00ca2-207">You can use any other Bonusly user account creation tools or APIs provided by Bonusly to provision AAD user accounts.</span></span>
>  

<span data-ttu-id="00ca2-208">**Para configurar o provisionamento de usuários, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="00ca2-208">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="00ca2-209">Em uma janela do navegador da Web, faça logon no seu locatário do Bonusly.</span><span class="sxs-lookup"><span data-stu-id="00ca2-209">In a web browser window, log in to your Bonusly tenant.</span></span>

2. <span data-ttu-id="00ca2-210">Clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="00ca2-210">Click **Settings**.</span></span>
 
    <span data-ttu-id="00ca2-211">![Configurações](./media/active-directory-saas-bonus-tutorial/ic781041.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="00ca2-211">![Settings](./media/active-directory-saas-bonus-tutorial/ic781041.png "Settings")</span></span>

3. <span data-ttu-id="00ca2-212">Clique na guia **Usuários e bônus** .</span><span class="sxs-lookup"><span data-stu-id="00ca2-212">Click the **Users and bonuses** tab.</span></span>
   
    <span data-ttu-id="00ca2-213">![Usuários e bônus](./media/active-directory-saas-bonus-tutorial/ic781042.png "Usuários e bônus")</span><span class="sxs-lookup"><span data-stu-id="00ca2-213">![Users and bonuses](./media/active-directory-saas-bonus-tutorial/ic781042.png "Users and bonuses")</span></span>

4. <span data-ttu-id="00ca2-214">Clique em **Gerenciar Usuários**.</span><span class="sxs-lookup"><span data-stu-id="00ca2-214">Click **Manage Users**.</span></span>
   
    <span data-ttu-id="00ca2-215">![Gerenciar Usuários](./media/active-directory-saas-bonus-tutorial/ic781043.png "Gerenciar Usuários")</span><span class="sxs-lookup"><span data-stu-id="00ca2-215">![Manage Users](./media/active-directory-saas-bonus-tutorial/ic781043.png "Manage Users")</span></span>

5. <span data-ttu-id="00ca2-216">Clique em **Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="00ca2-216">Click **Add User**.</span></span>
   
    <span data-ttu-id="00ca2-217">![Adicionar Usuário](./media/active-directory-saas-bonus-tutorial/ic781044.png "Adicionar Usuário")</span><span class="sxs-lookup"><span data-stu-id="00ca2-217">![Add User](./media/active-directory-saas-bonus-tutorial/ic781044.png "Add User")</span></span>

6. <span data-ttu-id="00ca2-218">No diálogo **Adicionar Usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="00ca2-218">On the **Add User** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="00ca2-219">![Adicionar Usuário](./media/active-directory-saas-bonus-tutorial/ic781045.png "Adicionar Usuário")</span><span class="sxs-lookup"><span data-stu-id="00ca2-219">![Add User](./media/active-directory-saas-bonus-tutorial/ic781045.png "Add User")</span></span>  

    <span data-ttu-id="00ca2-220">a.</span><span class="sxs-lookup"><span data-stu-id="00ca2-220">a.</span></span> <span data-ttu-id="00ca2-221">Na caixa de texto **Nome**, digite o nome do usuário, como **Brenda**.</span><span class="sxs-lookup"><span data-stu-id="00ca2-221">In the **First name** textbox, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="00ca2-222">b.</span><span class="sxs-lookup"><span data-stu-id="00ca2-222">b.</span></span> <span data-ttu-id="00ca2-223">Na caixa de texto **Sobrenome**, digite o sobrenome do usuário como **Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="00ca2-223">In the **Last name** textbox, enter the last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="00ca2-224">c.</span><span class="sxs-lookup"><span data-stu-id="00ca2-224">c.</span></span> <span data-ttu-id="00ca2-225">Na caixa de texto **Email**, insira o email do usuário, como **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="00ca2-225">In the **Email** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="00ca2-226">d.</span><span class="sxs-lookup"><span data-stu-id="00ca2-226">d.</span></span> <span data-ttu-id="00ca2-227">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="00ca2-227">Click **Save**.</span></span>
   
     >[!NOTE]
     ><span data-ttu-id="00ca2-228">O titular da conta do Azure AD recebe um email com um link de confirmação de conta antes que ela se torne ativa.</span><span class="sxs-lookup"><span data-stu-id="00ca2-228">The Azure AD account holder receives an email that includes a link to confirm the account before it becomes active.</span></span>
     >  

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="00ca2-229">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="00ca2-229">Assign the Azure AD test user</span></span>

<span data-ttu-id="00ca2-230">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Bonusly.</span><span class="sxs-lookup"><span data-stu-id="00ca2-230">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Bonusly.</span></span>

![Atribuir a função de usuário][200] 

<span data-ttu-id="00ca2-232">**Para atribuir Brenda Fernandes ao Bonusly, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="00ca2-232">**To assign Britta Simon to Bonusly, perform the following steps:**</span></span>

1. <span data-ttu-id="00ca2-233">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="00ca2-233">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="00ca2-235">Na lista de aplicativos, escolha o **Bonusly**.</span><span class="sxs-lookup"><span data-stu-id="00ca2-235">In the applications list, select **Bonusly**.</span></span>

    ![O link do Bonusly na lista de Aplicativos](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_app.png) 

3. <span data-ttu-id="00ca2-237">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="00ca2-237">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202] 

4. <span data-ttu-id="00ca2-239">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="00ca2-239">Click **Add** button.</span></span> <span data-ttu-id="00ca2-240">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="00ca2-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="00ca2-242">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="00ca2-242">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="00ca2-243">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="00ca2-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="00ca2-244">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="00ca2-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="00ca2-245">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="00ca2-245">Test single sign-on</span></span>

<span data-ttu-id="00ca2-246">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="00ca2-246">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="00ca2-247">Quando você clicar no bloco Bonusly no Painel de Acesso, deverá ser automaticamente conectado ao seu aplicativo Bonusly.</span><span class="sxs-lookup"><span data-stu-id="00ca2-247">When you click the Bonusly tile in the Access Panel, you should get automatically signed-on to your Bonusly application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="00ca2-248">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="00ca2-248">Additional resources</span></span>

* [<span data-ttu-id="00ca2-249">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="00ca2-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="00ca2-250">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="00ca2-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_203.png

