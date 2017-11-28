---
title: "Tutorial: integração do Azure Active Directory com o PagerDuty | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o PagerDuty."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0410456a-76f7-42a7-9bb5-f767de75a0e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: bf5263ce4d8fbc231029c101f167f4b55a921e60
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pagerduty"></a><span data-ttu-id="2b843-103">Tutorial: integração do Azure Active Directory com o PagerDuty</span><span class="sxs-lookup"><span data-stu-id="2b843-103">Tutorial: Azure Active Directory integration with PagerDuty</span></span>

<span data-ttu-id="2b843-104">Neste tutorial, você aprenderá a integrar o PagerDuty ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="2b843-104">In this tutorial, you learn how to integrate PagerDuty with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2b843-105">A integração do PagerDuty ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="2b843-105">Integrating PagerDuty with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2b843-106">No Azure AD, é possível controlar quem tem acesso ao PagerDuty</span><span class="sxs-lookup"><span data-stu-id="2b843-106">You can control in Azure AD who has access to PagerDuty</span></span>
- <span data-ttu-id="2b843-107">Você pode permitir que os usuários façam logon automaticamente no PagerDuty (logon único) com as respectivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b843-107">You can enable your users to automatically get signed-on to PagerDuty (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2b843-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2b843-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2b843-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2b843-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b843-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2b843-110">Prerequisites</span></span>

<span data-ttu-id="2b843-111">Para configurar a integração do Azure AD ao PagerDuty, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="2b843-111">To configure Azure AD integration with PagerDuty, you need the following items:</span></span>

- <span data-ttu-id="2b843-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2b843-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2b843-113">Uma assinatura do PagerDuty habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="2b843-113">A PagerDuty single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2b843-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="2b843-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2b843-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="2b843-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2b843-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="2b843-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2b843-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2b843-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2b843-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="2b843-118">Scenario description</span></span>
<span data-ttu-id="2b843-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="2b843-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2b843-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="2b843-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2b843-121">Adicionar o PagerDuty da galeria</span><span class="sxs-lookup"><span data-stu-id="2b843-121">Adding PagerDuty from the gallery</span></span>
2. <span data-ttu-id="2b843-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2b843-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pagerduty-from-the-gallery"></a><span data-ttu-id="2b843-123">Adicionar o PagerDuty da galeria</span><span class="sxs-lookup"><span data-stu-id="2b843-123">Adding PagerDuty from the gallery</span></span>
<span data-ttu-id="2b843-124">Para configurar a integração do PagerDuty ao Azure AD, você precisa adicionar o PagerDuty da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="2b843-124">To configure the integration of PagerDuty into Azure AD, you need to add PagerDuty from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2b843-125">**Para adicionar o PagerDuty da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="2b843-125">**To add PagerDuty from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2b843-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2b843-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="2b843-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="2b843-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2b843-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="2b843-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="2b843-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2b843-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="2b843-133">Na caixa de pesquisa, digite **PagerDuty**, selecione **PagerDuty** no painel de resultados e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2b843-133">In the search box, type **PagerDuty**, select  **PagerDuty**  from result panel then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="2b843-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b843-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="2b843-136">Nesta seção, você configurará e testará o logon único do Azure AD com o PagerDuty, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="2b843-136">In this section, you configure and test Azure AD single sign-on with PagerDuty based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2b843-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do PagerDuty é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2b843-137">For single sign-on to work, Azure AD needs to know what the counterpart user in PagerDuty is to a user in Azure AD.</span></span> <span data-ttu-id="2b843-138">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="2b843-138">In other words, a link relationship between an Azure AD user and the related user in PagerDuty needs to be established.</span></span>

