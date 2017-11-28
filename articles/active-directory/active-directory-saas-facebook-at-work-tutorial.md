---
title: "Tutorial: Integração do Azure Active Directory com o Workplace by Facebook| Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Workplace by Facebook."
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
ms.openlocfilehash: 27e62a00832484667117d8718db9f2fc05e2f4e2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="a5949-103">Tutorial: Integração do Azure Active Directory com o Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="a5949-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>

<span data-ttu-id="a5949-104">Neste tutorial, você aprenderá a integrar o Workplace by Facebook ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="a5949-104">In this tutorial, you learn how to integrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a5949-105">A integração do Workplace by Facebook ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="a5949-105">Integrating Workplace by Facebook with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a5949-106">No Azure AD, você pode controlar quem tem acesso ao Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="a5949-106">You can control in Azure AD who has access to Workplace by Facebook.</span></span>
- <span data-ttu-id="a5949-107">Você pode habilitar o logon automático de seus usuários no Workplace by Facebook (logon único) com as contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a5949-107">You can enable your users to automatically get signed on to Workplace by Facebook (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="a5949-108">Gerencie suas contas em um único local: o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a5949-108">You can manage your accounts in one central location: the Azure portal.</span></span>

<span data-ttu-id="a5949-109">Para obter mais detalhes sobre a integração de aplicativos de SaaS (software como serviço) ao Azure AD, consulte [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a5949-109">For more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5949-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a5949-110">Prerequisites</span></span>

<span data-ttu-id="a5949-111">Para configurar a integração do Azure AD com o Workplace by Facebook, são necessários os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="a5949-111">To configure Azure AD integration with Workplace by Facebook, you need the following items:</span></span>

- <span data-ttu-id="a5949-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a5949-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a5949-113">Uma assinatura do Workplace by Facebook habilitada para SSO (logon único)</span><span class="sxs-lookup"><span data-stu-id="a5949-113">A Workplace by Facebook single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="a5949-114">Para testar as etapas neste tutorial, siga estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="a5949-114">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="a5949-115">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="a5949-115">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a5949-116">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a5949-116">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a5949-117">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="a5949-117">Scenario description</span></span>
<span data-ttu-id="a5949-118">Neste tutorial, você testa o SSO do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="a5949-118">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="a5949-119">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="a5949-119">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a5949-120">Adicionar o Workplace by Facebook da galeria.</span><span class="sxs-lookup"><span data-stu-id="a5949-120">Add Workplace by Facebook from the gallery.</span></span>
2. <span data-ttu-id="a5949-121">Configurar e testar logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a5949-121">Configure and test Azure AD single sign-on.</span></span>

## <a name="add-workplace-by-facebook-from-the-gallery"></a><span data-ttu-id="a5949-122">Adicionar o Workplace by Facebook da galeria</span><span class="sxs-lookup"><span data-stu-id="a5949-122">Add Workplace by Facebook from the gallery</span></span>
<span data-ttu-id="a5949-123">Para configurar a integração do Workplace by Facebook ao Azure AD, adicione o Workplace by Facebook da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="a5949-123">To configure the integration of Workplace by Facebook into Azure AD, add Workplace by Facebook from the gallery to your list of managed SaaS apps.</span></span>

1. <span data-ttu-id="a5949-124">No [Portal do Azure](https://portal.azure.com), no painel esquerdo, selecione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a5949-124">In the [Azure portal](https://portal.azure.com), in the left pane, select **Azure Active Directory**.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="a5949-126">Navegue até **Aplicativos empresariais** > **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a5949-126">Browse to **Enterprise applications** > **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="a5949-128">Para adicionar o novo aplicativo, selecione **Novo aplicativo** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a5949-128">To add the new application, select **New application** on the top of the dialog box.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="a5949-130">Na caixa de pesquisa, digite **Workplace by Facebook** e selecione **Workplace by Facebook** nos resultados.</span><span class="sxs-lookup"><span data-stu-id="a5949-130">In the search box, type **Workplace by Facebook**, and select **Workplace by Facebook** from results.</span></span> <span data-ttu-id="a5949-131">Em seguida, selecione **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a5949-131">Then select **Add**, to add the application.</span></span>

    ![Workplace by Facebook na lista de resultados](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_search.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a5949-133">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5949-133">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="a5949-134">Nesta seção, você configurará e testará o SSO do Azure AD com o Workplace by Facebook, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="a5949-134">In this section, you configure and test Azure AD SSO with Workplace by Facebook, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a5949-135">Para que o SSO funcione, o Azure AD precisa saber qual usuário do Workplace by Facebook é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a5949-135">For SSO to work, Azure AD needs to know what the counterpart user in Workplace by Facebook is to a user in Azure AD.</span></span> <span data-ttu-id="a5949-136">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="a5949-136">In other words, a linked relationship between an Azure AD user and the related user in Workplace by Facebook should be established.</span></span>

<span data-ttu-id="a5949-137">Estabeleça essa relação atribuindo o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** no Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="a5949-137">Establish this relationship by assigning the value of the **user name** in Azure AD as the value of the **Username** in Workplace by Facebook.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a5949-138">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5949-138">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a5949-139">Nesta seção, você habilitará o SSO do Azure AD no Portal do Azure e configurará o SSO no aplicativo Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="a5949-139">In this section, you enable Azure AD SSO in the Azure portal, and you configure SSO in your Workplace by Facebook application.</span></span>

1. <span data-ttu-id="a5949-140">No Portal do Azure, na página de integração de aplicativos do **Workplace by Facebook**, selecione **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="a5949-140">In the Azure portal, on the **Workplace by Facebook** application integration page, select **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="a5949-142">Na caixa de diálogo **Logon único**, selecione o **Modo** **Logon baseado em SAML** para habilitar o SSO.</span><span class="sxs-lookup"><span data-stu-id="a5949-142">In the **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on** to enable SSO.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. <span data-ttu-id="a5949-144">Na seção **Domínio e URLs do Workplace by Facebook**, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="a5949-144">In the **Workplace by Facebook Domain and URLs** section, do the following:</span></span>

    <span data-ttu-id="a5949-145">a.</span><span class="sxs-lookup"><span data-stu-id="a5949-145">a.</span></span> <span data-ttu-id="a5949-146">Na caixa de texto **URL de Entrada**, digite uma URL que usa o seguinte padrão: `https://<company subdomain>.facebook.com`</span><span class="sxs-lookup"><span data-stu-id="a5949-146">In the **Sign-on URL** text box, type a URL that uses the following pattern: `https://<company subdomain>.facebook.com`</span></span>

    <span data-ttu-id="a5949-147">b.</span><span class="sxs-lookup"><span data-stu-id="a5949-147">b.</span></span> <span data-ttu-id="a5949-148">Na caixa de texto **Identificador**, digite uma URL que usa o seguinte padrão: `https://www.facebook.com/company/<scim company id>`</span><span class="sxs-lookup"><span data-stu-id="a5949-148">In the **Identifier** text box, type a URL that uses the following pattern: `https://www.facebook.com/company/<scim company id>`</span></span>

    > [!NOTE]
    > <span data-ttu-id="a5949-149">Esses valores são apenas um exemplo.</span><span class="sxs-lookup"><span data-stu-id="a5949-149">These values are an example only.</span></span> <span data-ttu-id="a5949-150">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="a5949-150">Update these values with the actual sign-on URL and identifier.</span></span> <span data-ttu-id="a5949-151">Contate a [Equipe de suporte ao cliente do Workplace by Facebook](https://workplace.fb.com/faq/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="a5949-151">Contact the [Workplace by Facebook Client support team](https://workplace.fb.com/faq/) to get these values.</span></span> 

4. <span data-ttu-id="a5949-152">Na seção **Certificado de Autenticação SAML**, selecione **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="a5949-152">In the **SAML Signing Certificate** section, select **Certificate (Base64)**, and then save the certificate file on your computer.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. <span data-ttu-id="a5949-154">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="a5949-154">Select **Save**.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a5949-156">Na seção **Configuração do Workplace by Facebook**, selecione **Configurar o Workplace by Facebook** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="a5949-156">In the **Workplace by Facebook Configuration** section, select **Configure Workplace by Facebook** to open the **Configure sign-on** window.</span></span> <span data-ttu-id="a5949-157">Copie a **URL de Saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da seção **Referência Rápida**.</span><span class="sxs-lookup"><span data-stu-id="a5949-157">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference** section.</span></span>

    ![Configuração do Workplace by Facebook](./media/active-directory-saas-facebook-at-work-tutorial/config.png) 

7. <span data-ttu-id="a5949-159">Em outra janela do navegador da Web, entre em seu site da empresa do Workplace by Facebook como administrador.</span><span class="sxs-lookup"><span data-stu-id="a5949-159">In a different web browser window, sign in to your Workplace by Facebook company site as an administrator.</span></span>
  
   > [!NOTE] 
   > <span data-ttu-id="a5949-160">Como parte do processo de autenticação SAML, o Workplace poderá utilizar cadeias de consulta de até 2,5 quilobytes para passar parâmetros para o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a5949-160">As part of the SAML authentication process, Workplace can use query strings of up to 2.5 kilobytes in size in order to pass parameters to Azure AD.</span></span>

8. <span data-ttu-id="a5949-161">No **Painel da Empresa**, acesse a guia **Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="a5949-161">In the **Company Dashboard**, go to the **Authentication** tab.</span></span>

9. <span data-ttu-id="a5949-162">Em **Autenticação SAML**, selecione **Somente SSO** na lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="a5949-162">Under **SAML Authentication**, select **SSO Only** from the drop-down list.</span></span>

10. <span data-ttu-id="a5949-163">Insira os valores copiados da seção **Configuração do Workplace by Facebook** do Portal do Azure nos campos correspondentes:</span><span class="sxs-lookup"><span data-stu-id="a5949-163">Enter the values copied from the **Workplace by Facebook Configuration** section of the Azure portal into the corresponding fields:</span></span>

    *   <span data-ttu-id="a5949-164">Na caixa de texto **URL de SAML**, cole o valor da **URL do Serviço de Logon Único** copiado do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a5949-164">In the **SAML URL** text box, paste the value of **Single Sign-On Service URL**, which you have copied from the Azure portal.</span></span>
    *   <span data-ttu-id="a5949-165">Na caixa de texto **URL do Emissor SAML**, cole o valor da **ID da Entidade SAML** copiado do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a5949-165">In the **SAML Issuer URL** text box, paste the value of **SAML Entity ID**, which you have copied from the Azure portal.</span></span>
    *   <span data-ttu-id="a5949-166">Em **Redirecionamento de Logoff SAML (opcional)**, cole o valor da **URL de Saída** que foi copiado do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a5949-166">In **SAML Logout Redirect (optional)**, paste the value of **Sign-Out URL**, which you have copied from the Azure portal.</span></span>
    *   <span data-ttu-id="a5949-167">Abra o **Certificado codificado Base 64** no Bloco de notas, baixado do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a5949-167">Open your **base-64 encoded certificate** in Notepad, downloaded from the Azure portal.</span></span> <span data-ttu-id="a5949-168">Copie o conteúdo dele para sua área de transferência e, em seguida, cole-o na caixa de texto **Certificado SAML**.</span><span class="sxs-lookup"><span data-stu-id="a5949-168">Copy the content of it into your clipboard, and then paste it to the **SAML Certificate** text box.</span></span>

11. <span data-ttu-id="a5949-169">Talvez seja necessário inserir a URL do público-alvo, a URL do destinatário e a URL do ACS (Serviço do Consumidor de Declaração) listadas na seção **Configuração do SAML**.</span><span class="sxs-lookup"><span data-stu-id="a5949-169">You might need to enter the audience URL, recipient URL, and ACS (Assertion Consumer Service) URL, listed under the **SAML Configuration** section.</span></span>

12. <span data-ttu-id="a5949-170">Role até o final da seção e selecione **Testar SSO**.</span><span class="sxs-lookup"><span data-stu-id="a5949-170">Scroll to the bottom of the section, and select **Test SSO**.</span></span> <span data-ttu-id="a5949-171">Uma janela pop-up será exibida, com a página de entrada do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a5949-171">A pop-up window appears, with the Azure AD sign-in page.</span></span> <span data-ttu-id="a5949-172">Para se autenticar, insira suas credenciais como de costume.</span><span class="sxs-lookup"><span data-stu-id="a5949-172">To authenticate, enter your credentials as normal.</span></span> <span data-ttu-id="a5949-173">Verifique se o endereço de email retornado do Azure AD é o mesmo da conta do Workplace na qual você está conectado.</span><span class="sxs-lookup"><span data-stu-id="a5949-173">Ensure the email address returned back from Azure AD is the same as the Workplace account you are logged in with.</span></span>

13. <span data-ttu-id="a5949-174">Se o teste for concluído com êxito, role até a parte inferior da página e selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="a5949-174">If the test has finished successfully, scroll to the bottom of the page and select **Save**.</span></span>

14. <span data-ttu-id="a5949-175">Agora, todas as pessoas que usam o Workplace verão a página de entrada do Azure AD para autenticação.</span><span class="sxs-lookup"><span data-stu-id="a5949-175">Anyone using Workplace is now presented with Azure AD sign-in page for authentication.</span></span>

<span data-ttu-id="a5949-176">Você pode optar por configurar uma URL de logoff SAML, que pode ser usada para apontar para a página de logoff do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a5949-176">You can choose to configure a SAML sign out URL, which can be used to point at the Azure AD sign-out page.</span></span> <span data-ttu-id="a5949-177">Quando essa configuração estiver habilitada e configurada, o usuário não será mais direcionado para a página de logoff do Workplace.</span><span class="sxs-lookup"><span data-stu-id="a5949-177">When this setting is enabled and configured, the user is no longer directed to the Workplace sign-out page.</span></span> <span data-ttu-id="a5949-178">Em vez disso, ele será redirecionado para a URL que foi adicionada à configuração de redirecionamento de logoff SAML.</span><span class="sxs-lookup"><span data-stu-id="a5949-178">Instead, the user is redirected to the URL that was added in the SAML sign-out redirect setting.</span></span>


> [!TIP]
> <span data-ttu-id="a5949-179">Agora, é possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a5949-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app.</span></span> <span data-ttu-id="a5949-180">Depois de adicionar esse aplicativo da seção **Active Directory** > **Aplicativos Empresariais**, basta selecionar a guia **Logon Único** e acessar a documentação inserida na seção **Configuração**, na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="a5949-180">After adding this app from the **Active Directory** > **Enterprise Applications** section, simply select the **Single Sign-On** tab, and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a5949-181">Saiba mais sobre o recurso de documentação inserida na [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="a5949-181">You can read more about the embedded documentation feature in the [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="configure-reauthentication-frequency"></a><span data-ttu-id="a5949-182">Configurar a frequência de reautenticação</span><span class="sxs-lookup"><span data-stu-id="a5949-182">Configure reauthentication frequency</span></span>

<span data-ttu-id="a5949-183">É possível configurar o Workplace para solicitar uma verificação SAML todos os dias, a cada três dias, toda semana, a cada duas semanas, todos os meses ou nunca.</span><span class="sxs-lookup"><span data-stu-id="a5949-183">You can configure Workplace to prompt for a SAML check every day, three days, one week, two weeks, one month, or never.</span></span>

> [!NOTE] 
><span data-ttu-id="a5949-184">O valor mínimo para a verificação SAML em aplicativos móveis é definido como uma semana.</span><span class="sxs-lookup"><span data-stu-id="a5949-184">The minimum value for the SAML check on mobile applications is set to one week.</span></span>

<span data-ttu-id="a5949-185">Você também pode forçar uma redefinição de SAML para todos os usuários.</span><span class="sxs-lookup"><span data-stu-id="a5949-185">You can also force a SAML reset for all users.</span></span> <span data-ttu-id="a5949-186">Para fazer isso, use o botão **Exigir autenticação SAML para todos os usuários agora**.</span><span class="sxs-lookup"><span data-stu-id="a5949-186">To do this, use the **Require SAML authentication for all users now** button.</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a5949-187">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5949-187">Create an Azure AD test user</span></span>
<span data-ttu-id="a5949-188">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="a5949-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

1. <span data-ttu-id="a5949-190">No **Portal do Azure**, no painel esquerdo, selecione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a5949-190">In the **Azure portal**, in the left pane, select **Azure Active Directory**.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a5949-192">Para exibir a lista de usuários, acesse **Usuários e grupos** e selecione **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="a5949-192">To display the list of users, go to **Users and groups**, and select **All users**.</span></span>
    
    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a5949-194">Para abrir a caixa de diálogo **Usuário**, selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a5949-194">To open the **User** dialog box, select **Add**.</span></span>
 
    ![O botão Adicionar](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a5949-196">Na caixa de diálogo **Usuário**, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="a5949-196">In the **User** dialog box, do the following:</span></span>
 
    ![A caixa de diálogo Usuário](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a5949-198">a.</span><span class="sxs-lookup"><span data-stu-id="a5949-198">a.</span></span> <span data-ttu-id="a5949-199">Na caixa de texto **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="a5949-199">In the **Name** text box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a5949-200">b.</span><span class="sxs-lookup"><span data-stu-id="a5949-200">b.</span></span> <span data-ttu-id="a5949-201">Na caixa de texto **Nome de usuário**, digite o **endereço de email** de BrendaFernandes.</span><span class="sxs-lookup"><span data-stu-id="a5949-201">In the **User name** text box, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a5949-202">c.</span><span class="sxs-lookup"><span data-stu-id="a5949-202">c.</span></span> <span data-ttu-id="a5949-203">Selecione **Mostrar Senha** e tome nota.</span><span class="sxs-lookup"><span data-stu-id="a5949-203">Select **Show Password**, and write it down.</span></span>

    <span data-ttu-id="a5949-204">d.</span><span class="sxs-lookup"><span data-stu-id="a5949-204">d.</span></span> <span data-ttu-id="a5949-205">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a5949-205">Select **Create**.</span></span>
 
### <a name="create-a-workplace-by-facebook-test-user"></a><span data-ttu-id="a5949-206">Criar um usuário de teste do Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="a5949-206">Create a Workplace by Facebook test user</span></span>

<span data-ttu-id="a5949-207">Nesta seção, um usuário chamado Brenda Fernandes será criado no Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="a5949-207">In this section, a user called Britta Simon is created in Workplace by Facebook.</span></span> <span data-ttu-id="a5949-208">O Workplace by Facebook dá suporte ao provisionamento Just-In-Time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="a5949-208">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="a5949-209">Não há nenhuma ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="a5949-209">There is no action for you in this section.</span></span> <span data-ttu-id="a5949-210">Se um usuário ainda não existir no Workplace by Facebook, um novo será criado quando você tentar acessar o Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="a5949-210">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt to access Workplace by Facebook.</span></span>

>[!Note]
><span data-ttu-id="a5949-211">Se precisar criar um usuário manualmente, entre em contato com a [Equipe de suporte ao cliente do Workplace by Facebook](https://workplace.fb.com/faq/).</span><span class="sxs-lookup"><span data-stu-id="a5949-211">If you need to create a user manually, contact the [Workplace by Facebook Client support team](https://workplace.fb.com/faq/).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="a5949-212">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5949-212">Assign the Azure AD test user</span></span>

<span data-ttu-id="a5949-213">Nesta seção, você permitirá que Brenda Fernandes use o SSO do Azure concedendo acesso ao Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="a5949-213">In this section, you enable Britta Simon to use Azure SSO by granting access to Workplace by Facebook.</span></span>

![Atribuir usuário][200] 

1. <span data-ttu-id="a5949-215">No Portal do Azure, abra o modo de exibição de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="a5949-215">In the Azure portal, open the applications view.</span></span> <span data-ttu-id="a5949-216">Vá até o odo de exibição de diretório, vá até **Aplicativos empresariais** e, em seguida, selecione **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a5949-216">Go to the directory view, go to **Enterprise applications**, and then select **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="a5949-218">Na lista de aplicativos, selecione **Workplace by Facebook**.</span><span class="sxs-lookup"><span data-stu-id="a5949-218">In the applications list, select **Workplace by Facebook**.</span></span>

    ![O link Workplace by Facebook na lista Aplicativos](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_app.png) 

3. <span data-ttu-id="a5949-220">No menu à esquerda, selecione **Usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="a5949-220">In the menu on the left, select **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202] 

4. <span data-ttu-id="a5949-222">Selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a5949-222">Select **Add**.</span></span> <span data-ttu-id="a5949-223">Em seguida, no painel **Adicionar Atribuição**, selecione **Usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="a5949-223">Then, in the **Add Assignment** pane, select **Users and groups**.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="a5949-225">Na caixa de diálogo **Usuários e grupos**, selecione **Brenda Fernandes** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="a5949-225">In the **Users and groups** dialog box, select **Britta Simon** in the users list.</span></span>

6. <span data-ttu-id="a5949-226">Na caixa de diálogo **Usuários e grupos**, selecione **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="a5949-226">In the **Users and groups** dialog box, select **Select**.</span></span>

7. <span data-ttu-id="a5949-227">Na caixa de diálogo **Adicionar Atribuição**, selecione **Atribuir**.</span><span class="sxs-lookup"><span data-stu-id="a5949-227">In the **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a5949-228">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="a5949-228">Test single sign-on</span></span>

<span data-ttu-id="a5949-229">Se você quiser testar suas configurações de SSO, abra o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="a5949-229">If you want to test your SSO settings, open the Access Panel.</span></span>
<span data-ttu-id="a5949-230">Para saber mais, confira [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a5949-230">For more information, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="a5949-231">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a5949-231">Next steps</span></span>

* <span data-ttu-id="a5949-232">Consulte a [lista de tutoriais sobre como integrar aplicativos de SaaS ao Azure Active Directory](active-directory-saas-tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="a5949-232">See the [list of tutorials on how to integrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md).</span></span>
* <span data-ttu-id="a5949-233">Leia [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a5949-233">Read [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>
* <span data-ttu-id="a5949-234">Saiba mais sobre como [configurar o provisionamento de usuário](active-directory-saas-facebook-at-work-provisioning-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="a5949-234">Learn more about how to [configure user provisioning](active-directory-saas-facebook-at-work-provisioning-tutorial.md).</span></span>



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

