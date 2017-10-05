---
title: "Tutorial: integração do Azure Active Directory ao FreshDesk | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o FreshDesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2a3e5aa-7b5a-4fe4-9285-45dbe6e8efcc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: f4b47e345a40b64f69ad8a4618564662b4a6c879
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshdesk"></a><span data-ttu-id="23517-103">Tutorial: integração do Azure Active Directory ao FreshDesk</span><span class="sxs-lookup"><span data-stu-id="23517-103">Tutorial: Azure Active Directory integration with FreshDesk</span></span>

<span data-ttu-id="23517-104">Neste tutorial, você aprenderá a integrar o FreshDesk ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="23517-104">In this tutorial, you learn how to integrate FreshDesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="23517-105">A integração do FreshDesk ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="23517-105">Integrating FreshDesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="23517-106">No Azure AD, é possível controlar quem tem acesso ao FreshDesk</span><span class="sxs-lookup"><span data-stu-id="23517-106">You can control in Azure AD who has access to FreshDesk</span></span>
- <span data-ttu-id="23517-107">Você pode habilitar seus usuários, com as respectivas contas do Azure AD, a fazer logon automaticamente no FreshDesk (logon único)</span><span class="sxs-lookup"><span data-stu-id="23517-107">You can enable your users to automatically get signed-on to FreshDesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="23517-108">Você pode gerenciar suas contas em um único local - o portal de Gerenciamento do Azure</span><span class="sxs-lookup"><span data-stu-id="23517-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="23517-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="23517-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="23517-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="23517-110">Prerequisites</span></span>

<span data-ttu-id="23517-111">Para configurar a integração do Azure AD ao FreshDesk, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="23517-111">To configure Azure AD integration with FreshDesk, you need the following items:</span></span>

- <span data-ttu-id="23517-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="23517-112">An Azure AD subscription</span></span>
- <span data-ttu-id="23517-113">Uma assinatura do FreshDesk com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="23517-113">A FreshDesk single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="23517-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="23517-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="23517-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="23517-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="23517-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="23517-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="23517-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="23517-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="23517-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="23517-118">Scenario description</span></span>
<span data-ttu-id="23517-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="23517-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="23517-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="23517-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="23517-121">Adicionar o FreshDesk da galeria</span><span class="sxs-lookup"><span data-stu-id="23517-121">Adding FreshDesk from the gallery</span></span>
2. <span data-ttu-id="23517-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="23517-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshdesk-from-the-gallery"></a><span data-ttu-id="23517-123">Adicionar o FreshDesk da galeria</span><span class="sxs-lookup"><span data-stu-id="23517-123">Adding FreshDesk from the gallery</span></span>
<span data-ttu-id="23517-124">Para configurar a integração do FreshDesk ao Azure AD, você precisa adicionar o FreshDesk da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="23517-124">To configure the integration of FreshDesk into Azure AD, you need to add FreshDesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="23517-125">**Para adicionar o FreshDesk por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="23517-125">**To add FreshDesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="23517-126">No **[Portal de Gerenciamento do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="23517-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="23517-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="23517-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="23517-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="23517-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="23517-131">Clique em **adicionar** botão na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="23517-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="23517-133">Na caixa de pesquisa, digite **FreshDesk**.</span><span class="sxs-lookup"><span data-stu-id="23517-133">In the search box, type **FreshDesk**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_search.png)

5. <span data-ttu-id="23517-135">No painel de resultados, selecione **FreshDesk** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="23517-135">In the results panel, select **FreshDesk**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="23517-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="23517-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="23517-138">Nesta seção, você configurará e testará o logon único do Azure AD com o FreshDesk, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="23517-138">In this section, you configure and test Azure AD single sign-on with FreshDesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="23517-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do FreshDesk é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="23517-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FreshDesk is to a user in Azure AD.</span></span> <span data-ttu-id="23517-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="23517-140">In other words, a link relationship between an Azure AD user and the related user in FreshDesk needs to be established.</span></span>