<span data-ttu-id="2b843-139">No PagerDuty, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="2b843-139">In PagerDuty, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2b843-140">Para configurar e testar o logon único do Azure AD com o PagerDuty, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="2b843-140">To configure and test Azure AD single sign-on with PagerDuty, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2b843-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="2b843-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2b843-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="2b843-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2b843-143">**[Criar um usuário de teste do PagerDuty](#create-a-pagerduty-test-user)** – para ter um equivalente de Brenda Fernandes no PagerDuty que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2b843-143">**[Create a PagerDuty test user](#create-a-pagerduty-test-user)** - to have a counterpart of Britta Simon in PagerDuty that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2b843-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2b843-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2b843-145">**[Testar o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="2b843-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="2b843-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b843-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="2b843-147">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="2b843-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PagerDuty application.</span></span>

<span data-ttu-id="2b843-148">**Para configurar o logon único do Azure AD com o PagerDuty, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="2b843-148">**To configure Azure AD single sign-on with PagerDuty, perform the following steps:**</span></span>

1. <span data-ttu-id="2b843-149">No Portal do Azure, na página de integração de aplicativos do **PagerDuty**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="2b843-149">In the Azure portal, on the **PagerDuty** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="2b843-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="2b843-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_samlbase.png)

3. <span data-ttu-id="2b843-153">Na seção **Domínio e URLs do PagerDuty**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="2b843-153">On the **PagerDuty Domain and URLs** section, perform the following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do PagerDuty](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_url.png)

    <span data-ttu-id="2b843-155">a.</span><span class="sxs-lookup"><span data-stu-id="2b843-155">a.</span></span> <span data-ttu-id="2b843-156">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<tenant-name>.pagerduty.com`</span><span class="sxs-lookup"><span data-stu-id="2b843-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.pagerduty.com`</span></span>

    <span data-ttu-id="2b843-157">b.</span><span class="sxs-lookup"><span data-stu-id="2b843-157">b.</span></span> <span data-ttu-id="2b843-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<tenant-name>.pagerduty.com`</span><span class="sxs-lookup"><span data-stu-id="2b843-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant-name>.pagerduty.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2b843-159">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="2b843-159">These values are not real.</span></span> <span data-ttu-id="2b843-160">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="2b843-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="2b843-161">Contate a [equipe de suporte ao cliente do PagerDuty](https://www.pagerduty.com/support/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="2b843-161">Contact [PagerDuty Client support team](https://www.pagerduty.com/support/) to get these values.</span></span> 

4. <span data-ttu-id="2b843-162">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="2b843-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_certificate.png) 

5. <span data-ttu-id="2b843-164">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="2b843-164">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-pagerduty-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2b843-166">Na seção **Configuração do PagerDuty**, clique em **Configurar o PagerDuty** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="2b843-166">On the **PagerDuty Configuration** section, click **Configure PagerDuty** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2b843-167">Copie a **URL do serviço de logon único do SAML e a URL de logoff** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="2b843-167">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuração do PagerDuty](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_configure.png) 

7. <span data-ttu-id="2b843-169">Em outra janela do navegador da Web, faça logon em seu site de empresa do Pagerduty como administrador.</span><span class="sxs-lookup"><span data-stu-id="2b843-169">In a different web browser window, log into your Pagerduty company site as an administrator.</span></span>

8. <span data-ttu-id="2b843-170">No menu na parte superior, clique em **Configurações de Conta**.</span><span class="sxs-lookup"><span data-stu-id="2b843-170">In the menu on the top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="2b843-171">![Configurações de Conta](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "Configurações de Conta")</span><span class="sxs-lookup"><span data-stu-id="2b843-171">![Account Settings](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "Account Settings")</span></span>

9. <span data-ttu-id="2b843-172">Clique em **Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="2b843-172">Click **Single Sign-on**.</span></span>
   
    <span data-ttu-id="2b843-173">![Logon Único](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "Logon Único")</span><span class="sxs-lookup"><span data-stu-id="2b843-173">![Single sign-on](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "Single sign-on")</span></span>

