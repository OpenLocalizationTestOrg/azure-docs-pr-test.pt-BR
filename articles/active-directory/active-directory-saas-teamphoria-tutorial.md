---
title: "Tutorial: integração do Azure Active Directory com o Teamphoria | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Teamphoria."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d569c705-6f0f-4ec1-b485-ba82526b5d32
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: 2a35efb04d7fe22abc6894c149caf090666ce016
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamphoria"></a><span data-ttu-id="3769a-103">Tutorial: integração do Azure Active Directory ao Teamphoria</span><span class="sxs-lookup"><span data-stu-id="3769a-103">Tutorial: Azure Active Directory integration with Teamphoria</span></span>

<span data-ttu-id="3769a-104">Neste tutorial, você aprenderá a integrar o Teamphoria ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="3769a-104">In this tutorial, you learn how to integrate Teamphoria with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3769a-105">A integração do Teamphoria com o Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="3769a-105">Integrating Teamphoria with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3769a-106">No Azure AD, é possível controlar quem tem acesso ao Teamphoria</span><span class="sxs-lookup"><span data-stu-id="3769a-106">You can control in Azure AD who has access to Teamphoria</span></span>
- <span data-ttu-id="3769a-107">É possível permitir que seus usuários façam logon automaticamente no Teamphoria (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3769a-107">You can enable your users to automatically get signed-on to Teamphoria (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3769a-108">Você pode gerenciar suas contas em um único local - o portal de Gerenciamento do Azure</span><span class="sxs-lookup"><span data-stu-id="3769a-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="3769a-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3769a-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with Teamphoria, it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in Teamphoria.

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="3769a-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3769a-110">Prerequisites</span></span>

<span data-ttu-id="3769a-111">Para configurar a integração do Azure AD com o Teamphoria, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="3769a-111">To configure Azure AD integration with Teamphoria, you need the following items:</span></span>

- <span data-ttu-id="3769a-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3769a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3769a-113">Uma assinatura habilitada para logon único do Teamphoria</span><span class="sxs-lookup"><span data-stu-id="3769a-113">A Teamphoria single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3769a-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="3769a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3769a-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="3769a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3769a-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="3769a-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="3769a-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3769a-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3769a-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="3769a-118">Scenario description</span></span>
<span data-ttu-id="3769a-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="3769a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3769a-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="3769a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3769a-121">Adicionar o Teamphoria da galeria</span><span class="sxs-lookup"><span data-stu-id="3769a-121">Adding Teamphoria from the gallery</span></span>
2. <span data-ttu-id="3769a-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3769a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamphoria-from-the-gallery"></a><span data-ttu-id="3769a-123">Adicionar o Teamphoria da galeria</span><span class="sxs-lookup"><span data-stu-id="3769a-123">Adding Teamphoria from the gallery</span></span>
<span data-ttu-id="3769a-124">Para configurar a integração do Teamphoria com o Azure AD, você precisará adicionar o Teamphoria da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="3769a-124">To configure the integration of Teamphoria into Azure AD, you need to add Teamphoria from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3769a-125">**Para adicionar o Teamphoria da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3769a-125">**To add Teamphoria from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3769a-126">No **[Portal de Gerenciamento do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3769a-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3769a-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="3769a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3769a-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3769a-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="3769a-131">Clique em **adicionar** botão na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3769a-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="3769a-133">Na caixa de pesquisa, digite **Teamphoria**.</span><span class="sxs-lookup"><span data-stu-id="3769a-133">In the search box, type **Teamphoria**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_search.png)

5. <span data-ttu-id="3769a-135">No painel de resultados, selecione **Teamphoria** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3769a-135">In the results panel, select **Teamphoria**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3769a-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3769a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3769a-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Teamphoria, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="3769a-138">In this section, you configure and test Azure AD single sign-on with Teamphoria based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3769a-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Teamphoria é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3769a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Teamphoria is to a user in Azure AD.</span></span> <span data-ttu-id="3769a-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="3769a-140">In other words, a link relationship between an Azure AD user and the related user in Teamphoria needs to be established.</span></span>

<span data-ttu-id="3769a-141">Essa relação de vínculo é estabelecida atribuindo o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** no Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="3769a-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Teamphoria.</span></span>

