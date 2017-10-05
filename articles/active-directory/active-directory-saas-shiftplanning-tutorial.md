---
title: "Tutorial: integração do Azure Active Directory com o Humanity | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Humanity."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6aa771e9-31c6-48d1-8dde-024bebc06943
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 327cc1e3d0836e79376e0a3cd5a4422a967f5943
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-humanity"></a><span data-ttu-id="df197-103">Tutorial: integração do Azure Active Directory com o Humanity</span><span class="sxs-lookup"><span data-stu-id="df197-103">Tutorial: Azure Active Directory integration with Humanity</span></span>

<span data-ttu-id="df197-104">Neste tutorial, você aprenderá a integrar o Humanity ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="df197-104">In this tutorial, you learn how to integrate Humanity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="df197-105">A integração do Humanity ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="df197-105">Integrating Humanity with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="df197-106">No Azure AD, é possível controlar quem tem acesso ao Humanity</span><span class="sxs-lookup"><span data-stu-id="df197-106">You can control in Azure AD who has access to Humanity</span></span>
- <span data-ttu-id="df197-107">Você pode permitir que seus usuários façam logon automaticamente no Humanity (logon único) com as contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="df197-107">You can enable your users to automatically get signed-on to Humanity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="df197-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="df197-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="df197-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="df197-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="df197-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="df197-110">Prerequisites</span></span>

<span data-ttu-id="df197-111">Para configurar a integração do Azure AD ao Humanity, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="df197-111">To configure Azure AD integration with Humanity, you need the following items:</span></span>

- <span data-ttu-id="df197-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="df197-112">An Azure AD subscription</span></span>
- <span data-ttu-id="df197-113">Uma assinatura do Humanity habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="df197-113">A Humanity single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="df197-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="df197-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="df197-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="df197-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="df197-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="df197-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="df197-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="df197-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="df197-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="df197-118">Scenario description</span></span>
<span data-ttu-id="df197-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="df197-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="df197-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="df197-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="df197-121">Adicionar o Humanity da galeria</span><span class="sxs-lookup"><span data-stu-id="df197-121">Adding Humanity from the gallery</span></span>
2. <span data-ttu-id="df197-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="df197-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-humanity-from-the-gallery"></a><span data-ttu-id="df197-123">Adicionar o Humanity da galeria</span><span class="sxs-lookup"><span data-stu-id="df197-123">Adding Humanity from the gallery</span></span>
<span data-ttu-id="df197-124">Para configurar a integração do Humanity ao Azure AD, você precisará adicionar o Humanity da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="df197-124">To configure the integration of Humanity into Azure AD, you need to add Humanity from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="df197-125">**Para adicionar o Humanity da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="df197-125">**To add Humanity from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="df197-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="df197-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="df197-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="df197-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="df197-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="df197-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="df197-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="df197-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="df197-133">Na caixa de pesquisa, digite **Humanity**.</span><span class="sxs-lookup"><span data-stu-id="df197-133">In the search box, type **Humanity**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_search.png)

5. <span data-ttu-id="df197-135">No painel de resultados, selecione **Humanity** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="df197-135">In the results panel, select **Humanity**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="df197-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="df197-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="df197-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Humanity, com base em uma usuária de teste chamada "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="df197-138">In this section, you configure and test Azure AD single sign-on with Humanity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="df197-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Humanity é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="df197-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Humanity is to a user in Azure AD.</span></span> <span data-ttu-id="df197-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Humanity.</span><span class="sxs-lookup"><span data-stu-id="df197-140">In other words, a link relationship between an Azure AD user and the related user in Humanity needs to be established.</span></span>

