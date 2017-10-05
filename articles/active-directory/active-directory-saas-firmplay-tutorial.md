---
title: "Tutorial: Integração do Azure Active Directory com o FirmPlay - Employee Advocacy for Recruiting | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o FirmPlay - Employee Advocacy for Recruiting."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a6799629-7546-43f8-a966-956db32864b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: 3cddd5b9508159089bf344dbb3882d462799747c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-firmplay---employee-advocacy-for-recruiting"></a><span data-ttu-id="44da8-103">Tutorial: Integração do Azure Active Directory com FirmPlay - Employee Advocacy for Recruiting</span><span class="sxs-lookup"><span data-stu-id="44da8-103">Tutorial: Azure Active Directory integration with FirmPlay - Employee Advocacy for Recruiting</span></span>

<span data-ttu-id="44da8-104">Neste tutorial, você aprenderá a integrar o FirmPlay - Employee Advocacy for Recruiting com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="44da8-104">In this tutorial, you learn how to integrate FirmPlay - Employee Advocacy for Recruiting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="44da8-105">Integrar o FirmPlay - Employee Advocacy for Recruiting com o Azure AD fornece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="44da8-105">Integrating FirmPlay - Employee Advocacy for Recruiting with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="44da8-106">Você pode controlar no Azure AD quem tem acesso ao FirmPlay - Employee Advocacy for Recruiting</span><span class="sxs-lookup"><span data-stu-id="44da8-106">You can control in Azure AD who has access to FirmPlay - Employee Advocacy for Recruiting</span></span>
- <span data-ttu-id="44da8-107">Você pode habilitar os usuários para fazerem logon automaticamente no FirmPlay - Employee Advocacy for Recruiting (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="44da8-107">You can enable your users to automatically get signed-on to FirmPlay - Employee Advocacy for Recruiting (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="44da8-108">Você pode gerenciar suas contas em um único local - o portal de Gerenciamento do Azure</span><span class="sxs-lookup"><span data-stu-id="44da8-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="44da8-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="44da8-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44da8-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="44da8-110">Prerequisites</span></span>

<span data-ttu-id="44da8-111">Para configurar a integração do Azure AD com FirmPlay - Employee Advocacy for Recruiting, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="44da8-111">To configure Azure AD integration with FirmPlay - Employee Advocacy for Recruiting, you need the following items:</span></span>

- <span data-ttu-id="44da8-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="44da8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="44da8-113">Uma assinatura habilitada com logon único do FirmPlay - Employee Advocacy for Recruiting</span><span class="sxs-lookup"><span data-stu-id="44da8-113">A FirmPlay - Employee Advocacy for Recruiting single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="44da8-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="44da8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="44da8-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="44da8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="44da8-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="44da8-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="44da8-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="44da8-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="44da8-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="44da8-118">Scenario description</span></span>
<span data-ttu-id="44da8-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="44da8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="44da8-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="44da8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="44da8-121">Adicionando o FirmPlay - Employee Advocacy for Recruiting a partir da galeria</span><span class="sxs-lookup"><span data-stu-id="44da8-121">Adding FirmPlay - Employee Advocacy for Recruiting from the gallery</span></span>
2. <span data-ttu-id="44da8-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="44da8-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-firmplay---employee-advocacy-for-recruiting-from-the-gallery"></a><span data-ttu-id="44da8-123">Adicionando o FirmPlay - Employee Advocacy for Recruiting a partir da galeria</span><span class="sxs-lookup"><span data-stu-id="44da8-123">Adding FirmPlay - Employee Advocacy for Recruiting from the gallery</span></span>
<span data-ttu-id="44da8-124">Para configurar a integração do FirmPlay - Employee Advocacy for Recruiting no Azure AD, você precisa adicionar o FirmPlay na galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="44da8-124">To configure the integration of FirmPlay - Employee Advocacy for Recruiting into Azure AD, you need to add FirmPlay - Employee Advocacy for Recruiting from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="44da8-125">**Para adicionar o FirmPlay - Employee Advocacy for Recruiting na galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="44da8-125">**To add FirmPlay - Employee Advocacy for Recruiting from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="44da8-126">No **[Portal de Gerenciamento do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="44da8-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="44da8-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="44da8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="44da8-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="44da8-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="44da8-131">Clique em **adicionar** botão na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="44da8-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="44da8-133">Na caixa de pesquisa, digite **FirmPlay - Employee Advocacy for Recruiting**.</span><span class="sxs-lookup"><span data-stu-id="44da8-133">In the search box, type **FirmPlay - Employee Advocacy for Recruiting**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_001.png)

5. <span data-ttu-id="44da8-135">No painel de resultados, selecione **FirmPlay - Employee Advocacy for Recruiting** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="44da8-135">In the results panel, select **FirmPlay - Employee Advocacy for Recruiting**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="44da8-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="44da8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="44da8-138">Nesta seção, você irá configurar e testar o logon único do Azure AD com o FirmPlay - Employee Advocacy for Recruiting com base em um usuário de teste denominado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="44da8-138">In this section, you configure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="44da8-139">Para o logon único funcionar, o Azure AD precisa saber qual usuário no FirmPlay - Employee Advocacy for Recruiting é equivalente a um usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="44da8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FirmPlay - Employee Advocacy for Recruiting is to a user in Azure AD.</span></span> <span data-ttu-id="44da8-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no FirmPlay - Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="44da8-140">In other words, a link relationship between an Azure AD user and the related user in FirmPlay - Employee Advocacy for Recruiting needs to be established.</span></span>

<span data-ttu-id="44da8-141">Essa relação de vínculo é estabelecida atribuindo o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** no FirmPlay - Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="44da8-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in FirmPlay - Employee Advocacy for Recruiting.</span></span>

<span data-ttu-id="44da8-142">Para configurar e testar o logon único do Azure AD com o FirmPlay - Employee Advocacy for Recruiting, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="44da8-142">To configure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="44da8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="44da8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="44da8-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** - para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="44da8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="44da8-145">**[Criando um usuário de teste FirmPlay - Employee Advocacy for Recruiting](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)** - para ter um equivalente de Brenda Fernandes no FirmPlay vinculado à representação dela no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="44da8-145">**[Creating a FirmPlay - Employee Advocacy for Recruiting test user](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)** - to have a counterpart of Britta Simon in FirmPlay: Employee Advocacy for Recruiting that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="44da8-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** - para habilitar Britta Simon a usar o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="44da8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="44da8-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="44da8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="44da8-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="44da8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="44da8-149">Nesta seção, você habilitará o logon único do Azure AD no portal de Gerenciamento do Azure e irá configurar o logon único no aplicativo FirmPlay - Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="44da8-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your FirmPlay - Employee Advocacy for Recruiting application.</span></span>

<span data-ttu-id="44da8-150">**Para configurar o logon único do Azure AD com o FirmPlay - Employee Advocacy for Recruiting, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="44da8-150">**To configure Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, perform the following steps:**</span></span>

1. <span data-ttu-id="44da8-151">No Portal de Gerenciamento do Azure, na página de integração do aplicativo **FirmPlay - Employee Advocacy for Recruiting**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="44da8-151">In the Azure Management portal, on the **FirmPlay - Employee Advocacy for Recruiting** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="44da8-153">Na caixa de diálogo **Logon único**, como **Modo**, selecione **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="44da8-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_01.png)

3. <span data-ttu-id="44da8-155">Na seção **Domínio e URLs do FirmPlay - Employee Advocacy for Recruiting** seção, na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão:`https://<your-subdomain>.firmplay.com/`</span><span class="sxs-lookup"><span data-stu-id="44da8-155">On the **FirmPlay - Employee Advocacy for Recruiting Domain and URLs** section, in the **Sign On URL** textbox, type a URL using the following pattern: `https://<your-subdomain>.firmplay.com/`</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_02.png)

    > [!NOTE] 
    > <span data-ttu-id="44da8-157">Observe que esse não é o valor real.</span><span class="sxs-lookup"><span data-stu-id="44da8-157">Please note that this is not the real value.</span></span> <span data-ttu-id="44da8-158">Você precisa atualizar esse valor com a URL de Entrada real.</span><span class="sxs-lookup"><span data-stu-id="44da8-158">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="44da8-159">Entre em contato com a [equipe de suporte do FirmPlay - Employee Advocacy for Recruiting](mailto:engineering@firmplay.com) para obter esse valor.</span><span class="sxs-lookup"><span data-stu-id="44da8-159">Contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) to get this value.</span></span> 

