---
title: "Tutorial: Integração do Azure Active Directory ao Slack | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Slack."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffc5e73f-6c38-4bbb-876a-a7dd269d4e1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 5aca630b2077d3f7d4ce9273ee668ed6a5f9843d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-slack"></a><span data-ttu-id="ae51c-103">Tutorial: Integração do Active Directory do Azure com o Slack</span><span class="sxs-lookup"><span data-stu-id="ae51c-103">Tutorial: Azure Active Directory integration with Slack</span></span>

<span data-ttu-id="ae51c-104">Neste tutorial, você aprenderá a integrar o Slack ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="ae51c-104">In this tutorial, you learn how to integrate Slack with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ae51c-105">A integração do Slack ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="ae51c-105">Integrating Slack with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ae51c-106">Você pode controlar no Azure AD quem terá acesso ao Slack</span><span class="sxs-lookup"><span data-stu-id="ae51c-106">You can control in Azure AD who has access to Slack</span></span>
- <span data-ttu-id="ae51c-107">Você pode permitir que seus usuários façam logon automaticamente no Slack (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae51c-107">You can enable your users to automatically get signed-on to Slack (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ae51c-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ae51c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ae51c-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ae51c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae51c-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ae51c-110">Prerequisites</span></span>

<span data-ttu-id="ae51c-111">Para configurar a integração do Azure AD ao Slack, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="ae51c-111">To configure Azure AD integration with Slack, you need the following items:</span></span>

- <span data-ttu-id="ae51c-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ae51c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ae51c-113">Uma assinatura habilitada para logon único do Slack</span><span class="sxs-lookup"><span data-stu-id="ae51c-113">A Slack single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ae51c-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="ae51c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ae51c-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="ae51c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ae51c-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="ae51c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ae51c-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ae51c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ae51c-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="ae51c-118">Scenario description</span></span>
<span data-ttu-id="ae51c-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="ae51c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ae51c-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="ae51c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ae51c-121">Adicionar o Slack da galeria</span><span class="sxs-lookup"><span data-stu-id="ae51c-121">Adding Slack from the gallery</span></span>
2. <span data-ttu-id="ae51c-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ae51c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-slack-from-the-gallery"></a><span data-ttu-id="ae51c-123">Adicionar o Slack da galeria</span><span class="sxs-lookup"><span data-stu-id="ae51c-123">Adding Slack from the gallery</span></span>
<span data-ttu-id="ae51c-124">Para configurar a integração do Slack ao Azure AD, você precisa adicionar o Slack por meio da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="ae51c-124">To configure the integration of Slack into Azure AD, you need to add Slack from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ae51c-125">**Para adicionar o Slack por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ae51c-125">**To add Slack from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ae51c-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ae51c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ae51c-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="ae51c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ae51c-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ae51c-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="ae51c-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ae51c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="ae51c-133">Na caixa de pesquisa, digite **Slack**.</span><span class="sxs-lookup"><span data-stu-id="ae51c-133">In the search box, type **Slack**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-slack-tutorial/tutorial_slack_search.png)

5. <span data-ttu-id="ae51c-135">No painel de resultados, selecione **Slack** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ae51c-135">In the results panel, select **Slack**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-slack-tutorial/tutorial_slack_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ae51c-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ae51c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ae51c-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Slack, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="ae51c-138">In this section, you configure and test Azure AD single sign-on with Slack based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ae51c-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Slack é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae51c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Slack is to a user in Azure AD.</span></span> <span data-ttu-id="ae51c-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Slack.</span><span class="sxs-lookup"><span data-stu-id="ae51c-140">In other words, a link relationship between an Azure AD user and the related user in Slack needs to be established.</span></span>

<span data-ttu-id="ae51c-141">No Slack, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="ae51c-141">In Slack, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ae51c-142">Para configurar e testar o logon único do Azure AD com o Slack, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="ae51c-142">To configure and test Azure AD single sign-on with Slack, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ae51c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="ae51c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ae51c-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="ae51c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ae51c-145">**[Criando um usuário de teste do Slack](#creating-a-slack-test-user)** – para ter um equivalente de Brenda Fernandes no Slack que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae51c-145">**[Creating a Slack test user](#creating-a-slack-test-user)** - to have a counterpart of Britta Simon in Slack that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ae51c-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="ae51c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ae51c-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="ae51c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ae51c-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae51c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ae51c-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Slack.</span><span class="sxs-lookup"><span data-stu-id="ae51c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Slack application.</span></span>

<span data-ttu-id="ae51c-150">**Para configurar o logon único do Azure AD com o Slack, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ae51c-150">**To configure Azure AD single sign-on with Slack, perform the following steps:**</span></span>

1. <span data-ttu-id="ae51c-151">No portal do Azure, na página de integração de aplicativos do **Slack**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="ae51c-151">In the Azure portal, on the **Slack** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="ae51c-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="ae51c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-slack-tutorial/tutorial_slack_samlbase.png)

