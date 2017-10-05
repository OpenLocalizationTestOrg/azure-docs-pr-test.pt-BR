---
title: "Tutorial: Integração do Azure Active Directory com o Procore SSO | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Procore SSO."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9818edd3-48c0-411d-b05a-3ec805eafb2e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: 042a41eaa6bb21670b4c12068f1b017222f64b99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-procore-sso"></a><span data-ttu-id="0ec67-103">Tutorial: integração do Azure Active Directory com o Procore SSO</span><span class="sxs-lookup"><span data-stu-id="0ec67-103">Tutorial: Azure Active Directory integration with Procore SSO</span></span>

<span data-ttu-id="0ec67-104">Neste tutorial, você aprenderá a integrar o Procore SSO ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="0ec67-104">In this tutorial, you learn how to integrate Procore SSO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0ec67-105">A integração do Procore SSO com o Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="0ec67-105">Integrating Procore SSO with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0ec67-106">É possível controlar, no Azure AD, quem tem acesso ao Procore SSO</span><span class="sxs-lookup"><span data-stu-id="0ec67-106">You can control in Azure AD who has access to Procore SSO</span></span>
- <span data-ttu-id="0ec67-107">É possível permitir que seus usuários façam logon automaticamente no Procore SSO (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ec67-107">You can enable your users to automatically get signed-on to Procore SSO (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0ec67-108">Você pode gerenciar suas contas em um único local - o portal de Gerenciamento do Azure</span><span class="sxs-lookup"><span data-stu-id="0ec67-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="0ec67-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0ec67-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with Procore SSO, it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in Procore SSO.

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="0ec67-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0ec67-110">Prerequisites</span></span>

<span data-ttu-id="0ec67-111">Para configurar a integração do Azure AD com o Procore SSO, são necessários os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="0ec67-111">To configure Azure AD integration with Procore SSO, you need the following items:</span></span>

- <span data-ttu-id="0ec67-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0ec67-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0ec67-113">Uma assinatura do Procore SSO habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="0ec67-113">A Procore SSO single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0ec67-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="0ec67-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0ec67-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="0ec67-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0ec67-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="0ec67-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="0ec67-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0ec67-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0ec67-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="0ec67-118">Scenario description</span></span>
<span data-ttu-id="0ec67-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="0ec67-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0ec67-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="0ec67-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0ec67-121">Adicionando o Procore SSO da galeria</span><span class="sxs-lookup"><span data-stu-id="0ec67-121">Adding Procore SSO from the gallery</span></span>
2. <span data-ttu-id="0ec67-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0ec67-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-procore-sso-from-the-gallery"></a><span data-ttu-id="0ec67-123">Adicionando o Procore SSO da galeria</span><span class="sxs-lookup"><span data-stu-id="0ec67-123">Adding Procore SSO from the gallery</span></span>
<span data-ttu-id="0ec67-124">Para configurar a integração do Procore SSO com o Azure AD, é necessário adicionar o Procore SSO da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="0ec67-124">To configure the integration of Procore SSO into Azure AD, you need to add Procore SSO from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0ec67-125">**Para adicionar o Procore SSO da galeria, siga as etapas abaixo:**</span><span class="sxs-lookup"><span data-stu-id="0ec67-125">**To add Procore SSO from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0ec67-126">No **[Portal de Gerenciamento do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0ec67-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0ec67-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="0ec67-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0ec67-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="0ec67-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="0ec67-131">Clique em **adicionar** botão na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0ec67-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="0ec67-133">Na caixa de pesquisa, digite **Procore SSO**.</span><span class="sxs-lookup"><span data-stu-id="0ec67-133">In the search box, type **Procore SSO**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_search.png)

5. <span data-ttu-id="0ec67-135">No painel de resultados, selecione **Procore SSO** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0ec67-135">In the results panel, select **Procore SSO**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0ec67-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0ec67-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0ec67-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Procore SSO, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="0ec67-138">In this section, you configure and test Azure AD single sign-on with Procore SSO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0ec67-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Procore SSO é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0ec67-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Procore SSO is to a user in Azure AD.</span></span> <span data-ttu-id="0ec67-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Procore SSO.</span><span class="sxs-lookup"><span data-stu-id="0ec67-140">In other words, a link relationship between an Azure AD user and the related user in Procore SSO needs to be established.</span></span>

<span data-ttu-id="0ec67-141">Essa relação de vínculo é estabelecida atribuindo o valor de **nome de usuário** ao Azure AD como sendo o valor de **Nome de usuário** no Procore SSO.</span><span class="sxs-lookup"><span data-stu-id="0ec67-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Procore SSO.</span></span>

<span data-ttu-id="0ec67-142">Para configurar e testar o logon único do Azure AD com o Procore SSO, é necessário concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="0ec67-142">To configure and test Azure AD single sign-on with Procore SSO, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0ec67-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="0ec67-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0ec67-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="0ec67-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0ec67-145">**[Criando um usuário de teste do Procore SSO](#creating-a-procore-sso-test-user)** – para ter um equivalente de Brenda Fernandes no Procore SSO que esteja vinculado à representação dela no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0ec67-145">**[Creating a Procore SSO test user](#creating-a-procore-sso-test-user)** - to have a counterpart of Britta Simon in Procore SSO that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="0ec67-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ec67-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0ec67-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="0ec67-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0ec67-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ec67-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0ec67-149">Nesta seção, você habilitará o logon único do Azure AD no portal de Gerenciamento do Azure e configurará o logon único em seu aplicativo Procore SSO.</span><span class="sxs-lookup"><span data-stu-id="0ec67-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Procore SSO application.</span></span>

<span data-ttu-id="0ec67-150">**Para configurar o logon único do Azure AD com o Procore SSO, siga as etapas abaixo:**</span><span class="sxs-lookup"><span data-stu-id="0ec67-150">**To configure Azure AD single sign-on with Procore SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="0ec67-151">No portal de Gerenciamento do Azure, na página de integração de aplicativos do **Procore SSO**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="0ec67-151">In the Azure Management portal, on the **Procore SSO** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o logon único][4]

2. <span data-ttu-id="0ec67-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="0ec67-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_samlbase.png)

