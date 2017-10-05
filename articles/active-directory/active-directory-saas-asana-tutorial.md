---
title: "Tutorial: Integração do Azure Active Directory ao Asana | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Asana."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 837e38fe-8f55-475c-87f4-6394dc1fee2b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: jeedes
ms.openlocfilehash: a2f0cecb93cc382bcfd710c44eb70f80ae67f9b6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asana"></a><span data-ttu-id="17131-103">Tutorial: Integração do Azure Active Directory ao Asana</span><span class="sxs-lookup"><span data-stu-id="17131-103">Tutorial: Azure Active Directory integration with Asana</span></span>

<span data-ttu-id="17131-104">Neste tutorial, você aprenderá a integrar o Asana ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="17131-104">In this tutorial, you learn how to integrate Asana with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="17131-105">A integração do Asana ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="17131-105">Integrating Asana with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="17131-106">Você pode controlar no Azure AD quem terá acesso ao Asana</span><span class="sxs-lookup"><span data-stu-id="17131-106">You can control in Azure AD who has access to Asana</span></span>
- <span data-ttu-id="17131-107">Você pode permitir que seus usuários faça logon automaticamente no Asana (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="17131-107">You can enable your users to automatically get signed-on to Asana (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="17131-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="17131-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="17131-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="17131-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="17131-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="17131-110">Prerequisites</span></span>

<span data-ttu-id="17131-111">Para configurar a integração do Azure AD ao Asana, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="17131-111">To configure Azure AD integration with Asana, you need the following items:</span></span>

- <span data-ttu-id="17131-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="17131-112">An Azure AD subscription</span></span>
- <span data-ttu-id="17131-113">Uma assinatura habilitada para logon único do Asana</span><span class="sxs-lookup"><span data-stu-id="17131-113">An Asana single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="17131-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="17131-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="17131-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="17131-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="17131-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="17131-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="17131-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="17131-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="17131-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="17131-118">Scenario description</span></span>
<span data-ttu-id="17131-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="17131-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="17131-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="17131-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="17131-121">Adicionando Asana da galeria</span><span class="sxs-lookup"><span data-stu-id="17131-121">Adding Asana from the gallery</span></span>
2. <span data-ttu-id="17131-122">configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="17131-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-asana-from-the-gallery"></a><span data-ttu-id="17131-123">Adicionando Asana da galeria</span><span class="sxs-lookup"><span data-stu-id="17131-123">Adding Asana from the gallery</span></span>
<span data-ttu-id="17131-124">Para configurar a integração do Asana ao Azure AD, você precisará adicionar o Asana da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="17131-124">To configure the integration of Asana into Azure AD, you need to add Asana from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="17131-125">**Para adicionar o Asana da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="17131-125">**To add Asana from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="17131-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="17131-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="17131-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="17131-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="17131-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="17131-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="17131-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="17131-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="17131-133">Na caixa de pesquisa, digite **Asana**, selecione **Asana** no painel de resultados e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="17131-133">In the search box, type **Asana**, select **Asana** from result panel then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-asana-tutorial/tutorial_asana_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="17131-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="17131-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="17131-136">Nesta seção, você configura e testa o logon único do Azure AD com o Asana, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="17131-136">In this section, you configure and test Azure AD single sign-on with Asana based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="17131-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Asana é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="17131-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Asana is to a user in Azure AD.</span></span> <span data-ttu-id="17131-138">Em outras palavras, é necessário estabelecer uma relação de vinculação entre um usuário do Azure AD e o usuário relacionado do Asana.</span><span class="sxs-lookup"><span data-stu-id="17131-138">In other words, a link relationship between an Azure AD user and the related user in Asana needs to be established.</span></span>

<span data-ttu-id="17131-139">No Asana, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="17131-139">In Asana, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="17131-140">Para configurar e testar o logon único do Azure AD com o Asana, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="17131-140">To configure and test Azure AD single sign-on with Asana, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="17131-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="17131-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="17131-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="17131-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="17131-143">**[Criar um usuário de teste do Asana](#create-an-asana-test-user)** – para ter um equivalente de Brenda Fernandes no Asana que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="17131-143">**[Create an Asana test user](#create-an-asana-test-user)** - to have a counterpart of Britta Simon in Asana that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="17131-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="17131-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="17131-145">**[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="17131-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="17131-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="17131-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="17131-147">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Asana.</span><span class="sxs-lookup"><span data-stu-id="17131-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Asana application.</span></span>

<span data-ttu-id="17131-148">**Para configurar o logon único do Azure AD com o Asana, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="17131-148">**To configure Azure AD single sign-on with Asana, perform the following steps:**</span></span>

1. <span data-ttu-id="17131-149">No portal do Azure, na página de integração do aplicativo do **Asana**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="17131-149">In the Azure portal, on the **Asana** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="17131-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="17131-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-asana-tutorial/tutorial_asana_samlbase.png)

3. <span data-ttu-id="17131-153">Na seção **Domínio e URLs do Asana**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="17131-153">On the **Asana Domain and URLs** section, perform the following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do Asana](./media/active-directory-saas-asana-tutorial/tutorial_asana_url.png)

    <span data-ttu-id="17131-155">a.</span><span class="sxs-lookup"><span data-stu-id="17131-155">a.</span></span> <span data-ttu-id="17131-156">Na caixa de texto **URL de Logon**, digite a URL: `https://app.asana.com/`</span><span class="sxs-lookup"><span data-stu-id="17131-156">In the **Sign-on URL** textbox, type URL: `https://app.asana.com/`</span></span>

    <span data-ttu-id="17131-157">b.</span><span class="sxs-lookup"><span data-stu-id="17131-157">b.</span></span> <span data-ttu-id="17131-158">Na caixa de texto **Identificador**, digite o valor: `https://app.asana.com/`</span><span class="sxs-lookup"><span data-stu-id="17131-158">In the **Identifier** textbox, type value: `https://app.asana.com/`</span></span>
 
4. <span data-ttu-id="17131-159">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="17131-159">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-asana-tutorial/tutorial_asana_certificate.png)
    
