---
title: "Tutorial: Integração do Azure Active Directory com o Workplace by Facebook| Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o local de trabalho pelo Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f71a59527394730757d501a973251dc293fd3683
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="47d1f-103">Tutorial: Integração do Azure Active Directory com o Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="47d1f-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>

<span data-ttu-id="47d1f-104">Neste tutorial, você aprenderá como toointegrate no local de trabalho pelo Facebook com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="47d1f-104">In this tutorial, you learn how toointegrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="47d1f-105">Integração do local de trabalho pelo Facebook com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="47d1f-105">Integrating Workplace by Facebook with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="47d1f-106">Você pode controlar no AD do Azure que tenha acesso tooWorkplace pelo Facebook</span><span class="sxs-lookup"><span data-stu-id="47d1f-106">You can control in Azure AD who has access tooWorkplace by Facebook</span></span>
- <span data-ttu-id="47d1f-107">Você pode habilitar seu usuários tooautomatically get conectado tooWorkplace pelo Facebook (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="47d1f-107">You can enable your users tooautomatically get signed-on tooWorkplace by Facebook (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="47d1f-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="47d1f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="47d1f-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="47d1f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47d1f-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="47d1f-110">Prerequisites</span></span>

<span data-ttu-id="47d1f-111">tooconfigure integração do AD do Azure com o local de trabalho pelo Facebook, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="47d1f-111">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following items:</span></span>

- <span data-ttu-id="47d1f-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="47d1f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="47d1f-113">Uma assinatura do Workplace by Facebook habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="47d1f-113">A Workplace by Facebook single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="47d1f-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="47d1f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="47d1f-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="47d1f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="47d1f-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="47d1f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="47d1f-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="47d1f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="47d1f-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="47d1f-118">Scenario description</span></span>
<span data-ttu-id="47d1f-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="47d1f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="47d1f-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="47d1f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="47d1f-121">Adicionando local de trabalho pelo Facebook da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="47d1f-121">Adding Workplace by Facebook from hello gallery</span></span>
2. <span data-ttu-id="47d1f-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="47d1f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workplace-by-facebook-from-hello-gallery"></a><span data-ttu-id="47d1f-123">Adicionando local de trabalho pelo Facebook da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="47d1f-123">Adding Workplace by Facebook from hello gallery</span></span>
<span data-ttu-id="47d1f-124">integração de saudação tooconfigure do local de trabalho pelo Facebook no AD do Azure, você precisa tooadd no local de trabalho pelo Facebook na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="47d1f-124">tooconfigure hello integration of Workplace by Facebook into Azure AD, you need tooadd Workplace by Facebook from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="47d1f-125">**tooadd no local de trabalho pelo Facebook da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="47d1f-125">**tooadd Workplace by Facebook from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="47d1f-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="47d1f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="47d1f-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="47d1f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="47d1f-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="47d1f-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="47d1f-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="47d1f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="47d1f-133">Na caixa de pesquisa hello, digite **no local de trabalho pelo Facebook**.</span><span class="sxs-lookup"><span data-stu-id="47d1f-133">In hello search box, type **Workplace by Facebook**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_search.png)

5. <span data-ttu-id="47d1f-135">No painel de resultados de saudação, selecione **no local de trabalho pelo Facebook**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="47d1f-135">In hello results panel, select **Workplace by Facebook**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="47d1f-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="47d1f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="47d1f-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Workplace by Facebook, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="47d1f-138">In this section, you configure and test Azure AD single sign-on with Workplace by Facebook based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="47d1f-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá na área de trabalho pelo Facebook é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="47d1f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workplace by Facebook is tooa user in Azure AD.</span></span> <span data-ttu-id="47d1f-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação na área de trabalho pelo Facebook precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="47d1f-140">In other words, a link relationship between an Azure AD user and hello related user in Workplace by Facebook needs toobe established.</span></span>

<span data-ttu-id="47d1f-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** na área de trabalho pelo Facebook.</span><span class="sxs-lookup"><span data-stu-id="47d1f-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Workplace by Facebook.</span></span>

<span data-ttu-id="47d1f-142">tooconfigure e teste de logon único do AD do Azure com o espaço de trabalho pelo Facebook, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="47d1f-142">tooconfigure and test Azure AD single sign-on with Workplace by Facebook, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="47d1f-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="47d1f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="47d1f-144">**[Configurar a frequência de reautenticação](#configuring-reauthentication-frequency)**  -tooconfigure tooprompt de local de trabalho para uma verificação SAML.</span><span class="sxs-lookup"><span data-stu-id="47d1f-144">**[Configuring Reauthentication Frequency](#configuring-reauthentication-frequency)** - tooconfigure Workplace tooprompt for a SAML check.</span></span>
3. <span data-ttu-id="47d1f-145">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="47d1f-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="47d1f-146">**[Criar um local de trabalho por usuário de teste do Facebook](#creating-a-workplace-by-facebook-test-user)**  -toohave um equivalente do Britta Simon na área de trabalho pelo Facebook é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="47d1f-146">**[Creating a Workplace by Facebook test user](#creating-a-workplace-by-facebook-test-user)** - toohave a counterpart of Britta Simon in Workplace by Facebook that is linked toohello Azure AD representation of user.</span></span>
5. <span data-ttu-id="47d1f-147">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="47d1f-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
6. <span data-ttu-id="47d1f-148">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="47d1f-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="47d1f-149">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="47d1f-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="47d1f-150">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único na área de trabalho pelo aplicativo do Facebook.</span><span class="sxs-lookup"><span data-stu-id="47d1f-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workplace by Facebook application.</span></span>

<span data-ttu-id="47d1f-151">**tooconfigure AD do Azure-logon único com espaço de trabalho pelo Facebook, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="47d1f-151">**tooconfigure Azure AD single sign-on with Workplace by Facebook, perform hello following steps:**</span></span>

1. <span data-ttu-id="47d1f-152">Em Olá portal do Azure, Olá **no local de trabalho pelo Facebook** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="47d1f-152">In hello Azure portal, on hello **Workplace by Facebook** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="47d1f-154">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="47d1f-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. <span data-ttu-id="47d1f-156">Em Olá **no local de trabalho pelo domínio do Facebook e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="47d1f-156">On hello **Workplace by Facebook Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_url.png)

    <span data-ttu-id="47d1f-158">a.</span><span class="sxs-lookup"><span data-stu-id="47d1f-158">a.</span></span> <span data-ttu-id="47d1f-159">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<instancename>.facebook.com`</span><span class="sxs-lookup"><span data-stu-id="47d1f-159">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instancename>.facebook.com`</span></span>

    <span data-ttu-id="47d1f-160">b.</span><span class="sxs-lookup"><span data-stu-id="47d1f-160">b.</span></span> <span data-ttu-id="47d1f-161">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://www.facebook.com/company/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="47d1f-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.facebook.com/company/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="47d1f-162">Esses valores não são Olá real.</span><span class="sxs-lookup"><span data-stu-id="47d1f-162">These values are not hello real.</span></span> <span data-ttu-id="47d1f-163">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="47d1f-163">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="47d1f-164">Entre em contato com [no local de trabalho pela equipe de suporte de cliente do Facebook](https://workplace.fb.com/faq/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="47d1f-164">Contact [Workplace by Facebook Client support team](https://workplace.fb.com/faq/) tooget these values.</span></span> 

4. <span data-ttu-id="47d1f-165">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="47d1f-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. <span data-ttu-id="47d1f-167">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="47d1f-167">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="47d1f-169">Em Olá **no local de trabalho pela configuração do Facebook** seção, clique em **configurar o local de trabalho pelo Facebook** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="47d1f-169">On hello **Workplace by Facebook Configuration** section, click **Configure Workplace by Facebook** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="47d1f-170">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="47d1f-170">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-workplacebyfacebook-tutorial/config.png) 

7. <span data-ttu-id="47d1f-172">Em uma janela de navegador web diferente, tooyour de logon local de trabalho por site de empresa do Facebook como um administrador.</span><span class="sxs-lookup"><span data-stu-id="47d1f-172">In a different web browser window, login tooyour Workplace by Facebook company site as an administrator.</span></span>
  
   > [!NOTE] 
   > <span data-ttu-id="47d1f-173">Como parte da saudação o processo de autenticação SAML, local de trabalho pode usar cadeias de caracteres de consulta de backup too2.5 KB de tamanho em ordem toopass parâmetros tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="47d1f-173">As part of hello SAML authentication process, Workplace may utilize query strings of up too2.5 kilobytes in size in order toopass parameters tooAzure AD.</span></span>

8. <span data-ttu-id="47d1f-174">Em Olá **empresa painel**, vá toohello **autenticação** guia.</span><span class="sxs-lookup"><span data-stu-id="47d1f-174">In hello **Company Dashboard**, go toohello **Authentication** tab.</span></span>

9. <span data-ttu-id="47d1f-175">Em **autenticação SAML**, selecione **SSO apenas** da lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="47d1f-175">Under **SAML Authentication**, select **SSO Only** from hello drop-down list.</span></span>

10. <span data-ttu-id="47d1f-176">Valores de entrada hello copiados do **no local de trabalho pela configuração do Facebook** seção Olá portal do Azure nos campos correspondentes hello:</span><span class="sxs-lookup"><span data-stu-id="47d1f-176">Input hello values copied from **Workplace by Facebook Configuration** section of hello Azure portal into hello corresponding fields:</span></span>

    *   <span data-ttu-id="47d1f-177">Em **URL SAML** caixa de texto valor Olá colar **o URL de serviço de logon único**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="47d1f-177">In **SAML URL** textbox, paste hello value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="47d1f-178">Em **caixa de texto URL do emissor SAML**, cole o valor de saudação do **ID da entidade SAML**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="47d1f-178">In **SAML Issuer URL textbox**, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="47d1f-179">Em **redirecionamento de Logout do SAML** (opcional), cole o valor de saudação do **URL de logout**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="47d1f-179">In **SAML Logout Redirect** (Optional), paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="47d1f-180">Abra o **certificado codificado na base 64** no bloco de notas baixado do portal do Azure, copie o conteúdo de saudação para sua área de transferência e, em seguida, cole-o toothe **certificado SAML** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="47d1f-180">Open your **base-64 encoded certificate** in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toothe **SAML Certificate** textbox.</span></span>

11. <span data-ttu-id="47d1f-181">Olá tooenter URL público, URL do destinatário, talvez seja necessário e a URL do ACS (serviço do consumidor de declaração) listados em Olá **configuração SAML** seção.</span><span class="sxs-lookup"><span data-stu-id="47d1f-181">You may need tooenter hello Audience URL, Recipient URL, and ACS (Assertion Consumer Service) URL listed under hello **SAML Configuration** section.</span></span>

12. <span data-ttu-id="47d1f-182">Role toohello inferior da seção hello e clique em Olá **teste SSO** botão.</span><span class="sxs-lookup"><span data-stu-id="47d1f-182">Scroll toohello bottom of hello section and click hello **Test SSO** button.</span></span> <span data-ttu-id="47d1f-183">Isso resultará na exibição de uma janela pop-up com a página de logon do Azure AD apresentada.</span><span class="sxs-lookup"><span data-stu-id="47d1f-183">This results in a popup window appearing with Azure AD login page presented.</span></span> <span data-ttu-id="47d1f-184">Insira suas credenciais no como tooauthenticate normal.</span><span class="sxs-lookup"><span data-stu-id="47d1f-184">Enter your credentials in as normal tooauthenticate.</span></span> 

    <span data-ttu-id="47d1f-185">**Solução de problemas:** endereço de email de saudação Certifique-se de que está sendo retornado pelo AD do Azure é Olá mesmo Olá você efetuou logon com conta da empresa.</span><span class="sxs-lookup"><span data-stu-id="47d1f-185">**Troubleshooting:** Ensure hello email address being returned back from Azure AD is hello same as hello Workplace account you are logged in with.</span></span>

13. <span data-ttu-id="47d1f-186">Depois que o teste de saudação for concluído com êxito, role toohello inferior da página hello e clique Olá **salvar** botão.</span><span class="sxs-lookup"><span data-stu-id="47d1f-186">Once hello test has been completed successfully, scroll toohello bottom of hello page and click hello **Save** button.</span></span>

14. <span data-ttu-id="47d1f-187">Agora, todos os usuários que usam o Workplace verão a página de logon do Azure AD para autenticação.</span><span class="sxs-lookup"><span data-stu-id="47d1f-187">All users using Workplace will now be presented with Azure AD login page for authentication.</span></span>

15. <span data-ttu-id="47d1f-188">**Redirecionamento de Logoff SAML (opcional)** -</span><span class="sxs-lookup"><span data-stu-id="47d1f-188">**SAML Logout Redirect (optional)** -</span></span> 

    <span data-ttu-id="47d1f-189">Você pode escolher toooptionally configurar uma Url de Logout do SAML, que pode ser usado toopoint na página de logout do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="47d1f-189">You can choose toooptionally configure a SAML Logout Url, which can be used toopoint at Azure AD's logout page.</span></span> <span data-ttu-id="47d1f-190">Quando essa configuração é habilitada e configurada, o usuário Olá não será direcionado toohello página de logout de área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="47d1f-190">When this setting is enabled and configured, hello user will no longer be directed toohello Workplace logout page.</span></span> <span data-ttu-id="47d1f-191">Em vez disso, o usuário de Olá será redirecionado toohello url que foi adicionado na configuração de redirecionamento de Logout do SAML de saudação.</span><span class="sxs-lookup"><span data-stu-id="47d1f-191">Instead, hello user will be redirected toohello url that was added in hello SAML Logout Redirect setting.</span></span>


> [!TIP]
> <span data-ttu-id="47d1f-192">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="47d1f-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="47d1f-193">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="47d1f-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="47d1f-194">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="47d1f-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="configuring-reauthentication-frequency"></a><span data-ttu-id="47d1f-195">Configurando a frequência de reautenticação</span><span class="sxs-lookup"><span data-stu-id="47d1f-195">Configuring Reauthentication Frequency</span></span>

<span data-ttu-id="47d1f-196">Você pode configurar tooprompt no local de trabalho para uma verificação SAML diariamente, três dias, semanas, duas semanas, meses ou nunca.</span><span class="sxs-lookup"><span data-stu-id="47d1f-196">You can configure Workplace tooprompt for a SAML check every day, three days, week, two weeks, month or never.</span></span>

> [!NOTE] 
><span data-ttu-id="47d1f-197">Olá valor mínimo para a seleção SAML Olá em aplicativos móveis é definido tooone semana.</span><span class="sxs-lookup"><span data-stu-id="47d1f-197">hello minimum value for hello SAML check on mobile applications is set tooone week.</span></span>

<span data-ttu-id="47d1f-198">Você também pode forçar um redefinição para todos os usuários usando o botão de saudação SAML: exigir autenticação SAML para todos os usuários agora.</span><span class="sxs-lookup"><span data-stu-id="47d1f-198">You can also force a SAML reset for all users using hello button: Require SAML authentication for all users now.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="47d1f-199">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="47d1f-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="47d1f-200">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="47d1f-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="47d1f-202">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="47d1f-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="47d1f-203">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="47d1f-203">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="47d1f-205">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="47d1f-205">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="47d1f-207">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="47d1f-207">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="47d1f-209">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="47d1f-209">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="47d1f-211">a.</span><span class="sxs-lookup"><span data-stu-id="47d1f-211">a.</span></span> <span data-ttu-id="47d1f-212">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="47d1f-212">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="47d1f-213">b.</span><span class="sxs-lookup"><span data-stu-id="47d1f-213">b.</span></span> <span data-ttu-id="47d1f-214">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="47d1f-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="47d1f-215">c.</span><span class="sxs-lookup"><span data-stu-id="47d1f-215">c.</span></span> <span data-ttu-id="47d1f-216">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="47d1f-216">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="47d1f-217">d.</span><span class="sxs-lookup"><span data-stu-id="47d1f-217">d.</span></span> <span data-ttu-id="47d1f-218">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="47d1f-218">Click **Create**.</span></span>
 
### <a name="creating-a-workplace-by-facebook-test-user"></a><span data-ttu-id="47d1f-219">Criação de um usuário de teste do Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="47d1f-219">Creating a Workplace by Facebook test user</span></span>

<span data-ttu-id="47d1f-220">Nesta seção, um usuário chamado Brenda Fernandes será criado no Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="47d1f-220">In this section, a user called Britta Simon is created in Workplace by Facebook.</span></span> <span data-ttu-id="47d1f-221">O Workplace by Facebook dá suporte ao provisionamento Just-In-Time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="47d1f-221">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="47d1f-222">Não há nenhuma ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="47d1f-222">There is no action for you in this section.</span></span> <span data-ttu-id="47d1f-223">Se um usuário não existe no local de trabalho pelo Facebook, um novo será criado quando você tenta tooaccess no local de trabalho pelo Facebook.</span><span class="sxs-lookup"><span data-stu-id="47d1f-223">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt tooaccess Workplace by Facebook.</span></span>

>[!Note]
><span data-ttu-id="47d1f-224">Se você precisar toocreate um usuário manualmente, entre em contato com [no local de trabalho pela equipe de suporte de cliente do Facebook](https://workplace.fb.com/faq/)</span><span class="sxs-lookup"><span data-stu-id="47d1f-224">If you need toocreate a user manually, Contact [Workplace by Facebook Client support team](https://workplace.fb.com/faq/)</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="47d1f-225">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="47d1f-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="47d1f-226">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooWorkplace pelo Facebook.</span><span class="sxs-lookup"><span data-stu-id="47d1f-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkplace by Facebook.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="47d1f-228">**tooassign Britta Simon tooWorkplace pelo Facebook, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="47d1f-228">**tooassign Britta Simon tooWorkplace by Facebook, perform hello following steps:**</span></span>

1. <span data-ttu-id="47d1f-229">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="47d1f-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="47d1f-231">Na lista de aplicativos hello, selecione **no local de trabalho pelo Facebook**.</span><span class="sxs-lookup"><span data-stu-id="47d1f-231">In hello applications list, select **Workplace by Facebook**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_app.png) 

3. <span data-ttu-id="47d1f-233">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="47d1f-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="47d1f-235">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="47d1f-235">Click **Add** button.</span></span> <span data-ttu-id="47d1f-236">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="47d1f-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="47d1f-238">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="47d1f-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="47d1f-239">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="47d1f-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="47d1f-240">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="47d1f-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="47d1f-241">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="47d1f-241">Testing single sign-on</span></span>

<span data-ttu-id="47d1f-242">Se você quiser tootest suas configurações de logon único, abra Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="47d1f-242">If you want tootest your single sign-on settings, open hello Access Panel.</span></span>
<span data-ttu-id="47d1f-243">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="47d1f-243">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="47d1f-244">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="47d1f-244">Additional resources</span></span>

* [<span data-ttu-id="47d1f-245">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="47d1f-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="47d1f-246">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="47d1f-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="47d1f-247">Configurar Provisionamento de Usuário</span><span class="sxs-lookup"><span data-stu-id="47d1f-247">Configure User Provisioning</span></span>](active-directory-saas-workplacebyfacebook-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_203.png