<span data-ttu-id="23517-141">Essa relação de vínculo é estabelecida atribuindo o valor de **nome de usuário** ao Azure AD como sendo o valor de **Nome de usuário** no FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="23517-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in FreshDesk.</span></span>

<span data-ttu-id="23517-142">Para configurar e testar o logon único do Azure AD com o FreshDesk, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="23517-142">To configure and test Azure AD single sign-on with FreshDesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="23517-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="23517-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="23517-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** - para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="23517-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="23517-145">**[Criação de um usuário de teste do FreshDesk](#creating-a-freshdesk-test-user)** – para ter um equivalente de Brenda Fernandes no FreshDesk que esteja vinculado à representação dela no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="23517-145">**[Creating a FreshDesk test user](#creating-a-freshdesk-test-user)** - to have a counterpart of Britta Simon in FreshDesk that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="23517-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** - para habilitar Britta Simon a usar o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="23517-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="23517-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="23517-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="23517-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="23517-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="23517-149">Nesta seção, você habilita o logon único do Azure AD no Portal de Gerenciamento do Azure e configura o logon único em seu aplicativo FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="23517-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your FreshDesk application.</span></span>

<span data-ttu-id="23517-150">**Para configurar o logon único do Azure AD com o FreshDesk, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="23517-150">**To configure Azure AD single sign-on with FreshDesk, perform the following steps:**</span></span>

1. <span data-ttu-id="23517-151">No Portal de Gerenciamento do Azure, na página de integração de aplicativos do **FreshDesk**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="23517-151">In the Azure Management portal, on the **FreshDesk** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="23517-153">Na caixa de diálogo **Logon único**, como **Modo**, selecione **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="23517-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_samlbase.png)

3. <span data-ttu-id="23517-155">Na seção **Domínio e URLs do FreshDesk**, insira a **URL de logon** como: `https://<tenant-name>.freshdesk.com` ou qualquer outro valor sugerido pelo FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="23517-155">On the **FreshDesk Domain and URLs** section, please enter the **Sign-on URL** as: `https://<tenant-name>.freshdesk.com` or any other value Freshdesk has suggested.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_url.png)

    > [!NOTE] 
    > <span data-ttu-id="23517-157">Observe que esse não é o valor real.</span><span class="sxs-lookup"><span data-stu-id="23517-157">Please note that this is not the real value.</span></span> <span data-ttu-id="23517-158">Você precisa atualizar o valor com a URL de Entrada real.</span><span class="sxs-lookup"><span data-stu-id="23517-158">You have to update the value with the actual Sign-on URL.</span></span> <span data-ttu-id="23517-159">Para obter esse valor, entre em contato com a [equipe de suporte do cliente FreshDesk](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg).</span><span class="sxs-lookup"><span data-stu-id="23517-159">Contact [FreshDesk Client support team](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg) to get this value.</span></span>  

4. <span data-ttu-id="23517-160">Na seção **Certificado de Autenticação SAML**, clique em **Certificado** e, em seguida, salve o certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="23517-160">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_certificate.png) 

5. <span data-ttu-id="23517-162">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="23517-162">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-freshdesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="23517-164">Na seção **Configuração do FreshDesk**, clique em **Configurar o FreshDesk** para abrir a janela Configurar logon.</span><span class="sxs-lookup"><span data-stu-id="23517-164">On the **FreshDesk Configuration** section, click **Configure FreshDesk** to open Configure sign-on window.</span></span> <span data-ttu-id="23517-165">Copie a URL do serviço de logon único do SAML e a URL de logoff da seção de **Referência Rápida**.</span><span class="sxs-lookup"><span data-stu-id="23517-165">Copy the SAML Single Sign-On Service URL and Sign-Out URL from the **Quick Reference** section.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_configure.png)

