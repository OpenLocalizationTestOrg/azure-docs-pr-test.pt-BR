---
title: "Tutorial: Integração do Azure Active Directory ao ScreenSteps | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o ScreenSteps."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4563fe94-a88f-4895-a07f-79df44889cf9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: b6ded8ba1adf03fdccbdb7573c09fae1857c8b16
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-screensteps"></a><span data-ttu-id="26857-103">Tutorial: Integração do Active Directory do Azure com o ScreenSteps</span><span class="sxs-lookup"><span data-stu-id="26857-103">Tutorial: Azure Active Directory integration with ScreenSteps</span></span>

<span data-ttu-id="26857-104">Neste tutorial, você aprende a integrar o ScreenSteps ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="26857-104">In this tutorial, you learn how to integrate ScreenSteps with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="26857-105">A integração do ScreenSteps ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="26857-105">Integrating ScreenSteps with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="26857-106">No Azure AD, é possível controlar quem tem acesso ao ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="26857-106">You can control in Azure AD who has access to ScreenSteps.</span></span>
- <span data-ttu-id="26857-107">Você pode permitir que seus usuários façam logon automaticamente no ScreenSteps (logon único) com as respectivas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26857-107">You can enable your users to automatically get signed-on to ScreenSteps (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="26857-108">Você pode gerenciar suas contas em um único local central – o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="26857-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="26857-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="26857-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26857-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="26857-110">Prerequisites</span></span>

<span data-ttu-id="26857-111">Para configurar a integração do Azure AD ao ScreenSteps, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="26857-111">To configure Azure AD integration with ScreenSteps, you need the following items:</span></span>