<span data-ttu-id="df197-141">No Humanity, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="df197-141">In Humanity, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="df197-142">Para configurar e testar o logon único do Azure AD com o Humanity, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="df197-142">To configure and test Azure AD single sign-on with Humanity, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="df197-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="df197-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="df197-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="df197-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="df197-145">**[Criação de um usuário de teste do Humanity](#creating-a-humanity-test-user)** – para ter um equivalente de Brenda Fernandes no Humanity que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="df197-145">**[Creating a Humanity test user](#creating-a-humanity-test-user)** - to have a counterpart of Britta Simon in Humanity that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="df197-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="df197-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="df197-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="df197-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="df197-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="df197-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="df197-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Humanity.</span><span class="sxs-lookup"><span data-stu-id="df197-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Humanity application.</span></span>

<span data-ttu-id="df197-150">**Para configurar o logon único do Azure AD com o Humanity, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="df197-150">**To configure Azure AD single sign-on with Humanity, perform the following steps:**</span></span>

1. <span data-ttu-id="df197-151">No portal do Azure, na página de integração de aplicativos do **Humanity**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="df197-151">In the Azure portal, on the **Humanity** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="df197-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="df197-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_samlbase.png)

3. <span data-ttu-id="df197-155">Na seção **Domínio e URLs do Humanity**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="df197-155">On the **Humanity Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_url.png)

    <span data-ttu-id="df197-157">a.</span><span class="sxs-lookup"><span data-stu-id="df197-157">a.</span></span> <span data-ttu-id="df197-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://company.humanity.com/includes/saml/`</span><span class="sxs-lookup"><span data-stu-id="df197-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://company.humanity.com/includes/saml/`</span></span>

    <span data-ttu-id="df197-159">b.</span><span class="sxs-lookup"><span data-stu-id="df197-159">b.</span></span> <span data-ttu-id="df197-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://company.humanity.com/app/`</span><span class="sxs-lookup"><span data-stu-id="df197-160">In the **Identifier** textbox, type a URL using the following pattern: `https://company.humanity.com/app/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="df197-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="df197-161">These values are not real.</span></span> <span data-ttu-id="df197-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="df197-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="df197-163">Contate a [equipe de suporte do Cliente Humanity](https://www.humanity.com/support/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="df197-163">Contact [Humanity Client support team](https://www.humanity.com/support/) to get these values.</span></span> 
 
4. <span data-ttu-id="df197-164">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="df197-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_certificate.png) 

5. <span data-ttu-id="df197-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="df197-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="df197-168">Na seção **Configuração do Humanity**, clique em **Configurar Humanity** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="df197-168">On the **Humanity Configuration** section, click **Configure Humanity** to open **Configure sign-on** window.</span></span> <span data-ttu-id="df197-169">Copie a **URL do Serviço de Logon Único do SAML e a URL de Logoff** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="df197-169">Copy the **SAML Single Sign-On Service URL, and Sign-Out URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_configure.png) 

7. <span data-ttu-id="df197-171">Em outra janela do navegador da Web, faça logon em seu site de empresa do **Humanity** como um administrador.</span><span class="sxs-lookup"><span data-stu-id="df197-171">In a different web browser window, log in to your **Humanity** company site as an administrator.</span></span>

8. <span data-ttu-id="df197-172">No menu na parte superior, clique em **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="df197-172">In the menu on the top, click **Admin**.</span></span>
   
    <span data-ttu-id="df197-173">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="df197-173">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span></span>

9. <span data-ttu-id="df197-174">Em **Integração**, clique em **Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="df197-174">Under **Integration**, click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="df197-175">![Logon Único](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "Logon Único")</span><span class="sxs-lookup"><span data-stu-id="df197-175">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "Single Sign-On")</span></span>