3. <span data-ttu-id="0ec67-155">Na seção **URLs e Domínio do Procore SSO**, o usuário não precisa seguir as etapas, já que o aplicativo está previamente integrado com o Azure.</span><span class="sxs-lookup"><span data-stu-id="0ec67-155">On the **Procore SSO Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_url.png)

4. <span data-ttu-id="0ec67-157">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo XML em seu computador.</span><span class="sxs-lookup"><span data-stu-id="0ec67-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_certificate.png) 

5. <span data-ttu-id="0ec67-159">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="0ec67-159">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-procoresso-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0ec67-161">Na seção **Configuração do Procore SSO**, clique em **Configurar Procore SSO** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="0ec67-161">On the **Procore SSO Configuration** section, click **Configure Procore SSO** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0ec67-162">Copie a **ID da entidade SAML e URL de serviço logon único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="0ec67-162">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_configure.png) 

7. <span data-ttu-id="0ec67-164">Para configurar o logon único no lado do **Procore SSO**, faça logon no site da sua empresa Procore como administrador.</span><span class="sxs-lookup"><span data-stu-id="0ec67-164">To configure single sign-on on **Procore SSO** side, login to your procore company site as an administrator.</span></span>

8. <span data-ttu-id="0ec67-165">Na lista suspensa da caixa de ferramentas, clique em **Admin** para abrir a página de configurações de SSO.</span><span class="sxs-lookup"><span data-stu-id="0ec67-165">From the toolbox drop down, click on **Admin** to open the SSO settings page.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-procoresso-tutorial/procore_tool_admin.png)

9. <span data-ttu-id="0ec67-167">Cole os valores nas caixas conforme descrito abaixo-</span><span class="sxs-lookup"><span data-stu-id="0ec67-167">Paste the values in the boxes as described below-</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-procoresso-tutorial/procore_setting_admin.png)    

    <span data-ttu-id="0ec67-169">a.</span><span class="sxs-lookup"><span data-stu-id="0ec67-169">a.</span></span> <span data-ttu-id="0ec67-170">Na caixa **URL do emissor de logon único**, cole a ID da entidade SAML copiada do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ec67-170">In the **Single Sign On Issuer URL** box, paste the SAML Entity ID copied from the Azure portal.</span></span>

    <span data-ttu-id="0ec67-171">b.</span><span class="sxs-lookup"><span data-stu-id="0ec67-171">b.</span></span> <span data-ttu-id="0ec67-172">Na caixa **URL de destino de logon único SAML**, cole a URL de serviço logon único SAML copiada do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ec67-172">In the **SAML Sign On Target URL** box, paste the SAML Single Sign-On Service URL copied from the Azure portal.</span></span>

    <span data-ttu-id="0ec67-173">c.</span><span class="sxs-lookup"><span data-stu-id="0ec67-173">c.</span></span> <span data-ttu-id="0ec67-174">Agora, abra o **XML de metadados** baixado acima do portal do Azure e copie o certificado na marcação nomeada **X509Certificate**.</span><span class="sxs-lookup"><span data-stu-id="0ec67-174">Now open the **Metadata XML** downloaded above from the Azure portal and copy the certficate in the tag named **X509Certificate**.</span></span> <span data-ttu-id="0ec67-175">Cole o valor copiado para a caixa **Certificado x509 de logon único**.</span><span class="sxs-lookup"><span data-stu-id="0ec67-175">Paste the copied value into the **Single Sign On x509 Certificate** box.</span></span>

