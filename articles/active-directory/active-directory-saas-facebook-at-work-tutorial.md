---
title: "Tutorial: Integração do Azure Active Directory com o Workplace by Facebook| Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o local de trabalho pelo Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: jeedes
ms.openlocfilehash: fd19b3f178a2aee7dd2f204d6d3cf6df8fe6b444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="86f9a-103">Tutorial: Integração do Azure Active Directory com o Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="86f9a-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>

<span data-ttu-id="86f9a-104">Neste tutorial, você aprenderá como toointegrate no local de trabalho pelo Facebook com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="86f9a-104">In this tutorial, you learn how toointegrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="86f9a-105">Integração do local de trabalho pelo Facebook com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="86f9a-105">Integrating Workplace by Facebook with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="86f9a-106">Você pode controlar no AD do Azure que tenha acesso tooWorkplace pelo Facebook.</span><span class="sxs-lookup"><span data-stu-id="86f9a-106">You can control in Azure AD who has access tooWorkplace by Facebook.</span></span>
- <span data-ttu-id="86f9a-107">Você pode permitir que os usuários tooautomatically obter conectado tooWorkplace pelo Facebook (logon único) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="86f9a-107">You can enable your users tooautomatically get signed on tooWorkplace by Facebook (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="86f9a-108">Você pode gerenciar suas contas em um local central: Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="86f9a-108">You can manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="86f9a-109">Para obter mais detalhes sobre a integração de aplicativos de SaaS (software como serviço) ao Azure AD, consulte [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="86f9a-109">For more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86f9a-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="86f9a-110">Prerequisites</span></span>

<span data-ttu-id="86f9a-111">tooconfigure integração do AD do Azure com o local de trabalho pelo Facebook, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="86f9a-111">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following items:</span></span>

- <span data-ttu-id="86f9a-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="86f9a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="86f9a-113">Uma assinatura do Workplace by Facebook habilitada para SSO (logon único)</span><span class="sxs-lookup"><span data-stu-id="86f9a-113">A Workplace by Facebook single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="86f9a-114">etapas de saudação tootest neste tutorial, siga estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="86f9a-114">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="86f9a-115">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="86f9a-115">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="86f9a-116">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="86f9a-116">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="86f9a-117">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="86f9a-117">Scenario description</span></span>
<span data-ttu-id="86f9a-118">Neste tutorial, você testa o SSO do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="86f9a-118">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="86f9a-119">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="86f9a-119">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="86f9a-120">Adicione espaço de trabalho pelo Facebook da Galeria de saudação.</span><span class="sxs-lookup"><span data-stu-id="86f9a-120">Add Workplace by Facebook from hello gallery.</span></span>
2. <span data-ttu-id="86f9a-121">Configurar e testar logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="86f9a-121">Configure and test Azure AD single sign-on.</span></span>

## <a name="add-workplace-by-facebook-from-hello-gallery"></a><span data-ttu-id="86f9a-122">Adicione o local de trabalho pelo Facebook da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="86f9a-122">Add Workplace by Facebook from hello gallery</span></span>
<span data-ttu-id="86f9a-123">tooconfigure Olá a integração da área de trabalho pelo Facebook AD do Azure, adicione no local de trabalho pelo Facebook na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="86f9a-123">tooconfigure hello integration of Workplace by Facebook into Azure AD, add Workplace by Facebook from hello gallery tooyour list of managed SaaS apps.</span></span>

1. <span data-ttu-id="86f9a-124">Em Olá [portal do Azure](https://portal.azure.com), no hello painel esquerdo, selecione **Active Directory do Azure**.</span><span class="sxs-lookup"><span data-stu-id="86f9a-124">In hello [Azure portal](https://portal.azure.com), in hello left pane, select **Azure Active Directory**.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="86f9a-126">Procurar muito**aplicativos empresariais** > **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="86f9a-126">Browse too**Enterprise applications** > **All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="86f9a-128">tooadd Olá novo aplicativo, selecione **novo aplicativo** na parte superior de Olá Olá da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="86f9a-128">tooadd hello new application, select **New application** on hello top of hello dialog box.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="86f9a-130">Na caixa de pesquisa hello, digite **no local de trabalho pelo Facebook**e selecione **no local de trabalho pelo Facebook** dos resultados.</span><span class="sxs-lookup"><span data-stu-id="86f9a-130">In hello search box, type **Workplace by Facebook**, and select **Workplace by Facebook** from results.</span></span> <span data-ttu-id="86f9a-131">Em seguida, selecione **adicionar**, aplicativo de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="86f9a-131">Then select **Add**, tooadd hello application.</span></span>

    ![Local de trabalho pelo Facebook na lista de resultados de saudação](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_search.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="86f9a-133">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="86f9a-133">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="86f9a-134">Nesta seção, você configurará e testará o SSO do Azure AD com o Workplace by Facebook, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="86f9a-134">In this section, you configure and test Azure AD SSO with Workplace by Facebook, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="86f9a-135">Para SSO toowork, o AD do Azure precisa tooknow que usuário de contraparte Olá na área de trabalho pelo Facebook é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="86f9a-135">For SSO toowork, Azure AD needs tooknow what hello counterpart user in Workplace by Facebook is tooa user in Azure AD.</span></span> <span data-ttu-id="86f9a-136">Em outras palavras, uma relação entre um usuário do AD do Azure e o usuário relacionado de saudação na área de trabalho pelo Facebook de vinculado deve ser estabelecida.</span><span class="sxs-lookup"><span data-stu-id="86f9a-136">In other words, a linked relationship between an Azure AD user and hello related user in Workplace by Facebook should be established.</span></span>

<span data-ttu-id="86f9a-137">Estabelecer essa relação, atribuindo o valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** na área de trabalho pelo Facebook.</span><span class="sxs-lookup"><span data-stu-id="86f9a-137">Establish this relationship by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Workplace by Facebook.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="86f9a-138">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="86f9a-138">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="86f9a-139">Nesta seção, você habilitar o SSO do AD do Azure no portal do Azure de saudação e configurar SSO na área de trabalho pelo aplicativo do Facebook.</span><span class="sxs-lookup"><span data-stu-id="86f9a-139">In this section, you enable Azure AD SSO in hello Azure portal, and you configure SSO in your Workplace by Facebook application.</span></span>

1. <span data-ttu-id="86f9a-140">Em Olá portal do Azure, Olá **no local de trabalho pelo Facebook** página de integração de aplicativos, selecione **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="86f9a-140">In hello Azure portal, on hello **Workplace by Facebook** application integration page, select **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="86f9a-142">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable SSO.</span><span class="sxs-lookup"><span data-stu-id="86f9a-142">In hello **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on** tooenable SSO.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. <span data-ttu-id="86f9a-144">Em Olá **no local de trabalho pelo domínio do Facebook e URLs** seção, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="86f9a-144">In hello **Workplace by Facebook Domain and URLs** section, do hello following:</span></span>

    <span data-ttu-id="86f9a-145">a.</span><span class="sxs-lookup"><span data-stu-id="86f9a-145">a.</span></span> <span data-ttu-id="86f9a-146">Em Olá **URL de logon** caixa de texto, digite uma URL que usa o saudação padrão a seguir:`https://<company subdomain>.facebook.com`</span><span class="sxs-lookup"><span data-stu-id="86f9a-146">In hello **Sign-on URL** text box, type a URL that uses hello following pattern: `https://<company subdomain>.facebook.com`</span></span>

    <span data-ttu-id="86f9a-147">b.</span><span class="sxs-lookup"><span data-stu-id="86f9a-147">b.</span></span> <span data-ttu-id="86f9a-148">Em Olá **identificador** caixa de texto, digite uma URL que usa o saudação padrão a seguir:`https://www.facebook.com/company/<scim company id>`</span><span class="sxs-lookup"><span data-stu-id="86f9a-148">In hello **Identifier** text box, type a URL that uses hello following pattern: `https://www.facebook.com/company/<scim company id>`</span></span>

    > [!NOTE]
    > <span data-ttu-id="86f9a-149">Esses valores são apenas um exemplo.</span><span class="sxs-lookup"><span data-stu-id="86f9a-149">These values are an example only.</span></span> <span data-ttu-id="86f9a-150">Atualize esses valores com URL de logon real hello e o identificador.</span><span class="sxs-lookup"><span data-stu-id="86f9a-150">Update these values with hello actual sign-on URL and identifier.</span></span> <span data-ttu-id="86f9a-151">Olá contato [no local de trabalho pela equipe de suporte de cliente do Facebook](https://workplace.fb.com/faq/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="86f9a-151">Contact hello [Workplace by Facebook Client support team](https://workplace.fb.com/faq/) tooget these values.</span></span> 

4. <span data-ttu-id="86f9a-152">Em Olá **o certificado de autenticação SAML** seção, selecione **certificado (Base64)**e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="86f9a-152">In hello **SAML Signing Certificate** section, select **Certificate (Base64)**, and then save hello certificate file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. <span data-ttu-id="86f9a-154">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="86f9a-154">Select **Save**.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="86f9a-156">Em Olá **no local de trabalho pela configuração do Facebook** seção, selecione **configurar o local de trabalho pelo Facebook** tooopen Olá **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="86f9a-156">In hello **Workplace by Facebook Configuration** section, select **Configure Workplace by Facebook** tooopen hello **Configure sign-on** window.</span></span> <span data-ttu-id="86f9a-157">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **referência rápida** seção.</span><span class="sxs-lookup"><span data-stu-id="86f9a-157">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference** section.</span></span>

    ![Configuração do Workplace by Facebook](./media/active-directory-saas-facebook-at-work-tutorial/config.png) 

7. <span data-ttu-id="86f9a-159">Em uma janela de navegador web diferente, entre tooyour no local de trabalho por site de empresa do Facebook como um administrador.</span><span class="sxs-lookup"><span data-stu-id="86f9a-159">In a different web browser window, sign in tooyour Workplace by Facebook company site as an administrator.</span></span>
  
   > [!NOTE] 
   > <span data-ttu-id="86f9a-160">Como parte da saudação o processo de autenticação SAML, o local de trabalho pode usar cadeias de caracteres de consulta de backup too2.5 quilobytes de tamanho em ordem toopass parâmetros tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="86f9a-160">As part of hello SAML authentication process, Workplace can use query strings of up too2.5 kilobytes in size in order toopass parameters tooAzure AD.</span></span>

8. <span data-ttu-id="86f9a-161">Em Olá **empresa painel**, vá toohello **autenticação** guia.</span><span class="sxs-lookup"><span data-stu-id="86f9a-161">In hello **Company Dashboard**, go toohello **Authentication** tab.</span></span>

9. <span data-ttu-id="86f9a-162">Em **autenticação SAML**, selecione **SSO apenas** da lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="86f9a-162">Under **SAML Authentication**, select **SSO Only** from hello drop-down list.</span></span>

10. <span data-ttu-id="86f9a-163">Insira valores hello copiados da saudação **no local de trabalho pela configuração do Facebook** seção Olá portal do Azure nos campos correspondentes hello:</span><span class="sxs-lookup"><span data-stu-id="86f9a-163">Enter hello values copied from hello **Workplace by Facebook Configuration** section of hello Azure portal into hello corresponding fields:</span></span>

    *   <span data-ttu-id="86f9a-164">No **URL SAML** caixa de texto valor Olá colar **o URL de serviço de logon único**, que você copiou de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="86f9a-164">In the **SAML URL** text box, paste hello value of **Single Sign-On Service URL**, which you have copied from hello Azure portal.</span></span>
    *   <span data-ttu-id="86f9a-165">No **URL do emissor SAML** caixa de texto valor Olá colar **ID da entidade SAML**, que você copiou de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="86f9a-165">In the **SAML Issuer URL** text box, paste hello value of **SAML Entity ID**, which you have copied from hello Azure portal.</span></span>
    *   <span data-ttu-id="86f9a-166">Em **redirecionamento de Logout de SAML (opcional)**, cole o valor de saudação do **URL de logout**, que você copiou de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="86f9a-166">In **SAML Logout Redirect (optional)**, paste hello value of **Sign-Out URL**, which you have copied from hello Azure portal.</span></span>
    *   <span data-ttu-id="86f9a-167">Abra o **certificado codificado na base 64** no bloco de notas, baixado do hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="86f9a-167">Open your **base-64 encoded certificate** in Notepad, downloaded from hello Azure portal.</span></span> <span data-ttu-id="86f9a-168">Copie o conteúdo de saudação para sua área de transferência e, em seguida, cole-o toothe **certificado SAML** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="86f9a-168">Copy hello content of it into your clipboard, and then paste it toothe **SAML Certificate** text box.</span></span>

11. <span data-ttu-id="86f9a-169">Talvez seja necessário público de saudação tooenter URL destinatário URL e o ACS (serviço do consumidor de declaração) URL, listado em Olá **configuração SAML** seção.</span><span class="sxs-lookup"><span data-stu-id="86f9a-169">You might need tooenter hello audience URL, recipient URL, and ACS (Assertion Consumer Service) URL, listed under hello **SAML Configuration** section.</span></span>

12. <span data-ttu-id="86f9a-170">Role toohello inferior da seção hello e selecione **teste SSO**.</span><span class="sxs-lookup"><span data-stu-id="86f9a-170">Scroll toohello bottom of hello section, and select **Test SSO**.</span></span> <span data-ttu-id="86f9a-171">Uma janela pop-up será exibida, com a página de entrada hello AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="86f9a-171">A pop-up window appears, with hello Azure AD sign-in page.</span></span> <span data-ttu-id="86f9a-172">tooauthenticate, insira suas credenciais como normal.</span><span class="sxs-lookup"><span data-stu-id="86f9a-172">tooauthenticate, enter your credentials as normal.</span></span> <span data-ttu-id="86f9a-173">Certifique-se de endereço de email Olá retornado pelo AD do Azure é Olá mesmo Olá você efetuou logon com conta da empresa.</span><span class="sxs-lookup"><span data-stu-id="86f9a-173">Ensure hello email address returned back from Azure AD is hello same as hello Workplace account you are logged in with.</span></span>

13. <span data-ttu-id="86f9a-174">Se o teste de saudação foi concluído com êxito, role toohello inferior da página hello e selecione **salvar**.</span><span class="sxs-lookup"><span data-stu-id="86f9a-174">If hello test has finished successfully, scroll toohello bottom of hello page and select **Save**.</span></span>

14. <span data-ttu-id="86f9a-175">Agora, todas as pessoas que usam o Workplace verão a página de entrada do Azure AD para autenticação.</span><span class="sxs-lookup"><span data-stu-id="86f9a-175">Anyone using Workplace is now presented with Azure AD sign-in page for authentication.</span></span>

<span data-ttu-id="86f9a-176">Você pode escolher tooconfigure uma URL, que pode ser usado toopoint na página de logout de saudação do AD do Azure de logout do SAML.</span><span class="sxs-lookup"><span data-stu-id="86f9a-176">You can choose tooconfigure a SAML sign out URL, which can be used toopoint at hello Azure AD sign-out page.</span></span> <span data-ttu-id="86f9a-177">Quando essa configuração é habilitada e configurada, Olá usuário não é mais direcionado toohello página de saída de local de trabalho.</span><span class="sxs-lookup"><span data-stu-id="86f9a-177">When this setting is enabled and configured, hello user is no longer directed toohello Workplace sign-out page.</span></span> <span data-ttu-id="86f9a-178">Em vez disso, o usuário de saudação é URL redirecionada toohello que foi adicionado na configuração de redirecionamento de saída do SAML hello.</span><span class="sxs-lookup"><span data-stu-id="86f9a-178">Instead, hello user is redirected toohello URL that was added in hello SAML sign-out redirect setting.</span></span>


> [!TIP]
> <span data-ttu-id="86f9a-179">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="86f9a-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app.</span></span> <span data-ttu-id="86f9a-180">Depois de adicionar a este aplicativo de saudação **do Active Directory** > **aplicativos empresariais** seção, basta selecionar Olá **Single Sign-On** guia e saudação de acesso inserido documentação por meio de saudação **configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="86f9a-180">After adding this app from hello **Active Directory** > **Enterprise Applications** section, simply select hello **Single Sign-On** tab, and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="86f9a-181">Você pode ler mais sobre recurso de documentação embedded Olá no hello [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="86f9a-181">You can read more about hello embedded documentation feature in hello [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="configure-reauthentication-frequency"></a><span data-ttu-id="86f9a-182">Configurar a frequência de reautenticação</span><span class="sxs-lookup"><span data-stu-id="86f9a-182">Configure reauthentication frequency</span></span>

<span data-ttu-id="86f9a-183">Você pode configurar o local de trabalho tooprompt uma verificação de SAML diariamente, três dias, uma semana, duas semanas, um mês, ou nunca.</span><span class="sxs-lookup"><span data-stu-id="86f9a-183">You can configure Workplace tooprompt for a SAML check every day, three days, one week, two weeks, one month, or never.</span></span>

> [!NOTE] 
><span data-ttu-id="86f9a-184">Olá valor mínimo para a seleção SAML Olá em aplicativos móveis é definido tooone semana.</span><span class="sxs-lookup"><span data-stu-id="86f9a-184">hello minimum value for hello SAML check on mobile applications is set tooone week.</span></span>

<span data-ttu-id="86f9a-185">Você também pode forçar uma redefinição de SAML para todos os usuários.</span><span class="sxs-lookup"><span data-stu-id="86f9a-185">You can also force a SAML reset for all users.</span></span> <span data-ttu-id="86f9a-186">toodo hello, use **exigem autenticação SAML para todos os usuários agora** botão.</span><span class="sxs-lookup"><span data-stu-id="86f9a-186">toodo this, use hello **Require SAML authentication for all users now** button.</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="86f9a-187">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="86f9a-187">Create an Azure AD test user</span></span>
<span data-ttu-id="86f9a-188">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="86f9a-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

1. <span data-ttu-id="86f9a-190">Em Olá **portal do Azure**, no hello painel esquerdo, selecione **Active Directory do Azure**.</span><span class="sxs-lookup"><span data-stu-id="86f9a-190">In hello **Azure portal**, in hello left pane, select **Azure Active Directory**.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="86f9a-192">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e selecione **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="86f9a-192">toodisplay hello list of users, go too**Users and groups**, and select **All users**.</span></span>
    
    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="86f9a-194">Olá tooopen **usuário** caixa de diálogo, selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="86f9a-194">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![botão Adicionar de saudação](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="86f9a-196">Em Olá **usuário** caixa de diálogo caixa, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="86f9a-196">In hello **User** dialog box, do hello following:</span></span>
 
    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="86f9a-198">a.</span><span class="sxs-lookup"><span data-stu-id="86f9a-198">a.</span></span> <span data-ttu-id="86f9a-199">Em Olá **nome** caixa de texto, digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="86f9a-199">In hello **Name** text box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="86f9a-200">b.</span><span class="sxs-lookup"><span data-stu-id="86f9a-200">b.</span></span> <span data-ttu-id="86f9a-201">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="86f9a-201">In hello **User name** text box, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="86f9a-202">c.</span><span class="sxs-lookup"><span data-stu-id="86f9a-202">c.</span></span> <span data-ttu-id="86f9a-203">Selecione **Mostrar Senha** e tome nota.</span><span class="sxs-lookup"><span data-stu-id="86f9a-203">Select **Show Password**, and write it down.</span></span>

    <span data-ttu-id="86f9a-204">d.</span><span class="sxs-lookup"><span data-stu-id="86f9a-204">d.</span></span> <span data-ttu-id="86f9a-205">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="86f9a-205">Select **Create**.</span></span>
 
### <a name="create-a-workplace-by-facebook-test-user"></a><span data-ttu-id="86f9a-206">Criar um usuário de teste do Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="86f9a-206">Create a Workplace by Facebook test user</span></span>

<span data-ttu-id="86f9a-207">Nesta seção, um usuário chamado Brenda Fernandes será criado no Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="86f9a-207">In this section, a user called Britta Simon is created in Workplace by Facebook.</span></span> <span data-ttu-id="86f9a-208">O Workplace by Facebook dá suporte ao provisionamento Just-In-Time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="86f9a-208">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="86f9a-209">Não há nenhuma ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="86f9a-209">There is no action for you in this section.</span></span> <span data-ttu-id="86f9a-210">Se um usuário não existe no local de trabalho pelo Facebook, um novo será criado quando você tenta tooaccess no local de trabalho pelo Facebook.</span><span class="sxs-lookup"><span data-stu-id="86f9a-210">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt tooaccess Workplace by Facebook.</span></span>

>[!Note]
><span data-ttu-id="86f9a-211">Se você precisar toocreate um usuário manualmente, entre em contato com o hello [no local de trabalho pela equipe de suporte de cliente do Facebook](https://workplace.fb.com/faq/).</span><span class="sxs-lookup"><span data-stu-id="86f9a-211">If you need toocreate a user manually, contact hello [Workplace by Facebook Client support team](https://workplace.fb.com/faq/).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="86f9a-212">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="86f9a-212">Assign hello Azure AD test user</span></span>

<span data-ttu-id="86f9a-213">Nesta seção, você pode habilitar Britta Simon toouse SSO do Azure, concedendo acesso tooWorkplace pelo Facebook.</span><span class="sxs-lookup"><span data-stu-id="86f9a-213">In this section, you enable Britta Simon toouse Azure SSO by granting access tooWorkplace by Facebook.</span></span>

![Atribuir usuário][200] 

1. <span data-ttu-id="86f9a-215">Hello Azure exibir aplicativos de portal, abra hello.</span><span class="sxs-lookup"><span data-stu-id="86f9a-215">In hello Azure portal, open hello applications view.</span></span> <span data-ttu-id="86f9a-216">Acesse o modo de exibição de diretório toohello, vá muito**aplicativos empresariais**e, em seguida, selecione **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="86f9a-216">Go toohello directory view, go too**Enterprise applications**, and then select **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="86f9a-218">Na lista de aplicativos hello, selecione **no local de trabalho pelo Facebook**.</span><span class="sxs-lookup"><span data-stu-id="86f9a-218">In hello applications list, select **Workplace by Facebook**.</span></span>

    ![Olá no local de trabalho por um link do Facebook na lista de aplicativos Olá](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_app.png) 

3. <span data-ttu-id="86f9a-220">No menu Olá Olá esquerda, selecione **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="86f9a-220">In hello menu on hello left, select **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202] 

4. <span data-ttu-id="86f9a-222">Selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="86f9a-222">Select **Add**.</span></span> <span data-ttu-id="86f9a-223">Em seguida, no hello **Adicionar atribuição** painel, selecione **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="86f9a-223">Then, in hello **Add Assignment** pane, select **Users and groups**.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="86f9a-225">Em Olá **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="86f9a-225">In hello **Users and groups** dialog box, select **Britta Simon** in hello users list.</span></span>

6. <span data-ttu-id="86f9a-226">Em Olá **usuários e grupos** caixa de diálogo, selecione **selecione**.</span><span class="sxs-lookup"><span data-stu-id="86f9a-226">In hello **Users and groups** dialog box, select **Select**.</span></span>

7. <span data-ttu-id="86f9a-227">Em Olá **Adicionar atribuição** caixa de diálogo, selecione **atribuir**.</span><span class="sxs-lookup"><span data-stu-id="86f9a-227">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="86f9a-228">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="86f9a-228">Test single sign-on</span></span>

<span data-ttu-id="86f9a-229">Se você quiser tootest suas configurações de SSO, abra Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="86f9a-229">If you want tootest your SSO settings, open hello Access Panel.</span></span>
<span data-ttu-id="86f9a-230">Para obter mais informações, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="86f9a-230">For more information, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="86f9a-231">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="86f9a-231">Next steps</span></span>

* <span data-ttu-id="86f9a-232">Consulte Olá [lista de tutoriais sobre como toointegrate aplicativos SaaS com o Azure Active Directory](active-directory-saas-tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="86f9a-232">See hello [list of tutorials on how toointegrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md).</span></span>
* <span data-ttu-id="86f9a-233">Leia [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="86f9a-233">Read [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>
* <span data-ttu-id="86f9a-234">Saiba mais sobre como muito[configurar provisionamento de usuário](active-directory-saas-facebook-at-work-provisioning-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="86f9a-234">Learn more about how too[configure user provisioning](active-directory-saas-facebook-at-work-provisioning-tutorial.md).</span></span>



<!--Image references-->

[1]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_203.png

