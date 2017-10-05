---
title: "Tutorial: Integração do Azure Active Directory ao Canvas LMS | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Canvas LMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfed291c-a33e-410d-b919-5b965a631d45
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: jeedes
ms.openlocfilehash: 2212b7a81b66d1afd1aa78d1487b07b6d7b84129
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-canvas-lms"></a><span data-ttu-id="41094-103">Tutorial: Integração do Azure Active Directory ao Canvas LMS</span><span class="sxs-lookup"><span data-stu-id="41094-103">Tutorial: Azure Active Directory integration with Canvas LMS</span></span>

<span data-ttu-id="41094-104">Neste tutorial, você aprende a integrar o Canvas ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="41094-104">In this tutorial, you learn how to integrate Canvas with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="41094-105">A integração do Canvas ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="41094-105">Integrating Canvas with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="41094-106">No Azure AD, é possível controlar quem tem acesso ao Canvas</span><span class="sxs-lookup"><span data-stu-id="41094-106">You can control in Azure AD who has access to Canvas</span></span>
- <span data-ttu-id="41094-107">É possível permitir que os usuários se conectem automaticamente ao Canvas (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="41094-107">You can enable your users to automatically get signed-on to Canvas (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="41094-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="41094-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="41094-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="41094-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41094-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="41094-110">Prerequisites</span></span>

<span data-ttu-id="41094-111">Para configurar a integração do Azure AD ao Canvas, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="41094-111">To configure Azure AD integration with Canvas, you need the following items:</span></span>

- <span data-ttu-id="41094-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="41094-112">An Azure AD subscription</span></span>
- <span data-ttu-id="41094-113">Uma assinatura habilitada para logon único do Canvas</span><span class="sxs-lookup"><span data-stu-id="41094-113">A Canvas single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="41094-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="41094-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="41094-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="41094-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="41094-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="41094-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="41094-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="41094-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="41094-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="41094-118">Scenario description</span></span>
<span data-ttu-id="41094-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="41094-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="41094-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="41094-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="41094-121">Adicionando o Canvas por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="41094-121">Adding Canvas from the gallery</span></span>
2. <span data-ttu-id="41094-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="41094-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-canvas-from-the-gallery"></a><span data-ttu-id="41094-123">Adicionando o Canvas por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="41094-123">Adding Canvas from the gallery</span></span>
<span data-ttu-id="41094-124">Para configurar a integração do Canvas ao Azure AD, você precisa adicionar o Canvas à lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="41094-124">To configure the integration of Canvas into Azure AD, you need to add Canvas from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="41094-125">**Para adicionar o Canvas por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="41094-125">**To add Canvas from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="41094-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="41094-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="41094-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="41094-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="41094-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="41094-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="41094-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="41094-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="41094-133">Na caixa de pesquisa, digite **Canvas**.</span><span class="sxs-lookup"><span data-stu-id="41094-133">In the search box, type **Canvas**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_search.png)

5. <span data-ttu-id="41094-135">No painel de resultados, selecione **Canvas** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="41094-135">In the results panel, select **Canvas**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="41094-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="41094-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="41094-138">Nesta seção, você configura e testa o logon único do Azure AD com o Canvas, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="41094-138">In this section, you configure and test Azure AD single sign-on with Canvas based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="41094-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Canvas é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="41094-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Canvas is to a user in Azure AD.</span></span> <span data-ttu-id="41094-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Canvas.</span><span class="sxs-lookup"><span data-stu-id="41094-140">In other words, a link relationship between an Azure AD user and the related user in Canvas needs to be established.</span></span>

<span data-ttu-id="41094-141">No Canvas, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="41094-141">In Canvas, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="41094-142">Para configurar e testar o logon único do Azure AD com o Canvas, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="41094-142">To configure and test Azure AD single sign-on with Canvas, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="41094-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="41094-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="41094-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="41094-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="41094-145">**[Criando um usuário de teste do Canvas](#creating-a-canvas-test-user)** – para ter um equivalente de Brenda Fernandes no Canvas que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="41094-145">**[Creating a Canvas test user](#creating-a-canvas-test-user)** - to have a counterpart of Britta Simon in Canvas that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="41094-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="41094-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="41094-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="41094-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="41094-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="41094-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="41094-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Canvas.</span><span class="sxs-lookup"><span data-stu-id="41094-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Canvas application.</span></span>

<span data-ttu-id="41094-150">**Para configurar o logon único do Azure AD com o Canvas, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="41094-150">**To configure Azure AD single sign-on with Canvas, perform the following steps:**</span></span>

1. <span data-ttu-id="41094-151">No portal do Azure, na página de integração do aplicativo do **Canvas**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="41094-151">In the Azure portal, on the **Canvas** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="41094-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="41094-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_samlbase.png)

3. <span data-ttu-id="41094-155">Na seção **Domínio e URLs do Canvas**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="41094-155">On the **Canvas Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_url.png)

    <span data-ttu-id="41094-157">a.</span><span class="sxs-lookup"><span data-stu-id="41094-157">a.</span></span> <span data-ttu-id="41094-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<tenant-name>.instructure.com`</span><span class="sxs-lookup"><span data-stu-id="41094-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.instructure.com`</span></span>

    <span data-ttu-id="41094-159">b.</span><span class="sxs-lookup"><span data-stu-id="41094-159">b.</span></span> <span data-ttu-id="41094-160">Na caixa de texto **Identificador**, digite o valor usando o seguinte padrão: `https://<tenant-name>.instructure.com/saml2`</span><span class="sxs-lookup"><span data-stu-id="41094-160">In the **Identifier** textbox, type the value using the following pattern: `https://<tenant-name>.instructure.com/saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="41094-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="41094-161">These values are not real.</span></span> <span data-ttu-id="41094-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="41094-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="41094-163">Contate a [equipe de suporte ao Cliente do Canvas](https://community.canvaslms.com/community/help) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="41094-163">Contact [Canvas Client support team](https://community.canvaslms.com/community/help) to get these values.</span></span> 
 