10. <span data-ttu-id="2b843-174">Na página **Habilitar Logon Único (SSO)**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="2b843-174">On the **Enable Single Sign-on (SSO)** page, perform the following steps:</span></span>
   
    <span data-ttu-id="2b843-175">![Habilitar logon único](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "Habilitar logon único")</span><span class="sxs-lookup"><span data-stu-id="2b843-175">![Enable single sign-on](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "Enable single sign-on")</span></span>
   
    <span data-ttu-id="2b843-176">a.</span><span class="sxs-lookup"><span data-stu-id="2b843-176">a.</span></span> <span data-ttu-id="2b843-177">Abra o certificado codificado em Base 64 baixado no Portal do Azure no bloco de notas, copie o conteúdo dele para a área de transferência e, depois, cole-o na caixa de texto **Certificado X.509**</span><span class="sxs-lookup"><span data-stu-id="2b843-177">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox</span></span>
  
    <span data-ttu-id="2b843-178">b.</span><span class="sxs-lookup"><span data-stu-id="2b843-178">b.</span></span> <span data-ttu-id="2b843-179">Na caixa de texto **URL de Logon**, cole a **URL do Serviço de Logon Único SAML** copiada do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2b843-179">In the **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="2b843-180">c.</span><span class="sxs-lookup"><span data-stu-id="2b843-180">c.</span></span> <span data-ttu-id="2b843-181">Na caixa de texto **URL de Logoff**, cole a **URL de Saída** copiada do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2b843-181">In the **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="2b843-182">d.</span><span class="sxs-lookup"><span data-stu-id="2b843-182">d.</span></span> <span data-ttu-id="2b843-183">Selecione **Ativar Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="2b843-183">Select **Turn on Single Sign-on**.</span></span>
 
    <span data-ttu-id="2b843-184">e.</span><span class="sxs-lookup"><span data-stu-id="2b843-184">e.</span></span> <span data-ttu-id="2b843-185">Clique em **Salvar Alterações**.</span><span class="sxs-lookup"><span data-stu-id="2b843-185">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="2b843-186">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="2b843-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2b843-187">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="2b843-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2b843-188">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2b843-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2b843-189">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b843-189">Create an Azure AD test user</span></span>