- <span data-ttu-id="26857-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="26857-112">An Azure AD subscription</span></span>
- <span data-ttu-id="26857-113">Uma assinatura do ScreenSteps habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="26857-113">A ScreenSteps single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="26857-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="26857-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="26857-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="26857-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="26857-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="26857-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="26857-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="26857-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="26857-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="26857-118">Scenario description</span></span>
<span data-ttu-id="26857-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="26857-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="26857-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="26857-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="26857-121">Adicionar o ScreenSteps por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="26857-121">Adding ScreenSteps from the gallery</span></span>
2. <span data-ttu-id="26857-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="26857-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-screensteps-from-the-gallery"></a><span data-ttu-id="26857-123">Adicionar o ScreenSteps por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="26857-123">Adding ScreenSteps from the gallery</span></span>
<span data-ttu-id="26857-124">Para configurar a integração do ScreenSteps ao Azure AD, é necessário adicionar o ScreenSteps à lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="26857-124">To configure the integration of ScreenSteps into Azure AD, you need to add ScreenSteps from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="26857-125">**Para adicionar o ScreenSteps por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="26857-125">**To add ScreenSteps from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="26857-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="26857-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="26857-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="26857-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="26857-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="26857-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="26857-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="26857-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="26857-133">Na caixa de pesquisa, digite **ScreenSteps**, selecione **ScreenSteps** no painel de resultados e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="26857-133">In the search box, type **ScreenSteps**, select **ScreenSteps** from result panel then click **Add** button to add the application.</span></span>

    ![ScreenSteps na lista de resultados](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="26857-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="26857-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="26857-136">Nesta seção, você configurará e testará o logon único do Azure AD com o ScreenSteps, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="26857-136">In this section, you configure and test Azure AD single sign-on with ScreenSteps based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="26857-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do ScreenSteps é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26857-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ScreenSteps is to a user in Azure AD.</span></span> <span data-ttu-id="26857-138">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="26857-138">In other words, a link relationship between an Azure AD user and the related user in ScreenSteps needs to be established.</span></span>

<span data-ttu-id="26857-139">No ScreenSteps, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="26857-139">In ScreenSteps, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="26857-140">Para configurar e testar o logon único do Azure AD com o ScreenSteps, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="26857-140">To configure and test Azure AD single sign-on with ScreenSteps, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="26857-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="26857-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="26857-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="26857-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="26857-143">**[Criar um usuário de teste do ScreenSteps](#create-a-screensteps-test-user)** – para ter um equivalente de Brenda Fernandes no ScreenSteps vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26857-143">**[Create a ScreenSteps test user](#create-a-screensteps-test-user)** - to have a counterpart of Britta Simon in ScreenSteps that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="26857-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26857-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="26857-145">**[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="26857-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="26857-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="26857-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="26857-147">Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único no aplicativo ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="26857-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ScreenSteps application.</span></span>

<span data-ttu-id="26857-148">**Para configurar o logon único do Azure AD com o ScreenSteps, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="26857-148">**To configure Azure AD single sign-on with ScreenSteps, perform the following steps:**</span></span>

1. <span data-ttu-id="26857-149">No Portal do Azure, na página de integração do aplicativo **ScreenSteps**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="26857-149">In the Azure portal, on the **ScreenSteps** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="26857-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="26857-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_samlbase.png)

3. <span data-ttu-id="26857-153">Na seção **Domínio e URLs do ScreenSteps**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="26857-153">On the **ScreenSteps Domain and URLs** section, perform the following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do ScreenSteps](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_url.png)

    <span data-ttu-id="26857-155">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<tenantname>.ScreenSteps.com`</span><span class="sxs-lookup"><span data-stu-id="26857-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.ScreenSteps.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="26857-156">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="26857-156">This value is not real.</span></span> <span data-ttu-id="26857-157">Atualize esse valor com a URL de logon real, o que é explicado posteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="26857-157">Update this value with the actual Sign-On URL, which is explained later in this tutorial.</span></span> 

4. <span data-ttu-id="26857-158">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="26857-158">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_certificate.png) 

5. <span data-ttu-id="26857-160">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="26857-160">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-screensteps-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="26857-162">Na seção **Configuração do ScreenSteps**, clique em **Configurar o ScreenSteps** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="26857-162">On the **ScreenSteps Configuration** section, click **Configure ScreenSteps** to open **Configure sign-on** window.</span></span> <span data-ttu-id="26857-163">Copie a **URL do serviço de logon único do SAML e a URL de logoff** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="26857-163">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuração do ScreenSteps](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_configure.png) 

7. <span data-ttu-id="26857-165">Em outra janela do navegador da Web, faça logon em seu site de empresa ScreenSteps como um administrador.</span><span class="sxs-lookup"><span data-stu-id="26857-165">In a different web browser window, log into your ScreenSteps company site as an administrator.</span></span>

8. <span data-ttu-id="26857-166">Clique em **Configurações da Conta**.</span><span class="sxs-lookup"><span data-stu-id="26857-166">Click **Account Settings**.</span></span>

    <span data-ttu-id="26857-167">![Gerenciamento de contas](./media/active-directory-saas-screensteps-tutorial/ic778523.png "Gerenciamento de contas")</span><span class="sxs-lookup"><span data-stu-id="26857-167">![Account management](./media/active-directory-saas-screensteps-tutorial/ic778523.png "Account management")</span></span>

9. <span data-ttu-id="26857-168">Clique em **Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="26857-168">Click **Single Sign-on**.</span></span>

    <span data-ttu-id="26857-169">![Autenticação Remota](./media/active-directory-saas-screensteps-tutorial/ic778524.png "Autenticação Remota")</span><span class="sxs-lookup"><span data-stu-id="26857-169">![Remote authentication](./media/active-directory-saas-screensteps-tutorial/ic778524.png "Remote authentication")</span></span>

10. <span data-ttu-id="26857-170">Clique em  **Criar Ponto de Extremidade de Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="26857-170">Click **Create Single Sign-on Endpoint**.</span></span>

    <span data-ttu-id="26857-171">![Autenticação Remota](./media/active-directory-saas-screensteps-tutorial/ic778525.png "Autenticação Remota")</span><span class="sxs-lookup"><span data-stu-id="26857-171">![Remote authentication](./media/active-directory-saas-screensteps-tutorial/ic778525.png "Remote authentication")</span></span>

11. <span data-ttu-id="26857-172">Na seção **Criar um Ponto de Extremidade de Logon Único**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="26857-172">In the **Create Single Sign-on Endpoint** section, perform the following steps:</span></span>

    <span data-ttu-id="26857-173">![Criar um Ponto de Extremidade de Autenticação](./media/active-directory-saas-screensteps-tutorial/ic778526.png "Criar um Ponto de Extremidade de Autenticação")</span><span class="sxs-lookup"><span data-stu-id="26857-173">![Create an authentication endpoint](./media/active-directory-saas-screensteps-tutorial/ic778526.png "Create an authentication endpoint")</span></span>
    
    <span data-ttu-id="26857-174">a.</span><span class="sxs-lookup"><span data-stu-id="26857-174">a.</span></span> <span data-ttu-id="26857-175">Na caixa de texto **Título** , digite um título.</span><span class="sxs-lookup"><span data-stu-id="26857-175">In the **Title** textbox, type a title.</span></span>
    
    <span data-ttu-id="26857-176">b.</span><span class="sxs-lookup"><span data-stu-id="26857-176">b.</span></span> <span data-ttu-id="26857-177">Na lista **Modo**, selecione **SAML**.</span><span class="sxs-lookup"><span data-stu-id="26857-177">From the **Mode** list, select **SAML**.</span></span>
    
    <span data-ttu-id="26857-178">c.</span><span class="sxs-lookup"><span data-stu-id="26857-178">c.</span></span> <span data-ttu-id="26857-179">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="26857-179">Click **Create**.</span></span>

12. <span data-ttu-id="26857-180">**Edite** o novo ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="26857-180">**Edit** the new endpoint.</span></span>

    <span data-ttu-id="26857-181">![Editar ponto de extremidade](./media/active-directory-saas-screensteps-tutorial/ic778528.png "Editar ponto de extremidade")</span><span class="sxs-lookup"><span data-stu-id="26857-181">![Edit endpoint](./media/active-directory-saas-screensteps-tutorial/ic778528.png "Edit endpoint")</span></span>

13. <span data-ttu-id="26857-182">Na seção **Editar um Ponto de Extremidade de Logon Único**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="26857-182">In the **Edit Single Sign-on Endpoint** section, perform the following steps:</span></span>

    <span data-ttu-id="26857-183">![Ponto de Extremidade de Autenticação Remota](./media/active-directory-saas-screensteps-tutorial/ic778527.png "Ponto de Extremidade de Autenticação Remota")</span><span class="sxs-lookup"><span data-stu-id="26857-183">![Remote authentication endpoint](./media/active-directory-saas-screensteps-tutorial/ic778527.png "Remote authentication endpoint")</span></span>

    <span data-ttu-id="26857-184">a.</span><span class="sxs-lookup"><span data-stu-id="26857-184">a.</span></span> <span data-ttu-id="26857-185">Clique em **Carregar novo arquivo de Certificado SAML** e carregue o certificado que você baixou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="26857-185">Click **Upload new SAML Certificate file**, and then upload the certificate, which you have downloaded from Azure portal.</span></span>
    
    <span data-ttu-id="26857-186">b.</span><span class="sxs-lookup"><span data-stu-id="26857-186">b.</span></span> <span data-ttu-id="26857-187">Cole o valor da **URL do Serviço de Logon Único SAML** copiado do Portal do Azure na caixa de texto **URL de Acesso Remoto**.</span><span class="sxs-lookup"><span data-stu-id="26857-187">Paste **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **Remote Login URL** textbox.</span></span>
    
    <span data-ttu-id="26857-188">c.</span><span class="sxs-lookup"><span data-stu-id="26857-188">c.</span></span> <span data-ttu-id="26857-189">Cole o valor da **URL de Saída** copiado do Portal do Azure na caixa de texto **URL de Logoff**.</span><span class="sxs-lookup"><span data-stu-id="26857-189">Paste **Sign-Out URL** value, which you have copied from the Azure portal into the **Log out URL** textbox.</span></span>
    
    <span data-ttu-id="26857-190">d.</span><span class="sxs-lookup"><span data-stu-id="26857-190">d.</span></span> <span data-ttu-id="26857-191">Selecione um **Grupo** para o qual atribuir usuários quando eles são provisionados.</span><span class="sxs-lookup"><span data-stu-id="26857-191">Select a **Group** to assign users to when they are provisioned.</span></span>
    
    <span data-ttu-id="26857-192">e.</span><span class="sxs-lookup"><span data-stu-id="26857-192">e.</span></span> <span data-ttu-id="26857-193">Clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="26857-193">Click **Update**.</span></span>

    <span data-ttu-id="26857-194">f.</span><span class="sxs-lookup"><span data-stu-id="26857-194">f.</span></span> <span data-ttu-id="26857-195">Copie a **URL do Consumidor SAML** para a área de transferência e cole-a na caixa de texto **URL de Logon** na seção **Domínio e URLs do ScreenSteps**.</span><span class="sxs-lookup"><span data-stu-id="26857-195">Copy the **SAML Consumer URL** to the clipboard and paste in to the **Sign-on URL** textbox in **ScreenSteps Domain and URLs** section.</span></span>
    
    <span data-ttu-id="26857-196">g.</span><span class="sxs-lookup"><span data-stu-id="26857-196">g.</span></span> <span data-ttu-id="26857-197">Retorne para **Editar Ponto de Extremidade de Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="26857-197">Return to the **Edit Single Sign-on Endpoint**.</span></span>
    
    <span data-ttu-id="26857-198">h.</span><span class="sxs-lookup"><span data-stu-id="26857-198">h.</span></span> <span data-ttu-id="26857-199">Clique no botão **Tornar padrão para a conta** para usar esse ponto de extremidade para todos os usuários que fizerem logon no ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="26857-199">Click the **Make default for account** button to use this endpoint for all users who log into ScreenSteps.</span></span> <span data-ttu-id="26857-200">Como alternativa, você pode clicar no botão **Adicionar ao Site** usar esse ponto de extremidade para sites específicos em **ScreenSteps**.</span><span class="sxs-lookup"><span data-stu-id="26857-200">Alternatively you can click the **Add to Site** button to use this endpoint for specific sites in **ScreenSteps**.</span></span>

> [!TIP]
> <span data-ttu-id="26857-201">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="26857-201">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="26857-202">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="26857-202">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="26857-203">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="26857-203">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="26857-204">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="26857-204">Create an Azure AD test user</span></span>

<span data-ttu-id="26857-205">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="26857-205">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="26857-207">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="26857-207">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="26857-208">No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="26857-208">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-screensteps-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="26857-210">Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="26857-210">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-screensteps-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="26857-212">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.</span><span class="sxs-lookup"><span data-stu-id="26857-212">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![O botão Adicionar](./media/active-directory-saas-screensteps-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="26857-214">Na caixa de diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="26857-214">In the **User** dialog box, perform the following steps:</span></span>

    ![A caixa de diálogo Usuário](./media/active-directory-saas-screensteps-tutorial/create_aaduser_04.png)

    <span data-ttu-id="26857-216">a.</span><span class="sxs-lookup"><span data-stu-id="26857-216">a.</span></span> <span data-ttu-id="26857-217">Na caixa **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="26857-217">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="26857-218">b.</span><span class="sxs-lookup"><span data-stu-id="26857-218">b.</span></span> <span data-ttu-id="26857-219">Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="26857-219">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="26857-220">c.</span><span class="sxs-lookup"><span data-stu-id="26857-220">c.</span></span> <span data-ttu-id="26857-221">Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.</span><span class="sxs-lookup"><span data-stu-id="26857-221">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="26857-222">d.</span><span class="sxs-lookup"><span data-stu-id="26857-222">d.</span></span> <span data-ttu-id="26857-223">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="26857-223">Click **Create**.</span></span>
 
### <a name="create-a-screensteps-test-user"></a><span data-ttu-id="26857-224">Criar um usuário de teste do ScreenSteps</span><span class="sxs-lookup"><span data-stu-id="26857-224">Create a ScreenSteps test user</span></span>

<span data-ttu-id="26857-225">Nesta seção, você criará um usuário chamado Brenda Fernandes no ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="26857-225">In this section, you create a user called Britta Simon in ScreenSteps.</span></span> <span data-ttu-id="26857-226">Trabalhe com a [equipe de suporte ao cliente do ScreenSteps](https://www.screensteps.com/contact) para adicionar usuários na plataforma do ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="26857-226">Work with [ScreenSteps Client support team](https://www.screensteps.com/contact) to add the users in the ScreenSteps platform.</span></span> <span data-ttu-id="26857-227">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="26857-227">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="26857-228">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="26857-228">Assign the Azure AD test user</span></span>

<span data-ttu-id="26857-229">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo a ela acesso ao ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="26857-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ScreenSteps.</span></span>

![Atribuir a função de usuário][200] 

<span data-ttu-id="26857-231">**Para atribuir Brenda Fernandes ao ScreenSteps, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="26857-231">**To assign Britta Simon to ScreenSteps, perform the following steps:**</span></span>

1. <span data-ttu-id="26857-232">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="26857-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="26857-234">Na lista de aplicativos, escolha **ScreenSteps**.</span><span class="sxs-lookup"><span data-stu-id="26857-234">In the applications list, select **ScreenSteps**.</span></span>

    ![O link do ScreenSteps na lista de Aplicativos](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_app.png)  

3. <span data-ttu-id="26857-236">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="26857-236">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202]

4. <span data-ttu-id="26857-238">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="26857-238">Click **Add** button.</span></span> <span data-ttu-id="26857-239">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="26857-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="26857-241">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="26857-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="26857-242">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="26857-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="26857-243">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="26857-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="26857-244">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="26857-244">Test single sign-on</span></span>

<span data-ttu-id="26857-245">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="26857-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="26857-246">Ao clicar no bloco do ScreenSteps no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="26857-246">When you click the ScreenSteps tile in the Access Panel, you should get automatically signed-on to your ScreenSteps application.</span></span>
<span data-ttu-id="26857-247">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="26857-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="26857-248">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="26857-248">Additional resources</span></span>

* [<span data-ttu-id="26857-249">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="26857-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="26857-250">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="26857-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_203.png

