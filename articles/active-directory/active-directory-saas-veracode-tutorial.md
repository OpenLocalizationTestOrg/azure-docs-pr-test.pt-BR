---
title: "Tutorial: Integração do Azure Active Directory com o Veracode | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Veracode."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4fe78050-cb6d-4db9-96ec-58cc0779167f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: d49349c5ae08e67d91e30967f3644623211823ce
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-veracode"></a><span data-ttu-id="235f5-103">Tutorial: Integração do Active Directory do Azure com o Veracode</span><span class="sxs-lookup"><span data-stu-id="235f5-103">Tutorial: Azure Active Directory integration with Veracode</span></span>

<span data-ttu-id="235f5-104">Neste tutorial, você aprenderá a integrar o Veracode ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="235f5-104">In this tutorial, you learn how to integrate Veracode with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="235f5-105">A integração do Veracode ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="235f5-105">Integrating Veracode with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="235f5-106">No Azure AD, é possível controlar quem tem acesso ao Veracode.</span><span class="sxs-lookup"><span data-stu-id="235f5-106">You can control in Azure AD who has access to Veracode.</span></span>
- <span data-ttu-id="235f5-107">Você pode permitir que os usuários façam logon automaticamente no Veracode (logon único) com as respectivas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="235f5-107">You can enable your users to automatically get signed-on to Veracode (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="235f5-108">Você pode gerenciar suas contas em um único local central – o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="235f5-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="235f5-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="235f5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="235f5-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="235f5-110">Prerequisites</span></span>

<span data-ttu-id="235f5-111">Para configurar a integração do Azure AD ao Veracode, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="235f5-111">To configure Azure AD integration with Veracode, you need the following items:</span></span>

- <span data-ttu-id="235f5-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="235f5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="235f5-113">Uma assinatura do Veracode habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="235f5-113">A Veracode single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="235f5-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="235f5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="235f5-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="235f5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="235f5-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="235f5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="235f5-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="235f5-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="235f5-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="235f5-118">Scenario description</span></span>
<span data-ttu-id="235f5-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="235f5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="235f5-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="235f5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="235f5-121">Adicionar o Veracode da galeria</span><span class="sxs-lookup"><span data-stu-id="235f5-121">Add Veracode from the gallery</span></span>
2. <span data-ttu-id="235f5-122">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="235f5-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-veracode-from-the-gallery"></a><span data-ttu-id="235f5-123">Adicionar o Veracode da galeria</span><span class="sxs-lookup"><span data-stu-id="235f5-123">Add Veracode from the gallery</span></span>
<span data-ttu-id="235f5-124">Para configurar a integração do Veracode ao Azure AD, você precisará adicionar o Veracode da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="235f5-124">To configure the integration of Veracode into Azure AD, you need to add Veracode from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="235f5-125">**Para adicionar o Veracode da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="235f5-125">**To add Veracode from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="235f5-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="235f5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="235f5-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="235f5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="235f5-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="235f5-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="235f5-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="235f5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="235f5-133">Na caixa de pesquisa, digite **Veracode**, selecione **Veracode** no painel de resultados e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="235f5-133">In the search box, type **Veracode**, select  **Veracode** from result panel then click **Add** button to add the application.</span></span>

    ![Veracode na lista de resultados](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="235f5-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="235f5-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="235f5-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Veracode, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="235f5-136">In this section, you configure and test Azure AD single sign-on with Veracode based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="235f5-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Veracode é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="235f5-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Veracode is to a user in Azure AD.</span></span> <span data-ttu-id="235f5-138">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Veracode.</span><span class="sxs-lookup"><span data-stu-id="235f5-138">In other words, a link relationship between an Azure AD user and the related user in Veracode needs to be established.</span></span>

<span data-ttu-id="235f5-139">No Veracode, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="235f5-139">In Veracode, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="235f5-140">Para configurar e testar o logon único do Azure AD com o Veracode, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="235f5-140">To configure and test Azure AD single sign-on with Veracode, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="235f5-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="235f5-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="235f5-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="235f5-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="235f5-143">**[Criar um usuário de teste do Veracode](#create-a-veracode-test-user)** – para ter um equivalente de Brenda Fernandes no Veracode vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="235f5-143">**[Create a Veracode test user](#create-a-veracode-test-user)** - to have a counterpart of Britta Simon in Veracode that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="235f5-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="235f5-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="235f5-145">**[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="235f5-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="235f5-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="235f5-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="235f5-147">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo Veracode.</span><span class="sxs-lookup"><span data-stu-id="235f5-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Veracode application.</span></span>

<span data-ttu-id="235f5-148">**Para configurar o logon único do Azure AD com o Veracode, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="235f5-148">**To configure Azure AD single sign-on with Veracode, perform the following steps:**</span></span>

1. <span data-ttu-id="235f5-149">No Portal do Azure, na página de integração de aplicativos do **Veracode**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="235f5-149">In the Azure portal, on the **Veracode** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="235f5-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="235f5-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_samlbase.png)

3. <span data-ttu-id="235f5-153">Na seção **URLs e Domínio do Veracode**, o usuário não precisa executar nenhuma etapa, já que o aplicativo já está pré-integrado ao Azure.</span><span class="sxs-lookup"><span data-stu-id="235f5-153">On the **Veracode Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_url.png)

4. <span data-ttu-id="235f5-155">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="235f5-155">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_certificate.png) 