<span data-ttu-id="2b843-190">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="2b843-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="2b843-192">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="2b843-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2b843-193">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2b843-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2b843-195">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="2b843-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2b843-197">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2b843-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![O botão Adicionar](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2b843-199">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="2b843-199">On the **User** dialog page, perform the following steps:</span></span>
 
    ![A caixa de diálogo Usuário](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2b843-201">a.</span><span class="sxs-lookup"><span data-stu-id="2b843-201">a.</span></span> <span data-ttu-id="2b843-202">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="2b843-202">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2b843-203">b.</span><span class="sxs-lookup"><span data-stu-id="2b843-203">b.</span></span> <span data-ttu-id="2b843-204">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="2b843-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2b843-205">c.</span><span class="sxs-lookup"><span data-stu-id="2b843-205">c.</span></span> <span data-ttu-id="2b843-206">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="2b843-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2b843-207">d.</span><span class="sxs-lookup"><span data-stu-id="2b843-207">d.</span></span> <span data-ttu-id="2b843-208">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="2b843-208">Click **Create**.</span></span>
 
### <a name="create-a-pagerduty-test-user"></a><span data-ttu-id="2b843-209">Criar um usuário de teste do PagerDuty</span><span class="sxs-lookup"><span data-stu-id="2b843-209">Create a PagerDuty test user</span></span>

<span data-ttu-id="2b843-210">Para permitir que os usuários do Azure AD façam logon no PagerDuty, eles devem ser provisionados no PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="2b843-210">To enable Azure AD users to log in to PagerDuty, they must be provisioned into PagerDuty.</span></span>  
<span data-ttu-id="2b843-211">No caso do PagerDuty, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="2b843-211">In the case of PagerDuty, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="2b843-212">É possível usar qualquer outra ferramenta de criação da conta de usuário do PagerDuty ou as APIs fornecidas pelo PagerDuty para provisionar as contas de usuário do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2b843-212">You can use any other Pagerduty user account creation tools or APIs provided by Pagerduty to provision Azure Active Directory user accounts.</span></span>

<span data-ttu-id="2b843-213">**Para provisionar uma conta de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="2b843-213">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="2b843-214">Faça logon em seu locatário do **Pagerduty** .</span><span class="sxs-lookup"><span data-stu-id="2b843-214">Log in to your **Pagerduty** tenant.</span></span>

2. <span data-ttu-id="2b843-215">No menu na parte superior, clique em **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="2b843-215">In the menu on the top, click **Users**.</span></span>

3. <span data-ttu-id="2b843-216">Clique em **Adicionar Usuários**.</span><span class="sxs-lookup"><span data-stu-id="2b843-216">Click **Add Users**.</span></span>
   
    <span data-ttu-id="2b843-217">![Adicionar Usuários](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "Adicionar Usuários")</span><span class="sxs-lookup"><span data-stu-id="2b843-217">![Add Users](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "Add Users")</span></span>

4.  <span data-ttu-id="2b843-218">No diálogo **Convidar sua equipe**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="2b843-218">On the **Invite your team** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="2b843-219">![Convidar suas equipe](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "Convidar suas equipe")</span><span class="sxs-lookup"><span data-stu-id="2b843-219">![Invite your team](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "Invite your team")</span></span>

    <span data-ttu-id="2b843-220">a.</span><span class="sxs-lookup"><span data-stu-id="2b843-220">a.</span></span> <span data-ttu-id="2b843-221">Digite o **Nome e Sobrenome** do usuário, por exemplo, **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="2b843-221">Type the **First and Last Name** of user like **Britta Simon**.</span></span> 
   
    <span data-ttu-id="2b843-222">b.</span><span class="sxs-lookup"><span data-stu-id="2b843-222">b.</span></span> <span data-ttu-id="2b843-223">Digite o endereço de **Email** do usuário, por exemplo, **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="2b843-223">Enter **Email** address of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="2b843-224">c.</span><span class="sxs-lookup"><span data-stu-id="2b843-224">c.</span></span> <span data-ttu-id="2b843-225">Clique em **Adicionar** e depois em **Enviar Convites**.</span><span class="sxs-lookup"><span data-stu-id="2b843-225">Click **Add**, and then click **Send Invites**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="2b843-226">Todos os usuários adicionados receberão um convite para criar uma conta do PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="2b843-226">All added users will receive an invite to create a PagerDuty account.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="2b843-227">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b843-227">Assign the Azure AD test user</span></span>

<span data-ttu-id="2b843-228">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="2b843-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PagerDuty.</span></span>

![Atribuir a função de usuário][200]

<span data-ttu-id="2b843-230">**Para atribuir Brenda Fernandes ao PagerDuty, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="2b843-230">**To assign Britta Simon to PagerDuty, perform the following steps:**</span></span>

1. <span data-ttu-id="2b843-231">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="2b843-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="2b843-233">Na lista de aplicativos, selecione **PagerDuty**.</span><span class="sxs-lookup"><span data-stu-id="2b843-233">In the applications list, select **PagerDuty**.</span></span>

    ![O link do PagerDuty na lista de Aplicativos](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_app.png) 

3. <span data-ttu-id="2b843-235">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="2b843-235">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202]

4. <span data-ttu-id="2b843-237">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="2b843-237">Click **Add** button.</span></span> <span data-ttu-id="2b843-238">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2b843-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="2b843-240">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="2b843-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2b843-241">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2b843-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2b843-242">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2b843-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="2b843-243">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="2b843-243">Test single sign-on</span></span>

<span data-ttu-id="2b843-244">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="2b843-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2b843-245">Ao clicar no bloco PagerDuty no Painel de Acesso, você deverá ser automaticamente conectado ao aplicativo PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="2b843-245">When you click the PagerDuty tile in the Access Panelyou should get automatically signed-on to your PagerDuty application.</span></span>

<span data-ttu-id="2b843-246">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2b843-246">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2b843-247">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="2b843-247">Additional resources</span></span>

* [<span data-ttu-id="2b843-248">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="2b843-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2b843-249">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2b843-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_203.png