7. <span data-ttu-id="23517-167">Em uma janela diferente do navegador da Web, faça logon no site da sua empresa do Freshdesk como administrador.</span><span class="sxs-lookup"><span data-stu-id="23517-167">In a different web browser window, log into your Freshdesk company site as an administrator.</span></span>

8. <span data-ttu-id="23517-168">No menu na parte superior, clique em **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="23517-168">In the menu on the top, click **Admin**.</span></span>
   
   <span data-ttu-id="23517-169">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="23517-169">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "Admin")</span></span>

9. <span data-ttu-id="23517-170">Na guia **Configurações Gerais**, clique em **Segurança**.</span><span class="sxs-lookup"><span data-stu-id="23517-170">In the **General Settings** tab, click **Security**.</span></span>
   
   <span data-ttu-id="23517-171">![Segurança](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "Segurança")</span><span class="sxs-lookup"><span data-stu-id="23517-171">![Security](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "Security")</span></span>

10. <span data-ttu-id="23517-172">Na seção **Segurança** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="23517-172">In the **Security** section, perform the following steps:</span></span>
   
    <span data-ttu-id="23517-173">![Logon Único](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "Logon Único")</span><span class="sxs-lookup"><span data-stu-id="23517-173">![Single Sign On](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "Single Sign On")</span></span>
   
    <span data-ttu-id="23517-174">a.</span><span class="sxs-lookup"><span data-stu-id="23517-174">a.</span></span> <span data-ttu-id="23517-175">Para **SSO (Logon Único)**, selecione **Ativado**.</span><span class="sxs-lookup"><span data-stu-id="23517-175">For **Single Sign On (SSO)**, select **On**.</span></span>

    <span data-ttu-id="23517-176">b.</span><span class="sxs-lookup"><span data-stu-id="23517-176">b.</span></span> <span data-ttu-id="23517-177">Selecione **SSO do SAML**.</span><span class="sxs-lookup"><span data-stu-id="23517-177">Select **SAML SSO**.</span></span>

    <span data-ttu-id="23517-178">c.</span><span class="sxs-lookup"><span data-stu-id="23517-178">c.</span></span> <span data-ttu-id="23517-179">Digite a **URL do serviço de logon único do SAML** que você copiou do Portal do Azure para a caixa de texto **URL de Logon do SAML**.</span><span class="sxs-lookup"><span data-stu-id="23517-179">Type the **SAML Single Sign-On Service URL** you copied from Azure portal into the **SAML Login URL** textbox.</span></span>

    <span data-ttu-id="23517-180">d.</span><span class="sxs-lookup"><span data-stu-id="23517-180">d.</span></span> <span data-ttu-id="23517-181">Digite a **URL de Saída** que você copiou do Portal do Azure para a caixa de texto **URL de Logoff**.</span><span class="sxs-lookup"><span data-stu-id="23517-181">Type the **Sign-Out URL**  you copied from Azure portal into the **Logout URL** textbox.</span></span>

    <span data-ttu-id="23517-182">e.</span><span class="sxs-lookup"><span data-stu-id="23517-182">e.</span></span> <span data-ttu-id="23517-183">Copie o valor de **Impressão Digital** do certificado baixado do Portal do Azure e cole-o na caixa de texto **Impressão Digital do Certificado de Segurança**.</span><span class="sxs-lookup"><span data-stu-id="23517-183">Copy the **Thumbprint** value from the downloaded certificate from Azure portal and paste it into the **Security Certificate Fingerprint** textbox.</span></span>  
 
    >[!TIP]
    ><span data-ttu-id="23517-184">Para obter mais detalhes, consulte [Como recuperar o valor de impressão digital de um certificado](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="23517-184">For more details, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span> 
    
    <span data-ttu-id="23517-185">f.</span><span class="sxs-lookup"><span data-stu-id="23517-185">f.</span></span> <span data-ttu-id="23517-186">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="23517-186">Click **Save**.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="23517-187">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="23517-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="23517-188">O objetivo desta seção é criar um usuário de teste no Portal de Gerenciamento do Azure chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="23517-188">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="23517-190">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="23517-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="23517-191">No **portal de Gerenciamento do Azure**, no painel navegação à esquerda, clique em **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="23517-191">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="23517-193">Vá para **usuários e grupos** e clique em **todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="23517-193">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="23517-195">Na parte superior da caixa de diálogo clique **adicionar** para abrir o **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="23517-195">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="23517-197">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="23517-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="23517-199">a.</span><span class="sxs-lookup"><span data-stu-id="23517-199">a.</span></span> <span data-ttu-id="23517-200">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="23517-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="23517-201">b.</span><span class="sxs-lookup"><span data-stu-id="23517-201">b.</span></span> <span data-ttu-id="23517-202">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="23517-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="23517-203">c.</span><span class="sxs-lookup"><span data-stu-id="23517-203">c.</span></span> <span data-ttu-id="23517-204">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="23517-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="23517-205">d.</span><span class="sxs-lookup"><span data-stu-id="23517-205">d.</span></span> <span data-ttu-id="23517-206">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="23517-206">Click **Create**.</span></span>
 
### <a name="creating-a-freshdesk-test-user"></a><span data-ttu-id="23517-207">Criar um usuário de teste FreshDesk</span><span class="sxs-lookup"><span data-stu-id="23517-207">Creating a FreshDesk test user</span></span>

<span data-ttu-id="23517-208">Para permitir que os usuários do Azure AD façam logon no FreshDesk, eles devem ser provisionados no FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="23517-208">In order to enable Azure AD users to log into FreshDesk, they must be provisioned into FreshDesk.</span></span>  
<span data-ttu-id="23517-209">No caso do FreshDesk, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="23517-209">In the case of FreshDesk, provisioning is a manual task.</span></span>

<span data-ttu-id="23517-210">**Para provisionar contas de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="23517-210">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="23517-211">Faça logon em seu locatário do **Freshdesk** .</span><span class="sxs-lookup"><span data-stu-id="23517-211">Log in to your **Freshdesk** tenant.</span></span>
2. <span data-ttu-id="23517-212">No menu na parte superior, clique em **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="23517-212">In the menu on the top, click **Admin**.</span></span>
   
   <span data-ttu-id="23517-213">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="23517-213">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "Admin")</span></span>

