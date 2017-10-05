---
title: "Tutorial: Integração do Azure Active Directory com o Envoy | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Envoy."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 71f7afcc-1033-4098-9b7e-4f9f2b26f734
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 49211b35ab3e28e0df914061e7fa623907935638
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-envoy"></a><span data-ttu-id="93ba0-103">Tutorial: integração do Active Directory do Azure ao Envoy</span><span class="sxs-lookup"><span data-stu-id="93ba0-103">Tutorial: Azure Active Directory integration with Envoy</span></span>

<span data-ttu-id="93ba0-104">Neste tutorial, você aprende a integrar o Envoy ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="93ba0-104">In this tutorial, you learn how to integrate Envoy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="93ba0-105">A integração do Envoy ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="93ba0-105">Integrating Envoy with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="93ba0-106">No Azure AD, é possível controlar quem tem acesso ao Envoy.</span><span class="sxs-lookup"><span data-stu-id="93ba0-106">You can control in Azure AD who has access to Envoy.</span></span>
- <span data-ttu-id="93ba0-107">Você pode permitir que seus usuários entrem automaticamente no Envoy (Logon Único) com as respectivas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="93ba0-107">You can enable your users to automatically get signed-on to Envoy (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="93ba0-108">Você pode gerenciar suas contas em um único local central – o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="93ba0-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="93ba0-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="93ba0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="93ba0-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="93ba0-110">Prerequisites</span></span>

<span data-ttu-id="93ba0-111">Para configurar a integração do Azure AD com o Envoy, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="93ba0-111">To configure Azure AD integration with Envoy, you need the following items:</span></span>

- <span data-ttu-id="93ba0-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="93ba0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="93ba0-113">Uma assinatura do Envoy habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="93ba0-113">An Envoy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="93ba0-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="93ba0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="93ba0-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="93ba0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="93ba0-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="93ba0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="93ba0-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="93ba0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="93ba0-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="93ba0-118">Scenario description</span></span>
<span data-ttu-id="93ba0-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="93ba0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="93ba0-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="93ba0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="93ba0-121">Adicionar o Envoy por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="93ba0-121">Adding Envoy from the gallery</span></span>
2. <span data-ttu-id="93ba0-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="93ba0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-envoy-from-the-gallery"></a><span data-ttu-id="93ba0-123">Adicionar o Envoy por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="93ba0-123">Adding Envoy from the gallery</span></span>
<span data-ttu-id="93ba0-124">Para configurar a integração do Envoy com o Azure AD, você precisará adicionar o Envoy à sua lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="93ba0-124">To configure the integration of Envoy into Azure AD, you need to add Envoy from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="93ba0-125">**Para adicionar o Envoy por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="93ba0-125">**To add Envoy from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="93ba0-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="93ba0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="93ba0-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="93ba0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="93ba0-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="93ba0-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="93ba0-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="93ba0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="93ba0-133">Na caixa de pesquisa, digite **Envoy**, selecione **Envoy** no painel de resultados e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="93ba0-133">In the search box, type **Envoy**, select **Envoy** from result panel then click **Add** button to add the application.</span></span>

    ![Envoy na lista de resultados](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="93ba0-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="93ba0-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="93ba0-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Envoy, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="93ba0-136">In this section, you configure and test Azure AD single sign-on with Envoy based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="93ba0-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Envoy é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="93ba0-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Envoy is to a user in Azure AD.</span></span> <span data-ttu-id="93ba0-138">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Envoy.</span><span class="sxs-lookup"><span data-stu-id="93ba0-138">In other words, a link relationship between an Azure AD user and the related user in Envoy needs to be established.</span></span>

<span data-ttu-id="93ba0-139">No Envoy, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="93ba0-139">In Envoy, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="93ba0-140">Para configurar e testar o logon único do Azure AD com o Envoy, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="93ba0-140">To configure and test Azure AD single sign-on with Envoy, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="93ba0-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="93ba0-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="93ba0-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="93ba0-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="93ba0-143">**[Criar um usuário de teste do Envoy](#create-an-envoy-test-user)** – para ter um equivalente de Brenda Fernandes no Envoy que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="93ba0-143">**[Create an Envoy test user](#create-an-envoy-test-user)** - to have a counterpart of Britta Simon in Envoy that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="93ba0-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="93ba0-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="93ba0-145">**[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="93ba0-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="93ba0-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="93ba0-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="93ba0-147">Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único no aplicativo Envoy.</span><span class="sxs-lookup"><span data-stu-id="93ba0-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Envoy application.</span></span>

<span data-ttu-id="93ba0-148">**Para configurar o logon único do Azure AD com o Envoy, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="93ba0-148">**To configure Azure AD single sign-on with Envoy, perform the following steps:**</span></span>

1. <span data-ttu-id="93ba0-149">No Portal do Azure, na página de integração do aplicativo **Envoy**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="93ba0-149">In the Azure portal, on the **Envoy** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="93ba0-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="93ba0-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_samlbase.png)

3. <span data-ttu-id="93ba0-153">Na seção **Domínio e URLs do Envoy**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="93ba0-153">On the **Envoy Domain and URLs** section, perform the following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do Envoy](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_url.png)

    <span data-ttu-id="93ba0-155">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<tenant-name>.Envoy.com`</span><span class="sxs-lookup"><span data-stu-id="93ba0-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.Envoy.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="93ba0-156">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="93ba0-156">This value is not real.</span></span> <span data-ttu-id="93ba0-157">Atualize esse valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="93ba0-157">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="93ba0-158">Entre em contato com a [equipe de suporte ao cliente do Envoy](https://envoy.com/contact/) para obter esse valor.</span><span class="sxs-lookup"><span data-stu-id="93ba0-158">Contact [Envoy Client support team](https://envoy.com/contact/) to get this value.</span></span>

4. <span data-ttu-id="93ba0-159">Na seção **Certificado de Autenticação SAML**, copie o valor da **IMPRESSÃO DIGITAL** do certificado.</span><span class="sxs-lookup"><span data-stu-id="93ba0-159">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate..</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_certificate.png) 

5. <span data-ttu-id="93ba0-161">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="93ba0-161">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-envoy-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="93ba0-163">Na seção **Configuração do Envoy**, clique em **Configurar o Envoy** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="93ba0-163">On the **Envoy Configuration** section, click **Configure Envoy** to open **Configure sign-on** window.</span></span> <span data-ttu-id="93ba0-164">Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="93ba0-164">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuração do Envoy](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_configure.png)

7. <span data-ttu-id="93ba0-166">Em outra janela do navegador da Web, faça logon em seu site de empresa do Envoy como administrador.</span><span class="sxs-lookup"><span data-stu-id="93ba0-166">In a different web browser window, log into your Envoy company site as an administrator.</span></span>

8. <span data-ttu-id="93ba0-167">Na barra de ferramentas na parte superior, clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="93ba0-167">In the toolbar on the top, click **Settings**.</span></span>

    <span data-ttu-id="93ba0-168">![Envoy](./media/active-directory-saas-envoy-tutorial/ic776782.png "Envoy")</span><span class="sxs-lookup"><span data-stu-id="93ba0-168">![Envoy](./media/active-directory-saas-envoy-tutorial/ic776782.png "Envoy")</span></span>

9. <span data-ttu-id="93ba0-169">Clique em **Empresa**.</span><span class="sxs-lookup"><span data-stu-id="93ba0-169">Click **Company**.</span></span>

    <span data-ttu-id="93ba0-170">![Empresa](./media/active-directory-saas-envoy-tutorial/ic776783.png "Empresa")</span><span class="sxs-lookup"><span data-stu-id="93ba0-170">![Company](./media/active-directory-saas-envoy-tutorial/ic776783.png "Company")</span></span>

10. <span data-ttu-id="93ba0-171">Clique em **SAML**.</span><span class="sxs-lookup"><span data-stu-id="93ba0-171">Click **SAML**.</span></span>

    <span data-ttu-id="93ba0-172">![SAML](./media/active-directory-saas-envoy-tutorial/ic776784.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="93ba0-172">![SAML](./media/active-directory-saas-envoy-tutorial/ic776784.png "SAML")</span></span>

11. <span data-ttu-id="93ba0-173">Na seção de configuração da **Autenticação SAML** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="93ba0-173">In the **SAML Authentication** configuration section, perform the following steps:</span></span>

    <span data-ttu-id="93ba0-174">![Autenticação SAML](./media/active-directory-saas-envoy-tutorial/ic776785.png "Autenticação SAML")</span><span class="sxs-lookup"><span data-stu-id="93ba0-174">![SAML authentication](./media/active-directory-saas-envoy-tutorial/ic776785.png "SAML authentication")</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="93ba0-175">O valor para a ID de Local de Matriz é automaticamente gerada pelo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="93ba0-175">The value for the HQ location ID is auto generated by the application.</span></span>
    
    <span data-ttu-id="93ba0-176">a.</span><span class="sxs-lookup"><span data-stu-id="93ba0-176">a.</span></span> <span data-ttu-id="93ba0-177">Na caixa de texto **Impressão digital**, cole o valor da **Impressão Digital** do certificado copiado do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="93ba0-177">In **Fingerprint** textbox, paste the **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="93ba0-178">b.</span><span class="sxs-lookup"><span data-stu-id="93ba0-178">b.</span></span> <span data-ttu-id="93ba0-179">Cole o valor da **URL do Serviço de Logon Único SAML** copiado do Portal do Azure na caixa de texto **URL SAML HTTP DO PROVEDOR DE IDENTIDADE**.</span><span class="sxs-lookup"><span data-stu-id="93ba0-179">Paste **SAML Single Sign-On Service URL** value, which you have copied form the Azure portal into the **IDENTITY PROVIDER HTTP SAML URL** textbox.</span></span>
    
    <span data-ttu-id="93ba0-180">c.</span><span class="sxs-lookup"><span data-stu-id="93ba0-180">c.</span></span> <span data-ttu-id="93ba0-181">Clique em **Salvar alterações**.</span><span class="sxs-lookup"><span data-stu-id="93ba0-181">Click **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="93ba0-182">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="93ba0-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="93ba0-183">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="93ba0-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="93ba0-184">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="93ba0-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="93ba0-185">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="93ba0-185">Create an Azure AD test user</span></span>

<span data-ttu-id="93ba0-186">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="93ba0-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="93ba0-188">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="93ba0-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="93ba0-189">No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="93ba0-189">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-envoy-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="93ba0-191">Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="93ba0-191">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-envoy-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="93ba0-193">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.</span><span class="sxs-lookup"><span data-stu-id="93ba0-193">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![O botão Adicionar](./media/active-directory-saas-envoy-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="93ba0-195">Na caixa de diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="93ba0-195">In the **User** dialog box, perform the following steps:</span></span>

    ![A caixa de diálogo Usuário](./media/active-directory-saas-envoy-tutorial/create_aaduser_04.png)

    <span data-ttu-id="93ba0-197">a.</span><span class="sxs-lookup"><span data-stu-id="93ba0-197">a.</span></span> <span data-ttu-id="93ba0-198">Na caixa **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="93ba0-198">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="93ba0-199">b.</span><span class="sxs-lookup"><span data-stu-id="93ba0-199">b.</span></span> <span data-ttu-id="93ba0-200">Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="93ba0-200">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="93ba0-201">c.</span><span class="sxs-lookup"><span data-stu-id="93ba0-201">c.</span></span> <span data-ttu-id="93ba0-202">Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.</span><span class="sxs-lookup"><span data-stu-id="93ba0-202">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="93ba0-203">d.</span><span class="sxs-lookup"><span data-stu-id="93ba0-203">d.</span></span> <span data-ttu-id="93ba0-204">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="93ba0-204">Click **Create**.</span></span>
 
### <a name="create-an-envoy-test-user"></a><span data-ttu-id="93ba0-205">Criar um usuário de teste do Envoy</span><span class="sxs-lookup"><span data-stu-id="93ba0-205">Create an Envoy test user</span></span>

<span data-ttu-id="93ba0-206">Não há qualquer item de ação para a configuração do provisionamento de usuário para o Envoy.</span><span class="sxs-lookup"><span data-stu-id="93ba0-206">There is no action item for you to configure user provisioning to Envoy.</span></span> <span data-ttu-id="93ba0-207">Quando um usuário atribuído tenta fazer logon no Envoy usando o painel de acesso, o Envoy verifica se o usuário existe.</span><span class="sxs-lookup"><span data-stu-id="93ba0-207">When an assigned user tries to log into Envoy using the access panel, Envoy checks whether the user exists.</span></span> <span data-ttu-id="93ba0-208">Se ainda não houver uma conta de usuário, ela será criada automaticamente pelo Envoy.</span><span class="sxs-lookup"><span data-stu-id="93ba0-208">If there is no user account available yet, it is automatically created by Envoy.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="93ba0-209">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="93ba0-209">Assign the Azure AD test user</span></span>

<span data-ttu-id="93ba0-210">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo a ela acesso ao Envoy.</span><span class="sxs-lookup"><span data-stu-id="93ba0-210">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Envoy.</span></span>

![Atribuir a função de usuário][200] 

<span data-ttu-id="93ba0-212">**Para atribuir Brenda Fernandes ao Envoy, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="93ba0-212">**To assign Britta Simon to Envoy, perform the following steps:**</span></span>

1. <span data-ttu-id="93ba0-213">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="93ba0-213">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="93ba0-215">Na lista de aplicativos, escolha **Envoy**.</span><span class="sxs-lookup"><span data-stu-id="93ba0-215">In the applications list, select **Envoy**.</span></span>

    ![O link do Envoy na lista de Aplicativos](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_app.png)  

3. <span data-ttu-id="93ba0-217">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="93ba0-217">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202]

4. <span data-ttu-id="93ba0-219">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="93ba0-219">Click **Add** button.</span></span> <span data-ttu-id="93ba0-220">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="93ba0-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="93ba0-222">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="93ba0-222">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="93ba0-223">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="93ba0-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="93ba0-224">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="93ba0-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="93ba0-225">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="93ba0-225">Test single sign-on</span></span>

<span data-ttu-id="93ba0-226">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="93ba0-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="93ba0-227">Quando você clicar no bloco Envoy no Painel de Acesso, deverá ser automaticamente conectado ao seu aplicativo Envoy.</span><span class="sxs-lookup"><span data-stu-id="93ba0-227">When you click the Envoy tile in the Access Panel, you should get automatically signed-on to your Envoy application.</span></span>
<span data-ttu-id="93ba0-228">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="93ba0-228">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="93ba0-229">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="93ba0-229">Additional resources</span></span>

* [<span data-ttu-id="93ba0-230">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="93ba0-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="93ba0-231">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="93ba0-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_203.png