5. <span data-ttu-id="17131-161">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="17131-161">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-asana-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="17131-163">Na seção **Configuração do Asana**, clique em **Configurar o Asana** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="17131-163">On the **Asana Configuration** section, click **Configure Asana** to open **Configure sign-on** window.</span></span> <span data-ttu-id="17131-164">Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="17131-164">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuração do Asana](./media/active-directory-saas-asana-tutorial/tutorial_asana_configure.png) 

7. <span data-ttu-id="17131-166">Em uma janela de navegador diferente, entre em seu aplicativo Asana.</span><span class="sxs-lookup"><span data-stu-id="17131-166">In a different browser window, sign-on to your Asana application.</span></span> <span data-ttu-id="17131-167">Para configurar o SSO no Asana, acesse as configurações de espaço de trabalho clicando no nome do espaço de trabalho no canto superior direito da tela.</span><span class="sxs-lookup"><span data-stu-id="17131-167">To configure SSO in Asana, access the workspace settings by clicking the workspace name on the top right corner of the screen.</span></span> <span data-ttu-id="17131-168">Em seguida, clique em **\<nome do espaço de trabalho\>Configurações**.</span><span class="sxs-lookup"><span data-stu-id="17131-168">Then, click on **\<your workspace name\> Settings**.</span></span> 
   
    ![configurações de sso do Asana](./media/active-directory-saas-asana-tutorial/tutorial_asana_09.png)