10. <span data-ttu-id="df197-176">Na seção **Logon Único** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="df197-176">In the **Single Sign-On** section, perform the following steps:</span></span>
   
    <span data-ttu-id="df197-177">![Logon Único](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "Logon Único")</span><span class="sxs-lookup"><span data-stu-id="df197-177">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "Single Sign-On")</span></span>
   
    <span data-ttu-id="df197-178">a.</span><span class="sxs-lookup"><span data-stu-id="df197-178">a.</span></span> <span data-ttu-id="df197-179">Selecione **SAML Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="df197-179">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="df197-180">b.</span><span class="sxs-lookup"><span data-stu-id="df197-180">b.</span></span> <span data-ttu-id="df197-181">Selecione **Permitir Logon de Senha**.</span><span class="sxs-lookup"><span data-stu-id="df197-181">Select **Allow Password Login**.</span></span>

    <span data-ttu-id="df197-182">c.</span><span class="sxs-lookup"><span data-stu-id="df197-182">c.</span></span> <span data-ttu-id="df197-183">Cole o valor da **URL do Serviço de Logon Único do SAML** na caixa de texto **URL do Emissor do SAML**.</span><span class="sxs-lookup"><span data-stu-id="df197-183">Paste the **SAML Single Sign-On Service URL** value into the **SAML Issuer URL** textbox.</span></span>

    <span data-ttu-id="df197-184">d.</span><span class="sxs-lookup"><span data-stu-id="df197-184">d.</span></span> <span data-ttu-id="df197-185">Cole o valor da **URL de Saída** na caixa de texto **URL de Logout Remota**.</span><span class="sxs-lookup"><span data-stu-id="df197-185">Paste the **Sign-Out URL** value into the **Remote Logout URL** textbox.</span></span>
   
    <span data-ttu-id="df197-186">e.</span><span class="sxs-lookup"><span data-stu-id="df197-186">e.</span></span> <span data-ttu-id="df197-187">Abra seu certificado codificado em Base 64 no bloco de notas, copie o conteúdo dele na área de transferência e cole-o na caixa de texto **Certificado X.509** .</span><span class="sxs-lookup"><span data-stu-id="df197-187">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.</span></span>

11. <span data-ttu-id="df197-188">Clique em **Salvar Configurações**.</span><span class="sxs-lookup"><span data-stu-id="df197-188">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="df197-189">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="df197-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="df197-190">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="df197-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="df197-191">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="df197-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="df197-192">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="df197-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="df197-193">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="df197-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="df197-195">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="df197-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="df197-196">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="df197-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="df197-198">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="df197-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="df197-200">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="df197-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="df197-202">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="df197-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="df197-204">a.</span><span class="sxs-lookup"><span data-stu-id="df197-204">a.</span></span> <span data-ttu-id="df197-205">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="df197-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="df197-206">b.</span><span class="sxs-lookup"><span data-stu-id="df197-206">b.</span></span> <span data-ttu-id="df197-207">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="df197-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="df197-208">c.</span><span class="sxs-lookup"><span data-stu-id="df197-208">c.</span></span> <span data-ttu-id="df197-209">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="df197-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="df197-210">d.</span><span class="sxs-lookup"><span data-stu-id="df197-210">d.</span></span> <span data-ttu-id="df197-211">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="df197-211">Click **Create**.</span></span>
 
### <a name="creating-a-humanity-test-user"></a><span data-ttu-id="df197-212">Criar um usuário de teste do Humanity</span><span class="sxs-lookup"><span data-stu-id="df197-212">Creating a Humanity test user</span></span>

<span data-ttu-id="df197-213">Para permitir que os usuários do Azure AD façam logon no Humanity, eles deverão ser provisionados no Humanity.</span><span class="sxs-lookup"><span data-stu-id="df197-213">In order to enable Azure AD users to log in to Humanity, they must be provisioned into Humanity.</span></span> <span data-ttu-id="df197-214">No caso do Humanity, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="df197-214">In the case of Humanity, provisioning is a manual task.</span></span>

<span data-ttu-id="df197-215">**Para provisionar uma conta de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="df197-215">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="df197-216">Faça logon em seu site de empresa do **Humanity** como administrador.</span><span class="sxs-lookup"><span data-stu-id="df197-216">Log in to your **Humanity** company site as an administrator.</span></span>

2. <span data-ttu-id="df197-217">Clique em **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="df197-217">Click **Admin**.</span></span>
   
    <span data-ttu-id="df197-218">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="df197-218">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span></span>