3. <span data-ttu-id="ae51c-155">Na seção **URLs e Domínio do Slack**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ae51c-155">On the **Slack Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-slack-tutorial/tutorial_slack_url.png)

    <span data-ttu-id="ae51c-157">a.</span><span class="sxs-lookup"><span data-stu-id="ae51c-157">a.</span></span> <span data-ttu-id="ae51c-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<companyname>.slack.com`</span><span class="sxs-lookup"><span data-stu-id="ae51c-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.slack.com`</span></span>

    <span data-ttu-id="ae51c-159">b.</span><span class="sxs-lookup"><span data-stu-id="ae51c-159">b.</span></span> <span data-ttu-id="ae51c-160">Na caixa de texto **Identificador**, digite a URL: `https://slack.com`</span><span class="sxs-lookup"><span data-stu-id="ae51c-160">In the **Identifier** textbox, type the URL: `https://slack.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ae51c-161">O valor não é real.</span><span class="sxs-lookup"><span data-stu-id="ae51c-161">The value is not real.</span></span> <span data-ttu-id="ae51c-162">Você precisa atualizar o valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="ae51c-162">You have to update the value with the actual Sign On URL.</span></span> <span data-ttu-id="ae51c-163">Contate a [equipe de suporte do Slack](https://slack.com/help/contact) para obter o valor</span><span class="sxs-lookup"><span data-stu-id="ae51c-163">Contact [Slack support team](https://slack.com/help/contact) to get the value</span></span>
     
4. <span data-ttu-id="ae51c-164">O aplicativo Slack espera que as declarações SAML estejam em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="ae51c-164">Slack application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="ae51c-165">Configure as declarações a seguir para este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ae51c-165">Configure the following claims for this application.</span></span> <span data-ttu-id="ae51c-166">Você pode gerenciar os valores desses atributos da seção "**Atributos de Usuário**" na página de integração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ae51c-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="ae51c-167">A captura de tela a seguir mostra um exemplo disso.</span><span class="sxs-lookup"><span data-stu-id="ae51c-167">The following screenshot shows an example for this.</span></span>
    
    ![Configurar o logon único](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute.png)

5. <span data-ttu-id="ae51c-169">Na seção **Atributos do Usuário**, na caixa de diálogo **Logon único**, selecione **user.mail** como **Identificador de Usuário** e, para cada linha mostrada na tabela a seguir, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ae51c-169">In the **User Attributes** section on the **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in the table below, perform the following steps:</span></span>
    
    | <span data-ttu-id="ae51c-170">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="ae51c-170">Attribute Name</span></span> | <span data-ttu-id="ae51c-171">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="ae51c-171">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="ae51c-172">first_name</span><span class="sxs-lookup"><span data-stu-id="ae51c-172">first_name</span></span> | <span data-ttu-id="ae51c-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="ae51c-173">user.givenname</span></span> |
    | <span data-ttu-id="ae51c-174">last_name</span><span class="sxs-lookup"><span data-stu-id="ae51c-174">last_name</span></span> | <span data-ttu-id="ae51c-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="ae51c-175">user.surname</span></span> |
    | <span data-ttu-id="ae51c-176">User.Email</span><span class="sxs-lookup"><span data-stu-id="ae51c-176">User.Email</span></span> | <span data-ttu-id="ae51c-177">user.mail</span><span class="sxs-lookup"><span data-stu-id="ae51c-177">user.mail</span></span> |  
    | <span data-ttu-id="ae51c-178">User.Username</span><span class="sxs-lookup"><span data-stu-id="ae51c-178">User.Username</span></span> | <span data-ttu-id="ae51c-179">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="ae51c-179">user.userprincipalname</span></span> |

    <span data-ttu-id="ae51c-180">a.</span><span class="sxs-lookup"><span data-stu-id="ae51c-180">a.</span></span> <span data-ttu-id="ae51c-181">Clique em **Atributo** para abrir a caixa de diálogo **Editar Atributo** e realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ae51c-181">Click on **Attribute** to open **Edit Attribute** dialog box and perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute1.png)

    <span data-ttu-id="ae51c-183">a.</span><span class="sxs-lookup"><span data-stu-id="ae51c-183">a.</span></span> <span data-ttu-id="ae51c-184">Na caixa de texto **Nome** , digite o nome do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="ae51c-184">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="ae51c-185">b.</span><span class="sxs-lookup"><span data-stu-id="ae51c-185">b.</span></span> <span data-ttu-id="ae51c-186">Na lista **Valor**, selecione o valor de atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="ae51c-186">From the **Value** list, select the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="ae51c-187">c.</span><span class="sxs-lookup"><span data-stu-id="ae51c-187">c.</span></span> <span data-ttu-id="ae51c-188">Clique em **OK**</span><span class="sxs-lookup"><span data-stu-id="ae51c-188">Click **OK**</span></span>

