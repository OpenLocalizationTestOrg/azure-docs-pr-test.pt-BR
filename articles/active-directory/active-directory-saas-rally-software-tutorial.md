---
title: "Tutorial: Integração do Azure Active Directory com o Rally Software | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Rally Software."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba25fade-e152-42dd-8377-a30bbc48c3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: jeedes
ms.openlocfilehash: 6481c9ef0ca71419ccfa6f7956f4702985743df3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rally-software"></a><span data-ttu-id="e32b7-103">Tutorial: Integração do Azure Active Directory com o Rally Software</span><span class="sxs-lookup"><span data-stu-id="e32b7-103">Tutorial: Azure Active Directory integration with Rally Software</span></span>

<span data-ttu-id="e32b7-104">Neste tutorial, você aprenderá a integrar o Rally Software ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="e32b7-104">In this tutorial, you learn how to integrate Rally Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e32b7-105">A integração do Rally Software ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="e32b7-105">Integrating Rally Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e32b7-106">No Azure AD, é possível controlar quem tem acesso ao Rally Software.</span><span class="sxs-lookup"><span data-stu-id="e32b7-106">You can control in Azure AD who has access to Rally Software.</span></span>
- <span data-ttu-id="e32b7-107">Você pode permitir que seus usuários façam logon automaticamente no Rally Software usando logon único com suas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e32b7-107">You can enable your users to automatically get signed-on to Rally Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="e32b7-108">Você pode gerenciar suas contas em um único local central – o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e32b7-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="e32b7-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e32b7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e32b7-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e32b7-110">Prerequisites</span></span>

<span data-ttu-id="e32b7-111">Para configurar a integração do Azure AD ao Rally Software, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="e32b7-111">To configure Azure AD integration with Rally Software, you need the following items:</span></span>

- <span data-ttu-id="e32b7-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e32b7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e32b7-113">Uma assinatura do Rally Software habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="e32b7-113">A Rally Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e32b7-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="e32b7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e32b7-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="e32b7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e32b7-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="e32b7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e32b7-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e32b7-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e32b7-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="e32b7-118">Scenario description</span></span>
<span data-ttu-id="e32b7-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="e32b7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e32b7-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="e32b7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e32b7-121">Adicionar o Rally Software por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="e32b7-121">Adding Rally Software from the gallery</span></span>
2. <span data-ttu-id="e32b7-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e32b7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rally-software-from-the-gallery"></a><span data-ttu-id="e32b7-123">Adicionar o Rally Software por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="e32b7-123">Adding Rally Software from the gallery</span></span>
<span data-ttu-id="e32b7-124">Para configurar a integração do Rally Software com o Azure AD, você precisará adicionar o Rally Software à sua lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="e32b7-124">To configure the integration of Rally Software into Azure AD, you need to add Rally Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e32b7-125">**Para adicionar o Rally Software por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e32b7-125">**To add Rally Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e32b7-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e32b7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="e32b7-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="e32b7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e32b7-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e32b7-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="e32b7-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e32b7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="e32b7-133">Na caixa de pesquisa, digite **Rally Software**, selecione **Rally Software** no painel de resultados e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e32b7-133">In the search box, type **Rally Software**, select **Rally Software** from result panel then click **Add** button to add the application.</span></span>

    ![Rally Software na lista de resultados](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e32b7-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e32b7-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="e32b7-136">Nesta seção, você configura e testa o logon único do Azure AD com o Rally Software com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="e32b7-136">In this section, you configure and test Azure AD single sign-on with Rally Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e32b7-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Rally Software é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e32b7-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Rally Software is to a user in Azure AD.</span></span> <span data-ttu-id="e32b7-138">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Rally Software.</span><span class="sxs-lookup"><span data-stu-id="e32b7-138">In other words, a link relationship between an Azure AD user and the related user in Rally Software needs to be established.</span></span>

<span data-ttu-id="e32b7-139">No Rally Software, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="e32b7-139">In Rally Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e32b7-140">Para configurar e testar o logon único do Azure AD com o Rally Software, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="e32b7-140">To configure and test Azure AD single sign-on with Rally Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e32b7-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="e32b7-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e32b7-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e32b7-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e32b7-143">**[Criar um usuário de teste do Rally Software](#create-a-rally-software-test-user)** – para ter um equivalente de Brenda Fernandes no Rally Software que esteja vinculado à representação do usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e32b7-143">**[Create a Rally Software test user](#create-a-rally-software-test-user)** - to have a counterpart of Britta Simon in Rally Software that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e32b7-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e32b7-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e32b7-145">**[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="e32b7-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e32b7-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e32b7-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e32b7-147">Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único em seu aplicativo do Rally Software.</span><span class="sxs-lookup"><span data-stu-id="e32b7-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Rally Software application.</span></span>

<span data-ttu-id="e32b7-148">**Para configurar o logon único do Azure AD com o Rally Software, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e32b7-148">**To configure Azure AD single sign-on with Rally Software, perform the following steps:**</span></span>

1. <span data-ttu-id="e32b7-149">No Portal do Azure, na página de integração do aplicativo **Rally Software**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="e32b7-149">In the Azure portal, on the **Rally Software** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="e32b7-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="e32b7-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_samlbase.png)

3. <span data-ttu-id="e32b7-153">Na seção **Domínio e URLs do Rally Software**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e32b7-153">On the **Rally Software Domain and URLs** section, perform the following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do Rally Software](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_url.png)

    <span data-ttu-id="e32b7-155">a.</span><span class="sxs-lookup"><span data-stu-id="e32b7-155">a.</span></span> <span data-ttu-id="e32b7-156">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<tenant-name>.rally.com`</span><span class="sxs-lookup"><span data-stu-id="e32b7-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.rally.com`</span></span>

    <span data-ttu-id="e32b7-157">b.</span><span class="sxs-lookup"><span data-stu-id="e32b7-157">b.</span></span> <span data-ttu-id="e32b7-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<tenant-name>.rally.com`</span><span class="sxs-lookup"><span data-stu-id="e32b7-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant-name>.rally.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e32b7-159">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="e32b7-159">These values are not real.</span></span> <span data-ttu-id="e32b7-160">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="e32b7-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e32b7-161">Entre em contato com a [equipe de suporte ao cliente do Rally Software](https://help.rallydev.com/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="e32b7-161">Contact [Rally Software Client support team](https://help.rallydev.com/) to get these values.</span></span> 
 


4. <span data-ttu-id="e32b7-162">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="e32b7-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_certificate.png) 

5. <span data-ttu-id="e32b7-164">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="e32b7-164">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-rally-software-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e32b7-166">Na seção **Configuração do Rally Software**, clique em **Configurar Rally Software** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="e32b7-166">On the **Rally Software Configuration** section, click **Configure Rally Software** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e32b7-167">Copie a **URL de Saída e a ID da Entidade SAML** da **seção Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="e32b7-167">Copy the **Sign-Out URL, and SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configuração do Rally Software](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_configure.png) 

