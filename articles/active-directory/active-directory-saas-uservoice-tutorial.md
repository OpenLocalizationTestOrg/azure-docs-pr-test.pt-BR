---
title: "Tutorial: Integração do Azure Active Directory com o UserVoice | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o UserVoice."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 684a405b-8932-46f6-b43a-4d97a42b6b87
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: fcfda1c2ecb162fb93b70574a18bd745b72ee4db
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-uservoice"></a><span data-ttu-id="0d2f0-103">Tutorial: Integração do Azure Active Directory com o UserVoice</span><span class="sxs-lookup"><span data-stu-id="0d2f0-103">Tutorial: Azure Active Directory integration with UserVoice</span></span>

<span data-ttu-id="0d2f0-104">Neste tutorial, você aprenderá a integrar o UserVoice ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="0d2f0-104">In this tutorial, you learn how to integrate UserVoice with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0d2f0-105">A integração do UserVoice ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="0d2f0-105">Integrating UserVoice with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0d2f0-106">No AD do Azure, é possível controlar quem tem acesso ao UserVoice.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-106">You can control in Azure AD who has access to UserVoice.</span></span>
- <span data-ttu-id="0d2f0-107">Você pode permitir que seus usuários façam logon automaticamente no UserVoice (logon único) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-107">You can enable your users to automatically get signed-on to UserVoice (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="0d2f0-108">Você pode gerenciar suas contas em um único local central – o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="0d2f0-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0d2f0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0d2f0-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0d2f0-110">Prerequisites</span></span>

<span data-ttu-id="0d2f0-111">Para configurar a integração do Azure AD ao UserVoice, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="0d2f0-111">To configure Azure AD integration with UserVoice, you need the following items:</span></span>