4. <span data-ttu-id="41094-164">Na seção **Certificado de Autenticação SAML**, copie o valor da **IMPRESSÃO DIGITAL** do certificado.</span><span class="sxs-lookup"><span data-stu-id="41094-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_certificate.png) 

5. <span data-ttu-id="41094-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="41094-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="41094-168">Na seção **Configuração do Canvas**, clique em **Configurar o Canvas** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="41094-168">On the **Canvas Configuration** section, click **Configure Canvas** to open **Configure sign-on** window.</span></span> <span data-ttu-id="41094-169">Copie a **URL de Alteração de Senha, a URL de Saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="41094-169">Copy the **Change Password URL, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_configure.png) 
 
7. <span data-ttu-id="41094-171">Em outra janela do navegador da Web, faça logon em seu site de empresa do Canvas como administrador.</span><span class="sxs-lookup"><span data-stu-id="41094-171">In a different web browser window, log in to your Canvas company site as an administrator.</span></span>

8. <span data-ttu-id="41094-172">Vá para **Cursos \> Contas Gerenciadas \> Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="41094-172">Go to **Courses \> Managed Accounts \> Microsoft**.</span></span>
   
    <span data-ttu-id="41094-173">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span><span class="sxs-lookup"><span data-stu-id="41094-173">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span></span>

9. <span data-ttu-id="41094-174">No painel de navegação à esquerda, selecione **Autenticação** e clique em **Adicionar Nova Config. do SAML**.</span><span class="sxs-lookup"><span data-stu-id="41094-174">In the navigation pane on the left, select **Authentication**, and then click **Add New SAML Config**.</span></span>
   
    <span data-ttu-id="41094-175">![Autenticação](./media/active-directory-saas-canvas-lms-tutorial/IC775991.png "Autenticação")</span><span class="sxs-lookup"><span data-stu-id="41094-175">![Authentication](./media/active-directory-saas-canvas-lms-tutorial/IC775991.png "Authentication")</span></span>

