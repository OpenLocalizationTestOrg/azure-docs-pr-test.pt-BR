---
title: "Tutorial: Integração do Azure Active Directory ao vxMaintain | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o vxMaintain."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 841a1066-593c-4603-9abe-f48496d73d10
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: ad87534af448356b8cc80d8ddd278bfb8a9165e7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-vxmaintain"></a><span data-ttu-id="11b6f-103">Tutorial: Integração do Azure Active Directory ao vxMaintain</span><span class="sxs-lookup"><span data-stu-id="11b6f-103">Tutorial: Integrate Azure Active Directory with vxMaintain</span></span>

<span data-ttu-id="11b6f-104">Neste tutorial, você aprenderá a integrar o vxMaintain ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="11b6f-104">In this tutorial, you learn how to integrate vxMaintain with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="11b6f-105">Essa integração oferece vários benefícios importantes.</span><span class="sxs-lookup"><span data-stu-id="11b6f-105">This integration provides several important benefits.</span></span> <span data-ttu-id="11b6f-106">Você pode:</span><span class="sxs-lookup"><span data-stu-id="11b6f-106">You can:</span></span>

- <span data-ttu-id="11b6f-107">Controle no Azure AD quem tem acesso ao vxMaintain.</span><span class="sxs-lookup"><span data-stu-id="11b6f-107">Control in Azure AD who has access to vxMaintain.</span></span>
- <span data-ttu-id="11b6f-108">Permita que seus usuários façam logon automaticamente no vxMaintain com logon único (SSO) usando suas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="11b6f-108">Enable your users to automatically sign in to vxMaintain with single sign-on (SSO) by using their Azure AD accounts.</span></span>
- <span data-ttu-id="11b6f-109">Gerenciar suas contas em um local central: o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="11b6f-109">Manage your accounts in one central location: the Azure portal.</span></span>