5. <span data-ttu-id="235f5-157">O objetivo desta seção é descrever como permitir que os usuários se autentiquem no Veracode com sua conta do AD do Azure usando a federação baseada no protocolo SAML.</span><span class="sxs-lookup"><span data-stu-id="235f5-157">The objective of this section is to outline how to enable users to authenticate to Veracode with their account in Azure AD using federation based on the SAML protocol.</span></span>

    <span data-ttu-id="235f5-158">Seu aplicativo Veracode espera as declarações do SAML em um formato específico, o que exige que você adicione mapeamentos de atributo personalizados de acordo com a sua configuração de **atributos de token SAML** .</span><span class="sxs-lookup"><span data-stu-id="235f5-158">Your Veracode application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span></span> <span data-ttu-id="235f5-159">A captura de tela a seguir mostra um exemplo disso.</span><span class="sxs-lookup"><span data-stu-id="235f5-159">The following screenshot shows an example for this.</span></span>
    
    <span data-ttu-id="235f5-160">![Atributos](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "Atributos")</span><span class="sxs-lookup"><span data-stu-id="235f5-160">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "Attributes")</span></span>

6. <span data-ttu-id="235f5-161">Para adicionar os mapeamentos de atributo necessários, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="235f5-161">To add the required attribute mappings, perform the following steps:</span></span>

    | <span data-ttu-id="235f5-162">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="235f5-162">Attribute Name</span></span> | <span data-ttu-id="235f5-163">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="235f5-163">Attribute Value</span></span> |
    |--- |--- |
    | <span data-ttu-id="235f5-164">nome</span><span class="sxs-lookup"><span data-stu-id="235f5-164">firstname</span></span> |<span data-ttu-id="235f5-165">User.givenname</span><span class="sxs-lookup"><span data-stu-id="235f5-165">User.givenname</span></span> |
    | <span data-ttu-id="235f5-166">sobrenome</span><span class="sxs-lookup"><span data-stu-id="235f5-166">lastname</span></span> |<span data-ttu-id="235f5-167">User.surname</span><span class="sxs-lookup"><span data-stu-id="235f5-167">User.surname</span></span> |
    | <span data-ttu-id="235f5-168">email</span><span class="sxs-lookup"><span data-stu-id="235f5-168">email</span></span> |<span data-ttu-id="235f5-169">User.mail</span><span class="sxs-lookup"><span data-stu-id="235f5-169">User.mail</span></span> |
    
    <span data-ttu-id="235f5-170">a.</span><span class="sxs-lookup"><span data-stu-id="235f5-170">a.</span></span> <span data-ttu-id="235f5-171">Para cada linha de dados na tabela acima, clique em **adicionar atributo do usuário**.</span><span class="sxs-lookup"><span data-stu-id="235f5-171">For each data row in the table above, click **add user attribute**.</span></span>
    
    <span data-ttu-id="235f5-172">![Atributos](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "Atributos")</span><span class="sxs-lookup"><span data-stu-id="235f5-172">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "Attributes")</span></span>
    
    <span data-ttu-id="235f5-173">![Atributos](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "Atributos")</span><span class="sxs-lookup"><span data-stu-id="235f5-173">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "Attributes")</span></span>
    
    <span data-ttu-id="235f5-174">b.</span><span class="sxs-lookup"><span data-stu-id="235f5-174">b.</span></span> <span data-ttu-id="235f5-175">Na caixa de texto **Nome do Atributo** , digite o nome do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="235f5-175">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="235f5-176">c.</span><span class="sxs-lookup"><span data-stu-id="235f5-176">c.</span></span> <span data-ttu-id="235f5-177">Na caixa de texto **Valor do Atributo** , selecione o valor do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="235f5-177">In the **Attribute Value** textbox, select the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="235f5-178">d.</span><span class="sxs-lookup"><span data-stu-id="235f5-178">d.</span></span> <span data-ttu-id="235f5-179">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="235f5-179">Click **Ok**.</span></span>