4. <span data-ttu-id="44da8-160">Na seção **Certificado de Autenticação SAML**, clique em **Criar novo certificado**.</span><span class="sxs-lookup"><span data-stu-id="44da8-160">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_03.png)   

5. <span data-ttu-id="44da8-162">Na caixa de diálogo **Criar um Novo Certificado**, clique no ícone de calendário e selecione uma **data de expiração**.</span><span class="sxs-lookup"><span data-stu-id="44da8-162">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="44da8-163">Em seguida, clique no botão **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="44da8-163">Then click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-firmplay-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="44da8-165">Na seção **Certificado de Autenticação SAML**, selecione **Ativar o novo certificado** e clique no botão **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="44da8-165">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_04.png)

7. <span data-ttu-id="44da8-167">Na janela pop-up **Certificado de substituição**, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="44da8-167">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-firmplay-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="44da8-169">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="44da8-169">On the **SAML Signing Certificate** section, click **Certificate (base64)** and then save the certificate file on your computer.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_05.png) 

9. <span data-ttu-id="44da8-171">Na seção **Configuração do FirmPlay - Employee Advocacy for Recruiting**, clique em **Configurar FirmPlay - Employee Advocacy for Recruiting** para abrir a caixa de diálogo **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="44da8-171">On the **FirmPlay - Employee Advocacy for Recruiting Configuration** section, click **Configure FirmPlay - Employee Advocacy for Recruiting** to open **Configure sign-on** dialog.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_06.png) 

    ![Configurar Logon Único](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_07.png)