10. <span data-ttu-id="0ec67-176">Clique em **Salvar alterações**.</span><span class="sxs-lookup"><span data-stu-id="0ec67-176">Click on **Save Changes**.</span></span>

11. <span data-ttu-id="0ec67-177">Após essas configurações, é necessário enviar o **nome de domínio** (por exemplo, **contoso.com**) por meio do qual você está fazendo logon no Procore para a [equipe de suporte Procore](https://support.procore.com/) e eles ativarão o SSO federado para esse domínio.</span><span class="sxs-lookup"><span data-stu-id="0ec67-177">After these settings, you needs to send the **domain name** (e.g **contoso.com**) through which you are logging into Procore to the [Procore Support team](https://support.procore.com/) and they will activate federated SSO for that domain.</span></span>

<!--### Next steps

To ensure users can sign-in to Procore SSO after it has been configured to use Azure Active Directory, review the following tasks and topics:

- User accounts must be pre-provisioned into Procore SSO prior to sign-in. To set this up, see Provisioning.
 
- Users must be assigned access to Procore SSO in Azure AD to sign-in. To assign users, see Users.
 
- To configure access polices for Procore SSO users, see Access Policies.
 
- For additional information on deploying single sign-on to users, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0ec67-178">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0ec67-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="0ec67-179">O objetivo desta seção é criar um usuário de teste no Portal de Gerenciamento do Azure chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0ec67-179">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="0ec67-181">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="0ec67-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0ec67-182">No **portal de Gerenciamento do Azure**, no painel navegação à esquerda, clique em **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0ec67-182">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-procoresso-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0ec67-184">Vá para **usuários e grupos** e clique em **todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="0ec67-184">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-procoresso-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0ec67-186">Na parte superior da caixa de diálogo clique **adicionar** para abrir o **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0ec67-186">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-procoresso-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0ec67-188">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="0ec67-188">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-procoresso-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0ec67-190">a.</span><span class="sxs-lookup"><span data-stu-id="0ec67-190">a.</span></span> <span data-ttu-id="0ec67-191">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="0ec67-191">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0ec67-192">b.</span><span class="sxs-lookup"><span data-stu-id="0ec67-192">b.</span></span> <span data-ttu-id="0ec67-193">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="0ec67-193">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0ec67-194">c.</span><span class="sxs-lookup"><span data-stu-id="0ec67-194">c.</span></span> <span data-ttu-id="0ec67-195">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="0ec67-195">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0ec67-196">d.</span><span class="sxs-lookup"><span data-stu-id="0ec67-196">d.</span></span> <span data-ttu-id="0ec67-197">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="0ec67-197">Click **Create**.</span></span>
 
### <a name="creating-a-procore-sso-test-user"></a><span data-ttu-id="0ec67-198">Criando um usuário de teste do Procore SSO</span><span class="sxs-lookup"><span data-stu-id="0ec67-198">Creating a Procore SSO test user</span></span>

<span data-ttu-id="0ec67-199">Siga as etapas abaixo para criar um usuário de teste do Procore no outro lado.</span><span class="sxs-lookup"><span data-stu-id="0ec67-199">Please follow the below steps to create a Procore test user on their side.</span></span>

1. <span data-ttu-id="0ec67-200">Faça logon no site da sua empresa do Procore como administrador.</span><span class="sxs-lookup"><span data-stu-id="0ec67-200">Login to your procore company site as an administrator.</span></span>  

2. <span data-ttu-id="0ec67-201">Na lista suspensa da caixa de ferramentas, clique em **Diretório** para abrir a página do diretório da empresa.</span><span class="sxs-lookup"><span data-stu-id="0ec67-201">From the toolbox drop down, click on **Directory** to open the company directory page.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-procoresso-tutorial/Procore_sso_directory.png)