- <span data-ttu-id="0d2f0-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0d2f0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0d2f0-113">Uma assinatura do UserVoice com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="0d2f0-113">A UserVoice single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0d2f0-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0d2f0-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="0d2f0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0d2f0-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0d2f0-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0d2f0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0d2f0-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="0d2f0-118">Scenario description</span></span>
<span data-ttu-id="0d2f0-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0d2f0-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="0d2f0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0d2f0-121">Adicionar UserVoice pela galeria</span><span class="sxs-lookup"><span data-stu-id="0d2f0-121">Adding UserVoice from the gallery</span></span>
2. <span data-ttu-id="0d2f0-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0d2f0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-uservoice-from-the-gallery"></a><span data-ttu-id="0d2f0-123">Adicionar UserVoice pela galeria</span><span class="sxs-lookup"><span data-stu-id="0d2f0-123">Adding UserVoice from the gallery</span></span>
<span data-ttu-id="0d2f0-124">Para configurar a integração do UserVoice com o Azure AD, você precisará adicionar o UserVoice à sua lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-124">To configure the integration of UserVoice into Azure AD, you need to add UserVoice from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0d2f0-125">**Para adicionar o UserVoice pela galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="0d2f0-125">**To add UserVoice from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0d2f0-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="0d2f0-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0d2f0-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="0d2f0-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="0d2f0-133">Na caixa de pesquisa, digite **UserVoice**, selecione **UserVoice** no painel de resultados e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-133">In the search box, type **UserVoice**, select **UserVoice** from result panel then click **Add** button to add the application.</span></span>

    ![UserVoice na lista de resultados](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0d2f0-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d2f0-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="0d2f0-136">Nesta seção, você configurará e testará o logon único do Azure AD com o UserVoice, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-136">In this section, you configure and test Azure AD single sign-on with UserVoice based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0d2f0-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do UserVoice é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-137">For single sign-on to work, Azure AD needs to know what the counterpart user in UserVoice is to a user in Azure AD.</span></span> <span data-ttu-id="0d2f0-138">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do AD do Azure e o usuário relacionado no UserVoice.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-138">In other words, a link relationship between an Azure AD user and the related user in UserVoice needs to be established.</span></span>

<span data-ttu-id="0d2f0-139">No UserVoice, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-139">In UserVoice, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0d2f0-140">Para configurar e testar o logon único do AD do Azure com o UserVoice, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="0d2f0-140">To configure and test Azure AD single sign-on with UserVoice, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0d2f0-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0d2f0-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0d2f0-143">**[Criar um usuário de teste do UserVoice](#create-a-uservoice-test-user)** – para ter um equivalente de Brenda Fernandes no UserVoice que esteja vinculado à representação de usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-143">**[Create a UserVoice test user](#create-a-uservoice-test-user)** - to have a counterpart of Britta Simon in UserVoice that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0d2f0-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0d2f0-145">**[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="0d2f0-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d2f0-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="0d2f0-147">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo UserVoice.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your UserVoice application.</span></span>

<span data-ttu-id="0d2f0-148">**Para configurar o logon único do Azure AD com o UserVoice, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="0d2f0-148">**To configure Azure AD single sign-on with UserVoice, perform the following steps:**</span></span>

1. <span data-ttu-id="0d2f0-149">No portal do Azure, na página de integração do aplicativo **UserVoice**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-149">In the Azure portal, on the **UserVoice** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="0d2f0-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_samlbase.png)

3. <span data-ttu-id="0d2f0-153">Na seção **URLs e Domínio do UserVoice**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="0d2f0-153">On the **UserVoice Domain and URLs** section, perform the following steps:</span></span>

    ![Informações de logon único de URLs e Domínio do UserVoice](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_url.png)

    <span data-ttu-id="0d2f0-155">a.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-155">a.</span></span> <span data-ttu-id="0d2f0-156">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<tenantname>.UserVoice.com`</span><span class="sxs-lookup"><span data-stu-id="0d2f0-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.UserVoice.com`</span></span>

    <span data-ttu-id="0d2f0-157">b.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-157">b.</span></span> <span data-ttu-id="0d2f0-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<tenantname>.UserVoice.com`</span><span class="sxs-lookup"><span data-stu-id="0d2f0-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.UserVoice.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0d2f0-159">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-159">These values are not real.</span></span> <span data-ttu-id="0d2f0-160">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0d2f0-161">Entre em contato com a [equipe de suporte do cliente do UserVoice](https://www.uservoice.com/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-161">Contact [UserVoice Client support team](https://www.uservoice.com/) to get these values.</span></span>

4. <span data-ttu-id="0d2f0-162">Na seção **Certificado de Autenticação SAML**, copie o valor da **IMPRESSÃO DIGITAL** do certificado.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-162">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_certificate.png) 

5. <span data-ttu-id="0d2f0-164">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="0d2f0-164">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-uservoice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0d2f0-166">Na seção **Configuração do UserVoice**, clique em **Configurar UserVoice** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-166">On the **UserVoice Configuration** section, click **Configure UserVoice** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0d2f0-167">Copie a **URL de Saída e a URL do Serviço de Logon Único SAML** da **seção Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="0d2f0-167">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuração do UserVoice](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_configure.png) 

7. <span data-ttu-id="0d2f0-169">Em uma janela diferente do navegador da Web, faça logon no site corporativo do UserVoice como administrador.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-169">In a different web browser window, log in to your UserVoice company site as an administrator.</span></span>

8. <span data-ttu-id="0d2f0-170">Na barra de ferramentas na parte superior, clique em **Configurações** e, em seguida, selecione o **portal da Web** no menu.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-170">In the toolbar on the top, click **Settings**, and then select **Web portal** from the menu.</span></span>
   
    <span data-ttu-id="0d2f0-171">![Seção Configurações no lado do aplicativo](./media/active-directory-saas-uservoice-tutorial/ic777519.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="0d2f0-171">![Settings Section On App Side](./media/active-directory-saas-uservoice-tutorial/ic777519.png "Settings")</span></span>

9. <span data-ttu-id="0d2f0-172">Na guia **Portal da Web**, na seção **Autenticação de usuário**, clique em **Editar** para abrir a página do diálogo **Editar Autenticação de Usuário**.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-172">On the **Web portal** tab, in the **User authentication** section, click **Edit** to open the **Edit User Authentication** dialog page.</span></span>
   
    <span data-ttu-id="0d2f0-173">![Guia Portal da Web](./media/active-directory-saas-uservoice-tutorial/ic777520.png "Portal da Web")</span><span class="sxs-lookup"><span data-stu-id="0d2f0-173">![Web portal Tab](./media/active-directory-saas-uservoice-tutorial/ic777520.png "Web portal")</span></span>

10. <span data-ttu-id="0d2f0-174">Na página do diálogo **Editar Autenticação de Usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="0d2f0-174">On the **Edit User Authentication** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="0d2f0-175">![Editar autenticação de usuário](./media/active-directory-saas-uservoice-tutorial/ic777521.png "Editar autenticação de usuário")</span><span class="sxs-lookup"><span data-stu-id="0d2f0-175">![Edit user authentication](./media/active-directory-saas-uservoice-tutorial/ic777521.png "Edit user authentication")</span></span>
   
    <span data-ttu-id="0d2f0-176">a.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-176">a.</span></span> <span data-ttu-id="0d2f0-177">Clique em **SSO (Logon Único)**.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-177">Click **Single Sign-On (SSO)**.</span></span>
 
    <span data-ttu-id="0d2f0-178">b.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-178">b.</span></span> <span data-ttu-id="0d2f0-179">Cole o valor da **URL do Serviço de Logon Único SAML** copiado do portal do Azure na caixa de texto **Entrada remota de SSO**.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-179">Paste the **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **SSO Remote Sign-In** textbox.</span></span>

    <span data-ttu-id="0d2f0-180">c.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-180">c.</span></span> <span data-ttu-id="0d2f0-181">Cole o valor da **URL de Saída** copiado do portal do Azure na caixa de texto **Entrada remota de SSO**.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-181">Paste the **Sign-Out URL** value, which you have copied from the Azure portal into the **SSO Remote Sign-Out textbox**.</span></span>
 
    <span data-ttu-id="0d2f0-182">d.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-182">d.</span></span> <span data-ttu-id="0d2f0-183">Cole o valor da **Impressão digital** copiado do portal do Azure na caixa de texto **Impressão digital de certificado SHA1 atual**.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-183">Paste the **Thumbprint** value , which you have copied from Azure portal  into the **Current certificate SHA1 fingerprint** textbox.</span></span>
    
    <span data-ttu-id="0d2f0-184">e.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-184">e.</span></span> <span data-ttu-id="0d2f0-185">Clique em **Salvar Configurações de Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-185">Click **Save authentication settings**.</span></span>

> [!TIP]
> <span data-ttu-id="0d2f0-186">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="0d2f0-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0d2f0-187">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0d2f0-188">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0d2f0-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0d2f0-189">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d2f0-189">Create an Azure AD test user</span></span>

<span data-ttu-id="0d2f0-190">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="0d2f0-192">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="0d2f0-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0d2f0-193">No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-193">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-uservoice-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="0d2f0-195">Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-195">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-uservoice-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="0d2f0-197">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-197">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![O botão Adicionar](./media/active-directory-saas-uservoice-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="0d2f0-199">Na caixa de diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="0d2f0-199">In the **User** dialog box, perform the following steps:</span></span>

    ![A caixa de diálogo Usuário](./media/active-directory-saas-uservoice-tutorial/create_aaduser_04.png)

    <span data-ttu-id="0d2f0-201">a.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-201">a.</span></span> <span data-ttu-id="0d2f0-202">Na caixa **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-202">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0d2f0-203">b.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-203">b.</span></span> <span data-ttu-id="0d2f0-204">Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-204">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="0d2f0-205">c.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-205">c.</span></span> <span data-ttu-id="0d2f0-206">Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-206">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="0d2f0-207">d.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-207">d.</span></span> <span data-ttu-id="0d2f0-208">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-208">Click **Create**.</span></span>
 
### <a name="create-a-uservoice-test-user"></a><span data-ttu-id="0d2f0-209">Criar um usuário de teste do UserVoice</span><span class="sxs-lookup"><span data-stu-id="0d2f0-209">Create a UserVoice test user</span></span>

<span data-ttu-id="0d2f0-210">Para permitir que os usuários do Azure AD façam logon no UserVoice, eles devem ser provisionados no UserVoice.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-210">To enable Azure AD users to log in to UserVoice, they must be provisioned into UserVoice.</span></span> <span data-ttu-id="0d2f0-211">No caso do UserVoice, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-211">In the case of UserVoice, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="0d2f0-212">Para provisionar uma conta de usuário, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="0d2f0-212">To provision a user account, perform the following steps:</span></span>
1. <span data-ttu-id="0d2f0-213">Faça logon no seu locatário **UserVoice** .</span><span class="sxs-lookup"><span data-stu-id="0d2f0-213">Log in to your **UserVoice** tenant.</span></span>

2. <span data-ttu-id="0d2f0-214">Vá para **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-214">Go to **Settings**.</span></span>
   
    <span data-ttu-id="0d2f0-215">![Configurações](./media/active-directory-saas-uservoice-tutorial/ic777811.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="0d2f0-215">![Settings](./media/active-directory-saas-uservoice-tutorial/ic777811.png "Settings")</span></span>

3. <span data-ttu-id="0d2f0-216">Clique em **Geral**.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-216">Click **General**.</span></span>

4. <span data-ttu-id="0d2f0-217">Clique em **Agentes e permissões**.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-217">Click **Agents and permissions**.</span></span>
   
    <span data-ttu-id="0d2f0-218">![Agentes e permissões](./media/active-directory-saas-uservoice-tutorial/ic777812.png "Agentes e permissões")</span><span class="sxs-lookup"><span data-stu-id="0d2f0-218">![Agents and permissions](./media/active-directory-saas-uservoice-tutorial/ic777812.png "Agents and permissions")</span></span>

5. <span data-ttu-id="0d2f0-219">Clique em **Adicionar administradores**.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-219">Click **Add admins**.</span></span>
   
    <span data-ttu-id="0d2f0-220">![Adicionar administradores](./media/active-directory-saas-uservoice-tutorial/ic777813.png "Adicionar administradores")</span><span class="sxs-lookup"><span data-stu-id="0d2f0-220">![Add admins](./media/active-directory-saas-uservoice-tutorial/ic777813.png "Add admins")</span></span>

6. <span data-ttu-id="0d2f0-221">No diálogo **Convidar administradores** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="0d2f0-221">On the **Invite admins** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="0d2f0-222">![Convidar administradores](./media/active-directory-saas-uservoice-tutorial/ic777814.png "Convidar administradores")</span><span class="sxs-lookup"><span data-stu-id="0d2f0-222">![Invite admins](./media/active-directory-saas-uservoice-tutorial/ic777814.png "Invite admins")</span></span>
   
    <span data-ttu-id="0d2f0-223">a.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-223">a.</span></span> <span data-ttu-id="0d2f0-224">Na caixa de texto Emails, digite o endereço de email da conta que você deseja provisionar e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-224">In the Emails textbox, type the email address of the account you want to provision, and then click **Add**.</span></span>
   
    <span data-ttu-id="0d2f0-225">b.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-225">b.</span></span> <span data-ttu-id="0d2f0-226">Clique em **Convidar**.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-226">Click **Invite**.</span></span>

> [!NOTE]
> <span data-ttu-id="0d2f0-227">Você pode usar qualquer outra ferramenta de criação de conta de usuário do UserVoice ou APIs fornecidas pelo UserVoice para provisionar contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-227">You can use any other UserVoice user account creation tools or APIs provided by UserVoice to provision AAD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="0d2f0-228">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d2f0-228">Assign the Azure AD test user</span></span>

<span data-ttu-id="0d2f0-229">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo acesso ao UserVoice.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to UserVoice.</span></span>

![Atribuir a função de usuário][200] 

<span data-ttu-id="0d2f0-231">**Para atribuir Brenda Fernandes ao UserVoice, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="0d2f0-231">**To assign Britta Simon to UserVoice, perform the following steps:**</span></span>

1. <span data-ttu-id="0d2f0-232">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="0d2f0-234">Na lista de aplicativos, selecione **UserVoice**.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-234">In the applications list, select **UserVoice**.</span></span>

    ![O link do UserVoice na lista de Aplicativos](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_app.png)  

3. <span data-ttu-id="0d2f0-236">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-236">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202]

4. <span data-ttu-id="0d2f0-238">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-238">Click **Add** button.</span></span> <span data-ttu-id="0d2f0-239">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="0d2f0-241">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0d2f0-242">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0d2f0-243">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="0d2f0-244">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="0d2f0-244">Test single sign-on</span></span>

<span data-ttu-id="0d2f0-245">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0d2f0-246">Quando você clicar no bloco UserVoice no Painel de Acesso, deverá ser conectado automaticamente ao seu aplicativo UserVoice.</span><span class="sxs-lookup"><span data-stu-id="0d2f0-246">When you click the UserVoice tile in the Access Panel, you should get automatically signed-on to your UserVoice application.</span></span>
<span data-ttu-id="0d2f0-247">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0d2f0-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0d2f0-248">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="0d2f0-248">Additional resources</span></span>

* [<span data-ttu-id="0d2f0-249">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="0d2f0-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0d2f0-250">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0d2f0-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_203.png