3. <span data-ttu-id="23517-214">Na guia **Configurações Gerais**, clique em **Agentes**.</span><span class="sxs-lookup"><span data-stu-id="23517-214">In the **General Settings** tab, click **Agents**.</span></span>
   
   <span data-ttu-id="23517-215">![Agentes](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "Agentes")</span><span class="sxs-lookup"><span data-stu-id="23517-215">![Agents](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "Agents")</span></span>

4. <span data-ttu-id="23517-216">Clique em **Novo Agente**.</span><span class="sxs-lookup"><span data-stu-id="23517-216">Click **New Agent**.</span></span>
   
    <span data-ttu-id="23517-217">![Novo Agente](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "Novo Agente")</span><span class="sxs-lookup"><span data-stu-id="23517-217">![New Agent](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "New Agent")</span></span>

5. <span data-ttu-id="23517-218">Na caixa de diálogo Informações sobre o Agente, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="23517-218">On the Agent Information dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="23517-219">![Informações de Agente](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "Informações de Agente")</span><span class="sxs-lookup"><span data-stu-id="23517-219">![Agent Information](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "Agent Information")</span></span>
   
   <span data-ttu-id="23517-220">a.</span><span class="sxs-lookup"><span data-stu-id="23517-220">a.</span></span> <span data-ttu-id="23517-221">Na caixa de texto **Nome Completo** , digite o nome da conta do Azure AD que você deseja provisionar.</span><span class="sxs-lookup"><span data-stu-id="23517-221">In the **Full Name** textbox, type the name of the Azure AD account you want to provision.</span></span>

   <span data-ttu-id="23517-222">b.</span><span class="sxs-lookup"><span data-stu-id="23517-222">b.</span></span> <span data-ttu-id="23517-223">Na caixa de texto **Email** , digite o endereço de email do Azure AD da conta do Azure AD que você deseja provisionar.</span><span class="sxs-lookup"><span data-stu-id="23517-223">In the **Email** textbox, type the Azure AD email address of the Azure AD account you want to provision.</span></span>

   <span data-ttu-id="23517-224">c.</span><span class="sxs-lookup"><span data-stu-id="23517-224">c.</span></span> <span data-ttu-id="23517-225">Na caixa de texto **Título** , digite a conta do Azure AD que você deseja provisionar.</span><span class="sxs-lookup"><span data-stu-id="23517-225">In the **Title** textbox, type the title of the Azure AD account you want to provision.</span></span>

   <span data-ttu-id="23517-226">d.</span><span class="sxs-lookup"><span data-stu-id="23517-226">d.</span></span> <span data-ttu-id="23517-227">Selecione **Função de agentes** e clique em **Atribuir**.</span><span class="sxs-lookup"><span data-stu-id="23517-227">Select **Agents role**, and then click **Assign**.</span></span>
       
   <span data-ttu-id="23517-228">e.</span><span class="sxs-lookup"><span data-stu-id="23517-228">e.</span></span> <span data-ttu-id="23517-229">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="23517-229">Click **Save**.</span></span>     
   
    >[!NOTE]
    ><span data-ttu-id="23517-230">O titular da conta do Azure AD receberá um email que inclui um link para confirmar a conta antes que ela se torne ativa.</span><span class="sxs-lookup"><span data-stu-id="23517-230">The Azure AD account holder will get an email that includes a link to confirm the account before it is activated.</span></span> 
    > 
    
    >[!NOTE]
    ><span data-ttu-id="23517-231">É possível usar qualquer outra ferramenta de criação da conta de usuário do Freshdesk ou APIs fornecidas pelo Freshdesk para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="23517-231">You can use any other Freshdesk user account creation tools or APIs provided by Freshdesk to provision AAD user accounts.</span></span> <span data-ttu-id="23517-232">para o FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="23517-232">to FreshDesk.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="23517-233">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="23517-233">Assigning the Azure AD test user</span></span>