10. <span data-ttu-id="41094-176">Na página de integração atual, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="41094-176">On the Current Integration page, perform the following steps:</span></span>
   
    <span data-ttu-id="41094-177">![Integração Atual](./media/active-directory-saas-canvas-lms-tutorial/IC775992.png "integração Atual")</span><span class="sxs-lookup"><span data-stu-id="41094-177">![Current Integration](./media/active-directory-saas-canvas-lms-tutorial/IC775992.png "Current Integration")</span></span>

    <span data-ttu-id="41094-178">a.</span><span class="sxs-lookup"><span data-stu-id="41094-178">a.</span></span> <span data-ttu-id="41094-179">Na caixa de texto **ID da Entidade do IdP**, cole o valor da **ID da Entidade SAML** copiado no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="41094-179">In **IdP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="41094-180">b.</span><span class="sxs-lookup"><span data-stu-id="41094-180">b.</span></span> <span data-ttu-id="41094-181">Na caixa de texto **URL de Logon**, cole o valor da **URL do Serviço de Logon Único SAML** copiado no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="41094-181">In **Log On URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal .</span></span>

    <span data-ttu-id="41094-182">c.</span><span class="sxs-lookup"><span data-stu-id="41094-182">c.</span></span> <span data-ttu-id="41094-183">Na caixa de texto **URL de Logoff**, cole o valor da **URL de Saída** copiado no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="41094-183">In **Log Out URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="41094-184">d.</span><span class="sxs-lookup"><span data-stu-id="41094-184">d.</span></span> <span data-ttu-id="41094-185">Na caixa de texto **Link Alteração de Senha**, cole o valor da **URL de Alteração de Senha** copiado no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="41094-185">In **Change Password Link** textbox, paste the value of **Change Password URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="41094-186">e.</span><span class="sxs-lookup"><span data-stu-id="41094-186">e.</span></span> <span data-ttu-id="41094-187">Na caixa de texto **Impressão Digital do Certificado**, cole o valor de **Impressão Digital** do certificado copiado do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="41094-187">In **Certificate Fingerprint** textbox, paste the **Thumbprint** value of certificate which you have copied from Azure portal.</span></span>      
        
    <span data-ttu-id="41094-188">f.</span><span class="sxs-lookup"><span data-stu-id="41094-188">f.</span></span> <span data-ttu-id="41094-189">Na lista **Atributo de Logon**, selecione **NameID**.</span><span class="sxs-lookup"><span data-stu-id="41094-189">From the **Login Attribute** list, select **NameID**.</span></span>

    <span data-ttu-id="41094-190">g.</span><span class="sxs-lookup"><span data-stu-id="41094-190">g.</span></span> <span data-ttu-id="41094-191">Na lista **Formato de Identificador**, selecione **emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="41094-191">From the **Identifier Format** list, select **emailAddress**.</span></span>

    <span data-ttu-id="41094-192">h.</span><span class="sxs-lookup"><span data-stu-id="41094-192">h.</span></span> <span data-ttu-id="41094-193">Clique em **Salvar Configurações de Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="41094-193">Click **Save Authentication Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="41094-194">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="41094-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="41094-195">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="41094-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="41094-196">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="41094-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="41094-197">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="41094-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="41094-198">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="41094-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="41094-200">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="41094-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="41094-201">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="41094-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="41094-203">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="41094-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="41094-205">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="41094-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="41094-207">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="41094-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="41094-209">a.</span><span class="sxs-lookup"><span data-stu-id="41094-209">a.</span></span> <span data-ttu-id="41094-210">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="41094-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="41094-211">b.</span><span class="sxs-lookup"><span data-stu-id="41094-211">b.</span></span> <span data-ttu-id="41094-212">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="41094-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="41094-213">c.</span><span class="sxs-lookup"><span data-stu-id="41094-213">c.</span></span> <span data-ttu-id="41094-214">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="41094-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="41094-215">d.</span><span class="sxs-lookup"><span data-stu-id="41094-215">d.</span></span> <span data-ttu-id="41094-216">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="41094-216">Click **Create**.</span></span>
 
### <a name="creating-a-canvas-test-user"></a><span data-ttu-id="41094-217">Criando um usuário de teste do Canvas</span><span class="sxs-lookup"><span data-stu-id="41094-217">Creating a Canvas test user</span></span>

<span data-ttu-id="41094-218">Para permitir que os usuários do Azure AD façam logon no Canvas, eles devem ser provisionados no Canvas.</span><span class="sxs-lookup"><span data-stu-id="41094-218">To enable Azure AD users to log in to Canvas, they must be provisioned into Canvas.</span></span>

<span data-ttu-id="41094-219">No caso do Canvas, o provisionamento de usuário é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="41094-219">In case of Canvas, user provisioning is a manual task.</span></span>

<span data-ttu-id="41094-220">**Para provisionar uma conta de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="41094-220">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="41094-221">Faça logon em seu locatário do **Canvas** .</span><span class="sxs-lookup"><span data-stu-id="41094-221">Log in to your **Canvas** tenant.</span></span>

2. <span data-ttu-id="41094-222">Vá para **Cursos \> Contas Gerenciadas \> Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="41094-222">Go to **Courses \> Managed Accounts \> Microsoft**.</span></span>
   
   <span data-ttu-id="41094-223">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span><span class="sxs-lookup"><span data-stu-id="41094-223">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span></span>