8. <span data-ttu-id="17131-170">Na janela **Configurações da organização**, clique em **Administração**.</span><span class="sxs-lookup"><span data-stu-id="17131-170">On the **Organization settings** window, click **Administration**.</span></span> <span data-ttu-id="17131-171">Em seguida, clique em **Os membros devem fazer logon por meio de SAML** para habilitar a configuração de SSO.</span><span class="sxs-lookup"><span data-stu-id="17131-171">Then, click **Members must log in via SAML** to enable the SSO configuration.</span></span> <span data-ttu-id="17131-172">Execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="17131-172">The perform the following steps:</span></span>
   
    ![Definições de Configurar Organização de Logon Único](./media/active-directory-saas-asana-tutorial/tutorial_asana_10.png)  

     <span data-ttu-id="17131-174">a.</span><span class="sxs-lookup"><span data-stu-id="17131-174">a.</span></span> <span data-ttu-id="17131-175">Na caixa de texto **URL da página de entrada**, cole a **URL do Serviço de Logon Único SAML**.</span><span class="sxs-lookup"><span data-stu-id="17131-175">In the **Sign-in page URL** textbox, paste the **SAML Single Sign-On Service URL**.</span></span>

     <span data-ttu-id="17131-176">b.</span><span class="sxs-lookup"><span data-stu-id="17131-176">b.</span></span> <span data-ttu-id="17131-177">Clique com o botão direito do mouse no certificado baixado no portal do Azure e, em seguida, abra o arquivo de certificado usando o Bloco de notas ou seu editor de texto preferido.</span><span class="sxs-lookup"><span data-stu-id="17131-177">Right click the certificate downloaded from Azure portal, then open the certificate file using Notepad or your preferred text editor.</span></span> <span data-ttu-id="17131-178">Copie o conteúdo entre o início e o final do título do certificado e cole-o na caixa de texto **Certificado X.509**.</span><span class="sxs-lookup"><span data-stu-id="17131-178">Copy the content between the begin and the end certificate title and paste it in the **X.509 Certificate** textbox.</span></span>

9. <span data-ttu-id="17131-179">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="17131-179">Click **Save**.</span></span> <span data-ttu-id="17131-180">Vá para [Guia do Asana para configurar SSO](https://asana.com/guide/help/premium/authentication#gl-saml) se precisar de assistência adicional.</span><span class="sxs-lookup"><span data-stu-id="17131-180">Go to [Asana guide for setting up SSO](https://asana.com/guide/help/premium/authentication#gl-saml) if you need further assistance.</span></span>

> [!TIP]
> <span data-ttu-id="17131-181">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="17131-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="17131-182">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="17131-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="17131-183">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="17131-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="17131-184">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="17131-184">Create an Azure AD test user</span></span>

<span data-ttu-id="17131-185">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="17131-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="17131-187">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="17131-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="17131-188">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="17131-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-asana-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="17131-190">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="17131-190">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-asana-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="17131-192">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="17131-192">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-asana-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="17131-194">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="17131-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![O botão Adicionar](./media/active-directory-saas-asana-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="17131-196">a.</span><span class="sxs-lookup"><span data-stu-id="17131-196">a.</span></span> <span data-ttu-id="17131-197">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="17131-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="17131-198">b.</span><span class="sxs-lookup"><span data-stu-id="17131-198">b.</span></span> <span data-ttu-id="17131-199">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="17131-199">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="17131-200">c.</span><span class="sxs-lookup"><span data-stu-id="17131-200">c.</span></span> <span data-ttu-id="17131-201">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="17131-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="17131-202">d.</span><span class="sxs-lookup"><span data-stu-id="17131-202">d.</span></span> <span data-ttu-id="17131-203">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="17131-203">Click **Create**.</span></span>
 
### <a name="create-an-asana-test-user"></a><span data-ttu-id="17131-204">Criar um usuário de teste do Asana</span><span class="sxs-lookup"><span data-stu-id="17131-204">Create an Asana test user</span></span>

<span data-ttu-id="17131-205">Nesta seção, você criará uma usuária chamada Brenda Fernandes no Asana.</span><span class="sxs-lookup"><span data-stu-id="17131-205">In this section, you create a user called Britta Simon in Asana.</span></span>

1. <span data-ttu-id="17131-206">No **Asana**, vá para a seção **Equipes** no painel esquerdo.</span><span class="sxs-lookup"><span data-stu-id="17131-206">On **Asana**, go to the **Teams** section on the left panel.</span></span> <span data-ttu-id="17131-207">Clique no botão de sinal de adição.</span><span class="sxs-lookup"><span data-stu-id="17131-207">Click the plus sign button.</span></span> 
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-asana-tutorial/tutorial_asana_12.png) 

2. <span data-ttu-id="17131-209">Digite o email britta.simon@contoso.com na caixa de texto e selecione **Convidar**.</span><span class="sxs-lookup"><span data-stu-id="17131-209">Type the email britta.simon@contoso.com in the text box and then select **Invite**.</span></span>

3. <span data-ttu-id="17131-210">Clique em **Enviar Convite**.</span><span class="sxs-lookup"><span data-stu-id="17131-210">Click **Send Invite**.</span></span> <span data-ttu-id="17131-211">A nova usuária receberá um email em sua conta de email.</span><span class="sxs-lookup"><span data-stu-id="17131-211">The new user will receive an email into her email account.</span></span> <span data-ttu-id="17131-212">Ela precisará criar e validar a conta.</span><span class="sxs-lookup"><span data-stu-id="17131-212">She will need to create and validate the account.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="17131-213">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="17131-213">Assign the Azure AD test user</span></span>

<span data-ttu-id="17131-214">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Asana.</span><span class="sxs-lookup"><span data-stu-id="17131-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Asana.</span></span>

![Atribuir a função de usuário][200]

<span data-ttu-id="17131-216">**Para atribuir Brenda Fernandes ao Asana, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="17131-216">**To assign Britta Simon to Asana, perform the following steps:**</span></span>

1. <span data-ttu-id="17131-217">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="17131-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="17131-219">Na lista de aplicativos, escolha **Asana**.</span><span class="sxs-lookup"><span data-stu-id="17131-219">In the applications list, select **Asana**.</span></span>

    ![O link do Asana na lista de Aplicativos](./media/active-directory-saas-asana-tutorial/tutorial_asana_app.png) 

3. <span data-ttu-id="17131-221">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="17131-221">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202]