7. <span data-ttu-id="e32b7-169">Faça logon em seu locatário do **Rally Software** .</span><span class="sxs-lookup"><span data-stu-id="e32b7-169">Log in to your **Rally Software** tenant.</span></span>

8. <span data-ttu-id="e32b7-170">Na barra de ferramentas na parte superior, clique em **Instalação** e selecione **Assinatura**.</span><span class="sxs-lookup"><span data-stu-id="e32b7-170">In the toolbar on the top, click **Setup**, and then select **Subscription**.</span></span>
   
    <span data-ttu-id="e32b7-171">![Assinatura](./media/active-directory-saas-rally-software-tutorial/ic769531.png "Assinatura")</span><span class="sxs-lookup"><span data-stu-id="e32b7-171">![Subscription](./media/active-directory-saas-rally-software-tutorial/ic769531.png "Subscription")</span></span>

9. <span data-ttu-id="e32b7-172">Clique no botão **Ação**.</span><span class="sxs-lookup"><span data-stu-id="e32b7-172">Click the **Action** button.</span></span> <span data-ttu-id="e32b7-173">Selecione **Editar Assinatura** no canto superior direito da barra de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="e32b7-173">Select **Edit Subscription** at the top right side of the toolbar.</span></span>

10. <span data-ttu-id="e32b7-174">Na página de diálogo **Assinatura**, realize as seguintes etapas e clique em **Salvar e Fechar**:</span><span class="sxs-lookup"><span data-stu-id="e32b7-174">On the **Subscription** dialog page, perform the following steps, and then click **Save & Close**:</span></span>
   
    <span data-ttu-id="e32b7-175">![Autenticação](./media/active-directory-saas-rally-software-tutorial/ic769542.png "Autenticação")</span><span class="sxs-lookup"><span data-stu-id="e32b7-175">![Authentication](./media/active-directory-saas-rally-software-tutorial/ic769542.png "Authentication")</span></span>
   
    <span data-ttu-id="e32b7-176">a.</span><span class="sxs-lookup"><span data-stu-id="e32b7-176">a.</span></span> <span data-ttu-id="e32b7-177">Selecione **Autenticação do Rally ou SSO** na lista suspensa Autenticação.</span><span class="sxs-lookup"><span data-stu-id="e32b7-177">Select **Rally or SSO authentication** from Authentication dropdown.</span></span>

    <span data-ttu-id="e32b7-178">b.</span><span class="sxs-lookup"><span data-stu-id="e32b7-178">b.</span></span> <span data-ttu-id="e32b7-179">Na caixa de texto **URL do Provedor de Identidade**, cole o valor da **ID da Entidade SAML** copiado do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e32b7-179">In the **Identity provider URL** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="e32b7-180">c.</span><span class="sxs-lookup"><span data-stu-id="e32b7-180">c.</span></span> <span data-ttu-id="e32b7-181">Na caixa de texto **Logoff do SSO**, cole o valor da **URL de Saída** copiado do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e32b7-181">In the **SSO Logout** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="e32b7-182">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="e32b7-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e32b7-183">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="e32b7-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e32b7-184">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e32b7-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e32b7-185">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e32b7-185">Create an Azure AD test user</span></span>

