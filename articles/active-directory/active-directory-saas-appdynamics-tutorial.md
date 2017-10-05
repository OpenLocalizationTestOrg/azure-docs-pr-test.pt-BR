---
title: "Tutorial: Integração do Azure Active Directory ao AppDynamics | Microsoft Azure"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o AppDynamics."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 25fd1df0-411c-4f55-8be3-4273b543100f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 634e68bdb937eba68b27b824dc62fe2677e24ffe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-appdynamics"></a><span data-ttu-id="73676-103">Tutorial: Integração do Active Directory do Azure ao AppDynamics</span><span class="sxs-lookup"><span data-stu-id="73676-103">Tutorial: Azure Active Directory integration with AppDynamics</span></span>

<span data-ttu-id="73676-104">Neste tutorial, você aprende a integrar o AppDynamics ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="73676-104">In this tutorial, you learn how to integrate AppDynamics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="73676-105">A integração do AppDynamics ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="73676-105">Integrating AppDynamics with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="73676-106">No Azure AD, é possível controlar quem tem acesso ao AppDynamics</span><span class="sxs-lookup"><span data-stu-id="73676-106">You can control in Azure AD who has access to AppDynamics</span></span>
- <span data-ttu-id="73676-107">É possível permitir que os usuários se conectem automaticamente ao AppDynamics (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="73676-107">You can enable your users to automatically get signed-on to AppDynamics (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="73676-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="73676-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="73676-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="73676-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="73676-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="73676-110">Prerequisites</span></span>

<span data-ttu-id="73676-111">Para configurar a integração do Azure AD ao AppDynamics, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="73676-111">To configure Azure AD integration with AppDynamics, you need the following items:</span></span>

- <span data-ttu-id="73676-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="73676-112">An Azure AD subscription</span></span>
- <span data-ttu-id="73676-113">Uma assinatura habilitada para logon único do AppDynamics</span><span class="sxs-lookup"><span data-stu-id="73676-113">An AppDynamics single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="73676-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="73676-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="73676-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="73676-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="73676-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="73676-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="73676-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="73676-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="73676-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="73676-118">Scenario description</span></span>
<span data-ttu-id="73676-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="73676-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="73676-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="73676-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="73676-121">Adicionando o AppDynamics por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="73676-121">Adding AppDynamics from the gallery</span></span>
2. <span data-ttu-id="73676-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="73676-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-appdynamics-from-the-gallery"></a><span data-ttu-id="73676-123">Adicionando o AppDynamics por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="73676-123">Adding AppDynamics from the gallery</span></span>
<span data-ttu-id="73676-124">Para configurar a integração do AppDynamics ao Azure AD, você precisa adicionar o AppDynamics à lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="73676-124">To configure the integration of AppDynamics into Azure AD, you need to add AppDynamics from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="73676-125">**Para adicionar o AppDynamics por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="73676-125">**To add AppDynamics from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="73676-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="73676-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="73676-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="73676-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="73676-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="73676-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="73676-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="73676-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="73676-133">Na caixa de pesquisa, digite **AppDynamics**.</span><span class="sxs-lookup"><span data-stu-id="73676-133">In the search box, type **AppDynamics**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_search.png)

5. <span data-ttu-id="73676-135">No painel de resultados, selecione **AppDynamics** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="73676-135">In the results panel, select **AppDynamics**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="73676-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="73676-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="73676-138">Nesta seção, você configura e testa o logon único do Azure AD com o AppDynamics, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="73676-138">In this section, you configure and test Azure AD single sign-on with AppDynamics based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="73676-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do AppDynamics é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="73676-139">For single sign-on to work, Azure AD needs to know what the counterpart user in AppDynamics is to a user in Azure AD.</span></span> <span data-ttu-id="73676-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="73676-140">In other words, a link relationship between an Azure AD user and the related user in AppDynamics needs to be established.</span></span>

<span data-ttu-id="73676-141">No AppDynamics, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="73676-141">In AppDynamics, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="73676-142">Para configurar e testar o logon único do Azure AD com o AppDynamics, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="73676-142">To configure and test Azure AD single sign-on with AppDynamics, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="73676-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="73676-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="73676-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="73676-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="73676-145">**[Criando um usuário de teste do AppDynamics](#creating-an-appdynamics-test-user)** – para ter um equivalente de Brenda Fernandes no AppDynamics que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="73676-145">**[Creating an AppDynamics test user](#creating-an-appdynamics-test-user)** - to have a counterpart of Britta Simon in AppDynamics that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="73676-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="73676-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="73676-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="73676-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="73676-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="73676-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="73676-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="73676-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AppDynamics application.</span></span>

<span data-ttu-id="73676-150">**Para configurar o logon único do Azure AD com o AppDynamics, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="73676-150">**To configure Azure AD single sign-on with AppDynamics, perform the following steps:**</span></span>

1. <span data-ttu-id="73676-151">No portal do Azure, na página de integração do aplicativo do **AppDynamics**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="73676-151">In the Azure portal, on the **AppDynamics** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="73676-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="73676-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_samlbase.png)

3. <span data-ttu-id="73676-155">Na seção **Domínio e URLs do AppDynamics**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="73676-155">On the **AppDynamics Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_url.png)

    <span data-ttu-id="73676-157">a.</span><span class="sxs-lookup"><span data-stu-id="73676-157">a.</span></span> <span data-ttu-id="73676-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<companyname>.saas.appdynamics.com`</span><span class="sxs-lookup"><span data-stu-id="73676-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.saas.appdynamics.com`</span></span>

    <span data-ttu-id="73676-159">b.</span><span class="sxs-lookup"><span data-stu-id="73676-159">b.</span></span> <span data-ttu-id="73676-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<companyname>.saas.appdynamics.com/controller`</span><span class="sxs-lookup"><span data-stu-id="73676-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.saas.appdynamics.com/controller`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="73676-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="73676-161">These values are not real.</span></span> <span data-ttu-id="73676-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="73676-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="73676-163">Contate a [equipe de suporte ao Cliente do AppDynamics](https://www.appdynamics.com/support/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="73676-163">Contact [AppDynamics Client support team](https://www.appdynamics.com/support/) to get these values.</span></span> 
 
4. <span data-ttu-id="73676-164">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="73676-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_certificate.png) 

5. <span data-ttu-id="73676-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="73676-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-appdynamics-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="73676-168">Na seção **Configuração do AppDynamics**, clique em **Configurar o AppDynamics** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="73676-168">On the **AppDynamics Configuration** section, click **Configure AppDynamics** to open **Configure sign-on** window.</span></span> <span data-ttu-id="73676-169">Copie a **URL de Saída e a URL do Serviço de Logon Único SAML** da **seção Referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="73676-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_configure.png) 

7. <span data-ttu-id="73676-171">Em outra janela do navegador da Web, faça logon em seu site de empresa do AppDynamics como administrador.</span><span class="sxs-lookup"><span data-stu-id="73676-171">In a different web browser window, log in to your AppDynamics company site as an administrator.</span></span>

8. <span data-ttu-id="73676-172">Na barra de ferramentas na parte superior, clique em **Configurações** e em **Administração**.</span><span class="sxs-lookup"><span data-stu-id="73676-172">In the toolbar on the top, click **Settings**, and then click **Administration**.</span></span>
   
    <span data-ttu-id="73676-173">![Administração](./media/active-directory-saas-appdynamics-tutorial/ic790216.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="73676-173">![Administration](./media/active-directory-saas-appdynamics-tutorial/ic790216.png "Administration")</span></span>

9. <span data-ttu-id="73676-174">Clique na guia **Provedor de Autenticação** .</span><span class="sxs-lookup"><span data-stu-id="73676-174">Click the **Authentication Provider** tab.</span></span>
   
    <span data-ttu-id="73676-175">![Provedor de Autenticação](./media/active-directory-saas-appdynamics-tutorial/ic790224.png "Provedor de Autenticação")</span><span class="sxs-lookup"><span data-stu-id="73676-175">![Authentication Provider](./media/active-directory-saas-appdynamics-tutorial/ic790224.png "Authentication Provider")</span></span>

10. <span data-ttu-id="73676-176">Na seção **Provedor de Autenticação** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="73676-176">In the **Authentication Provider** section, perform the following steps:</span></span>
   
    <span data-ttu-id="73676-177">![Configuração SAML](./media/active-directory-saas-appdynamics-tutorial/ic790225.png "configuração SAML")</span><span class="sxs-lookup"><span data-stu-id="73676-177">![SAML Configuration](./media/active-directory-saas-appdynamics-tutorial/ic790225.png "SAML Configuration")</span></span>   

    <span data-ttu-id="73676-178">a.</span><span class="sxs-lookup"><span data-stu-id="73676-178">a.</span></span> <span data-ttu-id="73676-179">Como **Provedor de Autenticação**, selecione **SAML**.</span><span class="sxs-lookup"><span data-stu-id="73676-179">As **Authentication Provider**, select **SAML**.</span></span>

    <span data-ttu-id="73676-180">b.</span><span class="sxs-lookup"><span data-stu-id="73676-180">b.</span></span> <span data-ttu-id="73676-181">Na caixa de texto **URL de Logon**, cole o valor da **URL do Serviço de Logon Único SAML** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="73676-181">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="73676-182">c.</span><span class="sxs-lookup"><span data-stu-id="73676-182">c.</span></span> <span data-ttu-id="73676-183">Na caixa de texto **URL de Logoff**, cole o valor da **URL de Saída** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="73676-183">In the **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
       
    <span data-ttu-id="73676-184">d.</span><span class="sxs-lookup"><span data-stu-id="73676-184">d.</span></span> <span data-ttu-id="73676-185">Abra seu certificado codificado em Base 64 no bloco de notas, copie o conteúdo dele na área de transferência e cole-o na caixa de texto **Certificado**</span><span class="sxs-lookup"><span data-stu-id="73676-185">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Certificate** textbox</span></span>

    <span data-ttu-id="73676-186">e.</span><span class="sxs-lookup"><span data-stu-id="73676-186">e.</span></span> <span data-ttu-id="73676-187">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="73676-187">Click **Save**.</span></span>

     <span data-ttu-id="73676-188">![Salvar](./media/active-directory-saas-appdynamics-tutorial/ic777673.png "Salvar")</span><span class="sxs-lookup"><span data-stu-id="73676-188">![Save](./media/active-directory-saas-appdynamics-tutorial/ic777673.png "Save")</span></span>

> [!TIP]
> <span data-ttu-id="73676-189">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="73676-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="73676-190">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="73676-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="73676-191">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="73676-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="73676-192">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="73676-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="73676-193">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="73676-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="73676-195">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="73676-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="73676-196">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="73676-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="73676-198">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="73676-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="73676-200">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="73676-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="73676-202">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="73676-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="73676-204">a.</span><span class="sxs-lookup"><span data-stu-id="73676-204">a.</span></span> <span data-ttu-id="73676-205">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="73676-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="73676-206">b.</span><span class="sxs-lookup"><span data-stu-id="73676-206">b.</span></span> <span data-ttu-id="73676-207">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="73676-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="73676-208">c.</span><span class="sxs-lookup"><span data-stu-id="73676-208">c.</span></span> <span data-ttu-id="73676-209">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="73676-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="73676-210">d.</span><span class="sxs-lookup"><span data-stu-id="73676-210">d.</span></span> <span data-ttu-id="73676-211">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="73676-211">Click **Create**.</span></span>
 
### <a name="creating-an-appdynamics-test-user"></a><span data-ttu-id="73676-212">Criando um usuário de teste do AppDynamics</span><span class="sxs-lookup"><span data-stu-id="73676-212">Creating an AppDynamics test user</span></span>

<span data-ttu-id="73676-213">Para permitir que os usuários do Azure AD façam logon no AppDynamics, eles devem ser provisionados no AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="73676-213">To enable Azure AD users to log in to AppDynamics, they must be provisioned into AppDynamics.</span></span> <span data-ttu-id="73676-214">No caso do AppDynamics, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="73676-214">In the case of AppDynamics, provisioning is a manual task.</span></span>

<span data-ttu-id="73676-215">**Para configurar o provisionamento de usuários, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="73676-215">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="73676-216">Faça logon em seu site de empresa do AppDynamics como administrador.</span><span class="sxs-lookup"><span data-stu-id="73676-216">Log in to your AppDynamics company site as an administrator.</span></span>

2. <span data-ttu-id="73676-217">Vá para **Usuários**, e, em seguida, clique em **+** para abrir o diálogo **Criar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="73676-217">Go to **Users**, and then click **+** to open the **Create User** dialog.</span></span>
   
    <span data-ttu-id="73676-218">![Usuários](./media/active-directory-saas-appdynamics-tutorial/ic790229.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="73676-218">![Users](./media/active-directory-saas-appdynamics-tutorial/ic790229.png "Users")</span></span>

3. <span data-ttu-id="73676-219">Na seção **Criar Usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="73676-219">In the **Create User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="73676-220">![Criar usuário](./media/active-directory-saas-appdynamics-tutorial/ic790230.png "Criar usuário")</span><span class="sxs-lookup"><span data-stu-id="73676-220">![Create User](./media/active-directory-saas-appdynamics-tutorial/ic790230.png "Create User")</span></span>
   
    <span data-ttu-id="73676-221">a.</span><span class="sxs-lookup"><span data-stu-id="73676-221">a.</span></span> <span data-ttu-id="73676-222">Preencha os campos **Nome de usuário**, **Nome**, **Email**, **Nova Senha**, **Repetir Nova Senha** de uma conta válida do AAD que deseja provisionar nas caixas de texto relacionadas.</span><span class="sxs-lookup"><span data-stu-id="73676-222">Type the **Username**, **Name**, **Email**, **New Password**, **Repeat New Password** of a valid AAD account you want to provision into the related textboxes.</span></span>

    <span data-ttu-id="73676-223">b.</span><span class="sxs-lookup"><span data-stu-id="73676-223">b.</span></span> <span data-ttu-id="73676-224">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="73676-224">Click **Save**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="73676-225">Você pode usar qualquer outra ferramenta de criação da conta de usuário do AppDynamics ou as APIs fornecidas pelo AppDynamics para provisionar as contas de usuário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="73676-225">You can use any other AppDynamics user account creation tools or APIs provided by AppDynamics to provision Azure AD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="73676-226">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="73676-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="73676-227">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="73676-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AppDynamics.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="73676-229">**Para atribuir Brenda Fernandes ao AppDynamics, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="73676-229">**To assign Britta Simon to AppDynamics, perform the following steps:**</span></span>

1. <span data-ttu-id="73676-230">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="73676-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="73676-232">Na lista de aplicativos, selecione **AppDynamics**.</span><span class="sxs-lookup"><span data-stu-id="73676-232">In the applications list, select **AppDynamics**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_app.png) 

3. <span data-ttu-id="73676-234">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="73676-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="73676-236">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="73676-236">Click **Add** button.</span></span> <span data-ttu-id="73676-237">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="73676-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="73676-239">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="73676-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="73676-240">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="73676-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="73676-241">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="73676-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="73676-242">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="73676-242">Testing single sign-on</span></span>

<span data-ttu-id="73676-243">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="73676-243">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="73676-244">Quando você clicar no bloco AppDynamics no Painel de Acesso, deverá ser automaticamente conectado ao aplicativo AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="73676-244">When you click the AppDynamics tile in the Access Panel, you should get automatically signed-on to your AppDynamics application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="73676-245">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="73676-245">Additional resources</span></span>

* [<span data-ttu-id="73676-246">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="73676-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="73676-247">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="73676-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_203.png