3. <span data-ttu-id="41094-224">Clique em **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="41094-224">Click **Users**.</span></span>
   
   <span data-ttu-id="41094-225">![Usuários](./media/active-directory-saas-canvas-lms-tutorial/IC775995.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="41094-225">![Users](./media/active-directory-saas-canvas-lms-tutorial/IC775995.png "Users")</span></span>

4. <span data-ttu-id="41094-226">Clique em **Adicionar Novo Usuário**.</span><span class="sxs-lookup"><span data-stu-id="41094-226">Click **Add New User**.</span></span>
   
   <span data-ttu-id="41094-227">![Usuários](./media/active-directory-saas-canvas-lms-tutorial/IC775996.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="41094-227">![Users](./media/active-directory-saas-canvas-lms-tutorial/IC775996.png "Users")</span></span>

5. <span data-ttu-id="41094-228">Na página da caixa de diálogo Adicionar um Novo Usuário, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="41094-228">On the Add a New User dialog page, perform the following steps:</span></span>
   
   <span data-ttu-id="41094-229">![Adicionar Usuário](./media/active-directory-saas-canvas-lms-tutorial/IC775997.png "Adicionar Usuário")</span><span class="sxs-lookup"><span data-stu-id="41094-229">![Add User](./media/active-directory-saas-canvas-lms-tutorial/IC775997.png "Add User")</span></span>
   
   <span data-ttu-id="41094-230">a.</span><span class="sxs-lookup"><span data-stu-id="41094-230">a.</span></span> <span data-ttu-id="41094-231">Na caixa de texto **Nome Completo**, insira o nome de usuário, como **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="41094-231">In the **Full Name** textbox, enter the name of user like **BrittaSimon**.</span></span>

   <span data-ttu-id="41094-232">b.</span><span class="sxs-lookup"><span data-stu-id="41094-232">b.</span></span> <span data-ttu-id="41094-233">Na caixa de texto **Email**, insira o email de usuário como **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="41094-233">In the **Email** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

   <span data-ttu-id="41094-234">c.</span><span class="sxs-lookup"><span data-stu-id="41094-234">c.</span></span> <span data-ttu-id="41094-235">Na caixa de texto **Logon**, insira o endereço de email do Azure AD do usuário como **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="41094-235">In the **Login** textbox, enter the user’s Azure AD email address like **brittasimon@contoso.com**.</span></span>

   <span data-ttu-id="41094-236">d.</span><span class="sxs-lookup"><span data-stu-id="41094-236">d.</span></span> <span data-ttu-id="41094-237">Selecione **Enviar email ao usuário sobre a criação desta conta**.</span><span class="sxs-lookup"><span data-stu-id="41094-237">Select **Email the user about this account creation**.</span></span>

   <span data-ttu-id="41094-238">e.</span><span class="sxs-lookup"><span data-stu-id="41094-238">e.</span></span> <span data-ttu-id="41094-239">Clique em **Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="41094-239">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="41094-240">É possível usar qualquer outra ferramenta de criação da conta de usuário do Canvas ou as APIs fornecidas pelo Canvas para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="41094-240">You can use any other Canvas user account creation tools or APIs provided by Canvas to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="41094-241">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="41094-241">Assigning the Azure AD test user</span></span>

<span data-ttu-id="41094-242">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Canvas.</span><span class="sxs-lookup"><span data-stu-id="41094-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Canvas.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="41094-244">**Para atribuir Brenda Fernandes ao Canvas, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="41094-244">**To assign Britta Simon to Canvas, perform the following steps:**</span></span>

1. <span data-ttu-id="41094-245">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="41094-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="41094-247">Na lista de aplicativos, selecione **Canvas**.</span><span class="sxs-lookup"><span data-stu-id="41094-247">In the applications list, select **Canvas**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_app.png) 

3. <span data-ttu-id="41094-249">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="41094-249">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="41094-251">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="41094-251">Click **Add** button.</span></span> <span data-ttu-id="41094-252">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="41094-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="41094-254">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="41094-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="41094-255">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="41094-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="41094-256">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="41094-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="41094-257">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="41094-257">Testing single sign-on</span></span>

<span data-ttu-id="41094-258">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="41094-258">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="41094-259">Quando você clicar no bloco Canvas no Painel de Acesso, deverá ser automaticamente conectado ao aplicativo Canvas.</span><span class="sxs-lookup"><span data-stu-id="41094-259">When you click the Canvas tile in the Access Panel, you should get automatically signed-on to your Canvas application.</span></span>
<span data-ttu-id="41094-260">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="41094-260">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="41094-261">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="41094-261">Additional resources</span></span>

* [<span data-ttu-id="41094-262">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="41094-262">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="41094-263">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="41094-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_203.png