<span data-ttu-id="e32b7-186">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e32b7-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="e32b7-188">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e32b7-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e32b7-189">No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e32b7-189">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-rally-software-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="e32b7-191">Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="e32b7-191">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-rally-software-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="e32b7-193">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.</span><span class="sxs-lookup"><span data-stu-id="e32b7-193">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![O botão Adicionar](./media/active-directory-saas-rally-software-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="e32b7-195">Na caixa de diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e32b7-195">In the **User** dialog box, perform the following steps:</span></span>

    ![A caixa de diálogo Usuário](./media/active-directory-saas-rally-software-tutorial/create_aaduser_04.png)

    <span data-ttu-id="e32b7-197">a.</span><span class="sxs-lookup"><span data-stu-id="e32b7-197">a.</span></span> <span data-ttu-id="e32b7-198">Na caixa **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="e32b7-198">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e32b7-199">b.</span><span class="sxs-lookup"><span data-stu-id="e32b7-199">b.</span></span> <span data-ttu-id="e32b7-200">Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e32b7-200">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="e32b7-201">c.</span><span class="sxs-lookup"><span data-stu-id="e32b7-201">c.</span></span> <span data-ttu-id="e32b7-202">Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.</span><span class="sxs-lookup"><span data-stu-id="e32b7-202">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="e32b7-203">d.</span><span class="sxs-lookup"><span data-stu-id="e32b7-203">d.</span></span> <span data-ttu-id="e32b7-204">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e32b7-204">Click **Create**.</span></span>
 
### <a name="create-a-rally-software-test-user"></a><span data-ttu-id="e32b7-205">Criar um usuário de teste do Rally Software</span><span class="sxs-lookup"><span data-stu-id="e32b7-205">Create a Rally Software test user</span></span>

<span data-ttu-id="e32b7-206">Para usuários do Azure AD conseguirem entrar, eles devem ser provisionados para o aplicativo Rally Software usando os respectivos nomes de usuário do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e32b7-206">For Azure AD users to be able to sign in, they must be provisioned to the Rally Software application using their Azure Active Directory user names.</span></span>

<span data-ttu-id="e32b7-207">**Para configurar o provisionamento de usuários, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e32b7-207">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="e32b7-208">Faça logon no seu locatário do Rally Software.</span><span class="sxs-lookup"><span data-stu-id="e32b7-208">Log in to your Rally Software tenant.</span></span>

2. <span data-ttu-id="e32b7-209">Vá para **Instalação \> USUÁRIOS** e clique em **+ Adicionar Novo**.</span><span class="sxs-lookup"><span data-stu-id="e32b7-209">Go to **Setup \> USERS**, and then click **+ Add New**.</span></span>
   
    <span data-ttu-id="e32b7-210">![Usuários](./media/active-directory-saas-rally-software-tutorial/ic781039.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="e32b7-210">![Users](./media/active-directory-saas-rally-software-tutorial/ic781039.png "Users")</span></span>

3. <span data-ttu-id="e32b7-211">Digite o nome na caixa de texto Novo Usuário e clique em **Adicionar com Detalhes**.</span><span class="sxs-lookup"><span data-stu-id="e32b7-211">Type the name in the New User textbox, and then click **Add with Details**.</span></span>

4. <span data-ttu-id="e32b7-212">Na seção **Criar Usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e32b7-212">In the **Create User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="e32b7-213">![Criar usuário](./media/active-directory-saas-rally-software-tutorial/ic781040.png "Criar usuário")</span><span class="sxs-lookup"><span data-stu-id="e32b7-213">![Create User](./media/active-directory-saas-rally-software-tutorial/ic781040.png "Create User")</span></span>

    <span data-ttu-id="e32b7-214">a.</span><span class="sxs-lookup"><span data-stu-id="e32b7-214">a.</span></span> <span data-ttu-id="e32b7-215">Na caixa de texto **Nome de Usuário**, digite o nome de usuário como **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="e32b7-215">In the **User Name** textbox, type the name of user like **Brittsimon**.</span></span>
   
    <span data-ttu-id="e32b7-216">b.</span><span class="sxs-lookup"><span data-stu-id="e32b7-216">b.</span></span> <span data-ttu-id="e32b7-217">Na caixa de texto **Endereço de Email**, insira o email do usuário como **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="e32b7-217">In **E-mail Address** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="e32b7-218">c.</span><span class="sxs-lookup"><span data-stu-id="e32b7-218">c.</span></span> <span data-ttu-id="e32b7-219">Na caixa de texto **Nome**, insira o nome do usuário como **Brenda**.</span><span class="sxs-lookup"><span data-stu-id="e32b7-219">In **First Name** text box, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="e32b7-220">d.</span><span class="sxs-lookup"><span data-stu-id="e32b7-220">d.</span></span> <span data-ttu-id="e32b7-221">Na caixa de texto **Sobrenome**, insira o nome do usuário como **Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="e32b7-221">In **Last Name** text box, enter the last name of user like **Simon**.</span></span>

    <span data-ttu-id="e32b7-222">e.</span><span class="sxs-lookup"><span data-stu-id="e32b7-222">e.</span></span> <span data-ttu-id="e32b7-223">Clique em **Salvar e Fechar**.</span><span class="sxs-lookup"><span data-stu-id="e32b7-223">Click **Save & Close**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="e32b7-224">É possível usar qualquer outra ferramenta de criação da conta de usuário do Rally Software ou as APIs fornecidas pelo Rally Software para provisionar as contas de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e32b7-224">You can use any other Rally Software user account creation tools or APIs provided by Rally Software to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="e32b7-225">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e32b7-225">Assign the Azure AD test user</span></span>

<span data-ttu-id="e32b7-226">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo a ela acesso ao Rally Software.</span><span class="sxs-lookup"><span data-stu-id="e32b7-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Rally Software.</span></span>

![Atribuir a função de usuário][200] 

<span data-ttu-id="e32b7-228">**Para atribuir Brenda Fernandes ao Rally Software, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e32b7-228">**To assign Britta Simon to Rally Software, perform the following steps:**</span></span>

1. <span data-ttu-id="e32b7-229">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e32b7-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="e32b7-231">Na lista de aplicativos, selecione **Rally Software**.</span><span class="sxs-lookup"><span data-stu-id="e32b7-231">In the applications list, select **Rally Software**.</span></span>

    ![O link do Rally Software na lista de Aplicativos](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_app.png)  

3. <span data-ttu-id="e32b7-233">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="e32b7-233">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202]

4. <span data-ttu-id="e32b7-235">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e32b7-235">Click **Add** button.</span></span> <span data-ttu-id="e32b7-236">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e32b7-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="e32b7-238">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="e32b7-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e32b7-239">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e32b7-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e32b7-240">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e32b7-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e32b7-241">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="e32b7-241">Test single sign-on</span></span>

<span data-ttu-id="e32b7-242">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="e32b7-242">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e32b7-243">Ao clicar no bloco Rally Software no Painel de Acesso, você deve fazer logon automaticamente no seu aplicativo Rally Software.</span><span class="sxs-lookup"><span data-stu-id="e32b7-243">When you click the Rally Software tile in the Access Panel, you should get automatically signed-on to your Rally Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e32b7-244">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="e32b7-244">Additional resources</span></span>

* [<span data-ttu-id="e32b7-245">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="e32b7-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e32b7-246">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e32b7-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_203.png

