---
title: "Tutorial: integração do Azure Active Directory com o TINFOIL SECURITY | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o TINFOIL SECURITY."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: da02da92-e3b0-4c09-ad6c-180882b0f9f8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 614e4de3335574f4b56c7d641af4fcfafdb17d12
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tinfoil-security"></a><span data-ttu-id="6bc3f-103">Tutorial: integração do Azure Active Directory com o TINFOIL SECURITY</span><span class="sxs-lookup"><span data-stu-id="6bc3f-103">Tutorial: Azure Active Directory integration with TINFOIL SECURITY</span></span>

<span data-ttu-id="6bc3f-104">Neste tutorial, você aprenderá como integrar o TINFOIL SECURITY ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="6bc3f-104">In this tutorial, you learn how to integrate TINFOIL SECURITY with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6bc3f-105">A integração do TINFOIL SECURITY com o Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="6bc3f-105">Integrating TINFOIL SECURITY with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6bc3f-106">No Azure AD, é possível controlar quem tem acesso ao TINFOIL SECURITY</span><span class="sxs-lookup"><span data-stu-id="6bc3f-106">You can control in Azure AD who has access to TINFOIL SECURITY</span></span>
- <span data-ttu-id="6bc3f-107">É possível permitir que seus usuários façam logon automaticamente no TINFOIL SECURITY (logon único) com as contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6bc3f-107">You can enable your users to automatically get signed-on to TINFOIL SECURITY (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6bc3f-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6bc3f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6bc3f-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6bc3f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6bc3f-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6bc3f-110">Prerequisites</span></span>

<span data-ttu-id="6bc3f-111">Para configurar a integração do Azure AD com o TINFOIL SECURITY, serão necessários os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="6bc3f-111">To configure Azure AD integration with TINFOIL SECURITY, you need the following items:</span></span>