<span data-ttu-id="3769a-142">Para configurar e testar o logon único do Azure AD com o Teamphoria, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="3769a-142">To configure and test Azure AD single sign-on with Teamphoria, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3769a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="3769a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3769a-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="3769a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3769a-145">**[Criação de um usuário de teste do Teamphoria](#creating-a-teamphoria-test-user)** – para ter um equivalente a Brenda Fernandes no Teamphoria que esteja vinculado à sua representação no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3769a-145">**[Creating a Teamphoria test user](#creating-a-teamphoria-test-user)** - to have a counterpart of Britta Simon in Teamphoria that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="3769a-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** - para habilitar Britta Simon a usar o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="3769a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3769a-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="3769a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3769a-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3769a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3769a-149">Nesta seção, você habilita o logon único do Azure AD no Portal de Gerenciamento do Azure e configura o logon único em seu aplicativo Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="3769a-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Teamphoria application.</span></span>

<span data-ttu-id="3769a-150">**Para configurar o logon único do Azure AD com o Teamphoria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3769a-150">**To configure Azure AD single sign-on with Teamphoria, perform the following steps:**</span></span>

1. <span data-ttu-id="3769a-151">No Portal de Gerenciamento do Azure, na página de integração de aplicativos do **Teamphoria**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="3769a-151">In the Azure Management portal, on the **Teamphoria** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o logon único][4]

2. <span data-ttu-id="3769a-153">Na caixa de diálogo **Logon único**, como **Modo**, selecione **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="3769a-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_samlbase.png)

3. <span data-ttu-id="3769a-155">Na seção **URLs e Domínio do Teamphoria**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3769a-155">On the **Teamphoria Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_url.png)

    <span data-ttu-id="3769a-157">a.</span><span class="sxs-lookup"><span data-stu-id="3769a-157">a.</span></span> <span data-ttu-id="3769a-158">Na caixa de texto **URL de Entrada**, digite a URL usando o seguinte padrão: `https://<sub-domain>.teamphoria.com/login`</span><span class="sxs-lookup"><span data-stu-id="3769a-158">In the **Sign-on URL** textbox, type the URL using the following pattern: `https://<sub-domain>.teamphoria.com/login`</span></span>    

    > [!NOTE] 
    > <span data-ttu-id="3769a-159">Observe que esses não são os valores reais.</span><span class="sxs-lookup"><span data-stu-id="3769a-159">Please note that these are not the real values.</span></span> <span data-ttu-id="3769a-160">Você precisa atualizar esses valores com a URL de Entrada real.</span><span class="sxs-lookup"><span data-stu-id="3769a-160">You have to update these values with the actual Sign-On URL.</span></span> <span data-ttu-id="3769a-161">Entre em contato com a [Equipe de suporte do cliente do Teamphoria](https://www.teamphoria.com/) para obter a URL de Entrada.</span><span class="sxs-lookup"><span data-stu-id="3769a-161">Contact [Teamphoria Client support team](https://www.teamphoria.com/) to get the Sign-on URL.</span></span> 

4. <span data-ttu-id="3769a-162">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="3769a-162">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_certificate.png) 

5. <span data-ttu-id="3769a-164">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="3769a-164">Click **Save** button.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-teamphoria-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3769a-166">Na seção **Configuração do Teamphoria**, clique em **Configurar o Teamphoria** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="3769a-166">On the **Teamphoria Configuration** section, click **Configure Teamphoria** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3769a-167">Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="3769a-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_configure.png) 

7. <span data-ttu-id="3769a-169">Para configurar o logon único pelo **Teamphoria**, faça logon em seu aplicativo Teamphoria como administrador.</span><span class="sxs-lookup"><span data-stu-id="3769a-169">To configure single sign-on on **Teamphoria** side, Login to your Teamphoria application as an administrator.</span></span>

8. <span data-ttu-id="3769a-170">Vá até a opção **CONFIGURAÇÕES DE ADMINISTRAÇÃO** na barra de ferramentas à esquerda e, na guia Configurar, clique em **LOGON ÚNICO** para abrir a janela de configuração de SSO.</span><span class="sxs-lookup"><span data-stu-id="3769a-170">Go to **ADMIN SETTINGS** option in the left toolbar and under the the Configure Tab click on **SINGLE SIGN-ON** to open the SSO configuration window.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-teamphoria-tutorial/admin_sso_configure.png)

9. <span data-ttu-id="3769a-172">Clique na opção **ADICIONAR NOVO PROVEDOR DE IDENTIDADE** no canto superior direito para abrir o formulário para adicionar as configurações de SSO.</span><span class="sxs-lookup"><span data-stu-id="3769a-172">Click on **ADD NEW IDENTITY PROVIDER** option in the top right corner to open the form for adding the settings for SSO.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-teamphoria-tutorial/add_new_identity_provider.png)