<span data-ttu-id="11b6f-110">Para saber mais sobre a integração de aplicativos SaaS ao Azure AD, consulte [O que é o acesso de aplicativos e o logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="11b6f-110">To learn more about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="11b6f-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="11b6f-111">Prerequisites</span></span>

<span data-ttu-id="11b6f-112">Para configurar a integração do Azure AD ao vxMaintain, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="11b6f-112">To configure Azure AD integration with vxMaintain, you need the following items:</span></span>

- <span data-ttu-id="11b6f-113">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="11b6f-113">An Azure AD subscription</span></span>
- <span data-ttu-id="11b6f-114">Uma assinatura habilitada pelo SSO do vxMaintain</span><span class="sxs-lookup"><span data-stu-id="11b6f-114">A vxMaintain SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="11b6f-115">Ao testar as etapas deste tutorial, recomendamos que você não use um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="11b6f-115">When you test the steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="11b6f-116">Para testar as etapas neste tutorial, siga estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="11b6f-116">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="11b6f-117">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="11b6f-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="11b6f-118">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="11b6f-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="11b6f-119">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="11b6f-119">Scenario description</span></span>
<span data-ttu-id="11b6f-120">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="11b6f-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="11b6f-121">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="11b6f-121">The scenario that this tutorial outlines consists of two main building blocks:</span></span>

* <span data-ttu-id="11b6f-122">Adicionando vxMaintain da Galeria</span><span class="sxs-lookup"><span data-stu-id="11b6f-122">Adding vxMaintain from the gallery</span></span>
* <span data-ttu-id="11b6f-123">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="11b6f-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-vxmaintain-from-the-gallery"></a><span data-ttu-id="11b6f-124">Adicionar vxMaintain da galeria</span><span class="sxs-lookup"><span data-stu-id="11b6f-124">Add vxMaintain from the gallery</span></span>
<span data-ttu-id="11b6f-125">Para configurar a integração do vxMaintain com o Azure AD, você precisará adicionar o vxMaintain a partir da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="11b6f-125">To configure the integration of vxMaintain with Azure AD, you need to add vxMaintain from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="11b6f-126">Para adicionar o vxMaintain a partir da galeria, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="11b6f-126">To add vxMaintain from the gallery, do the following:</span></span>

1. <span data-ttu-id="11b6f-127">No [portal do Azure](https://portal.azure.com), no painel esquerdo, selecione o botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="11b6f-127">In the [Azure portal](https://portal.azure.com), in the left pane, select the **Azure Active Directory** button.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="11b6f-129">Selecione **Aplicativos empresariais** > **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="11b6f-129">Select **Enterprise applications** > **All applications**.</span></span>

    ![O painel “Aplicativos empresariais”][2]
    
3. <span data-ttu-id="11b6f-131">Para adicionar um aplicativo, na caixa de diálogo **Todos os aplicativos**, selecione **Novo aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="11b6f-131">To add an application, in the **All applications** dialog box, select **New application**.</span></span>

    ![O botão “Novo aplicativo”][3]

4. <span data-ttu-id="11b6f-133">Na caixa de pesquisa, digite **vxMaintain**.</span><span class="sxs-lookup"><span data-stu-id="11b6f-133">In the search box, type **vxMaintain**.</span></span>

    ![A lista suspensa "Modo Logon Único"](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_search.png)

5. <span data-ttu-id="11b6f-135">Na lista de resultados, selecione **vxMaintain**e, em seguida, selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="11b6f-135">In the results list, select **vxMaintain**, and then select **Add**.</span></span>

    ![O link do vxMaintain](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="11b6f-137">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="11b6f-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="11b6f-138">Nesta seção, você configurará e testará o SSO do Azure AD usando o vxMaintain, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="11b6f-138">In this section, you configure and test Azure AD SSO by using vxMaintain, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="11b6f-139">Para o SSO funcionar, o Azure AD precisa saber qual é o equivalente do usuário do Azure AD no vxMaintain.</span><span class="sxs-lookup"><span data-stu-id="11b6f-139">For SSO to work, Azure AD needs to know the vxMaintain counterpart to the Azure AD user.</span></span> <span data-ttu-id="11b6f-140">Ou seja, você deve estabelecer uma relação de link entre o usuário do Azure AD e o usuário vxMaintain correspondente.</span><span class="sxs-lookup"><span data-stu-id="11b6f-140">That is, you must establish a link relationship between the Azure AD user and the corresponding vxMaintain user.</span></span>

<span data-ttu-id="11b6f-141">Para estabelecer a relação de vínculo, atribua o valor **nome de usuário** do vxMaintain como o valor de **Nome do usuário** do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="11b6f-141">To establish the link relationship, assign the vxMaintain **user name** value as the Azure AD **Username** value.</span></span>

<span data-ttu-id="11b6f-142">Para configurar e testar o SSO do Azure AD usando o vxMaintain, você precisa concluir os seguintes blocos de construção.</span><span class="sxs-lookup"><span data-stu-id="11b6f-142">To configure and test Azure AD SSO by using vxMaintain, complete the following building blocks.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="11b6f-143">Configurar o SSO do Azure AD</span><span class="sxs-lookup"><span data-stu-id="11b6f-143">Configure Azure AD SSO</span></span>

<span data-ttu-id="11b6f-144">Nesta seção, você pode habilitar o SSO do Azure AD no portal do Azure e configurar o SSO em seu aplicativo vxMaintain fazendo seguinte:</span><span class="sxs-lookup"><span data-stu-id="11b6f-144">In this section, you can both enable Azure AD SSO in the Azure portal and configure SSO in your vxMaintain application by doing the following:</span></span>

1. <span data-ttu-id="11b6f-145">No Portal do Azure, na página de integração de aplicativos do **vxMaintain**, selecione **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="11b6f-145">In the Azure portal, on the **vxMaintain** application integration page, select **Single sign-on**.</span></span>

    ![O comando "Logon único"][4]

2. <span data-ttu-id="11b6f-147">Para habilitar o SSO, na lista suspensa **Modo de Logon Único**, selecione **Logon baseado em SAML**.</span><span class="sxs-lookup"><span data-stu-id="11b6f-147">To enable SSO, in the **Single Sign-on Mode** drop-down list, select **SAML-based Sign-on**.</span></span>
 
    ![O comando "Logon único baseado em SAML"](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_samlbase.png)

3. <span data-ttu-id="11b6f-149">Em **Domínio e URLs do vxMaintain**, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="11b6f-149">Under **vxMaintain Domain and URLs**, do the following:</span></span>

    ![Seção Domínio e URLs do vxMaintain](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_url.png)

    <span data-ttu-id="11b6f-151">a.</span><span class="sxs-lookup"><span data-stu-id="11b6f-151">a.</span></span> <span data-ttu-id="11b6f-152">Na caixa **Identificador**, digite uma URL com a seguinte sintaxe: `https://<company name>.verisae.com`</span><span class="sxs-lookup"><span data-stu-id="11b6f-152">In the **Identifier** box, type a URL that has the following syntax: `https://<company name>.verisae.com`</span></span>

    <span data-ttu-id="11b6f-153">b.</span><span class="sxs-lookup"><span data-stu-id="11b6f-153">b.</span></span> <span data-ttu-id="11b6f-154">Na caixa **URL de Resposta**, digite uma URL com a seguinte sintaxe: `https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`</span><span class="sxs-lookup"><span data-stu-id="11b6f-154">In the **Reply URL** box, type a URL that has the following syntax: `https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="11b6f-155">Os valores anteriores não são reais.</span><span class="sxs-lookup"><span data-stu-id="11b6f-155">The preceding values are not real.</span></span> <span data-ttu-id="11b6f-156">Atualize-os com o identificador e a URL de resposta reais.</span><span class="sxs-lookup"><span data-stu-id="11b6f-156">Update them with the actual identifier and reply URL.</span></span> <span data-ttu-id="11b6f-157">Para obter os valores, entre em contato com a [equipe de suporte do vxMaintain](http://www.verisae.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="11b6f-157">To obtain the values, contact the [vxMaintain support team](http://www.verisae.com/contact-us).</span></span>
 
4. <span data-ttu-id="11b6f-158">Em **Certificado de Autenticação SAML**, selecione **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="11b6f-158">Under **SAML Signing Certificate**, select **Metadata XML**, and then save the metadata file to your computer.</span></span>

    ![A seção “Certificado de Autenticação SAML”](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_certificate.png) 

5. <span data-ttu-id="11b6f-160">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="11b6f-160">Select **Save**.</span></span>

    ![O botão Salvar](./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="11b6f-162">Para configurar o SSO do **vxMaintain**, envie o arquivo de **Metadados XML** baixado para [a equipe de suporte do vxMaintain](http://www.verisae.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="11b6f-162">To configure **vxMaintain** SSO, send the downloaded **Metadata XML** file to the [vxMaintain support team](http://www.verisae.com/contact-us).</span></span>

> [!TIP]
> <span data-ttu-id="11b6f-163">Ao configurar o aplicativo, você pode ler as instruções anteriores em uma versão concisa no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="11b6f-163">As you set up the app, you can read a concise version of the preceding instructions in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="11b6f-164">Depois de adicionar o aplicativo na seção **Active Directory** > **Aplicativos Empresariais**, selecione a guia **Logon Único** e, depois, acesse a documentação inserida na seção **Configuração**.</span><span class="sxs-lookup"><span data-stu-id="11b6f-164">After you add the app from the **Active Directory** > **Enterprise Applications** section, select the **Single Sign-On** tab, and then access the embedded documentation from the **Configuration** section.</span></span> 
>
><span data-ttu-id="11b6f-165">Para saber mais sobre o recurso incorporado de documentação, consulte [Gerenciar logon único para aplicativos empresariais](https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="11b6f-165">To learn more about the embedded documentation feature, see [Managing single sign-on for enterprise apps](https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="11b6f-166">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="11b6f-166">Create an Azure AD test user</span></span>
<span data-ttu-id="11b6f-167">Nesta seção, você cria o usuário de teste Brenda Fernandes no portal do Azure fazendo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="11b6f-167">In this section, you create test user Britta Simon in the Azure portal by doing the following:</span></span>

![Usuário de teste do Azure AD][100]

1. <span data-ttu-id="11b6f-169">No **portal do Azure**, no painel esquerdo, selecione o botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="11b6f-169">In the **Azure portal**, in the left pane, select the **Azure Active Directory** button.</span></span>

    ![Botão "Azure Active Directory"](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="11b6f-171">Para exibir uma lista de usuários, vá para **Usuários e grupos** > **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="11b6f-171">To display a list of users, go to **Users and groups** > **All users**.</span></span>
    
    <span data-ttu-id="11b6f-172">![O link “Todos os usuários”](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)</span><span class="sxs-lookup"><span data-stu-id="11b6f-172">![The "All users" link](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)</span></span>  
    <span data-ttu-id="11b6f-173">A caixa de diálogo **Todos os usuários** é aberta.</span><span class="sxs-lookup"><span data-stu-id="11b6f-173">The **All users** dialog box opens.</span></span> 

3. <span data-ttu-id="11b6f-174">Para abrir a caixa de diálogo **Usuário**, selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="11b6f-174">To open the **User** dialog box, select **Add**.</span></span>
 
    ![O botão Adicionar](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="11b6f-176">Na caixa de diálogo **Usuário**, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="11b6f-176">In the **User** dialog box, do the following:</span></span>
 
    ![A caixa de diálogo Usuário](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="11b6f-178">a.</span><span class="sxs-lookup"><span data-stu-id="11b6f-178">a.</span></span> <span data-ttu-id="11b6f-179">Na caixa **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="11b6f-179">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="11b6f-180">b.</span><span class="sxs-lookup"><span data-stu-id="11b6f-180">b.</span></span> <span data-ttu-id="11b6f-181">Na caixa **Nome de usuário**, digite o endereço de email do usuário de teste Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="11b6f-181">In the **User name** box, type the email address of test user Britta Simon.</span></span>

    <span data-ttu-id="11b6f-182">c.</span><span class="sxs-lookup"><span data-stu-id="11b6f-182">c.</span></span> <span data-ttu-id="11b6f-183">Marque a caixa de seleção **Mostrar Senha** e anote o valor gerado na caixa **Senha**.</span><span class="sxs-lookup"><span data-stu-id="11b6f-183">Select the **Show Password** check box, and then note the value that was generated in the **Password** box.</span></span>

    <span data-ttu-id="11b6f-184">d.</span><span class="sxs-lookup"><span data-stu-id="11b6f-184">d.</span></span> <span data-ttu-id="11b6f-185">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="11b6f-185">Select **Create**.</span></span>
 
### <a name="create-a-vxmaintain-test-user"></a><span data-ttu-id="11b6f-186">Criar um usuário de teste vxMaintain</span><span class="sxs-lookup"><span data-stu-id="11b6f-186">Create a vxMaintain test user</span></span>

<span data-ttu-id="11b6f-187">Nesta seção, você cria a usuária de teste Brenda Fernandes no vxMaintain.</span><span class="sxs-lookup"><span data-stu-id="11b6f-187">In this section, you create test user Britta Simon in vxMaintain.</span></span> <span data-ttu-id="11b6f-188">Para adicionar os usuários na plataforma do vxMaintain, trabalhe com a [equipe de suporte do vxMaintain](http://www.verisae.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="11b6f-188">To add users in the vxMaintain platform, work with the [vxMaintain support team](http://www.verisae.com/contact-us).</span></span> <span data-ttu-id="11b6f-189">Antes de usar o SSO, crie e ative os usuários.</span><span class="sxs-lookup"><span data-stu-id="11b6f-189">Before you use SSO, create and activate the users.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="11b6f-190">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="11b6f-190">Assign the Azure AD test user</span></span>

<span data-ttu-id="11b6f-191">Nesta seção, você permitirá que o usuário de teste Brenda Fernandes use o SSO do Azure concedendo-lhe acesso ao vxMaintain.</span><span class="sxs-lookup"><span data-stu-id="11b6f-191">In this section, you enable test user Britta Simon to use Azure SSO by granting access to vxMaintain.</span></span> <span data-ttu-id="11b6f-192">Para fazer isso, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="11b6f-192">To do so, do the following:</span></span>

![Usuário de teste na Lista de Nomes de Exibição][200] 

1. <span data-ttu-id="11b6f-194">Na exibição de **Aplicativos** do portal do Azure, vá para a exibição de **Diretório** > **Aplicativos empresariais** > **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="11b6f-194">In the Azure portal **Applications** view, go to **Directory** view > **Enterprise applications** > **All applications**.</span></span>

    ![O link "Todos os aplicativos"][201] 

2. <span data-ttu-id="11b6f-196">Na lista de **Aplicativos**, selecione **vxMaintain**.</span><span class="sxs-lookup"><span data-stu-id="11b6f-196">In the **Applications** list, select **vxMaintain**.</span></span>

    ![O link do vxMaintain](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_app.png) 

3. <span data-ttu-id="11b6f-198">No painel esquerdo, selecione **Usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="11b6f-198">In the left pane, select **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202] 

4. <span data-ttu-id="11b6f-200">Selecione **Adicionar** e, em seguida, no painel **Adicionar Atribuição**, selecione **Usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="11b6f-200">Select **Add** and then, in the **Add Assignment** pane, select **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][203]

5. <span data-ttu-id="11b6f-202">Na caixa de diálogo **Usuários e grupos**, na lista **Usuários**, selecione **Brenda Fernandes** e, em seguida, selecione o botão **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="11b6f-202">In the **Users and groups** dialog box, in the **Users** list, select **Britta Simon**, and then select the **Select** button.</span></span>

7. <span data-ttu-id="11b6f-203">Na caixa de diálogo **Adicionar Atribuição**, selecione **Atribuir**.</span><span class="sxs-lookup"><span data-stu-id="11b6f-203">In the **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-your-azure-ad-single-sign-on"></a><span data-ttu-id="11b6f-204">Testar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="11b6f-204">Test your Azure AD single sign-on</span></span>

<span data-ttu-id="11b6f-205">Nesta seção, você testará sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="11b6f-205">In this section, you test your Azure AD SSO configuration by using the Access Panel.</span></span>

<span data-ttu-id="11b6f-206">Selecionar o bloco **vxMaintain** no Painel de Acesso deve fazer com que você entre automaticamente no seu aplicativo vxMaintain.</span><span class="sxs-lookup"><span data-stu-id="11b6f-206">Selecting the **vxMaintain** tile in the Access Panel should sign you in to your vxMaintain application automatically.</span></span>

<span data-ttu-id="11b6f-207">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="11b6f-207">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="11b6f-208">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="11b6f-208">Next steps</span></span>

* [<span data-ttu-id="11b6f-209">Lista de tutoriais sobre como integrar aplicativos SaaS com o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="11b6f-209">List of tutorials on integrating SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="11b6f-210">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="11b6f-210">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_203.png