<span data-ttu-id="23517-234">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Box.</span><span class="sxs-lookup"><span data-stu-id="23517-234">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Box.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="23517-236">**Para atribuir Brenda Fernandes ao FreshDesk, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="23517-236">**To assign Britta Simon to FreshDesk, perform the following steps:**</span></span>

1. <span data-ttu-id="23517-237">No portal de gerenciamento do Azure, abra a exibição de aplicativos e, em seguida, navegue até o modo de exibição de diretório e vá para **aplicativos empresariais** e clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="23517-237">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="23517-239">Na lista de aplicativos, escolha **FreshDesk**.</span><span class="sxs-lookup"><span data-stu-id="23517-239">In the applications list, select **FreshDesk**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_app.png) 

3. <span data-ttu-id="23517-241">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="23517-241">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="23517-243">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="23517-243">Click **Add** button.</span></span> <span data-ttu-id="23517-244">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="23517-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="23517-246">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="23517-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="23517-247">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="23517-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="23517-248">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="23517-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="23517-249">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="23517-249">Testing single sign-on</span></span>

<span data-ttu-id="23517-250">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="23517-250">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="23517-251">Quando clicar no bloco FreshDesk no Painel de Acesso, você deverá ser conduzido à página de logon para ser conectado automaticamente ao seu aplicativo FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="23517-251">When you click the FreshDesk tile in the Access Panel, you should get login page to get signed-on to your FreshDesk application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="23517-252">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="23517-252">Additional resources</span></span>

* [<span data-ttu-id="23517-253">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="23517-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="23517-254">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="23517-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_203.png