10. <span data-ttu-id="3769a-174">Insira os detalhes nos campos conforme descrito abaixo:</span><span class="sxs-lookup"><span data-stu-id="3769a-174">Enter the details in the fields as described below-</span></span>

    ![Configurar o logon único](./media/active-directory-saas-teamphoria-tutorial/Teamphoria_sso_save.png)

    <span data-ttu-id="3769a-176">a.</span><span class="sxs-lookup"><span data-stu-id="3769a-176">a.</span></span> <span data-ttu-id="3769a-177">**NOME DE EXIBIÇÃO**: insira o nome de exibição do plug-in na página de administração.</span><span class="sxs-lookup"><span data-stu-id="3769a-177">**DISPLAY NAME** : Enter the display name of the plugin on the admin page.</span></span>

    <span data-ttu-id="3769a-178">b.</span><span class="sxs-lookup"><span data-stu-id="3769a-178">b.</span></span> <span data-ttu-id="3769a-179">**NOME DO BOTÃO**: o nome da guia que será exibido na página de logon para fazer logon por meio do SSO.</span><span class="sxs-lookup"><span data-stu-id="3769a-179">**BUTTON NAME** : The name of the tab which will display on the login page for logging in via SSO.</span></span>

    <span data-ttu-id="3769a-180">c.</span><span class="sxs-lookup"><span data-stu-id="3769a-180">c.</span></span> <span data-ttu-id="3769a-181">**CERTIFICADO**: abra o certificado baixado anteriormente do Portal do Azure no bloco de notas, copie seu conteúdo e cole-o nesta caixa.</span><span class="sxs-lookup"><span data-stu-id="3769a-181">**CERTIFICATE** : Open the Certificate downloaded earlier from the Azure portal in notepad, copy the contents of the same and paste it here in the box.</span></span>

    <span data-ttu-id="3769a-182">d.</span><span class="sxs-lookup"><span data-stu-id="3769a-182">d.</span></span> <span data-ttu-id="3769a-183">**PONTO DE ENTRADA**: cole a **URL de serviço de logon único SAML** copiada do anteriormente do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3769a-183">**ENTRY POINT** : Paste the **SAML Single Sign-On Service URL** copied earlier form the Azure portal.</span></span>

    <span data-ttu-id="3769a-184">e.</span><span class="sxs-lookup"><span data-stu-id="3769a-184">e.</span></span> <span data-ttu-id="3769a-185">Alterne a opção para **LIGADO** e clique em **SALVAR**.</span><span class="sxs-lookup"><span data-stu-id="3769a-185">Switch the option to **ON** and click on **SAVE**.</span></span>   

<!--### Next steps

To ensure users can sign-in to Teamphoria after it has been configured to use Azure Active Directory, review the following tasks and topics:

- User accounts must be pre-provisioned into Teamphoria prior to sign-in. To set this up, see Provisioning.
 
- Users must be assigned access to Teamphoria in Azure AD to sign-in. To assign users, see Users.
 
- To configure access polices for Teamphoria users, see Access Policies.
 
- For additional information on deploying single sign-on to users, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3769a-186">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3769a-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="3769a-187">O objetivo desta seção é criar um usuário de teste no Portal de Gerenciamento do Azure chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3769a-187">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="3769a-189">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3769a-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3769a-190">No **portal de Gerenciamento do Azure**, no painel navegação à esquerda, clique em **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3769a-190">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3769a-192">Vá para **usuários e grupos** e clique em **todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="3769a-192">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3769a-194">Na parte superior da caixa de diálogo clique **adicionar** para abrir o **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3769a-194">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3769a-196">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3769a-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3769a-198">a.</span><span class="sxs-lookup"><span data-stu-id="3769a-198">a.</span></span> <span data-ttu-id="3769a-199">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="3769a-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3769a-200">b.</span><span class="sxs-lookup"><span data-stu-id="3769a-200">b.</span></span> <span data-ttu-id="3769a-201">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="3769a-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3769a-202">c.</span><span class="sxs-lookup"><span data-stu-id="3769a-202">c.</span></span> <span data-ttu-id="3769a-203">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="3769a-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3769a-204">d.</span><span class="sxs-lookup"><span data-stu-id="3769a-204">d.</span></span> <span data-ttu-id="3769a-205">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3769a-205">Click **Create**.</span></span>
 
### <a name="creating-a-teamphoria-test-user"></a><span data-ttu-id="3769a-206">Criar um usuário de teste do Teamphoria</span><span class="sxs-lookup"><span data-stu-id="3769a-206">Creating a Teamphoria test user</span></span>

<span data-ttu-id="3769a-207">Para permitir que usuários do Azure AD façam logon no Teamphoria, eles deverão ser provisionados no Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="3769a-207">In order to enable Azure AD users to log into Teamphoria, they must be provisioned into Teamphoria.</span></span> <span data-ttu-id="3769a-208">No caso do Teamphoria, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="3769a-208">In the case of Teamphoria, provisioning is a manual task.</span></span>