3. <span data-ttu-id="df197-219">Clique em **Equipe**.</span><span class="sxs-lookup"><span data-stu-id="df197-219">Click **Staff**.</span></span>
   
    <span data-ttu-id="df197-220">![Equipe](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "Equipe")</span><span class="sxs-lookup"><span data-stu-id="df197-220">![Staff](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "Staff")</span></span>

4. <span data-ttu-id="df197-221">Em **Ações**, clique em **Adicionar Funcionários**.</span><span class="sxs-lookup"><span data-stu-id="df197-221">Under **Actions**, click **Add Employees**.</span></span>
   
    <span data-ttu-id="df197-222">![Adicionar Funcionários](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "Adicionar Funcionários")</span><span class="sxs-lookup"><span data-stu-id="df197-222">![Add Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "Add Employees")</span></span>

5. <span data-ttu-id="df197-223">Na seção **Adicionar Funcionários** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="df197-223">In the **Add Employees** section, perform the following steps:</span></span>
   
    <span data-ttu-id="df197-224">![Salvar Funcionários](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "Salvar Funcionários")</span><span class="sxs-lookup"><span data-stu-id="df197-224">![Save Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "Save Employees")</span></span>
   
    <span data-ttu-id="df197-225">a.</span><span class="sxs-lookup"><span data-stu-id="df197-225">a.</span></span> <span data-ttu-id="df197-226">Nas caixas de texto correspondentes, digite o **Nome**, o **Sobrenome** e o **Email** de uma conta válida do AAD que você deseja provisionar.</span><span class="sxs-lookup"><span data-stu-id="df197-226">Type the **First Name**, **Last Name**, and **Email** of a valid AAD account you want to provision into the related textboxes.</span></span>

    <span data-ttu-id="df197-227">b.</span><span class="sxs-lookup"><span data-stu-id="df197-227">b.</span></span> <span data-ttu-id="df197-228">Clique em **Salvar Funcionários**.</span><span class="sxs-lookup"><span data-stu-id="df197-228">Click **Save Employees**.</span></span>

>[!NOTE]
><span data-ttu-id="df197-229">É possível usar qualquer outra ferramenta de criação da conta de usuário do Humanity ou as APIs fornecidas pelo Humanity para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="df197-229">You can use any other Humanity user account creation tools or APIs provided by Humanity to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="df197-230">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="df197-230">Assigning the Azure AD test user</span></span>

<span data-ttu-id="df197-231">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Humanity.</span><span class="sxs-lookup"><span data-stu-id="df197-231">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Humanity.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="df197-233">**Para atribuir Brenda Fernandes ao Humanity, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="df197-233">**To assign Britta Simon to Humanity, perform the following steps:**</span></span>

1. <span data-ttu-id="df197-234">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="df197-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="df197-236">Na lista de aplicativos, selecione **Humanity**.</span><span class="sxs-lookup"><span data-stu-id="df197-236">In the applications list, select **Humanity**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_app.png) 

3. <span data-ttu-id="df197-238">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="df197-238">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="df197-240">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="df197-240">Click **Add** button.</span></span> <span data-ttu-id="df197-241">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="df197-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="df197-243">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="df197-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="df197-244">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="df197-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="df197-245">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="df197-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="df197-246">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="df197-246">Testing single sign-on</span></span>

<span data-ttu-id="df197-247">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="df197-247">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="df197-248">Quando você clicar no bloco Humanity no Painel de Acesso, deverá ser automaticamente conectado ao seu aplicativo Humanity.</span><span class="sxs-lookup"><span data-stu-id="df197-248">When you click the Humanity tile in the Access Panel, you should get automatically signed-on to your Humanity application.</span></span>
<span data-ttu-id="df197-249">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="df197-249">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="df197-250">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="df197-250">Additional resources</span></span>

* [<span data-ttu-id="df197-251">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="df197-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="df197-252">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="df197-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_203.png