- <span data-ttu-id="6bc3f-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6bc3f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6bc3f-113">Uma assinatura do TINFOIL SECURITY habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="6bc3f-113">A TINFOIL SECURITY single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6bc3f-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6bc3f-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="6bc3f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6bc3f-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6bc3f-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6bc3f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6bc3f-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="6bc3f-118">Scenario description</span></span>
<span data-ttu-id="6bc3f-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6bc3f-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="6bc3f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6bc3f-121">Adicionar TINFOIL SECURITY da galeria</span><span class="sxs-lookup"><span data-stu-id="6bc3f-121">Add TINFOIL SECURITY from the gallery</span></span>
2. <span data-ttu-id="6bc3f-122">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6bc3f-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tinfoil-security-from-the-gallery"></a><span data-ttu-id="6bc3f-123">Adicionar TINFOIL SECURITY da galeria</span><span class="sxs-lookup"><span data-stu-id="6bc3f-123">Add TINFOIL SECURITY from the gallery</span></span>
<span data-ttu-id="6bc3f-124">Para configurar a integração do TINFOIL SECURITY com o Azure AD, é necessário adicionar o TINFOIL SECURITY da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-124">To configure the integration of TINFOIL SECURITY into Azure AD, you need to add TINFOIL SECURITY from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6bc3f-125">**Para adicionar o TINFOIL SECURITY da galeria, siga as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="6bc3f-125">**To add TINFOIL SECURITY from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6bc3f-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6bc3f-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6bc3f-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="6bc3f-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="6bc3f-133">Na caixa de pesquisa, digite **TINFOIL SECURITY**, selecione **TINFOIL SECURITY** no painel de resultados e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-133">In the search box, type **TINFOIL SECURITY**, select  **TINFOIL SECURITY** from result panel then click **Add** button to add the application.</span></span>

    ![TINFOIL SECURITY da galeria](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6bc3f-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6bc3f-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="6bc3f-136">Nesta seção, você configurará e testará o logon único do Azure AD com o TINFOIL SECURITY com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-136">In this section, you configure and test Azure AD single sign-on with TINFOIL SECURITY based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6bc3f-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do TINFOIL SECURITY é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TINFOIL SECURITY is to a user in Azure AD.</span></span> <span data-ttu-id="6bc3f-138">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-138">In other words, a link relationship between an Azure AD user and the related user in TINFOIL SECURITY needs to be established.</span></span>

<span data-ttu-id="6bc3f-139">No TINFOIL SECURITY, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-139">In TINFOIL SECURITY, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6bc3f-140">Para configurar e testar o logon único do Azure AD com o TINFOIL SECURITY, é necessário concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="6bc3f-140">To configure and test Azure AD single sign-on with TINFOIL SECURITY, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6bc3f-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6bc3f-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6bc3f-143">**[Criar um usuário de teste do TINFOIL SECURITY](#create-a-tinfoil-security-test-user)** – para ter um equivalente de Brenda Fernandes no TINFOIL SECURITY que esteja vinculado à representação de usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-143">**[Create a TINFOIL SECURITY test user](#create-a-tinfoil-security-test-user)** - to have a counterpart of Britta Simon in TINFOIL SECURITY that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6bc3f-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6bc3f-145">**[Testar o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6bc3f-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6bc3f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="6bc3f-147">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único em seu aplicativo TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TINFOIL SECURITY application.</span></span>

<span data-ttu-id="6bc3f-148">**Para configurar o logon único do Azure AD com o TINFOIL SECURITY, siga as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="6bc3f-148">**To configure Azure AD single sign-on with TINFOIL SECURITY, perform the following steps:**</span></span>

1. <span data-ttu-id="6bc3f-149">No Portal do Azure, na página de integração de aplicativos do **TINFOIL SECURITY**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-149">In the Azure portal, on the **TINFOIL SECURITY** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="6bc3f-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Logon baseado em SAML](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_samlbase.png)

3. <span data-ttu-id="6bc3f-153">Na seção **URLs e Domínio do TINFOIL SECURITY**, o usuário não precisa seguir nenhuma etapa, uma vez que o aplicativo já está integrado ao Azure.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-153">On the **TINFOIL SECURITY Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_url.png)


4. <span data-ttu-id="6bc3f-155">Na seção **Certificado de Autenticação SAML**, copie o valor da **IMPRESSÃO DIGITAL**.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-155">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value.</span></span>

    ![Seção Certificado de Autenticação SAML](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_certificate.png) 

5. <span data-ttu-id="6bc3f-157">Para adicionar os mapeamentos de atributo necessários, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="6bc3f-157">To add the required attribute mappings, perform the following steps:</span></span>
    
    <span data-ttu-id="6bc3f-158">![Atributos](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "Atributos")</span><span class="sxs-lookup"><span data-stu-id="6bc3f-158">![Attributes](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "Attributes")</span></span>
    
    | <span data-ttu-id="6bc3f-159">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="6bc3f-159">Attribute Name</span></span>    |   <span data-ttu-id="6bc3f-160">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="6bc3f-160">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="6bc3f-161">accountid</span><span class="sxs-lookup"><span data-stu-id="6bc3f-161">accountid</span></span> | <span data-ttu-id="6bc3f-162">UXXXXXXXXXXXXX</span><span class="sxs-lookup"><span data-stu-id="6bc3f-162">UXXXXXXXXXXXXX</span></span> |
    
    <span data-ttu-id="6bc3f-163">a.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-163">a.</span></span> <span data-ttu-id="6bc3f-164">Clique em **adicionar atributo de usuário**.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-164">Click **add user attribute**.</span></span>
    
    <span data-ttu-id="6bc3f-165">![ADICIONAR atributo](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "Atributos")</span><span class="sxs-lookup"><span data-stu-id="6bc3f-165">![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "Attributes")</span></span>
    
    <span data-ttu-id="6bc3f-166">![ADICIONAR atributo](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "Atributos")</span><span class="sxs-lookup"><span data-stu-id="6bc3f-166">![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "Attributes")</span></span>
    
    <span data-ttu-id="6bc3f-167">b.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-167">b.</span></span> <span data-ttu-id="6bc3f-168">Na caixa de texto **Nome do Atributo**, digite **accountid**.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-168">In the **Attribute Name** textbox, type **accountid**.</span></span>
    
    <span data-ttu-id="6bc3f-169">c.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-169">c.</span></span> <span data-ttu-id="6bc3f-170">Na caixa de texto **Valor do atributo**, cole o valor da ID da conta que você obterá posteriormente no tutorial.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-170">In the **Attribute Value** textbox, paste the account ID value which you will get later on the tutorial.</span></span>
    
    <span data-ttu-id="6bc3f-171">d.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-171">d.</span></span> <span data-ttu-id="6bc3f-172">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-172">Click **Ok**.</span></span>    

6. <span data-ttu-id="6bc3f-173">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="6bc3f-173">Click **Save** button.</span></span>

    ![Botão Salvar](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="6bc3f-175">Na seção **Configuração do TINFOIL SECURITY**, clique em **Configurar o TINFOIL SECURITY** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-175">On the **TINFOIL SECURITY Configuration** section, click **Configure TINFOIL SECURITY** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6bc3f-176">Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="6bc3f-176">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuração do TINFOIL SECURITY](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_configure.png) 

8. <span data-ttu-id="6bc3f-178">Em uma janela diferente do navegador da Web, faça logon no site da empresa TINFOIL SECURITY como administrador.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-178">In a different web browser window, log into your TINFOIL SECURITY company site as an administrator.</span></span>

9. <span data-ttu-id="6bc3f-179">Na barra de ferramentas na parte superior, clique em **Minha Conta**.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-179">In the toolbar on the top, click **My Account**.</span></span>
   
    <span data-ttu-id="6bc3f-180">![Painel](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "Painel")</span><span class="sxs-lookup"><span data-stu-id="6bc3f-180">![Dashboard](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "Dashboard")</span></span>

10. <span data-ttu-id="6bc3f-181">Clique em **Segurança**.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-181">Click **Security**.</span></span>
   
    <span data-ttu-id="6bc3f-182">![Segurança](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "Segurança")</span><span class="sxs-lookup"><span data-stu-id="6bc3f-182">![Security](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "Security")</span></span>

11. <span data-ttu-id="6bc3f-183">Na página de configuração **Logon Único** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="6bc3f-183">On the **Single Sign-On** configuration page, perform the following steps:</span></span>
   
    <span data-ttu-id="6bc3f-184">![Logon Único](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "Logon Único")</span><span class="sxs-lookup"><span data-stu-id="6bc3f-184">![Single Sign-On](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "Single Sign-On")</span></span>
   
    <span data-ttu-id="6bc3f-185">a.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-185">a.</span></span> <span data-ttu-id="6bc3f-186">Selecione **Habilitar SAML**.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-186">Select **Enable SAML**.</span></span>
   
    <span data-ttu-id="6bc3f-187">b.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-187">b.</span></span> <span data-ttu-id="6bc3f-188">Clique em **Configuração Manual**.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-188">Click **Manual Configuration**.</span></span>
   
    <span data-ttu-id="6bc3f-189">c.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-189">c.</span></span> <span data-ttu-id="6bc3f-190">Na caixa de texto **URL da Postagem SAML**, cole o valor da **URL do Serviço de Logon Único SAML** copiada do Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6bc3f-190">In **SAML Post URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal</span></span>
   
    <span data-ttu-id="6bc3f-191">d.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-191">d.</span></span> <span data-ttu-id="6bc3f-192">Na caixa de texto **Impressão Digital do Certificado SAML**, cole o valor de **Impressão Digital** copiado da seção **Certificado de Autenticação SAML**.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-192">In **SAML Certificate Fingerprint** textbox, paste the value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span></span>
  
    <span data-ttu-id="6bc3f-193">e.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-193">e.</span></span> <span data-ttu-id="6bc3f-194">Copie o valor da **ID da Sua Conta** e cole-o na caixa de texto **Valor do Atributo** na seção **Adicionar Atributo** no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-194">Copy **Your Account ID** value and paste the value in **Attribute Value** textbox under **Add Attribute** section in Azure portal.</span></span>
   
    <span data-ttu-id="6bc3f-195">f.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-195">f.</span></span> <span data-ttu-id="6bc3f-196">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-196">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="6bc3f-197">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="6bc3f-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6bc3f-198">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6bc3f-199">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6bc3f-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6bc3f-200">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6bc3f-200">Create an Azure AD test user</span></span>
<span data-ttu-id="6bc3f-201">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="6bc3f-203">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="6bc3f-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6bc3f-204">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6bc3f-206">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![<span data-ttu-id="6bc3f-207">Usuários e grupos -> Todos os usuários</span><span class="sxs-lookup"><span data-stu-id="6bc3f-207">Users and groups -> All users</span></span> ](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6bc3f-208">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Usuário](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6bc3f-210">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="6bc3f-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6bc3f-212">a.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-212">a.</span></span> <span data-ttu-id="6bc3f-213">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6bc3f-214">b.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-214">b.</span></span> <span data-ttu-id="6bc3f-215">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6bc3f-216">c.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-216">c.</span></span> <span data-ttu-id="6bc3f-217">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6bc3f-218">d.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-218">d.</span></span> <span data-ttu-id="6bc3f-219">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-219">Click **Create**.</span></span>
 
### <a name="create-a-tinfoil-security-test-user"></a><span data-ttu-id="6bc3f-220">Criar um usuário de teste do TINFOIL SECURITY</span><span class="sxs-lookup"><span data-stu-id="6bc3f-220">Create a TINFOIL SECURITY test user</span></span>

<span data-ttu-id="6bc3f-221">Para permitir que os usuários do Azure AD façam logon no TINFOIL SECURITY, eles devem ser provisionados no TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-221">In order to enable Azure AD users to log into TINFOIL SECURITY, they must be provisioned into TINFOIL SECURITY.</span></span> <span data-ttu-id="6bc3f-222">No caso do TINFOIL SECURITY, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-222">In the case of TINFOIL SECURITY, provisioning is a manual task.</span></span>

<span data-ttu-id="6bc3f-223">**Para provisionar um usuário, siga as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="6bc3f-223">**To get a user provisioned, perform the following steps:**</span></span>

1. <span data-ttu-id="6bc3f-224">Se o usuário fizer parte de uma conta Enterprise, será necessário [contatar a equipe de suporte do TINFOIL SECURITY](https://www.tinfoilsecurity.com/contact) para que a conta de usuário seja criada.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-224">If the user is a part of an Enterprise account, you need to [contact the TINFOIL SECURITY support team](https://www.tinfoilsecurity.com/contact) to get the user account created.</span></span>

2. <span data-ttu-id="6bc3f-225">Se o usuário for um usuário de SaaS do TINFOIL SECURITY regular, ele poderá adicionar um colaborador a qualquer um dos sites do usuário.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-225">If the user is a regular TINFOIL SECURITY SaaS user, then the user can add a collaborator to any of the user’s sites.</span></span> <span data-ttu-id="6bc3f-226">Isso dispara um processo para enviar um convite ao email especificado para criar uma nova conta de usuário do TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-226">This triggers a process to send an invitation to the specified email to create a new TINFOIL SECURITY user account.</span></span>

> [!NOTE]
> <span data-ttu-id="6bc3f-227">É possível usar qualquer outra ferramenta de criação de conta de usuário do TINFOIL SECURITY ou APIs fornecidas pelo TINFOIL SECURITY para provisionar as contas de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-227">You can use any other TINFOIL SECURITY user account creation tools or APIs provided by TINFOIL SECURITY to provision Azure AD user accounts.</span></span>
> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="6bc3f-228">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6bc3f-228">Assign the Azure AD test user</span></span>

<span data-ttu-id="6bc3f-229">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure, concedendo acesso ao TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TINFOIL SECURITY.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="6bc3f-231">**Para atribuir Brenda Fernandes ao TINFOIL SECURITY, siga as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="6bc3f-231">**To assign Britta Simon to TINFOIL SECURITY, perform the following steps:**</span></span>

1. <span data-ttu-id="6bc3f-232">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="6bc3f-234">Na lista de aplicativos, selecione **TINFOIL SECURITY**.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-234">In the applications list, select **TINFOIL SECURITY**.</span></span>

    ![selecione TINFOIL SECURITY](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_app.png) 

3. <span data-ttu-id="6bc3f-236">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-236">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="6bc3f-238">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-238">Click **Add** button.</span></span> <span data-ttu-id="6bc3f-239">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="6bc3f-241">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6bc3f-242">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6bc3f-243">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="6bc3f-244">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="6bc3f-244">Test single sign-on</span></span>

<span data-ttu-id="6bc3f-245">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6bc3f-246">Quando você clicar no bloco TINFOIL SECURITY no Painel de Acesso, você deverá entrar automaticamente no seu aplicativo TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="6bc3f-246">When you click the TINFOIL SECURITY tile in the Access Panel, you should get automatically signed-on to your TINFOIL SECURITY application.</span></span> <span data-ttu-id="6bc3f-247">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6bc3f-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6bc3f-248">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="6bc3f-248">Additional resources</span></span>

* [<span data-ttu-id="6bc3f-249">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="6bc3f-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6bc3f-250">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6bc3f-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_203.png