6. <span data-ttu-id="ae51c-189">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="ae51c-189">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-slack-tutorial/tutorial_slack_certificate.png)

7. <span data-ttu-id="ae51c-191">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="ae51c-191">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-slack-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="ae51c-193">Na seção **Configuração do Slack**, clique em **Configurar o Slack** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="ae51c-193">On the **Slack Configuration** section, click **Configure Slack** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ae51c-194">Copie a **ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="ae51c-194">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-slack-tutorial/tutorial_slack_configure.png) 

9.  <span data-ttu-id="ae51c-196">Em outra janela do navegador da Web, faça logon em seu site de empresa do Slack como administrador.</span><span class="sxs-lookup"><span data-stu-id="ae51c-196">In a different web browser window, log in to your Slack company site as an administrator.</span></span>

10.  <span data-ttu-id="ae51c-197">Navegue até **Microsoft Azure AD** e depois em **Configurações de Equipe**.</span><span class="sxs-lookup"><span data-stu-id="ae51c-197">Navigate to **Microsoft Azure AD** then go to **Team Settings**.</span></span>

     ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-slack-tutorial/tutorial_slack_001.png)

11.  <span data-ttu-id="ae51c-199">Na seção **Configurações de Equipe**, clique na guia **Autenticação** e em **Alterar Configurações**.</span><span class="sxs-lookup"><span data-stu-id="ae51c-199">In the **Team Settings** section, click the **Authentication** tab, and then click **Change Settings**.</span></span>

     ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-slack-tutorial/tutorial_slack_002.png)

12. <span data-ttu-id="ae51c-201">No diálogo **Configurações de Autenticação SAML** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ae51c-201">On the **SAML Authentication Settings** dialog, perform the following steps:</span></span>

    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-slack-tutorial/tutorial_slack_003.png)

    <span data-ttu-id="ae51c-203">a.</span><span class="sxs-lookup"><span data-stu-id="ae51c-203">a.</span></span>  <span data-ttu-id="ae51c-204">Na caixa de texto **Ponto de Extremidade do SAML 2.0 (HTTP)**, cole o valor da **URL do Serviço de Logon Único SAML** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ae51c-204">In the **SAML 2.0 Endpoint (HTTP)** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="ae51c-205">b.</span><span class="sxs-lookup"><span data-stu-id="ae51c-205">b.</span></span>  <span data-ttu-id="ae51c-206">Na caixa de texto **Emissor do Provedor de Identidade**, cole o valor da **ID da Entidade SAML** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ae51c-206">In the **Identity Provider Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="ae51c-207">c.</span><span class="sxs-lookup"><span data-stu-id="ae51c-207">c.</span></span>  <span data-ttu-id="ae51c-208">Abra seu arquivo de certificado baixado no bloco de notas, copie o conteúdo dele na área de transferência e cole-o na caixa de texto **Certificado Público**.</span><span class="sxs-lookup"><span data-stu-id="ae51c-208">Open your downloaded certificate file in notepad, copy the content of it into your clipboard, and then paste it to the **Public Certificate** textbox.</span></span>

    <span data-ttu-id="ae51c-209">d.</span><span class="sxs-lookup"><span data-stu-id="ae51c-209">d.</span></span> <span data-ttu-id="ae51c-210">Defina as três configurações acima conforme apropriado para sua equipe do Slack.</span><span class="sxs-lookup"><span data-stu-id="ae51c-210">Configure the above three settings as appropriate for your Slack team.</span></span> <span data-ttu-id="ae51c-211">Para saber mais sobre as configurações, encontre o **guia de configuração de SSO do Slack** aqui.</span><span class="sxs-lookup"><span data-stu-id="ae51c-211">For more information about the settings, please find the **Slack's SSO configuration guide** here.</span></span> `https://get.slack.help/hc/articles/220403548-Guide-to-single-sign-on-with-Slack%60`

    <span data-ttu-id="ae51c-212">e.</span><span class="sxs-lookup"><span data-stu-id="ae51c-212">e.</span></span>  <span data-ttu-id="ae51c-213">Clique em **Salvar Configuração**.</span><span class="sxs-lookup"><span data-stu-id="ae51c-213">Click **Save Configuration**.</span></span>
     
    <!-- Deselect **Allow users to change their email address**.

    e.  Select **Allow users to choose their own username**.

    f.  As **Authentication for your team must be used by**, select **It’s optional**. -->