10. <span data-ttu-id="44da8-174">Para que o SSO seja configurado para seu aplicativo, entre em contato com a [equipe de suporte do FirmPlay - Employee Advocacy for Recruiting](mailto:engineering@firmplay.com) e forneça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="44da8-174">To get SSO configured for your application, contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) and provide them with the following:</span></span> 

    <span data-ttu-id="44da8-175">• O **Arquivo de certificado** baixado</span><span class="sxs-lookup"><span data-stu-id="44da8-175">•  The downloaded **Certificate file**</span></span>

    <span data-ttu-id="44da8-176">• A **URL do Serviço de Logon Único SAML**</span><span class="sxs-lookup"><span data-stu-id="44da8-176">•  The **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="44da8-177">• A **ID da entidade SAML**</span><span class="sxs-lookup"><span data-stu-id="44da8-177">•  The **SAML Entity ID**</span></span>

    <span data-ttu-id="44da8-178">• A **URL de Saída**</span><span class="sxs-lookup"><span data-stu-id="44da8-178">•  The **Sign-Out URL**</span></span>
  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="44da8-179">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="44da8-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="44da8-180">O objetivo desta seção é criar um usuário de teste no Portal de Gerenciamento do Azure chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="44da8-180">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="44da8-182">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="44da8-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="44da8-183">No **portal de Gerenciamento do Azure**, no painel navegação à esquerda, clique em **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="44da8-183">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-firmplay-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="44da8-185">Vá para **usuários e grupos** e clique em **todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="44da8-185">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-firmplay-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="44da8-187">Na parte superior da caixa de diálogo clique **adicionar** para abrir o **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="44da8-187">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-firmplay-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="44da8-189">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="44da8-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-firmplay-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="44da8-191">a.</span><span class="sxs-lookup"><span data-stu-id="44da8-191">a.</span></span> <span data-ttu-id="44da8-192">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="44da8-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="44da8-193">b.</span><span class="sxs-lookup"><span data-stu-id="44da8-193">b.</span></span> <span data-ttu-id="44da8-194">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="44da8-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="44da8-195">c.</span><span class="sxs-lookup"><span data-stu-id="44da8-195">c.</span></span> <span data-ttu-id="44da8-196">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="44da8-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="44da8-197">d.</span><span class="sxs-lookup"><span data-stu-id="44da8-197">d.</span></span> <span data-ttu-id="44da8-198">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="44da8-198">Click **Create**.</span></span> 