7. <span data-ttu-id="235f5-180">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="235f5-180">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-veracode-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="235f5-182">Na seção **Configuração do Veracode**, clique em **Configurar o Veracode** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="235f5-182">On the **Veracode Configuration** section, click **Configure Veracode** to open **Configure sign-on** window.</span></span> <span data-ttu-id="235f5-183">Copie a **ID da Entidade SAML** da **seção Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="235f5-183">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configuração do Veracode](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_configure.png) 

9. <span data-ttu-id="235f5-185">Em uma janela diferente do navegador da Web, faça logon no site da sua empresa do Veracode como administrador.</span><span class="sxs-lookup"><span data-stu-id="235f5-185">In a different web browser window, log into your Veracode company site as an administrator.</span></span>

10. <span data-ttu-id="235f5-186">No menu na parte superior, clique em **Configurações** e em **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="235f5-186">In the menu on the top, click **Settings**, and then click **Admin**.</span></span>
   
    <span data-ttu-id="235f5-187">![Administração](./media/active-directory-saas-veracode-tutorial/ic802911.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="235f5-187">![Administration](./media/active-directory-saas-veracode-tutorial/ic802911.png "Administration")</span></span>

11. <span data-ttu-id="235f5-188">Clique na guia **SAML** .</span><span class="sxs-lookup"><span data-stu-id="235f5-188">Click the **SAML** tab.</span></span>

12. <span data-ttu-id="235f5-189">Na seção **Configurações do SAML da Organização** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="235f5-189">In the **Organization SAML Settings** section, perform the following steps:</span></span>
   
    <span data-ttu-id="235f5-190">![Administração](./media/active-directory-saas-veracode-tutorial/ic802912.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="235f5-190">![Administration](./media/active-directory-saas-veracode-tutorial/ic802912.png "Administration")</span></span>
   
    <span data-ttu-id="235f5-191">a.</span><span class="sxs-lookup"><span data-stu-id="235f5-191">a.</span></span>  <span data-ttu-id="235f5-192">Na caixa de texto **Emissor**, cole o valor da **ID da Entidade SAML** copiado do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="235f5-192">In  **Issuer** textbox, paste the value of  **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="235f5-193">b.</span><span class="sxs-lookup"><span data-stu-id="235f5-193">b.</span></span> <span data-ttu-id="235f5-194">Para carregar seu certificado baixado do Portal do Azure, clique em **Escolher Arquivo**.</span><span class="sxs-lookup"><span data-stu-id="235f5-194">To upload your downloaded certificate from Azure portal, click **Choose File**.</span></span>
   
    <span data-ttu-id="235f5-195">c.</span><span class="sxs-lookup"><span data-stu-id="235f5-195">c.</span></span> <span data-ttu-id="235f5-196">Selecione **Habilitar Autorregistro**.</span><span class="sxs-lookup"><span data-stu-id="235f5-196">Select **Enable Self Registration**.</span></span>

13. <span data-ttu-id="235f5-197">Na seção **Configurações de Autorregistro**, realize as seguintes etapas e clique em **Salvar**:</span><span class="sxs-lookup"><span data-stu-id="235f5-197">In the **Self Registration Settings** section, perform the following steps, and then click **Save**:</span></span>
   
    <span data-ttu-id="235f5-198">![Administração](./media/active-directory-saas-veracode-tutorial/ic802913.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="235f5-198">![Administration](./media/active-directory-saas-veracode-tutorial/ic802913.png "Administration")</span></span>
   
    <span data-ttu-id="235f5-199">a.</span><span class="sxs-lookup"><span data-stu-id="235f5-199">a.</span></span> <span data-ttu-id="235f5-200">Para **Ativação de Novo Usuário**, selecione **Sem Ativação Necessária**.</span><span class="sxs-lookup"><span data-stu-id="235f5-200">As **New User Activation**, select **No Activation Required**.</span></span>
   
    <span data-ttu-id="235f5-201">b.</span><span class="sxs-lookup"><span data-stu-id="235f5-201">b.</span></span> <span data-ttu-id="235f5-202">Para **Atualizações de Dados do Usuário**, selecione **Dados do Usuário de Preferência do Veracode**.</span><span class="sxs-lookup"><span data-stu-id="235f5-202">As **User Data Updates**, select **Preference Veracode User Data**.</span></span>
   
    <span data-ttu-id="235f5-203">c.</span><span class="sxs-lookup"><span data-stu-id="235f5-203">c.</span></span> <span data-ttu-id="235f5-204">Para **Detalhes de Atributos do SAML**, selecione o seguinte:</span><span class="sxs-lookup"><span data-stu-id="235f5-204">For **SAML Attribute Details**, select the following:</span></span>
      * <span data-ttu-id="235f5-205">**Funções de usuário**</span><span class="sxs-lookup"><span data-stu-id="235f5-205">**User Roles**</span></span>
      * <span data-ttu-id="235f5-206">**Administrador de políticas**</span><span class="sxs-lookup"><span data-stu-id="235f5-206">**Policy Administrator**</span></span>
      * <span data-ttu-id="235f5-207">**Revisor**</span><span class="sxs-lookup"><span data-stu-id="235f5-207">**Reviewer**</span></span>
      * <span data-ttu-id="235f5-208">**Orientações de Segurança**</span><span class="sxs-lookup"><span data-stu-id="235f5-208">**Security Lead**</span></span>
      * <span data-ttu-id="235f5-209">**Executivo**</span><span class="sxs-lookup"><span data-stu-id="235f5-209">**Executive**</span></span>
      * <span data-ttu-id="235f5-210">**Emissor**</span><span class="sxs-lookup"><span data-stu-id="235f5-210">**Submitter**</span></span>
      * <span data-ttu-id="235f5-211">**Criador**</span><span class="sxs-lookup"><span data-stu-id="235f5-211">**Creator**</span></span>
      * <span data-ttu-id="235f5-212">**Todos os Tipos de Verificação**</span><span class="sxs-lookup"><span data-stu-id="235f5-212">**All Scan Types**</span></span>
      * <span data-ttu-id="235f5-213">**Associações de Equipe**</span><span class="sxs-lookup"><span data-stu-id="235f5-213">**Team Memberships**</span></span>
      * <span data-ttu-id="235f5-214">**Equipe Padrão**</span><span class="sxs-lookup"><span data-stu-id="235f5-214">**Default Team**</span></span>

> [!TIP]
> <span data-ttu-id="235f5-215">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="235f5-215">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="235f5-216">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="235f5-216">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="235f5-217">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="235f5-217">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="235f5-218">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="235f5-218">Create an Azure AD test user</span></span>

<span data-ttu-id="235f5-219">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="235f5-219">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="235f5-221">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="235f5-221">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="235f5-222">No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="235f5-222">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-veracode-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="235f5-224">Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="235f5-224">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-veracode-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="235f5-226">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.</span><span class="sxs-lookup"><span data-stu-id="235f5-226">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![O botão Adicionar](./media/active-directory-saas-veracode-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="235f5-228">Na caixa de diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="235f5-228">In the **User** dialog box, perform the following steps:</span></span>

    ![A caixa de diálogo Usuário](./media/active-directory-saas-veracode-tutorial/create_aaduser_04.png)

    <span data-ttu-id="235f5-230">a.</span><span class="sxs-lookup"><span data-stu-id="235f5-230">a.</span></span> <span data-ttu-id="235f5-231">Na caixa **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="235f5-231">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="235f5-232">b.</span><span class="sxs-lookup"><span data-stu-id="235f5-232">b.</span></span> <span data-ttu-id="235f5-233">Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="235f5-233">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="235f5-234">c.</span><span class="sxs-lookup"><span data-stu-id="235f5-234">c.</span></span> <span data-ttu-id="235f5-235">Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.</span><span class="sxs-lookup"><span data-stu-id="235f5-235">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="235f5-236">d.</span><span class="sxs-lookup"><span data-stu-id="235f5-236">d.</span></span> <span data-ttu-id="235f5-237">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="235f5-237">Click **Create**.</span></span>
 
### <a name="create-a-veracode-test-user"></a><span data-ttu-id="235f5-238">Criar um usuário de teste do Veracode</span><span class="sxs-lookup"><span data-stu-id="235f5-238">Create a Veracode test user</span></span>
<span data-ttu-id="235f5-239">Para permitir que os usuários do AD do Azure façam logon no Veracode, eles devem ser provisionados no Veracode.</span><span class="sxs-lookup"><span data-stu-id="235f5-239">In order to enable Azure AD users to log into Veracode, they must be provisioned into Veracode.</span></span> <span data-ttu-id="235f5-240">No caso do Veracode, o provisionamento é uma tarefa automatizada.</span><span class="sxs-lookup"><span data-stu-id="235f5-240">In the case of Veracode, provisioning is an automated task.</span></span> <span data-ttu-id="235f5-241">Não há nenhum item de ação para você.</span><span class="sxs-lookup"><span data-stu-id="235f5-241">There is no action item for you.</span></span> <span data-ttu-id="235f5-242">Os usuários são criados automaticamente, se necessário, durante a primeira tentativa de logon único.</span><span class="sxs-lookup"><span data-stu-id="235f5-242">Users are automatically created if necessary during the first single sign-on attempt.</span></span>

> [!NOTE]
> <span data-ttu-id="235f5-243">É possível usar qualquer outra ferramenta de criação da conta de usuário do Veracode ou APIs fornecidas pelo Veracode para provisionar as contas de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="235f5-243">You can use any other Veracode user account creation tools or APIs provided by Veracode to provision Azure AD user accounts.</span></span>
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="235f5-244">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="235f5-244">Assign the Azure AD test user</span></span>

<span data-ttu-id="235f5-245">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Veracode.</span><span class="sxs-lookup"><span data-stu-id="235f5-245">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Veracode.</span></span>

![Atribuir a função de usuário][200] 

<span data-ttu-id="235f5-247">**Para atribuir Brenda Fernandes ao Veracode, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="235f5-247">**To assign Britta Simon to Veracode, perform the following steps:**</span></span>

1. <span data-ttu-id="235f5-248">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="235f5-248">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="235f5-250">Na lista de aplicativos, selecione **Veracode**.</span><span class="sxs-lookup"><span data-stu-id="235f5-250">In the applications list, select **Veracode**.</span></span>

    ![O link do Veracode na lista de Aplicativos](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_app.png)  

3. <span data-ttu-id="235f5-252">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="235f5-252">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202]

4. <span data-ttu-id="235f5-254">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="235f5-254">Click **Add** button.</span></span> <span data-ttu-id="235f5-255">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="235f5-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="235f5-257">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="235f5-257">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="235f5-258">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="235f5-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="235f5-259">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="235f5-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="235f5-260">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="235f5-260">Test single sign-on</span></span>

<span data-ttu-id="235f5-261">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="235f5-261">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="235f5-262">Ao clicar no bloco do Veracode no Painel de Acesso, você deverá ser conectado automaticamente ao aplicativo Veracode.</span><span class="sxs-lookup"><span data-stu-id="235f5-262">When you click the Veracode tile in the Access Panel, you should get automatically signed-on to your Veracode application.</span></span>
<span data-ttu-id="235f5-263">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="235f5-263">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="235f5-264">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="235f5-264">Additional resources</span></span>

* [<span data-ttu-id="235f5-265">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="235f5-265">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="235f5-266">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="235f5-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_203.png