4. <span data-ttu-id="17131-223">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="17131-223">Click **Add** button.</span></span> <span data-ttu-id="17131-224">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="17131-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="17131-226">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="17131-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="17131-227">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="17131-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="17131-228">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="17131-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="17131-229">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="17131-229">Test single sign-on</span></span>

<span data-ttu-id="17131-230">O objetivo desta seção é testar o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="17131-230">The objective of this section is to test your Azure AD single sign-on.</span></span>

<span data-ttu-id="17131-231">Vá para a página de logon do Asana.</span><span class="sxs-lookup"><span data-stu-id="17131-231">Go to Asana login page.</span></span> <span data-ttu-id="17131-232">Na caixa de texto Endereço de email, insira o endereço de email britta.simon@contoso.com. Deixe a caixa de texto de senha em branco e clique em **Fazer Logon**.</span><span class="sxs-lookup"><span data-stu-id="17131-232">In the Email address textbox, insert the email address britta.simon@contoso.com. Leave the password textbox in blank and then click **Log In**.</span></span> <span data-ttu-id="17131-233">Você será redirecionado à página de logon do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="17131-233">You will be redirected to Azure AD login page.</span></span> <span data-ttu-id="17131-234">Preencha suas credenciais do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="17131-234">Complete your Azure AD credentials.</span></span> <span data-ttu-id="17131-235">Agora, você está conectado ao Asana.</span><span class="sxs-lookup"><span data-stu-id="17131-235">Now, you are logged in on Asana.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="17131-236">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="17131-236">Additional resources</span></span>

* [<span data-ttu-id="17131-237">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="17131-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="17131-238">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="17131-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-asana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-asana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-asana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-asana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-asana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-asana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-asana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-asana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-asana-tutorial/tutorial_general_203.png
[10]: ./media/active-directory-saas-asana-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-asana-tutorial/tutorial_general_070.png
