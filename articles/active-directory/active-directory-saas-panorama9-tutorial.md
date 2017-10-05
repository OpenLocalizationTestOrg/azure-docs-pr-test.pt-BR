---
title: "Tutorial: Integração do Azure Active Directory com o Panorama9 | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Panorama9."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5e28d7fa-03be-49f3-96c8-b567f1257d44
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 934c0743464fd32398071aa3d07f7af76fdf7e3b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-panorama9"></a><span data-ttu-id="67fe3-103">Tutorial: Integração do Active Directory do Azure com o Panorama9</span><span class="sxs-lookup"><span data-stu-id="67fe3-103">Tutorial: Azure Active Directory integration with Panorama9</span></span>

<span data-ttu-id="67fe3-104">Neste tutorial, você aprende a integrar o Panorama9 ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="67fe3-104">In this tutorial, you learn how to integrate Panorama9 with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="67fe3-105">A integração do Panorama9 ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="67fe3-105">Integrating Panorama9 with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="67fe3-106">No Azure AD, é possível controlar quem tem acesso ao Panorama9</span><span class="sxs-lookup"><span data-stu-id="67fe3-106">You can control in Azure AD who has access to Panorama9</span></span>
- <span data-ttu-id="67fe3-107">É possível permitir que os usuários se conectem automaticamente ao Panorama9 (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="67fe3-107">You can enable your users to automatically get signed-on to Panorama9 (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="67fe3-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="67fe3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="67fe3-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="67fe3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="67fe3-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="67fe3-110">Prerequisites</span></span>

<span data-ttu-id="67fe3-111">Para configurar a integração do Azure AD ao Panorama9, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="67fe3-111">To configure Azure AD integration with Panorama9, you need the following items:</span></span>

- <span data-ttu-id="67fe3-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="67fe3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="67fe3-113">Uma assinatura habilitada para logon único do Panorama9</span><span class="sxs-lookup"><span data-stu-id="67fe3-113">A Panorama9 single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="67fe3-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="67fe3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="67fe3-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="67fe3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="67fe3-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="67fe3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="67fe3-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="67fe3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="67fe3-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="67fe3-118">Scenario description</span></span>
<span data-ttu-id="67fe3-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="67fe3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="67fe3-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="67fe3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="67fe3-121">Adicionando o Panorama9 por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="67fe3-121">Adding Panorama9 from the gallery</span></span>
2. <span data-ttu-id="67fe3-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="67fe3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-panorama9-from-the-gallery"></a><span data-ttu-id="67fe3-123">Adicionando o Panorama9 por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="67fe3-123">Adding Panorama9 from the gallery</span></span>
<span data-ttu-id="67fe3-124">Para configurar a integração do Panorama9 ao Azure AD, é necessário adicionar o Panorama9 à lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="67fe3-124">To configure the integration of Panorama9 into Azure AD, you need to add Panorama9 from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="67fe3-125">**Para adicionar o Panorama9 por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="67fe3-125">**To add Panorama9 from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="67fe3-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="67fe3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="67fe3-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="67fe3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="67fe3-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="67fe3-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="67fe3-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="67fe3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="67fe3-133">Na caixa de pesquisa, digite **Panorama9**.</span><span class="sxs-lookup"><span data-stu-id="67fe3-133">In the search box, type **Panorama9**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_search.png)

5. <span data-ttu-id="67fe3-135">No painel de resultados, selecione **Panorama9** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="67fe3-135">In the results panel, select **Panorama9**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="67fe3-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="67fe3-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="67fe3-138">Nesta seção, você configura e testa o logon único do Azure AD com o Panorama9, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="67fe3-138">In this section, you configure and test Azure AD single sign-on with Panorama9 based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="67fe3-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Panorama9 é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="67fe3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Panorama9 is to a user in Azure AD.</span></span> <span data-ttu-id="67fe3-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Panorama9.</span><span class="sxs-lookup"><span data-stu-id="67fe3-140">In other words, a link relationship between an Azure AD user and the related user in Panorama9 needs to be established.</span></span>

<span data-ttu-id="67fe3-141">No Panorama9, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="67fe3-141">In Panorama9, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="67fe3-142">Para configurar e testar o logon único do Azure AD com o Panorama9, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="67fe3-142">To configure and test Azure AD single sign-on with Panorama9, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="67fe3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="67fe3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="67fe3-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="67fe3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="67fe3-145">**[Criando um usuário de teste do Panorama9](#creating-a-panorama9-test-user)** – para ter um equivalente de Brenda Fernandes no Panorama9 que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="67fe3-145">**[Creating a Panorama9 test user](#creating-a-panorama9-test-user)** - to have a counterpart of Britta Simon in Panorama9 that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="67fe3-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="67fe3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="67fe3-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="67fe3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="67fe3-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="67fe3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="67fe3-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Panorama9.</span><span class="sxs-lookup"><span data-stu-id="67fe3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Panorama9 application.</span></span>

<span data-ttu-id="67fe3-150">**Para configurar o logon único do Azure AD com o Panorama9, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="67fe3-150">**To configure Azure AD single sign-on with Panorama9, perform the following steps:**</span></span>

1. <span data-ttu-id="67fe3-151">No portal do Azure, na página de integração do aplicativo **Panorama9**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="67fe3-151">In the Azure portal, on the **Panorama9** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="67fe3-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="67fe3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_samlbase.png)

3. <span data-ttu-id="67fe3-155">Na seção **Domínio e URLs do Panorama9**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="67fe3-155">On the **Panorama9 Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_url.png)

    <span data-ttu-id="67fe3-157">a.</span><span class="sxs-lookup"><span data-stu-id="67fe3-157">a.</span></span> <span data-ttu-id="67fe3-158">Na caixa de texto **URL de Logon**, digite uma URL como: `https://dashboard.panorama9.com/saml/access/3262`</span><span class="sxs-lookup"><span data-stu-id="67fe3-158">In the **Sign-on URL** textbox, type a URL as: `https://dashboard.panorama9.com/saml/access/3262`</span></span>

    <span data-ttu-id="67fe3-159">b.</span><span class="sxs-lookup"><span data-stu-id="67fe3-159">b.</span></span> <span data-ttu-id="67fe3-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `http://www.panorama9.com/saml20/<tenant-name>`</span><span class="sxs-lookup"><span data-stu-id="67fe3-160">In the **Identifier** textbox, type a URL using the following pattern: `http://www.panorama9.com/saml20/<tenant-name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="67fe3-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="67fe3-161">These values are not real.</span></span> <span data-ttu-id="67fe3-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="67fe3-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="67fe3-163">Contate a [equipe de suporte ao Cliente do Panorama9](https://support.panorama9.com) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="67fe3-163">Contact [Panorama9 Client support team](https://support.panorama9.com) to get these values.</span></span> 
 
4. <span data-ttu-id="67fe3-164">Na seção **Certificado de Autenticação SAML**, copie o valor da **IMPRESSÃO DIGITAL** do certificado.</span><span class="sxs-lookup"><span data-stu-id="67fe3-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_certificate.png) 

5. <span data-ttu-id="67fe3-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="67fe3-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-panorama9-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="67fe3-168">Na seção **Configuração do Panorama9**, clique em **Configurar o Panorama9** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="67fe3-168">On the **Panorama9 Configuration** section, click **Configure Panorama9** to open **Configure sign-on** window.</span></span> <span data-ttu-id="67fe3-169">Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="67fe3-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_configure.png) 

5. <span data-ttu-id="67fe3-171">Em uma janela de navegador da Web diferente, faça logon no site de sua empresa do Panorama9 como administrador.</span><span class="sxs-lookup"><span data-stu-id="67fe3-171">In a different web browser window, log into your Panorama9 company site as an administrator.</span></span>

6. <span data-ttu-id="67fe3-172">Na barra de ferramentas na parte superior, clique em **Gerenciar** e em **Extensões**.</span><span class="sxs-lookup"><span data-stu-id="67fe3-172">In the toolbar on the top, click **Manage**, and then click **Extensions**.</span></span>
   
   <span data-ttu-id="67fe3-173">![Extensões](./media/active-directory-saas-panorama9-tutorial/ic790023.png "Extensões")</span><span class="sxs-lookup"><span data-stu-id="67fe3-173">![Extensions](./media/active-directory-saas-panorama9-tutorial/ic790023.png "Extensions")</span></span>
7. <span data-ttu-id="67fe3-174">No diálogo **Extensões**, clique em **Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="67fe3-174">On the **Extensions** dialog, click **Single Sign-On**.</span></span>
   
   <span data-ttu-id="67fe3-175">![Logon Único](./media/active-directory-saas-panorama9-tutorial/ic790024.png "Logon Único")</span><span class="sxs-lookup"><span data-stu-id="67fe3-175">![Single Sign-On](./media/active-directory-saas-panorama9-tutorial/ic790024.png "Single Sign-On")</span></span>
8. <span data-ttu-id="67fe3-176">Na seção **Configurações** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="67fe3-176">In the **Settings** section, perform the following steps:</span></span>
   
   <span data-ttu-id="67fe3-177">![Configurações](./media/active-directory-saas-panorama9-tutorial/ic790025.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="67fe3-177">![Settings](./media/active-directory-saas-panorama9-tutorial/ic790025.png "Settings")</span></span>
   
    <span data-ttu-id="67fe3-178">a.</span><span class="sxs-lookup"><span data-stu-id="67fe3-178">a.</span></span> <span data-ttu-id="67fe3-179">Na caixa de texto **URL do Provedor de Identidade**, cole o valor da **URL do Serviço de Logon Único** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="67fe3-179">In **Identity provider URL** textbox, paste the value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="67fe3-180">b.</span><span class="sxs-lookup"><span data-stu-id="67fe3-180">b.</span></span> <span data-ttu-id="67fe3-181">Na caixa de texto **Impressão digital do certificado**, cole o valor da **Impressão Digital** do certificado copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="67fe3-181">In **Certificate fingerprint** textbox, paste the **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>    
         
9. <span data-ttu-id="67fe3-182">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="67fe3-182">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="67fe3-183">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="67fe3-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="67fe3-184">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="67fe3-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="67fe3-185">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="67fe3-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="67fe3-186">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="67fe3-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="67fe3-187">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="67fe3-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="67fe3-189">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="67fe3-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="67fe3-190">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="67fe3-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-panorama9-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="67fe3-192">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="67fe3-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-panorama9-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="67fe3-194">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="67fe3-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-panorama9-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="67fe3-196">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="67fe3-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-panorama9-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="67fe3-198">a.</span><span class="sxs-lookup"><span data-stu-id="67fe3-198">a.</span></span> <span data-ttu-id="67fe3-199">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="67fe3-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="67fe3-200">b.</span><span class="sxs-lookup"><span data-stu-id="67fe3-200">b.</span></span> <span data-ttu-id="67fe3-201">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="67fe3-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="67fe3-202">c.</span><span class="sxs-lookup"><span data-stu-id="67fe3-202">c.</span></span> <span data-ttu-id="67fe3-203">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="67fe3-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="67fe3-204">d.</span><span class="sxs-lookup"><span data-stu-id="67fe3-204">d.</span></span> <span data-ttu-id="67fe3-205">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="67fe3-205">Click **Create**.</span></span>
 
### <a name="creating-a-panorama9-test-user"></a><span data-ttu-id="67fe3-206">Criando um usuário de teste do Panorama9</span><span class="sxs-lookup"><span data-stu-id="67fe3-206">Creating a Panorama9 test user</span></span>

<span data-ttu-id="67fe3-207">Para permitir que os usuários do AD do Azure façam logon no Panorama9, eles devem ser provisionados no Panorama9.</span><span class="sxs-lookup"><span data-stu-id="67fe3-207">In order to enable Azure AD users to log into Panorama9, they must be provisioned into Panorama9.</span></span>  

<span data-ttu-id="67fe3-208">No caso do Panorama9, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="67fe3-208">In the case of Panorama9, provisioning is a manual task.</span></span>

<span data-ttu-id="67fe3-209">**Para configurar o provisionamento de usuários, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="67fe3-209">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="67fe3-210">Faça logon em seu site de empresa do **Panorama9** como administrador.</span><span class="sxs-lookup"><span data-stu-id="67fe3-210">Log in to your **Panorama9** company site as an administrator.</span></span>

2. <span data-ttu-id="67fe3-211">No menu na parte superior, clique em **Gerenciar** e em **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="67fe3-211">In the menu on the top, click **Manage**, and then click **Users**.</span></span>
   
  <span data-ttu-id="67fe3-212">![Usuários](./media/active-directory-saas-panorama9-tutorial/ic790027.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="67fe3-212">![Users](./media/active-directory-saas-panorama9-tutorial/ic790027.png "Users")</span></span>

3. <span data-ttu-id="67fe3-213">Na seção Usuários, clique em **+** para adicionar um novo usuário.</span><span class="sxs-lookup"><span data-stu-id="67fe3-213">In the Users section, Click **+** to add new user.</span></span>

 <span data-ttu-id="67fe3-214">![Usuários](./media/active-directory-saas-panorama9-tutorial/ic790028.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="67fe3-214">![Users](./media/active-directory-saas-panorama9-tutorial/ic790028.png "Users")</span></span>

4. <span data-ttu-id="67fe3-215">Acesse a seção Dados do usuário e digite o endereço de email de um usuário válido do Azure Active Directory que você deseja provisionar na caixa de texto **Email**.</span><span class="sxs-lookup"><span data-stu-id="67fe3-215">Go to the User data section, type the email address of a valid Azure Active Directory user you want to provision into the **Email** textbox.</span></span>

5. <span data-ttu-id="67fe3-216">Acesse a seção Usuários e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="67fe3-216">Come to the Users section, Click **Save**.</span></span>
   
> [!NOTE]
    > <span data-ttu-id="67fe3-217">O titular da conta do Azure Active Directory recebe um email e segue um link para confirmar sua conta antes que ela se torne ativa.</span><span class="sxs-lookup"><span data-stu-id="67fe3-217">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="67fe3-218">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="67fe3-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="67fe3-219">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Panorama9.</span><span class="sxs-lookup"><span data-stu-id="67fe3-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Panorama9.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="67fe3-221">**Para atribuir Brenda Fernandes ao Panorama9, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="67fe3-221">**To assign Britta Simon to Panorama9, perform the following steps:**</span></span>

1. <span data-ttu-id="67fe3-222">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="67fe3-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="67fe3-224">Na lista de aplicativos, selecione **Panorama9**.</span><span class="sxs-lookup"><span data-stu-id="67fe3-224">In the applications list, select **Panorama9**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_app.png) 

3. <span data-ttu-id="67fe3-226">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="67fe3-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="67fe3-228">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="67fe3-228">Click **Add** button.</span></span> <span data-ttu-id="67fe3-229">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="67fe3-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="67fe3-231">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="67fe3-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="67fe3-232">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="67fe3-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="67fe3-233">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="67fe3-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="67fe3-234">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="67fe3-234">Testing single sign-on</span></span>

<span data-ttu-id="67fe3-235">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="67fe3-235">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="67fe3-236">Quando você clicar no bloco do Panorama9 no Painel de Acesso, deverá ser conectado automaticamente ao aplicativo Panorama9.</span><span class="sxs-lookup"><span data-stu-id="67fe3-236">When you click the Panorama9 tile in the Access Panel, you should get automatically signed-on to Panorama9 application.</span></span>
<span data-ttu-id="67fe3-237">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="67fe3-237">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="67fe3-238">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="67fe3-238">Additional resources</span></span>

* [<span data-ttu-id="67fe3-239">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="67fe3-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="67fe3-240">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="67fe3-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_203.png