3. <span data-ttu-id="0ec67-203">Clique na opção **Adicionar uma pessoa** para abrir o formulário e insira as seguintes opções –</span><span class="sxs-lookup"><span data-stu-id="0ec67-203">Click on **Add a Person** option to open the form and enter perform following options -</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-procoresso-tutorial/Procore_user_add.png)

    <span data-ttu-id="0ec67-205">a.</span><span class="sxs-lookup"><span data-stu-id="0ec67-205">a.</span></span> <span data-ttu-id="0ec67-206">Na caixa de texto **Nome**, digite o nome do usuário como **Brenda**.</span><span class="sxs-lookup"><span data-stu-id="0ec67-206">In the **First Name** textbox, type user's first name like **Britta**.</span></span>

    <span data-ttu-id="0ec67-207">b.</span><span class="sxs-lookup"><span data-stu-id="0ec67-207">b.</span></span> <span data-ttu-id="0ec67-208">Na caixa de texto **Sobrenome**, digite o sobrenome do usuário como **Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="0ec67-208">In the **Last name** textbox, type user's last name like **Simon**.</span></span>

    <span data-ttu-id="0ec67-209">c.</span><span class="sxs-lookup"><span data-stu-id="0ec67-209">c.</span></span> <span data-ttu-id="0ec67-210">Na caixa de texto **Endereço de email**, digite o endereço de email do usuário como **BrittaSimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="0ec67-210">In the **Email Address** textbox, type user's email address like **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="0ec67-211">d.</span><span class="sxs-lookup"><span data-stu-id="0ec67-211">d.</span></span> <span data-ttu-id="0ec67-212">Selecione **Modelo de permissão** como **Aplicar o modelo de permissão mais tarde**.</span><span class="sxs-lookup"><span data-stu-id="0ec67-212">Select **Permission Template** as **Apply Permission Template Later**.</span></span>

    <span data-ttu-id="0ec67-213">e.</span><span class="sxs-lookup"><span data-stu-id="0ec67-213">e.</span></span> <span data-ttu-id="0ec67-214">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="0ec67-214">Click **Create**.</span></span>

4. <span data-ttu-id="0ec67-215">Verifique e atualize os detalhes do contato recém-adicionado.</span><span class="sxs-lookup"><span data-stu-id="0ec67-215">Check and update the details for the newly added contact.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-procoresso-tutorial/Procore_user_check.png)

5. <span data-ttu-id="0ec67-217">Clique em **Salvar e enviar convite** (se for necessário enviar um convite por email) ou **Salvar** (Salvar diretamente) para concluir o registro do usuário.</span><span class="sxs-lookup"><span data-stu-id="0ec67-217">Click on **Save and Send Invitiation** (if an invite through mail is required) or **Save** (Save directly) to complete the user registration.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-procoresso-tutorial/Procore_user_save.png)    

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0ec67-219">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0ec67-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0ec67-220">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure, concedendo-lhe acesso ao Procore SSO.</span><span class="sxs-lookup"><span data-stu-id="0ec67-220">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Procore SSO.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="0ec67-222">**Para atribuir Brenda Fernandes ao Procore SSO, siga as etapas abaixo:**</span><span class="sxs-lookup"><span data-stu-id="0ec67-222">**To assign Britta Simon to Procore SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="0ec67-223">No portal de gerenciamento do Azure, abra a exibição de aplicativos e, em seguida, navegue até o modo de exibição de diretório e vá para **aplicativos empresariais** e clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="0ec67-223">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="0ec67-225">Na lista de aplicativos, selecione **Procore SSO**.</span><span class="sxs-lookup"><span data-stu-id="0ec67-225">In the applications list, select **Procore SSO**.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_app.png) 

3. <span data-ttu-id="0ec67-227">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="0ec67-227">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="0ec67-229">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="0ec67-229">Click **Add** button.</span></span> <span data-ttu-id="0ec67-230">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0ec67-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="0ec67-232">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="0ec67-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0ec67-233">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0ec67-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0ec67-234">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0ec67-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0ec67-235">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="0ec67-235">Testing single sign-on</span></span>

<span data-ttu-id="0ec67-236">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="0ec67-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0ec67-237">Se você quiser testar suas configurações de logon único, abra o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="0ec67-237">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="0ec67-238">Para obter mais detalhes sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="0ec67-238">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> <span data-ttu-id="0ec67-239">Ao clicar no bloco Procore SSO no Painel de Acesso, seu logon deverá ser feito automaticamente no aplicativo Procore SSO.</span><span class="sxs-lookup"><span data-stu-id="0ec67-239">When you click the Procore SSO tile in the Access Panel, you should get automatically signed-on to your Procore SSO application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0ec67-240">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="0ec67-240">Additional resources</span></span>

* [<span data-ttu-id="0ec67-241">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="0ec67-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0ec67-242">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0ec67-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_203.png

