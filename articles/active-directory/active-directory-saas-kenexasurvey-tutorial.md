---
title: "Tutorial: Integração do Azure Active Directory com o IBM Kenexa Survey Enterprise | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o IBM Kenexa Survey Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c7aac6da-f4bf-419e-9e1a-16b460641a52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 5c276c23288292a1c54dd9d57177d5072b90c9e3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ibm-kenexa-survey-enterprise"></a><span data-ttu-id="943ae-103">Tutorial: Integração do Azure Active Directory com o IBM Kenexa Survey Enterprise</span><span class="sxs-lookup"><span data-stu-id="943ae-103">Tutorial: Azure Active Directory integration with IBM Kenexa Survey Enterprise</span></span>

<span data-ttu-id="943ae-104">Neste tutorial, você aprenderá como integrar o IBM Kenexa Survey Enterprise ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="943ae-104">In this tutorial, you learn how to integrate IBM Kenexa Survey Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="943ae-105">A integração do IBM Kenexa Survey Enterprise ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="943ae-105">Integrating IBM Kenexa Survey Enterprise with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="943ae-106">No Azure AD, é possível controlar quem tem acesso ao IBM Kenexa Survey Enterprise.</span><span class="sxs-lookup"><span data-stu-id="943ae-106">You can control in Azure AD who has access to IBM Kenexa Survey Enterprise.</span></span>
- <span data-ttu-id="943ae-107">É possível permitir que os usuários entrem automaticamente no IBM Kenexa Survey Enterprise com o logon único (SSO) com suas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="943ae-107">You can enable your users to automatically sign in to IBM Kenexa Survey Enterprise by using single sign-on (SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="943ae-108">Gerencie suas contas em um único local: o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="943ae-108">You can manage your accounts in one central location: the Azure portal.</span></span>

<span data-ttu-id="943ae-109">Se desejar saber mais sobre a integração de aplicativos SaaS (software como serviço) ao Azure AD, consulte [O que é o acesso do aplicativo e o logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="943ae-109">If you want to know more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="943ae-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="943ae-110">Prerequisites</span></span>

<span data-ttu-id="943ae-111">Para configurar a integração do Azure AD com o IBM Kenexa Survey Enterprise, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="943ae-111">To configure Azure AD integration with IBM Kenexa Survey Enterprise, you need the following items:</span></span>

- <span data-ttu-id="943ae-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="943ae-112">An Azure AD subscription</span></span>
- <span data-ttu-id="943ae-113">Uma assinatura habilitada para SSO do IBM Kenexa Survey Enterprise</span><span class="sxs-lookup"><span data-stu-id="943ae-113">An IBM Kenexa Survey Enterprise SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="943ae-114">Ao testar as etapas deste tutorial, recomendamos que você não use um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="943ae-114">When you test the steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="943ae-115">Para testar as etapas neste tutorial, siga estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="943ae-115">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="943ae-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="943ae-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="943ae-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="943ae-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="943ae-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="943ae-118">Scenario description</span></span>
<span data-ttu-id="943ae-119">Neste tutorial, você testa o SSO do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="943ae-119">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="943ae-120">O cenário descrito no tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="943ae-120">The scenario outlined in the tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="943ae-121">Adicionando o IBM Kenexa Survey Enterprise da galeria</span><span class="sxs-lookup"><span data-stu-id="943ae-121">Adding IBM Kenexa Survey Enterprise from the gallery</span></span>
* <span data-ttu-id="943ae-122">Configurar e testar o SSO do Azure AD</span><span class="sxs-lookup"><span data-stu-id="943ae-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-ibm-kenexa-survey-enterprise-from-the-gallery"></a><span data-ttu-id="943ae-123">Adicionar o IBM Kenexa Survey Enterprise por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="943ae-123">Add IBM Kenexa Survey Enterprise from the gallery</span></span>
<span data-ttu-id="943ae-124">Para configurar a integração do IBM Kenexa Survey Enterprise ao Azure AD, adicione o IBM Kenexa Survey Enterprise à lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="943ae-124">To configure the integration of IBM Kenexa Survey Enterprise into Azure AD, add IBM Kenexa Survey Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="943ae-125">Para adicionar o IBM Kenexa Survey Enterprise por meio da galeria, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="943ae-125">To add IBM Kenexa Survey Enterprise from the gallery, do the following:</span></span>

1. <span data-ttu-id="943ae-126">No [portal do Azure](https://portal.azure.com), no painel esquerdo, clique no botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="943ae-126">In the [Azure portal](https://portal.azure.com), in the left pane, click the **Azure Active Directory** button.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="943ae-128">Selecione **Aplicativos empresariais** e, em seguida, selecione **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="943ae-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="943ae-130">Para adicionar um aplicativo, clique no botão **Novo aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="943ae-130">To add an application, click the **New application** button.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="943ae-132">Na caixa de pesquisa, digite **IBM Kenexa Survey Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="943ae-132">In the search box, type **IBM Kenexa Survey Enterprise**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_search.png)

5. <span data-ttu-id="943ae-134">Na lista de resultados, selecione **IBM Kenexa Survey Enterprise** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="943ae-134">In the results list, select **IBM Kenexa Survey Enterprise**, and then click the **Add** button to add the application.</span></span>

    ![IBM Kenexa Survey Enterprise na lista de resultados](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="943ae-136">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="943ae-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="943ae-137">Nesta seção, você configura e testa o SSO do Azure AD com o IBM Kenexa Survey Enterprise, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="943ae-137">In this section, you configure and test Azure AD SSO with IBM Kenexa Survey Enterprise based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="943ae-138">Para que o SSO funcione, o Azure AD precisa identificar o usuário do IBM Kenexa Survey Enterprise que é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="943ae-138">For SSO to work, Azure AD needs to identify the IBM Kenexa Survey Enterprise user counterpart in Azure AD.</span></span> <span data-ttu-id="943ae-139">Em outras palavras, o Azure AD precisa estabelecer uma relação de vínculo entre um usuário do Azure AD e um usuário relacionado do IBM Kenexa Survey Enterprise.</span><span class="sxs-lookup"><span data-stu-id="943ae-139">In other words, Azure AD must establish a link relationship between an Azure AD user and a related user in IBM Kenexa Survey Enterprise.</span></span>

<span data-ttu-id="943ae-140">Para estabelecer a relação de vínculo, atribua o valor do **nome de usuário** no IBM Kenexa Survey Enterprise como o valor do **Nome de usuário** no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="943ae-140">To establish the link relationship, assign the value of the **user name** in IBM Kenexa Survey Enterprise as the value of the **Username** in Azure AD.</span></span>

<span data-ttu-id="943ae-141">Para configurar e testar o SSO do Azure AD com o IBM Kenexa Survey Enterprise, conclua os blocos de construção nas duas próximas seções.</span><span class="sxs-lookup"><span data-stu-id="943ae-141">To configure and test Azure AD SSO with IBM Kenexa Survey Enterprise, complete the building blocks in the next two sections.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="943ae-142">Configurar o SSO do Azure AD</span><span class="sxs-lookup"><span data-stu-id="943ae-142">Configure Azure AD SSO</span></span>

<span data-ttu-id="943ae-143">Nesta seção, você habilita o SSO do Azure AD no portal do Azure e configura o SSO no aplicativo IBM Kenexa Survey Enterprise fazendo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="943ae-143">In this section, you enable Azure AD SSO in the Azure portal and configure SSO in your IBM Kenexa Survey Enterprise application by doing the following:</span></span>

1. <span data-ttu-id="943ae-144">No portal do Azure, na página de integração do aplicativo **IBM Kenexa Survey Enterprise**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="943ae-144">In the Azure portal, on the **IBM Kenexa Survey Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único do IBM Kenexa Survey Enterprise][4]

2. <span data-ttu-id="943ae-146">Na caixa de diálogo **Logon único**, na caixa **Modo**, selecione **Logon baseado em SAML** para habilitar o SSO.</span><span class="sxs-lookup"><span data-stu-id="943ae-146">In the **Single sign-on** dialog box, in the **Mode** box, select **SAML-based Sign-on** to enable SSO.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_samlbase.png)

3. <span data-ttu-id="943ae-148">Na seção **Domínio e URLs do IBM Kenexa Survey Enterprise**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="943ae-148">In the **IBM Kenexa Survey Enterprise Domain and URLs** section, perform the following steps:</span></span>

    ![Informações de logon único em Domínio e URLs do IBM Kenexa Survey Enterprise](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_url.png)

    <span data-ttu-id="943ae-150">a.</span><span class="sxs-lookup"><span data-stu-id="943ae-150">a.</span></span> <span data-ttu-id="943ae-151">Na caixa de texto **Identificador**, digite uma URL com o seguinte padrão: `https://surveys.kenexa.com/<companycode>`</span><span class="sxs-lookup"><span data-stu-id="943ae-151">In the **Identifier** textbox, type a URL with the following pattern: `https://surveys.kenexa.com/<companycode>`</span></span>

    <span data-ttu-id="943ae-152">b.</span><span class="sxs-lookup"><span data-stu-id="943ae-152">b.</span></span> <span data-ttu-id="943ae-153">Na caixa de texto **URL de Resposta**, digite uma URL com o seguinte padrão: `https://surveys.kenexa.com/<companycode>/tools/sso.asp`</span><span class="sxs-lookup"><span data-stu-id="943ae-153">In the **Reply URL** textbox, type a URL with the following pattern: `https://surveys.kenexa.com/<companycode>/tools/sso.asp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="943ae-154">Os valores anteriores não são reais.</span><span class="sxs-lookup"><span data-stu-id="943ae-154">The preceding values are not real.</span></span> <span data-ttu-id="943ae-155">Atualize-os com o identificador e a URL de resposta reais.</span><span class="sxs-lookup"><span data-stu-id="943ae-155">Update them with the actual identifier and reply URL.</span></span> <span data-ttu-id="943ae-156">Para obter os valores reais, contate a [equipe de suporte do IBM Kenexa Survey Enterprise](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="943ae-156">To obtain the actual values, contact the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span>

4. <span data-ttu-id="943ae-157">Em **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo de certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="943ae-157">Under **SAML Signing Certificate**, click **Certificate (Base64)**, and then save the certificate file to your computer.</span></span>

    ![O link de download do Certificado (Base64)](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_certificate.png) 

    <span data-ttu-id="943ae-159">O aplicativo IBM Kenexa Survey Enterprise espera receber as declarações SAML (Security Assertions Markup Language) em um formato específico, o que exige a adição de mapeamentos de atributo personalizados para a configuração dos atributos do token SAML.</span><span class="sxs-lookup"><span data-stu-id="943ae-159">The IBM Kenexa Survey Enterprise application expects to receive the Security Assertions Markup Language (SAML) assertions in a specific format, which requires you to add custom attribute mappings to the configuration of your SAML token attributes.</span></span> <span data-ttu-id="943ae-160">O valor da declaração do identificador de usuário na resposta deve corresponder à ID de SSO configurada no sistema do Kenexa.</span><span class="sxs-lookup"><span data-stu-id="943ae-160">The value of the user-identifier claim in the response must match the SSO ID that's configured in the Kenexa system.</span></span> <span data-ttu-id="943ae-161">Para mapear o identificador de usuário apropriado em sua organização como o protocolo IDP de SSO, trabalhe com a [equipe de suporte do IBM Kenexa Survey Enterprise](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="943ae-161">To map the appropriate user identifier in your organization as SSO Internet Datagram Protocol (IDP), work with the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span> 

    <span data-ttu-id="943ae-162">Por padrão, o Azure AD define o identificador de usuário como o valor de nome UPN.</span><span class="sxs-lookup"><span data-stu-id="943ae-162">By default, Azure AD sets the user identifier as the user principal name (UPN) value.</span></span> <span data-ttu-id="943ae-163">Altere esse valor na guia **Atributo**, conforme mostrado na captura de tela a seguir.</span><span class="sxs-lookup"><span data-stu-id="943ae-163">You can change this value on the **Attribute** tab, as shown in the following screenshot.</span></span> <span data-ttu-id="943ae-164">A integração funciona somente após a conclusão correta do mapeamento.</span><span class="sxs-lookup"><span data-stu-id="943ae-164">The integration works only after you've completed the mapping correctly.</span></span>
    
    ![A caixa de diálogo Atributos de Usuário](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_attribute.png)   

5. <span data-ttu-id="943ae-166">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="943ae-166">Click **Save**.</span></span>

    ![O botão Salvar de Configurar Logon Único](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="943ae-168">Para abrir a janela **Configurar logon**, em **Configuração do IBM Kenexa Survey Enterprise**, clique em **Configurar o IBM Kenexa Survey Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="943ae-168">To open the **Configure sign-on** window, under **IBM Kenexa Survey Enterprise Configuration**, click **Configure IBM Kenexa Survey Enterprise**.</span></span> 
 
    ![O link Configurar o IBM Kenexa Survey Enterprise](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_configure.png)

7. <span data-ttu-id="943ae-170">Copie os valores da **URL de Saída**, **ID da Entidade SAML** e **URL do Serviço de logon único SAML** da seção **Referência Rápida**.</span><span class="sxs-lookup"><span data-stu-id="943ae-170">Copy the **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values from the **Quick Reference** section.</span></span>

8. <span data-ttu-id="943ae-171">Na janela **Configurar logon**, em **Referência Rápida**, copie os valores da **URL de Saída**, da **ID da Entidade SAML** e da **URL do Serviço de Logon Único SAML**.</span><span class="sxs-lookup"><span data-stu-id="943ae-171">In the **Configure sign-on** window, under **Quick Reference**, copy the **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values.</span></span>

9. <span data-ttu-id="943ae-172">Para configurar o SSO no lado do **IBM Kenexa Survey Enterprise**, envie o **Certificado (Base64)** baixado, a **URL de Saída**, a **ID da Entidade SAML** e a **URL do Serviço de Logon Único SAML** para a [equipe de suporte do IBM Kenexa Survey Enterprise](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="943ae-172">To configure SSO on the **IBM Kenexa Survey Enterprise** side, send the downloaded **Certificate (Base64)**, **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values to the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span>

> [!TIP]
> <span data-ttu-id="943ae-173">Consulte uma versão concisa dessas instruções no [portal do Azure](https://portal.azure.com) enquanto estiver configurando o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="943ae-173">You can refer to a concise version of these instructions in the [Azure portal](https://portal.azure.com) while you are setting up the app.</span></span> <span data-ttu-id="943ae-174">Depois de adicionar o aplicativo na seção **Active Directory** > **Aplicativos Empresariais**, basta clicar na guia **Logon único** e, depois, acessar a documentação inserida por meio da seção **Configuração** ao final.</span><span class="sxs-lookup"><span data-stu-id="943ae-174">After you add the app from the **Active Directory** > **Enterprise Applications** section, simply click the **single sign-on** tab, and then access the embedded documentation through the **Configuration** section at the end.</span></span> <span data-ttu-id="943ae-175">Para saber mais sobre o recurso de documentação inserida, consulte [Documentação inserida do Azure AD](https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="943ae-175">To learn more about the embedded documentation feature, see [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="943ae-176">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="943ae-176">Create an Azure AD test user</span></span>
<span data-ttu-id="943ae-177">Nesta seção, você cria o usuário de teste Brenda Fernandes no portal do Azure fazendo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="943ae-177">In this section, you create test user Britta Simon in the Azure portal by doing the following:</span></span>

![Criar um usuário de teste do Azure AD][100]

1. <span data-ttu-id="943ae-179">No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="943ae-179">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="943ae-181">Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="943ae-181">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>
    
    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="943ae-183">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.</span><span class="sxs-lookup"><span data-stu-id="943ae-183">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>
 
    ![O botão Adicionar](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="943ae-185">Na caixa de diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="943ae-185">In the **User** dialog box, perform the following steps:</span></span>
 
    ![A caixa de diálogo Usuário](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="943ae-187">a.</span><span class="sxs-lookup"><span data-stu-id="943ae-187">a.</span></span> <span data-ttu-id="943ae-188">Na caixa **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="943ae-188">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="943ae-189">b.</span><span class="sxs-lookup"><span data-stu-id="943ae-189">b.</span></span> <span data-ttu-id="943ae-190">Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="943ae-190">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="943ae-191">c.</span><span class="sxs-lookup"><span data-stu-id="943ae-191">c.</span></span> <span data-ttu-id="943ae-192">Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.</span><span class="sxs-lookup"><span data-stu-id="943ae-192">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="943ae-193">d.</span><span class="sxs-lookup"><span data-stu-id="943ae-193">d.</span></span> <span data-ttu-id="943ae-194">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="943ae-194">Click **Create**.</span></span>
 
### <a name="create-an-ibm-kenexa-survey-enterprise-test-user"></a><span data-ttu-id="943ae-195">Criar um usuário de teste do IBM Kenexa Survey Enterprise</span><span class="sxs-lookup"><span data-stu-id="943ae-195">Create an IBM Kenexa Survey Enterprise test user</span></span>

<span data-ttu-id="943ae-196">Nesta seção, você criará uma usuária chamada Brenda Fernandes no IBM Kenexa Survey Enterprise.</span><span class="sxs-lookup"><span data-stu-id="943ae-196">In this section, you create a user called Britta Simon in IBM Kenexa Survey Enterprise.</span></span> 

<span data-ttu-id="943ae-197">Para criar usuários no sistema do IBM Kenexa Survey Enterprise e mapear a ID de SSO para eles, trabalhe com a [equipe de suporte do IBM Kenexa Survey Enterprise](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="943ae-197">To create users in the IBM Kenexa Survey Enterprise system and map the SSO ID for them, you can work with the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span> <span data-ttu-id="943ae-198">Esse valor de ID de SSO também deve ser mapeado para o valor de identificador de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="943ae-198">This SSO ID value should also be mapped to the user identifier value from Azure AD.</span></span> <span data-ttu-id="943ae-199">Altere essa configuração padrão na guia **Atributo**.</span><span class="sxs-lookup"><span data-stu-id="943ae-199">You can change this default setting on the **Attribute** tab.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="943ae-200">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="943ae-200">Assign the Azure AD test user</span></span>

<span data-ttu-id="943ae-201">Nesta seção, você permite que o usuário Brenda Fernandes use o SSO do Azure concedendo acesso ao IBM Kenexa Survey Enterprise.</span><span class="sxs-lookup"><span data-stu-id="943ae-201">In this section, you enable user Britta Simon to use Azure SSO by granting access to IBM Kenexa Survey Enterprise.</span></span>

![Atribuir a função de usuário][200] 

<span data-ttu-id="943ae-203">Para atribuir o usuário Brenda Fernandes ao IBM Kenexa Survey Enterprise, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="943ae-203">To assign user Britta Simon to IBM Kenexa Survey Enterprise, do the following:</span></span>

1. <span data-ttu-id="943ae-204">No portal do Azure, abra a exibição **Aplicativos**, acesse a exibição **Diretório**, selecione **Aplicativos empresariais** e, depois, clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="943ae-204">In the Azure portal, open the **Applications** view, go to the **Directory** view, select **Enterprise applications**, and then click **All applications**.</span></span>

    ![Os links “Aplicativos empresariais” e “Todos os aplicativos”][201] 

2. <span data-ttu-id="943ae-206">Na lista **Aplicativos**, selecione **IBM Kenexa Survey Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="943ae-206">In the **Applications** list, select **IBM Kenexa Survey Enterprise**.</span></span>

    ![O link do IBM Kenexa Survey Enterprise na lista de Aplicativos](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_app.png) 

3. <span data-ttu-id="943ae-208">No painel esquerdo, clique em **Usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="943ae-208">In the left pane, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202] 

4. <span data-ttu-id="943ae-210">Clique no botão **Adicionar** e, em seguida, no painel **Adicionar Atribuição**, selecione **Usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="943ae-210">Click the **Add** button and then, in the **Add Assignment** pane, select **Users and groups**.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="943ae-212">Na caixa de diálogo **Usuários e grupos**, na lista **Usuários**, selecione **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="943ae-212">In the **Users and groups** dialog box, in the **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="943ae-213">Na caixa de diálogo **Usuários e grupos**, clique no botão **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="943ae-213">In the **Users and groups** dialog box, click the **Select** button.</span></span>

7. <span data-ttu-id="943ae-214">Na caixa de diálogo **Adicionar Atribuição**, clique no botão **Atribuir**.</span><span class="sxs-lookup"><span data-stu-id="943ae-214">In the **Add Assignment** dialog box, click the **Assign** button.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="943ae-215">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="943ae-215">Test single sign-on</span></span>

<span data-ttu-id="943ae-216">Nesta seção, você testará sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="943ae-216">In this section, you test your Azure AD SSO configuration by using the Access Panel.</span></span>

<span data-ttu-id="943ae-217">Quando você clicar no bloco do **IBM Kenexa Survey Enterprise** no Painel de Acesso, deverá ser conectado automaticamente ao aplicativo IBM Kenexa Survey Enterprise.</span><span class="sxs-lookup"><span data-stu-id="943ae-217">When you click the **IBM Kenexa Survey Enterprise** tile in the Access Panel, you should be automatically signed in to your IBM Kenexa Survey Enterprise application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="943ae-218">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="943ae-218">Additional resources</span></span>

* [<span data-ttu-id="943ae-219">Lista de tutoriais sobre como integrar aplicativos SaaS ao Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="943ae-219">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="943ae-220">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="943ae-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_203.png

 
