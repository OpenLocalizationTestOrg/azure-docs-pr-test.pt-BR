---
title: "Tutorial: Integração do Azure Active Directory com o AWS (Amazon Web Services) | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o AWS (Amazon Web Services)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7561c20b-2325-4d97-887f-693aa383c7be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 0fb9c8f428368271b548e3f174726fa01ea910c5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-amazon-web-services-aws"></a><span data-ttu-id="4f775-103">Tutorial: Integração do Azure Active Directory com o AWS (Amazon Web Services)</span><span class="sxs-lookup"><span data-stu-id="4f775-103">Tutorial: Azure Active Directory integration with Amazon Web Services (AWS)</span></span>

<span data-ttu-id="4f775-104">Neste tutorial, você aprenderá a integrar o AWS (Amazon Web Services) ao Azure AD (Active Directory).</span><span class="sxs-lookup"><span data-stu-id="4f775-104">In this tutorial, you learn how to integrate Amazon Web Services (AWS) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4f775-105">A integração do AWS (Amazon Web Services) ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="4f775-105">Integrating Amazon Web Services (AWS) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4f775-106">Você pode controlar no Azure AD quem tem acesso ao AWS (Amazon Web Services)</span><span class="sxs-lookup"><span data-stu-id="4f775-106">You can control in Azure AD who has access to Amazon Web Services (AWS)</span></span>
- <span data-ttu-id="4f775-107">Você pode habilitar seus usuários a fazerem logon automaticamente no AWS (Amazon Web Services) (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f775-107">You can enable your users to automatically get signed-on to Amazon Web Services (AWS) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4f775-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4f775-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4f775-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4f775-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with Amazon Web Services (AWS), it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in Amazon Web Services (AWS).

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="4f775-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4f775-110">Prerequisites</span></span>

<span data-ttu-id="4f775-111">Para configurar a integração do Azure AD com o AWS (Amazon Web Services), você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="4f775-111">To configure Azure AD integration with Amazon Web Services (AWS), you need the following items:</span></span>

- <span data-ttu-id="4f775-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4f775-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4f775-113">Uma assinatura habilitada para logon único do AWS (Amazon Web Services)</span><span class="sxs-lookup"><span data-stu-id="4f775-113">Amazon Web Services (AWS) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4f775-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="4f775-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4f775-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="4f775-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4f775-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="4f775-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="4f775-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4f775-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4f775-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="4f775-118">Scenario description</span></span>
<span data-ttu-id="4f775-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="4f775-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4f775-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="4f775-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4f775-121">Adicionar o AWS (Amazon Web Services) da galeria</span><span class="sxs-lookup"><span data-stu-id="4f775-121">Adding Amazon Web Services (AWS) from the gallery</span></span>
2. <span data-ttu-id="4f775-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4f775-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-amazon-web-services-aws-from-the-gallery"></a><span data-ttu-id="4f775-123">Adicionar o AWS (Amazon Web Services) da galeria</span><span class="sxs-lookup"><span data-stu-id="4f775-123">Adding Amazon Web Services (AWS) from the gallery</span></span>
<span data-ttu-id="4f775-124">Para configurar a integração do AWS (Amazon Web Services) com o Azure AD, você precisa adicionar o AWS (Amazon Web Services), por meio da galeria, à sua lista de aplicativos de SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="4f775-124">To configure the integration of Amazon Web Services (AWS) into Azure AD, you need to add Amazon Web Services (AWS) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4f775-125">**Para adicionar o AWS (Amazon Web Services) da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4f775-125">**To add Amazon Web Services (AWS) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4f775-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4f775-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4f775-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="4f775-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4f775-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4f775-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="4f775-131">Clique em **adicionar** botão na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4f775-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="4f775-133">Na caixa de pesquisa, digite **serviço AWS (Amazon Web Services)**.</span><span class="sxs-lookup"><span data-stu-id="4f775-133">In the search box, type **Amazon Web Services (AWS)**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_search.png)

5. <span data-ttu-id="4f775-135">No painel de resultados, selecione **AWS (Amazon Web Services)** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4f775-135">In the results panel, select **Amazon Web Services (AWS)**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4f775-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4f775-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4f775-138">Nesta seção, você vai configurar e testar o logon único do Azure AD com o AWS (Amazon Web Services), com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="4f775-138">In this section, you configure and test Azure AD single sign-on with Amazon Web Services (AWS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4f775-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do AWS (Amazon Web Services) é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4f775-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Amazon Web Services (AWS) is to a user in Azure AD.</span></span> <span data-ttu-id="4f775-140">Em outras palavras, uma relação de link entre um usuário do Azure AD e o usuário relacionado no serviço AWS (Amazon Web Services) deve ser estabelecida.</span><span class="sxs-lookup"><span data-stu-id="4f775-140">In other words, a link relationship between an Azure AD user and the related user in Amazon Web Services (AWS) needs to be established.</span></span>

<span data-ttu-id="4f775-141">Essa relação de vínculo é estabelecida, atribuindo-se o valor do **nome de usuário** no Azure AD como o valor da **nome de usuário** no AWS (Amazon Web Services).</span><span class="sxs-lookup"><span data-stu-id="4f775-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Amazon Web Services (AWS).</span></span>

<span data-ttu-id="4f775-142">Para configurar e testar o logon único do Azure AD com o AWS (Amazon Web Services), você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="4f775-142">To configure and test Azure AD single sign-on with Amazon Web Services (AWS), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4f775-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="4f775-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4f775-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4f775-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4f775-145">**[Criação de um usuário de teste do Amazon Web Services](#creating-an-amazon-web-services-test-user)**: para ter um equivalente de Brenda Fernandes no AWS (Amazon Web Services) que esteja vinculado à representação dela no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4f775-145">**[Creating an Amazon Web Services test user](#creating-an-amazon-web-services-test-user)** - to have a counterpart of Britta Simon in Amazon Web Services (AWS) that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="4f775-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4f775-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4f775-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="4f775-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4f775-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f775-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4f775-149">Nesta seção, você vai habilitar o logon único do Azure AD no Portal do Azure e configurar o logon único em seu aplicativo AWS (Amazon Web Services).</span><span class="sxs-lookup"><span data-stu-id="4f775-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Amazon Web Services (AWS) application.</span></span>

<span data-ttu-id="4f775-150">**Para configurar o logon único do Azure AD com o AWS (Amazon Web Services), execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4f775-150">**To configure Azure AD single sign-on with Amazon Web Services (AWS), perform the following steps:**</span></span>

1. <span data-ttu-id="4f775-151">No Portal do Azure, na página de integração de aplicativos do **AWS (Amazon Web Services)**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="4f775-151">In the Azure Portal, on the **Amazon Web Services (AWS)** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="4f775-153">Na caixa de diálogo **Logon único**, como **Modo**, selecione **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="4f775-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_samlbase.png)

3. <span data-ttu-id="4f775-155">Na seção **Domínio e URLs do AWS (Amazon Web Services)**, o usuário não precisa seguir as etapas, uma vez que o aplicativo já está pré-integrado ao Azure.</span><span class="sxs-lookup"><span data-stu-id="4f775-155">On the **Amazon Web Services (AWS) Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_url.png)

4. <span data-ttu-id="4f775-157">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo XML em seu computador.</span><span class="sxs-lookup"><span data-stu-id="4f775-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_certificate.png)

5. <span data-ttu-id="4f775-159">O aplicativo AWS (Amazon Web Services) espera que as declarações SAML estejam em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="4f775-159">The Amazon Web Services (AWS) Software application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="4f775-160">Configure as seguintes declarações para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4f775-160">Please configure the following claims for this application.</span></span> <span data-ttu-id="4f775-161">Você pode gerenciar os valores desses atributos da seção "**Atributos de Usuário**" na página de integração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4f775-161">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="4f775-162">A captura de tela a seguir mostra um exemplo disso.</span><span class="sxs-lookup"><span data-stu-id="4f775-162">The following screenshot shows an example for this.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_attribute.png)

6. <span data-ttu-id="4f775-164">Na seção **Atributos do usuário**, na caixa de diálogo **Logon único**, configure o atributo do token SAML na imagem acima e siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="4f775-164">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="4f775-165">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="4f775-165">Attribute Name</span></span>  | <span data-ttu-id="4f775-166">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="4f775-166">Attribute Value</span></span> | <span data-ttu-id="4f775-167">Namespace</span><span class="sxs-lookup"><span data-stu-id="4f775-167">Namespace</span></span> |
    | --------------- | --------------- | --------------- |
    | <span data-ttu-id="4f775-168">RoleSessionName</span><span class="sxs-lookup"><span data-stu-id="4f775-168">RoleSessionName</span></span> | <span data-ttu-id="4f775-169">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="4f775-169">user.userprincipalname</span></span> | <span data-ttu-id="4f775-170">https://aws.amazon.com/SAML/Attributes</span><span class="sxs-lookup"><span data-stu-id="4f775-170">https://aws.amazon.com/SAML/Attributes</span></span> |
    | <span data-ttu-id="4f775-171">Função</span><span class="sxs-lookup"><span data-stu-id="4f775-171">Role</span></span>            | <span data-ttu-id="4f775-172">user.assignedroles</span><span class="sxs-lookup"><span data-stu-id="4f775-172">user.assignedroles</span></span> |  <span data-ttu-id="4f775-173">https://aws.amazon.com/SAML/Attributes</span><span class="sxs-lookup"><span data-stu-id="4f775-173">https://aws.amazon.com/SAML/Attributes</span></span> |
    
    >[!TIP]
    ><span data-ttu-id="4f775-174">Você precisa configurar o provisionamento do usuário no Azure AD para buscar todas as funções no Console do AWS.</span><span class="sxs-lookup"><span data-stu-id="4f775-174">You need to configure the user provisioning in Azure AD to fetch all the roles from AWS Console.</span></span> <span data-ttu-id="4f775-175">Veja as etapas de provisionamento abaixo.</span><span class="sxs-lookup"><span data-stu-id="4f775-175">Please refer the provisioning steps below.</span></span>

    <span data-ttu-id="4f775-176">a.</span><span class="sxs-lookup"><span data-stu-id="4f775-176">a.</span></span> <span data-ttu-id="4f775-177">Clique em **Adicionar atributo** para abrir o diálogo **Adicionar Atributo**.</span><span class="sxs-lookup"><span data-stu-id="4f775-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="4f775-179">b.</span><span class="sxs-lookup"><span data-stu-id="4f775-179">b.</span></span> <span data-ttu-id="4f775-180">Na caixa de texto **Nome** , digite o nome do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="4f775-180">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="4f775-182">c.</span><span class="sxs-lookup"><span data-stu-id="4f775-182">c.</span></span> <span data-ttu-id="4f775-183">Na lista **Valor**, digite o valor do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="4f775-183">From the **Value** list, type the attribute value shown for that row.</span></span> <span data-ttu-id="4f775-184">Adicione o valor de Namespace conforme indicado acima.</span><span class="sxs-lookup"><span data-stu-id="4f775-184">Add the Namespace value as given above.</span></span>
    
    <span data-ttu-id="4f775-185">d.</span><span class="sxs-lookup"><span data-stu-id="4f775-185">d.</span></span> <span data-ttu-id="4f775-186">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="4f775-186">Click **Ok**.</span></span>

7. <span data-ttu-id="4f775-187">Clique no botão **Salvar** para salvar as configurações no Azure.</span><span class="sxs-lookup"><span data-stu-id="4f775-187">Click **Save** button to save the settings on Azure.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="4f775-189">Em uma janela de navegador diferente, entre no site de sua empresa do AWS (Amazon Web Services) como administrador.</span><span class="sxs-lookup"><span data-stu-id="4f775-189">In a different browser window, sign-on to your Amazon Web Services (AWS) company site as administrator.</span></span>

9. <span data-ttu-id="4f775-190">Clique em **página inicial do Console**.</span><span class="sxs-lookup"><span data-stu-id="4f775-190">Click **Console Home**.</span></span>
   
    ![Configurar Logon Único][11]

10. <span data-ttu-id="4f775-192">Clique em **IAM** no serviço **Segurança, Identidade e Conformidade**.</span><span class="sxs-lookup"><span data-stu-id="4f775-192">Click **IAM** from **Security, Identity & Compliance** service.</span></span>
   
    ![Configurar Logon Único][12]

11. <span data-ttu-id="4f775-194">Clique em **Provedores de identidade**, e, em seguida, clique em **Criar provedor**.</span><span class="sxs-lookup"><span data-stu-id="4f775-194">Click **Identity Providers**, and then click **Create Provider**.</span></span>
   
    ![Configurar Logon Único][13]

12. <span data-ttu-id="4f775-196">Na página da caixa de diálogo **Configurar provedor** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4f775-196">On the **Configure Provider** dialog page, perform the following steps:</span></span>
   
    ![Configurar Logon Único][14]
 
    <span data-ttu-id="4f775-198">a.</span><span class="sxs-lookup"><span data-stu-id="4f775-198">a.</span></span> <span data-ttu-id="4f775-199">Como **Tipo de provedor**, selecione **SAML**.</span><span class="sxs-lookup"><span data-stu-id="4f775-199">As **Provider Type**, select **SAML**.</span></span>

    <span data-ttu-id="4f775-200">b.</span><span class="sxs-lookup"><span data-stu-id="4f775-200">b.</span></span> <span data-ttu-id="4f775-201">Na caixa de texto **Nome do provedor**, digite um nome de provedor (p. ex.: *WAAD*).</span><span class="sxs-lookup"><span data-stu-id="4f775-201">In the **Provider Name** textbox, type a provider name (e.g.: *WAAD*).</span></span>

    <span data-ttu-id="4f775-202">c.</span><span class="sxs-lookup"><span data-stu-id="4f775-202">c.</span></span> <span data-ttu-id="4f775-203">Para carregar o arquivo de metadados baixado, clique em **Escolher arquivo**.</span><span class="sxs-lookup"><span data-stu-id="4f775-203">To upload your downloaded metadata file, click **Choose File**.</span></span>

    <span data-ttu-id="4f775-204">d.</span><span class="sxs-lookup"><span data-stu-id="4f775-204">d.</span></span> <span data-ttu-id="4f775-205">Clique em **Próxima etapa**.</span><span class="sxs-lookup"><span data-stu-id="4f775-205">Click **Next Step**.</span></span>

13. <span data-ttu-id="4f775-206">Na página de diálogo **Verificar informações do provedor**, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="4f775-206">On the **Verify Provider Information** dialog page, click **Create**.</span></span> 
    
    ![Configurar Logon Único][15]

14. <span data-ttu-id="4f775-208">Clique em **Funções** e, em seguida, clique em **Criar Nova Função**.</span><span class="sxs-lookup"><span data-stu-id="4f775-208">Click **Roles**, and then click **Create New Role**.</span></span> 
    
    ![Configurar o logon único][16]

15. <span data-ttu-id="4f775-210">Na caixa de diálogo **Definir Nome de Função** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4f775-210">On the **Set Role Name** dialog, perform the following steps:</span></span> 
    
    ![Configurar Logon Único][17] 

    <span data-ttu-id="4f775-212">a.</span><span class="sxs-lookup"><span data-stu-id="4f775-212">a.</span></span> <span data-ttu-id="4f775-213">Na caixa de texto **Nome da função** , digite um nome de função (por exemplo: *TestUser*).</span><span class="sxs-lookup"><span data-stu-id="4f775-213">In the **Role Name** textbox, type a role name (e.g.: *TestUser*).</span></span> 

    <span data-ttu-id="4f775-214">b.</span><span class="sxs-lookup"><span data-stu-id="4f775-214">b.</span></span> <span data-ttu-id="4f775-215">Clique em **Próxima etapa**.</span><span class="sxs-lookup"><span data-stu-id="4f775-215">Click **Next Step**.</span></span>

16. <span data-ttu-id="4f775-216">Na caixa de diálogo **Selecionar Tipo de Função** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4f775-216">On the **Select Role Type** dialog, perform the following steps:</span></span> 
    
    ![Configurar Logon Único][18] 

    <span data-ttu-id="4f775-218">a.</span><span class="sxs-lookup"><span data-stu-id="4f775-218">a.</span></span> <span data-ttu-id="4f775-219">Selecione **Função de acesso do provedor de identidade**.</span><span class="sxs-lookup"><span data-stu-id="4f775-219">Select **Role For Identity Provider Access**.</span></span> 

    <span data-ttu-id="4f775-220">b.</span><span class="sxs-lookup"><span data-stu-id="4f775-220">b.</span></span> <span data-ttu-id="4f775-221">Na seção **Conceder acesso de logon único da Web (WebSSO) a provedores SAML**, clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="4f775-221">In the **Grant Web Single Sign-On (WebSSO) access to SAML providers** section, click **Select**.</span></span>

17. <span data-ttu-id="4f775-222">Na caixa de diálogo **Estabelecer Confiança** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4f775-222">On the **Establish Trust** dialog, perform the following steps:</span></span>  
    
    ![Configurar Logon Único][19] 

    <span data-ttu-id="4f775-224">a.</span><span class="sxs-lookup"><span data-stu-id="4f775-224">a.</span></span> <span data-ttu-id="4f775-225">Como provedor SAML, selecione o provedor SAML criado anteriormente (por exemplo: *WAAD*)</span><span class="sxs-lookup"><span data-stu-id="4f775-225">As SAML provider, select the SAML provider you have created previously (e.g.: *WAAD*)</span></span>
  
    <span data-ttu-id="4f775-226">b.</span><span class="sxs-lookup"><span data-stu-id="4f775-226">b.</span></span> <span data-ttu-id="4f775-227">Clique em **Próxima etapa**.</span><span class="sxs-lookup"><span data-stu-id="4f775-227">Click **Next Step**.</span></span>

18. <span data-ttu-id="4f775-228">Na caixa de diálogo **Verificar Confiança na Função**, clique em **Próxima Etapa**.</span><span class="sxs-lookup"><span data-stu-id="4f775-228">On the **Verify Role Trust** dialog, click **Next Step**.</span></span>
    
    ![Configurar o logon único][32]

19. <span data-ttu-id="4f775-230">Na caixa de diálogo **Anexar Política**, clique em **Próxima Etapa**.</span><span class="sxs-lookup"><span data-stu-id="4f775-230">On the **Attach Policy** dialog, click **Next Step**.</span></span>
    
    ![Configurar Logon Único][33]

20. <span data-ttu-id="4f775-232">Na caixa de diálogo **Examinar** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4f775-232">On the **Review** dialog, perform the following steps:</span></span>
    
    ![Configurar Logon Único][34]
 
    <span data-ttu-id="4f775-234">a.</span><span class="sxs-lookup"><span data-stu-id="4f775-234">a.</span></span> <span data-ttu-id="4f775-235">Clique em **Criar função**.</span><span class="sxs-lookup"><span data-stu-id="4f775-235">Click **Create Role**.</span></span>

    <span data-ttu-id="4f775-236">b.</span><span class="sxs-lookup"><span data-stu-id="4f775-236">b.</span></span> <span data-ttu-id="4f775-237">Crie quantas funções forem necessárias e mapeie-as para o Provedor de Identidade.</span><span class="sxs-lookup"><span data-stu-id="4f775-237">Create as many roles as needed and map them to the Identity Provider.</span></span>

21. <span data-ttu-id="4f775-238">Agora, configure o provisionamento de usuário para buscar todas as funções no AWS</span><span class="sxs-lookup"><span data-stu-id="4f775-238">Now configure the user provisioning to fetch all the roles from AWS</span></span>

    <span data-ttu-id="4f775-239">a.</span><span class="sxs-lookup"><span data-stu-id="4f775-239">a.</span></span> <span data-ttu-id="4f775-240">No Console do AWS, faça logon com sua conta raiz</span><span class="sxs-lookup"><span data-stu-id="4f775-240">In the AWS Console login with your root account</span></span>

    <span data-ttu-id="4f775-241">b.</span><span class="sxs-lookup"><span data-stu-id="4f775-241">b.</span></span> <span data-ttu-id="4f775-242">No canto superior direito, clique em seu nome e na opção **Minhas Credenciais de Segurança**.</span><span class="sxs-lookup"><span data-stu-id="4f775-242">In the top right corner click your name and then click the **My Security Credentials** option.</span></span> <span data-ttu-id="4f775-243">Isso abrirá uma tela como uma mensagem de aviso.</span><span class="sxs-lookup"><span data-stu-id="4f775-243">This will open up a screen as a warning message.</span></span> <span data-ttu-id="4f775-244">Clique no botão **Credenciais de Segurança** para passar a tela.</span><span class="sxs-lookup"><span data-stu-id="4f775-244">Click the button **Security Credentials** button to pass the screen.</span></span>
        
       ![Configurar o logon único][36]

       ![Configurar Logon Único][37]

    <span data-ttu-id="4f775-247">c.</span><span class="sxs-lookup"><span data-stu-id="4f775-247">c.</span></span> <span data-ttu-id="4f775-248">Na seção Chaves de Acesso, clique no botão **Criar Nova Chave de Acesso**.</span><span class="sxs-lookup"><span data-stu-id="4f775-248">In the Access Keys section click the **Create New Access Key** button.</span></span> <span data-ttu-id="4f775-249">Isso gera a ID da Chave de Acesso e um valor de token.</span><span class="sxs-lookup"><span data-stu-id="4f775-249">This generates the Access Key ID and a token value.</span></span>
    
       ![Configurar o logon único][38]

    <span data-ttu-id="4f775-251">d.</span><span class="sxs-lookup"><span data-stu-id="4f775-251">d.</span></span> <span data-ttu-id="4f775-252">Copie esses dois valores e baixe-os também para não perdê-los.</span><span class="sxs-lookup"><span data-stu-id="4f775-252">Copy both these values and also download it, so that you don't lose it.</span></span>

    <span data-ttu-id="4f775-253">e.</span><span class="sxs-lookup"><span data-stu-id="4f775-253">e.</span></span> <span data-ttu-id="4f775-254">No Portal do Azure, na página de integração de aplicativos do AWS (Amazon Web Services), clique em **Provisionamento**.</span><span class="sxs-lookup"><span data-stu-id="4f775-254">In the Azure Portal, on the Amazon Web Services (AWS) application integration page, click **Provisioning**.</span></span>
        
       ![Configurar o logon único][35]

    <span data-ttu-id="4f775-256">f.</span><span class="sxs-lookup"><span data-stu-id="4f775-256">f.</span></span> <span data-ttu-id="4f775-257">Defina o Modo de provisionamento como **Automático**</span><span class="sxs-lookup"><span data-stu-id="4f775-257">Set the Provisioning mode to **Automatic**</span></span>
        
       ![Configurar Logon Único][39]

    <span data-ttu-id="4f775-259">g.</span><span class="sxs-lookup"><span data-stu-id="4f775-259">g.</span></span> <span data-ttu-id="4f775-260">Agora, em **clientsecret** e **Token Secreto**, cole os valores correspondentes, aqueles copiados do Console do AWS.</span><span class="sxs-lookup"><span data-stu-id="4f775-260">Now in the **clientsecret** and **Secret Token** paste the corresponding values, which you have copied from AWS Console.</span></span>
    
    <span data-ttu-id="4f775-261">h.</span><span class="sxs-lookup"><span data-stu-id="4f775-261">h.</span></span> <span data-ttu-id="4f775-262">Você pode clicar no botão **Testar Conectividade** para testar a conectividade.</span><span class="sxs-lookup"><span data-stu-id="4f775-262">You can click the **Test Connection** button to test the connectivity.</span></span> <span data-ttu-id="4f775-263">Depois que for bem-sucedida, você poderá iniciar o conector de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="4f775-263">Once that is successful then you can start the provisioning connector.</span></span>
       
       ![Configurar o logon único][40]

    <span data-ttu-id="4f775-265">i.</span><span class="sxs-lookup"><span data-stu-id="4f775-265">i.</span></span> <span data-ttu-id="4f775-266">Agora, habilite o Status do Provisionamento para **Ativado**.</span><span class="sxs-lookup"><span data-stu-id="4f775-266">Now enable the Provisioning Status to **On**.</span></span> <span data-ttu-id="4f775-267">Isso inicia a busca das funções no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4f775-267">This starts fetching the roles from the application.</span></span>

       ![Configurar o logon único][41]

    > [!NOTE]
    > <span data-ttu-id="4f775-269">O serviço Provisionamento do Azure AD é executado sempre de tempos em tempos para sincronizar as funções do AWS.</span><span class="sxs-lookup"><span data-stu-id="4f775-269">Azure AD Provisioning service runs every after some time to sync the roles from AWS.</span></span> <span data-ttu-id="4f775-270">Você deve ver todas as funções do AWS anexadas ao Provedor de Identidade no Azure AD e pode usá-las ao atribuir o aplicativo a usuários ou grupos.</span><span class="sxs-lookup"><span data-stu-id="4f775-270">You should see all the Identity Provider attached AWS roles into Azure AD and you can use them while assigning the application to users or groups.</span></span>

<!--### Next steps

To ensure users can sign-in to Amazon Web Services (AWS) after it has been configured to use Azure Active Directory, review the following tasks and topics:

- User accounts must be pre-provisioned into Amazon Web Services (AWS) prior to sign-in. To set this up, see Provisioning.
 
- Users must be assigned access to Amazon Web Services (AWS) in Azure AD to sign-in. To assign users, see Users.
 
- To configure access polices for Amazon Web Services (AWS) users, see Access Policies.
 
- For additional information on deploying single sign-on to users, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4f775-271">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4f775-271">Creating an Azure AD test user</span></span>
<span data-ttu-id="4f775-272">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4f775-272">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="4f775-274">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4f775-274">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4f775-275">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4f775-275">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4f775-277">Vá para **usuários e grupos** e clique em **todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="4f775-277">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4f775-279">Na parte superior da caixa de diálogo clique **adicionar** para abrir o **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4f775-279">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4f775-281">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4f775-281">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4f775-283">a.</span><span class="sxs-lookup"><span data-stu-id="4f775-283">a.</span></span> <span data-ttu-id="4f775-284">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="4f775-284">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4f775-285">b.</span><span class="sxs-lookup"><span data-stu-id="4f775-285">b.</span></span> <span data-ttu-id="4f775-286">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4f775-286">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4f775-287">c.</span><span class="sxs-lookup"><span data-stu-id="4f775-287">c.</span></span> <span data-ttu-id="4f775-288">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="4f775-288">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4f775-289">d.</span><span class="sxs-lookup"><span data-stu-id="4f775-289">d.</span></span> <span data-ttu-id="4f775-290">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="4f775-290">Click **Create**.</span></span>
 
### <a name="creating-an-amazon-web-services-test-user"></a><span data-ttu-id="4f775-291">Criação de um usuário de teste do Amazon Web Services</span><span class="sxs-lookup"><span data-stu-id="4f775-291">Creating an Amazon Web Services test user</span></span>

<span data-ttu-id="4f775-292">Para permitir que os usuários do Azure AD façam logon no AWS (Amazon Web Services), eles devem ser provisionados no AWS.</span><span class="sxs-lookup"><span data-stu-id="4f775-292">In order to enable Azure AD users to log in to Amazon Web Services (AWS), they must be provisioned into Amazon Web Services (AWS).</span></span> <span data-ttu-id="4f775-293">No caso do AWS, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="4f775-293">In the case of Amazon Web Services (AWS), provisioning is a manual task.</span></span>

<span data-ttu-id="4f775-294">**Para provisionar uma conta de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4f775-294">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="4f775-295">Faça logon no site da sua empresa **AWS (Amazon Web Services)** como administrador.</span><span class="sxs-lookup"><span data-stu-id="4f775-295">Log in to your **Amazon Web Services (AWS)** company site as administrator.</span></span>

2. <span data-ttu-id="4f775-296">Clique no ícone **Página Inicial do Console** .</span><span class="sxs-lookup"><span data-stu-id="4f775-296">Click the **Console Home** icon.</span></span> 
   
    ![Configurar Logon Único][11]

3. <span data-ttu-id="4f775-298">Clique em Gerenciamento de identidades e acesso.</span><span class="sxs-lookup"><span data-stu-id="4f775-298">Click Identity and Access Management.</span></span> 
   
    ![Configurar Logon Único][28]

4. <span data-ttu-id="4f775-300">No Painel, clique em **Usuários** e em **Criar Novos Usuários**.</span><span class="sxs-lookup"><span data-stu-id="4f775-300">In the Dashboard, click **Users**, and then click **Create New Users**.</span></span> 
   
    ![Configurar o logon único][29]

5. <span data-ttu-id="4f775-302">No diálogo Criar Usuário, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4f775-302">On the Create User dialog, perform the following steps:</span></span> 
   
    ![Configurar Logon Único][30]   
    
    <span data-ttu-id="4f775-304">a.</span><span class="sxs-lookup"><span data-stu-id="4f775-304">a.</span></span> <span data-ttu-id="4f775-305">Na caixa de texto **Inserir Nomes de Usuário** , digite o nome de usuário (userprincipalname) de Brenda Fernandes no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4f775-305">In the **Enter User Names** textboxes, type Brita Simon's user name (userprincipalname) in Azure AD.</span></span>

    <span data-ttu-id="4f775-306">b.</span><span class="sxs-lookup"><span data-stu-id="4f775-306">b.</span></span> <span data-ttu-id="4f775-307">Clicar em **Criar.**</span><span class="sxs-lookup"><span data-stu-id="4f775-307">Click **Create.**</span></span>
        
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4f775-308">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4f775-308">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4f775-309">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo a ela acesso ao AWS (Amazon Web Services).</span><span class="sxs-lookup"><span data-stu-id="4f775-309">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Amazon Web Services (AWS).</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="4f775-311">**Para atribuir Brenda Fernandes ao AWS (Amazon Web Services), execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4f775-311">**To assign Britta Simon to Amazon Web Services (AWS), perform the following steps:**</span></span>

1. <span data-ttu-id="4f775-312">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4f775-312">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="4f775-314">Na lista de aplicativos, selecione **AWS (Amazon Web Services)**.</span><span class="sxs-lookup"><span data-stu-id="4f775-314">In the applications list, select **Amazon Web Services (AWS)**.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_app.png) 

3. <span data-ttu-id="4f775-316">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="4f775-316">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="4f775-318">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4f775-318">Click **Add** button.</span></span> <span data-ttu-id="4f775-319">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4f775-319">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="4f775-321">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="4f775-321">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4f775-322">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4f775-322">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4f775-323">Na guia **Selecionar Função**, selecione a função apropriada para o usuário.</span><span class="sxs-lookup"><span data-stu-id="4f775-323">On **Select Role** tab, select the appropriate role for the user.</span></span> <span data-ttu-id="4f775-324">Todas essas funções são mostradas com o nome de função e o nome do provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="4f775-324">All these roles are shown with the role name and identity provider name.</span></span> <span data-ttu-id="4f775-325">Dessa forma, você pode identificar facilmente as funções do AWS.</span><span class="sxs-lookup"><span data-stu-id="4f775-325">This way you can easily identify the roles from AWS.</span></span>

8. <span data-ttu-id="4f775-326">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4f775-326">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4f775-327">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="4f775-327">Testing single sign-on</span></span>

<span data-ttu-id="4f775-328">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="4f775-328">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4f775-329">Ao clicar no bloco AWS (Amazon Web Services) no Painel de Acesso, você deve fazer logon automaticamente em seu aplicativo AWS (Amazon Web Services).</span><span class="sxs-lookup"><span data-stu-id="4f775-329">When you click the Amazon Web Services (AWS) tile in the Access Panel, you should get automatically signed-on to your Amazon Web Services (AWS) application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4f775-330">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="4f775-330">Additional resources</span></span>

* [<span data-ttu-id="4f775-331">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="4f775-331">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4f775-332">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4f775-332">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_203.png
[11]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795031.png
[12]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795032.png
[13]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795033.png
[14]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795034.png
[15]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795035.png
[16]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795022.png
[17]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795023.png
[18]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795024.png
[19]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795025.png
[20]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950351.png
[21]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_80.png
[22]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950352.png
[23]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_81.png
[24]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950353.png
[25]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_15.png

[28]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950321.png
[29]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795037.png
[30]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795038.png
[32]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950251.png
[33]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950252.png
[34]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950253.png
[35]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning.png
[36]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials.png
[37]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials_continue.png
[38]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_createnewaccesskey.png
[39]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_automatic.png
[40]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_testconnection.png
[41]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_on.png
