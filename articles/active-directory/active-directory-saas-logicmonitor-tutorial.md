---
title: "Tutorial: Integração do Azure Active Directory com o LogicMonitor | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o LogicMonitor."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 496156c3-0e22-4492-b36f-2c29c055e087
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: e49960cac868f80af3e9165a9f75e49be87515f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-logicmonitor"></a><span data-ttu-id="994d6-103">Tutorial: Integração do Active Directory do Azure com o LogicMonitor</span><span class="sxs-lookup"><span data-stu-id="994d6-103">Tutorial: Azure Active Directory integration with LogicMonitor</span></span>

<span data-ttu-id="994d6-104">Neste tutorial, você aprenderá a integrar o LogicMonitor ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="994d6-104">In this tutorial, you learn how to integrate LogicMonitor with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="994d6-105">A integração do LogicMonitor ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="994d6-105">Integrating LogicMonitor with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="994d6-106">Você pode controlar no Azure AD quem tem acesso ao LogicMonitor</span><span class="sxs-lookup"><span data-stu-id="994d6-106">You can control in Azure AD who has access to LogicMonitor</span></span>
- <span data-ttu-id="994d6-107">Você pode permitir que os usuários façam logon automaticamente no LogicMonitor (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="994d6-107">You can enable your users to automatically get signed-on to LogicMonitor (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="994d6-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="994d6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="994d6-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="994d6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="994d6-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="994d6-110">Prerequisites</span></span>

<span data-ttu-id="994d6-111">Para configurar a integração do Azure AD ao LogicMonitor, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="994d6-111">To configure Azure AD integration with LogicMonitor, you need the following items:</span></span>

- <span data-ttu-id="994d6-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="994d6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="994d6-113">Uma assinatura habilitada para logon único do LogicMonitor</span><span class="sxs-lookup"><span data-stu-id="994d6-113">A LogicMonitor single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="994d6-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="994d6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="994d6-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="994d6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="994d6-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="994d6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="994d6-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="994d6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="994d6-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="994d6-118">Scenario description</span></span>
<span data-ttu-id="994d6-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="994d6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="994d6-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="994d6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="994d6-121">Adicionar o LogicMonitor da galeria</span><span class="sxs-lookup"><span data-stu-id="994d6-121">Adding LogicMonitor from the gallery</span></span>
2. <span data-ttu-id="994d6-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="994d6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-logicmonitor-from-the-gallery"></a><span data-ttu-id="994d6-123">Adicionar o LogicMonitor da galeria</span><span class="sxs-lookup"><span data-stu-id="994d6-123">Adding LogicMonitor from the gallery</span></span>
<span data-ttu-id="994d6-124">Para configurar a integração do LogicMonitor ao Azure AD, você precisará adicionar o LogicMonitor da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="994d6-124">To configure the integration of LogicMonitor into Azure AD, you need to add LogicMonitor from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="994d6-125">**Para adicionar o LogicMonitor da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="994d6-125">**To add LogicMonitor from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="994d6-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="994d6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="994d6-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="994d6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="994d6-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="994d6-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="994d6-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="994d6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="994d6-133">Na caixa de pesquisa, digite **LogicMonitor**.</span><span class="sxs-lookup"><span data-stu-id="994d6-133">In the search box, type **LogicMonitor**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_search.png)

5. <span data-ttu-id="994d6-135">No painel de resultados, selecione **LogicMonitor** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="994d6-135">In the results panel, select **LogicMonitor**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="994d6-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="994d6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="994d6-138">Nesta seção, você configurará e testará o logon único do Azure AD com o LogicMonitor, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="994d6-138">In this section, you configure and test Azure AD single sign-on with LogicMonitor based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="994d6-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do LogicMonitor é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="994d6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LogicMonitor is to a user in Azure AD.</span></span> <span data-ttu-id="994d6-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do LogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="994d6-140">In other words, a link relationship between an Azure AD user and the related user in LogicMonitor needs to be established.</span></span>

<span data-ttu-id="994d6-141">No LogicMonitor, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="994d6-141">In LogicMonitor, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="994d6-142">Para configurar e testar o logon único do Azure AD com o LogicMonitor, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="994d6-142">To configure and test Azure AD single sign-on with LogicMonitor, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="994d6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="994d6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="994d6-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="994d6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="994d6-145">**[Criação de um usuário de teste do LogicMonitor](#creating-a-logicmonitor-test-user)** – para ter um equivalente de Brenda Fernandes no LogicMonitor que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="994d6-145">**[Creating a LogicMonitor test user](#creating-a-logicmonitor-test-user)** - to have a counterpart of Britta Simon in LogicMonitor that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="994d6-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="994d6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="994d6-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="994d6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="994d6-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="994d6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="994d6-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo LogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="994d6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LogicMonitor application.</span></span>

<span data-ttu-id="994d6-150">**Para configurar o logon único do Azure AD com o LogicMonitor, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="994d6-150">**To configure Azure AD single sign-on with LogicMonitor, perform the following steps:**</span></span>

1. <span data-ttu-id="994d6-151">No portal do Azure, na página de integração de aplicativos do **LogicMonitor**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="994d6-151">In the Azure portal, on the **LogicMonitor** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="994d6-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="994d6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_samlbase.png)

3. <span data-ttu-id="994d6-155">Na seção **Domínio e URLs do LogicMonitor**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="994d6-155">On the **LogicMonitor Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_url.png)

    <span data-ttu-id="994d6-157">a.</span><span class="sxs-lookup"><span data-stu-id="994d6-157">a.</span></span> <span data-ttu-id="994d6-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<companyname>.logicmonitor.com`</span><span class="sxs-lookup"><span data-stu-id="994d6-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.logicmonitor.com`</span></span>

    <span data-ttu-id="994d6-159">b.</span><span class="sxs-lookup"><span data-stu-id="994d6-159">b.</span></span> <span data-ttu-id="994d6-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<companyname>.logicmonitor.com`</span><span class="sxs-lookup"><span data-stu-id="994d6-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.logicmonitor.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="994d6-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="994d6-161">These values are not real.</span></span> <span data-ttu-id="994d6-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="994d6-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="994d6-163">Entre em contato com a [equipe de suporte do cliente do LogicMonitor](https://www.logicmonitor.com/contact/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="994d6-163">Contact [LogicMonitor Client support team](https://www.logicmonitor.com/contact/) to get these values.</span></span> 
 


4. <span data-ttu-id="994d6-164">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="994d6-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_certificate.png) 

5. <span data-ttu-id="994d6-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="994d6-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="994d6-168">Faça logon em seu site de empresa do **LogicMonitor** como administrador.</span><span class="sxs-lookup"><span data-stu-id="994d6-168">Log in to your **LogicMonitor** company site as an administrator.</span></span>

7. <span data-ttu-id="994d6-169">No menu na parte superior, clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="994d6-169">In the menu on the top, click **Settings**.</span></span>
   
   <span data-ttu-id="994d6-170">![Configurações](./media/active-directory-saas-logicmonitor-tutorial/ic790052.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="994d6-170">![Settings](./media/active-directory-saas-logicmonitor-tutorial/ic790052.png "Settings")</span></span>

8. <span data-ttu-id="994d6-171">Na guia de navegação à esquerda, clique em **Logon Único**</span><span class="sxs-lookup"><span data-stu-id="994d6-171">In the navigation bat on the left side, click **Single Sign On**</span></span>
   
   <span data-ttu-id="994d6-172">![Logon Único](./media/active-directory-saas-logicmonitor-tutorial/ic790053.png "Logon Único")</span><span class="sxs-lookup"><span data-stu-id="994d6-172">![Single Sign-On](./media/active-directory-saas-logicmonitor-tutorial/ic790053.png "Single Sign-On")</span></span>

9. <span data-ttu-id="994d6-173">Na seção **Configurações de SSO (logon único)** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="994d6-173">In the **Single Sign-on (SSO) settings** section, perform the following steps:</span></span>
   
   <span data-ttu-id="994d6-174">![Configurações de Logon Único](./media/active-directory-saas-logicmonitor-tutorial/ic790054.png "Configurações de Logon Único")</span><span class="sxs-lookup"><span data-stu-id="994d6-174">![Single Sign-On Settings](./media/active-directory-saas-logicmonitor-tutorial/ic790054.png "Single Sign-On Settings")</span></span>
   
   <span data-ttu-id="994d6-175">a.</span><span class="sxs-lookup"><span data-stu-id="994d6-175">a.</span></span> <span data-ttu-id="994d6-176">Selecione **Habilitar Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="994d6-176">Select **Enable Single Sign-on**.</span></span>

   <span data-ttu-id="994d6-177">b.</span><span class="sxs-lookup"><span data-stu-id="994d6-177">b.</span></span> <span data-ttu-id="994d6-178">Para **Atribuição de Função Padrão**, selecione **readonly**.</span><span class="sxs-lookup"><span data-stu-id="994d6-178">As **Default Role Assignment**, select **readonly**.</span></span>
   
   <span data-ttu-id="994d6-179">c.</span><span class="sxs-lookup"><span data-stu-id="994d6-179">c.</span></span> <span data-ttu-id="994d6-180">Abra o arquivo de metadados baixado no bloco de notas e cole o conteúdo do arquivo na caixa de texto **Metadados do Provedor de Identidade** .</span><span class="sxs-lookup"><span data-stu-id="994d6-180">Open the downloaded metadata file in notepad, and then paste content of the file into the **Identity Provider Metadata** textbox.</span></span>
   
   <span data-ttu-id="994d6-181">d.</span><span class="sxs-lookup"><span data-stu-id="994d6-181">d.</span></span> <span data-ttu-id="994d6-182">Clique em **Salvar Alterações**.</span><span class="sxs-lookup"><span data-stu-id="994d6-182">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="994d6-183">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="994d6-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="994d6-184">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="994d6-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="994d6-185">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="994d6-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="994d6-186">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="994d6-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="994d6-187">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="994d6-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="994d6-189">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="994d6-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="994d6-190">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="994d6-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="994d6-192">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="994d6-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="994d6-194">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="994d6-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="994d6-196">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="994d6-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="994d6-198">a.</span><span class="sxs-lookup"><span data-stu-id="994d6-198">a.</span></span> <span data-ttu-id="994d6-199">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="994d6-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="994d6-200">b.</span><span class="sxs-lookup"><span data-stu-id="994d6-200">b.</span></span> <span data-ttu-id="994d6-201">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="994d6-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="994d6-202">c.</span><span class="sxs-lookup"><span data-stu-id="994d6-202">c.</span></span> <span data-ttu-id="994d6-203">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="994d6-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="994d6-204">d.</span><span class="sxs-lookup"><span data-stu-id="994d6-204">d.</span></span> <span data-ttu-id="994d6-205">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="994d6-205">Click **Create**.</span></span>
 
### <a name="creating-a-logicmonitor-test-user"></a><span data-ttu-id="994d6-206">Criar um usuário de teste do LogicMonitor</span><span class="sxs-lookup"><span data-stu-id="994d6-206">Creating a LogicMonitor test user</span></span>

<span data-ttu-id="994d6-207">Para usuários do AAD conseguirem efetuar logon, eles devem ser provisionados para o aplicativo LogicMonitor usando seus nomes de usuário do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="994d6-207">For AAD users to be able to sign in, they must be provisioned to the LogicMonitor application using their Azure Active Directory user names.</span></span>

<span data-ttu-id="994d6-208">**Para configurar o provisionamento de usuários, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="994d6-208">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="994d6-209">Faça logon no site da sua empresa LogicMonitor como um administrador.</span><span class="sxs-lookup"><span data-stu-id="994d6-209">Log in to your LogicMonitor company site as an administrator.</span></span>

2. <span data-ttu-id="994d6-210">No menu na parte superior, clique em **Configurações** e em **Funções e Usuários**.</span><span class="sxs-lookup"><span data-stu-id="994d6-210">In the menu on the top, click **Settings**, and then click **Roles and Users**.</span></span>
   
   <span data-ttu-id="994d6-211">![Funções e Usuários](./media/active-directory-saas-logicmonitor-tutorial/ic790056.png "Funções e Usuários")</span><span class="sxs-lookup"><span data-stu-id="994d6-211">![Roles and Users](./media/active-directory-saas-logicmonitor-tutorial/ic790056.png "Roles and Users")</span></span>

3. <span data-ttu-id="994d6-212">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="994d6-212">Click **Add**.</span></span>

4. <span data-ttu-id="994d6-213">Na seção **Adicionar uma conta** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="994d6-213">In the **Add an account** section, perform the following steps:</span></span>
   
   <span data-ttu-id="994d6-214">![Adicionar uma conta](./media/active-directory-saas-logicmonitor-tutorial/ic790057.png "Adicionar uma conta")</span><span class="sxs-lookup"><span data-stu-id="994d6-214">![Add an account](./media/active-directory-saas-logicmonitor-tutorial/ic790057.png "Add an account")</span></span>
   
   <span data-ttu-id="994d6-215">a.</span><span class="sxs-lookup"><span data-stu-id="994d6-215">a.</span></span> <span data-ttu-id="994d6-216">Digite os valores para **Nome de usuário**, **Email**, **Senha** e **Digitar senha novamente** do usuário do Azure Active Directory que você deseja provisionar nas caixas de texto relacionadas.</span><span class="sxs-lookup"><span data-stu-id="994d6-216">Type the **Username**, **Email**, **Password**, and **Retype password** values of the Azure Active Directory user you want to provision into the related textboxes.</span></span>
   
   <span data-ttu-id="994d6-217">b.</span><span class="sxs-lookup"><span data-stu-id="994d6-217">b.</span></span> <span data-ttu-id="994d6-218">Selecione **Funções**, **Exibir Permissões** e **Status**.</span><span class="sxs-lookup"><span data-stu-id="994d6-218">Select **Roles**, **View Permissions**, and the **Status**.</span></span>
   
   <span data-ttu-id="994d6-219">c.</span><span class="sxs-lookup"><span data-stu-id="994d6-219">c.</span></span> <span data-ttu-id="994d6-220">Clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="994d6-220">Click **Submit**.</span></span>

>[!NOTE]
><span data-ttu-id="994d6-221">Você pode usar qualquer outra ferramenta de criação da conta de usuário do LogicMonitor ou APIs fornecidas pelo LogicMonitor para provisionar as contas de usuário do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="994d6-221">You can use any other LogicMonitor user account creation tools or APIs provided by LogicMonitor to provision Azure Active Directory user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="994d6-222">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="994d6-222">Assigning the Azure AD test user</span></span>

<span data-ttu-id="994d6-223">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao LogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="994d6-223">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LogicMonitor.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="994d6-225">**Para atribuir Brenda Fernandes ao LogicMonitor, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="994d6-225">**To assign Britta Simon to LogicMonitor, perform the following steps:**</span></span>

1. <span data-ttu-id="994d6-226">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="994d6-226">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="994d6-228">Na lista de aplicativos, selecione **LogicMonitor**.</span><span class="sxs-lookup"><span data-stu-id="994d6-228">In the applications list, select **LogicMonitor**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_app.png) 

3. <span data-ttu-id="994d6-230">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="994d6-230">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="994d6-232">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="994d6-232">Click **Add** button.</span></span> <span data-ttu-id="994d6-233">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="994d6-233">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="994d6-235">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="994d6-235">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="994d6-236">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="994d6-236">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="994d6-237">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="994d6-237">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="994d6-238">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="994d6-238">Testing single sign-on</span></span>

<span data-ttu-id="994d6-239">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="994d6-239">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
 
<span data-ttu-id="994d6-240">Ao clicar no bloco do LogicMonitor no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo LogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="994d6-240">When you click the LogicMonitor tile in the Access Panel, you should get automatically signed-on to your LogicMonitor application.</span></span>
<span data-ttu-id="994d6-241">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="994d6-241">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="994d6-242">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="994d6-242">Additional resources</span></span>

* [<span data-ttu-id="994d6-243">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="994d6-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="994d6-244">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="994d6-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_203.png