<span data-ttu-id="3769a-209">**Para provisionar contas de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3769a-209">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="3769a-210">Faça logon em seu site da empresa do Teamphoria como administrador.</span><span class="sxs-lookup"><span data-stu-id="3769a-210">Log in to your Teamphoria company site as an administrator.</span></span>

2. <span data-ttu-id="3769a-211">Clique nas configurações de **ADMIN** na barra de ferramentas à esquerda e, na guia **GERENCIAR**, clique em **USUÁRIOS** para abrir a página de administração para usuários.</span><span class="sxs-lookup"><span data-stu-id="3769a-211">Click on **ADMIN** settings on the left toolbar and under the **MANAGE** tab Click on **USERS** to open the admin page for users.</span></span>

    ![Adicionar Funcionário](./media/active-directory-saas-teamphoria-tutorial/admin_manage_users.png)

3. <span data-ttu-id="3769a-213">Clique na opção **CONVITE MANUAL**.</span><span class="sxs-lookup"><span data-stu-id="3769a-213">Click on the **MANUAL INVITE** option.</span></span>

    ![Convidar Pessoas](./media/active-directory-saas-teamphoria-tutorial/admin_manage_add_users.png)  

4. <span data-ttu-id="3769a-215">Nessa página, realize a ação a seguir.</span><span class="sxs-lookup"><span data-stu-id="3769a-215">On this page, perform following action.</span></span> 
    
    ![Convidar Pessoas](./media/active-directory-saas-teamphoria-tutorial/manual_user_invite.png)  

    <span data-ttu-id="3769a-217">a.</span><span class="sxs-lookup"><span data-stu-id="3769a-217">a.</span></span> <span data-ttu-id="3769a-218">Na caixa de texto **ENDEREÇO DE EMAIL**, digite o **endereço de email** de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="3769a-218">In the **EMAIL ADDRESS** textbox, the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3769a-219">b.</span><span class="sxs-lookup"><span data-stu-id="3769a-219">b.</span></span> <span data-ttu-id="3769a-220">Na caixa de texto **NOME**, digite **Brenda**.</span><span class="sxs-lookup"><span data-stu-id="3769a-220">In the **FIRST NAME** textbox, type **Britta**.</span></span>

    <span data-ttu-id="3769a-221">c.</span><span class="sxs-lookup"><span data-stu-id="3769a-221">c.</span></span> <span data-ttu-id="3769a-222">Na caixa de texto **SOBRENOME**, digite **Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="3769a-222">In the **LAST NAME** textbox, type **Simon**.</span></span>

    <span data-ttu-id="3769a-223">d.</span><span class="sxs-lookup"><span data-stu-id="3769a-223">d.</span></span> <span data-ttu-id="3769a-224">Clique em **CONVIDAR 1 USUÁRIO**.</span><span class="sxs-lookup"><span data-stu-id="3769a-224">Click **INVITE 1 USER**.</span></span> <span data-ttu-id="3769a-225">O usuário deve aceitar o convite para ser criado no sistema.</span><span class="sxs-lookup"><span data-stu-id="3769a-225">User needs to accept the invite to get created in the system.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3769a-226">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3769a-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3769a-227">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="3769a-227">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Teamphoria.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="3769a-229">**Para atribuir Brenda Fernandes ao Teamphoria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3769a-229">**To assign Britta Simon to Teamphoria, perform the following steps:**</span></span>

1. <span data-ttu-id="3769a-230">No portal de gerenciamento do Azure, abra a exibição de aplicativos e, em seguida, navegue até o modo de exibição de diretório e vá para **aplicativos empresariais** e clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3769a-230">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="3769a-232">Na lista de aplicativos, selecione **Teamphoria**.</span><span class="sxs-lookup"><span data-stu-id="3769a-232">In the applications list, select **Teamphoria**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_app.png) 

3. <span data-ttu-id="3769a-234">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="3769a-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="3769a-236">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="3769a-236">Click **Add** button.</span></span> <span data-ttu-id="3769a-237">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3769a-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="3769a-239">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="3769a-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3769a-240">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3769a-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3769a-241">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3769a-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3769a-242">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="3769a-242">Testing single sign-on</span></span>

<span data-ttu-id="3769a-243">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="3769a-243">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3769a-244">Se você quiser testar suas configurações de logon único, abra o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="3769a-244">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="3769a-245">Para obter mais detalhes sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="3769a-245">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3769a-246">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="3769a-246">Additional resources</span></span>

* [<span data-ttu-id="3769a-247">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="3769a-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3769a-248">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3769a-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_203.png