### <a name="creating-a-firmplay---employee-advocacy-for-recruiting-test-user"></a><span data-ttu-id="44da8-199">Criando um usuário de teste do FirmPlay - Employee Advocacy for Recruiting</span><span class="sxs-lookup"><span data-stu-id="44da8-199">Creating a FirmPlay - Employee Advocacy for Recruiting test user</span></span>

<span data-ttu-id="44da8-200">Nesta seção, você irá criar um usuário denominado Brenda Fernandes no FirmPlay - Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="44da8-200">In this section, you create a user called Britta Simon in FirmPlay - Employee Advocacy for Recruiting.</span></span> <span data-ttu-id="44da8-201">Trabalhe com a [ equipe de suporte do FirmPlay - Employee Advocacy for Recruiting](mailto:engineering@firmplay.com) para adicionar os usuários na plataforma do FirmPlay - Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="44da8-201">Please work with [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) to add the users in the FirmPlay - Employee Advocacy for Recruiting platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="44da8-202">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="44da8-202">Assigning the Azure AD test user</span></span>

<span data-ttu-id="44da8-203">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao FirmPlay - Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="44da8-203">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to FirmPlay - Employee Advocacy for Recruiting.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="44da8-205">**Para adicionar Brenda Fernandes ao FirmPlay - Employee Advocacy for Recruiting, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="44da8-205">**To assign Britta Simon to FirmPlay - Employee Advocacy for Recruiting, perform the following steps:**</span></span>

1. <span data-ttu-id="44da8-206">No Portal de Gerenciamento do Azure, abra a exibição de aplicativos e, em seguida, navegue até o modo de exibição de diretório e vá para **Aplicativos empresariais**, depois clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="44da8-206">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="44da8-208">Na lista de aplicativos, selecione **FirmPlay - Employee Advocacy for Recruiting**.</span><span class="sxs-lookup"><span data-stu-id="44da8-208">In the applications list, select **FirmPlay - Employee Advocacy for Recruiting**.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_50.png) 

3. <span data-ttu-id="44da8-210">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="44da8-210">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="44da8-212">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="44da8-212">Click **Add** button.</span></span> <span data-ttu-id="44da8-213">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="44da8-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="44da8-215">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="44da8-215">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="44da8-216">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="44da8-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="44da8-217">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="44da8-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="44da8-218">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="44da8-218">Testing single sign-on</span></span>

<span data-ttu-id="44da8-219">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="44da8-219">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="44da8-220">Quando você clicar no bloco FirmPlay - Employee Advocacy for Recruiting no Painel de Acesso, deverá ser automaticamente conectado ao aplicativo FirmPlay - Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="44da8-220">When you click the FirmPlay - Employee Advocacy for Recruiting tile in the Access Panel, you should get automatically signed-on to your FirmPlay - Employee Advocacy for Recruiting application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="44da8-221">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="44da8-221">Additional resources</span></span>

* [<span data-ttu-id="44da8-222">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="44da8-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="44da8-223">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="44da8-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_203.png