> [!TIP]
> <span data-ttu-id="ae51c-214">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="ae51c-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ae51c-215">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="ae51c-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ae51c-216">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ae51c-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ae51c-217">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ae51c-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="ae51c-218">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="ae51c-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="ae51c-220">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ae51c-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ae51c-221">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ae51c-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-slack-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ae51c-223">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="ae51c-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-slack-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ae51c-225">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ae51c-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-slack-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ae51c-227">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ae51c-227">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-slack-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ae51c-229">a.</span><span class="sxs-lookup"><span data-stu-id="ae51c-229">a.</span></span> <span data-ttu-id="ae51c-230">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="ae51c-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ae51c-231">b.</span><span class="sxs-lookup"><span data-stu-id="ae51c-231">b.</span></span> <span data-ttu-id="ae51c-232">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="ae51c-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ae51c-233">c.</span><span class="sxs-lookup"><span data-stu-id="ae51c-233">c.</span></span> <span data-ttu-id="ae51c-234">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="ae51c-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ae51c-235">d.</span><span class="sxs-lookup"><span data-stu-id="ae51c-235">d.</span></span> <span data-ttu-id="ae51c-236">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="ae51c-236">Click **Create**.</span></span>
 
### <a name="creating-a-slack-test-user"></a><span data-ttu-id="ae51c-237">Criar um usuário de teste do Slack</span><span class="sxs-lookup"><span data-stu-id="ae51c-237">Creating a Slack test user</span></span>

<span data-ttu-id="ae51c-238">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no Slack.</span><span class="sxs-lookup"><span data-stu-id="ae51c-238">The objective of this section is to create a user called Britta Simon in Slack.</span></span> <span data-ttu-id="ae51c-239">O Slack dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="ae51c-239">Slack supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="ae51c-240">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="ae51c-240">There is no action item for you in this section.</span></span> <span data-ttu-id="ae51c-241">Um novo usuário é criado durante uma tentativa de acessar o Slack, caso ele ainda não exista.</span><span class="sxs-lookup"><span data-stu-id="ae51c-241">A new user is created during an attempt to access Slack if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="ae51c-242">Se você precisar criar um usuário manualmente, contate a [equipe de suporte do Slack](https://slack.com/help/contact).</span><span class="sxs-lookup"><span data-stu-id="ae51c-242">If you need to create a user manually, you need to Contact [Slack support team](https://slack.com/help/contact).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ae51c-243">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ae51c-243">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ae51c-244">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Slack.</span><span class="sxs-lookup"><span data-stu-id="ae51c-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Slack.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="ae51c-246">**Para atribuir Brenda Fernandes ao Slack, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ae51c-246">**To assign Britta Simon to Slack, perform the following steps:**</span></span>

1. <span data-ttu-id="ae51c-247">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ae51c-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="ae51c-249">Na lista de aplicativos, escolha **Slack**.</span><span class="sxs-lookup"><span data-stu-id="ae51c-249">In the applications list, select **Slack**.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-slack-tutorial/tutorial_slack_app.png) 

3. <span data-ttu-id="ae51c-251">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="ae51c-251">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="ae51c-253">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ae51c-253">Click **Add** button.</span></span> <span data-ttu-id="ae51c-254">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ae51c-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="ae51c-256">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="ae51c-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ae51c-257">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ae51c-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ae51c-258">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ae51c-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ae51c-259">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="ae51c-259">Testing single sign-on</span></span>

<span data-ttu-id="ae51c-260">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="ae51c-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ae51c-261">Ao clicar no bloco Slack no Painel de Acesso, você deverá ser conectado automaticamente ao aplicativo de Slack.</span><span class="sxs-lookup"><span data-stu-id="ae51c-261">When you click the Slack tile in the Access Panel, you should get automatically signed-on to your Slack application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ae51c-262">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="ae51c-262">Additional resources</span></span>

* [<span data-ttu-id="ae51c-263">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="ae51c-263">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ae51c-264">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ae51c-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-slack-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-slack-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-slack-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-slack-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-slack-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-slack-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-slack-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-slack-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-slack-tutorial/tutorial_general_203.png

