---
title: "Tutorial: integração do Azure Active Directory ao FileCloud | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o FileCloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f39f0ddd-b504-4562-971f-77b88d1e75fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: ad03516f684acc59912ffc57f6e0712828bd03f2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filecloud"></a><span data-ttu-id="3346b-103">Tutorial: integração do Azure Active Directory ao FileCloud</span><span class="sxs-lookup"><span data-stu-id="3346b-103">Tutorial: Azure Active Directory integration with FileCloud</span></span>

<span data-ttu-id="3346b-104">Neste tutorial, você aprende a integrar o FileCloud ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="3346b-104">In this tutorial, you learn how to integrate FileCloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3346b-105">A integração do FileCloud ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="3346b-105">Integrating FileCloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3346b-106">No Azure AD, é possível controlar quem tem acesso ao FileCloud.</span><span class="sxs-lookup"><span data-stu-id="3346b-106">You can control in Azure AD who has access to FileCloud.</span></span>
- <span data-ttu-id="3346b-107">É possível permitir que os usuários se conectem automaticamente ao FileCloud (Logon Único) com suas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3346b-107">You can enable your users to automatically get signed-on to FileCloud (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="3346b-108">Você pode gerenciar suas contas em um único local central – o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3346b-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="3346b-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3346b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3346b-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3346b-110">Prerequisites</span></span>

<span data-ttu-id="3346b-111">Para configurar a integração do Azure AD com o FileCloud, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="3346b-111">To configure Azure AD integration with FileCloud, you need the following items:</span></span>

- <span data-ttu-id="3346b-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3346b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3346b-113">Uma assinatura habilitada para logon único do FileCloud</span><span class="sxs-lookup"><span data-stu-id="3346b-113">A FileCloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3346b-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="3346b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3346b-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="3346b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3346b-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="3346b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3346b-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3346b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3346b-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="3346b-118">Scenario description</span></span>
<span data-ttu-id="3346b-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="3346b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3346b-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="3346b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3346b-121">Adicionando FileCloud da Galeria</span><span class="sxs-lookup"><span data-stu-id="3346b-121">Adding FileCloud from the gallery</span></span>
2. <span data-ttu-id="3346b-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3346b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-filecloud-from-the-gallery"></a><span data-ttu-id="3346b-123">Adicionando FileCloud da Galeria</span><span class="sxs-lookup"><span data-stu-id="3346b-123">Adding FileCloud from the gallery</span></span>
<span data-ttu-id="3346b-124">Para configurar a integração do FileCloud ao Azure AD, você precisará adicionar o FileCloud da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="3346b-124">To configure the integration of FileCloud into Azure AD, you need to add FileCloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3346b-125">**Para adicionar o FileCloud da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3346b-125">**To add FileCloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3346b-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3346b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="3346b-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="3346b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3346b-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3346b-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="3346b-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3346b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="3346b-133">Na caixa de pesquisa, digite **FileCloud**, selecione **FileCloud** no painel de resultados e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3346b-133">In the search box, type **FileCloud**, select **FileCloud** from result panel then click **Add** button to add the application.</span></span>

    ![FileCloud na lista de resultados](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3346b-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3346b-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="3346b-136">Nesta seção, você configura e testa o logon único do Azure AD com o FileCloud, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="3346b-136">In this section, you configure and test Azure AD single sign-on with FileCloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3346b-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do FileCloud é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3346b-137">For single sign-on to work, Azure AD needs to know what the counterpart user in FileCloud is to a user in Azure AD.</span></span> <span data-ttu-id="3346b-138">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do FileCloud.</span><span class="sxs-lookup"><span data-stu-id="3346b-138">In other words, a link relationship between an Azure AD user and the related user in FileCloud needs to be established.</span></span>

<span data-ttu-id="3346b-139">No FileCloud, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="3346b-139">In FileCloud, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3346b-140">Para configurar e testar o logon único do Azure AD com o FileCloud, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="3346b-140">To configure and test Azure AD single sign-on with FileCloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3346b-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="3346b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3346b-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="3346b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3346b-143">**[Criar um usuário de teste do FileCloud](#create-a-filecloud-test-user)** – para ter um equivalente de Brenda Fernandes no FileCloud que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3346b-143">**[Create a FileCloud test user](#create-a-filecloud-test-user)** - to have a counterpart of Britta Simon in FileCloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3346b-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3346b-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3346b-145">**[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="3346b-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="3346b-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3346b-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="3346b-147">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo FileCloud.</span><span class="sxs-lookup"><span data-stu-id="3346b-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your FileCloud application.</span></span>

<span data-ttu-id="3346b-148">**Para configurar o logon único do Azure AD com o FileCloud, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3346b-148">**To configure Azure AD single sign-on with FileCloud, perform the following steps:**</span></span>

1. <span data-ttu-id="3346b-149">No portal do Azure, na página de integração do aplicativo **FileCloud**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="3346b-149">In the Azure portal, on the **FileCloud** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="3346b-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="3346b-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_samlbase.png)

3. <span data-ttu-id="3346b-153">Na seção **Domínio e URLs do FileCloud**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3346b-153">On the **FileCloud Domain and URLs** section, perform the following steps:</span></span>

    ![Informações de logon único em Domínio e URLs do FileCloud](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_url.png)

    <span data-ttu-id="3346b-155">a.</span><span class="sxs-lookup"><span data-stu-id="3346b-155">a.</span></span> <span data-ttu-id="3346b-156">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<subdomain>.filecloudhosted.com`</span><span class="sxs-lookup"><span data-stu-id="3346b-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.filecloudhosted.com`</span></span>

    <span data-ttu-id="3346b-157">b.</span><span class="sxs-lookup"><span data-stu-id="3346b-157">b.</span></span> <span data-ttu-id="3346b-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<subdomain>.filecloudhosted.com/simplesaml/module.php/saml/sp/metadata.php/default-sp`</span><span class="sxs-lookup"><span data-stu-id="3346b-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.filecloudhosted.com/simplesaml/module.php/saml/sp/metadata.php/default-sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3346b-159">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="3346b-159">These values are not real.</span></span> <span data-ttu-id="3346b-160">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="3346b-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="3346b-161">Contate a [equipe de suporte ao Cliente do FileCloud](mailto:support@codelathe.com) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="3346b-161">Contact [FileCloud Client support team](mailto:support@codelathe.com) to get these values.</span></span>

4. <span data-ttu-id="3346b-162">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="3346b-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_certificate.png) 

5. <span data-ttu-id="3346b-164">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="3346b-164">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-filecloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3346b-166">Na seção **Configuração do FileCloud**, clique em **Configurar o FileCloud** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="3346b-166">On the **FileCloud Configuration** section, click **Configure FileCloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3346b-167">Copie a **ID da Entidade SAML** da **seção Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="3346b-167">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configuração do FileCloud](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_configure.png) 

7. <span data-ttu-id="3346b-169">Em uma janela diferente do navegador da Web, faça logon em seu locatário do FileCloud como administrador.</span><span class="sxs-lookup"><span data-stu-id="3346b-169">In a different web browser window, sign-on to your FileCloud tenant as an administrator.</span></span>

8. <span data-ttu-id="3346b-170">No painel de navegação esquerdo, clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="3346b-170">On the left navigation pane, click **Settings**.</span></span> 
   
    ![Seção Configurações no lado do aplicativo](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_000.png)

9. <span data-ttu-id="3346b-172">Clique na guia **SSO** na seção Configurações.</span><span class="sxs-lookup"><span data-stu-id="3346b-172">Click **SSO** tab on Settings section.</span></span> 
   
    ![Guia Logon Único no lado do aplicativo](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_001.png)

10. <span data-ttu-id="3346b-174">Selecione **SAML** como **Tipo de SSO Padrão** em **Configurações de SSO (Logon Único)** painel.</span><span class="sxs-lookup"><span data-stu-id="3346b-174">Select **SAML** as **Default SSO Type** on **Single Sign On (SSO) Settings** panel.</span></span>
   
    ![Painel de Configurações de Logon Único no lado do aplicativo](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_002.png)

11. <span data-ttu-id="3346b-176">Cole a **ID da Entidade SAML** copiada do portal do Azure na caixa de texto **URL do Ponto de Extremidade do IdP**.</span><span class="sxs-lookup"><span data-stu-id="3346b-176">Paste **SAML Entity ID**, which you have copied from Azure portal into the **IdP End Point URL** textbox.</span></span>

    ![Caixa de texto URL do Ponto de Extremidade do IDP](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_003.png)

12. <span data-ttu-id="3346b-178">Abra o arquivo de metadados baixado no bloco de notas, copie o conteúdo dele para sua área de transferência e, em seguida, cole-o na caixa de texto **Metadados IdP** no painel **Configurações de SAML**.</span><span class="sxs-lookup"><span data-stu-id="3346b-178">Open your downloaded metadata file in notepad, copy the content of it into your clipboard, and then paste it to the **IdP Meta Data** textbox on **SAML Settings** panel.</span></span>

    ![Seção Metadados do IDP no lado do aplicativo](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_004.png)

13. <span data-ttu-id="3346b-180">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="3346b-180">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="3346b-181">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="3346b-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3346b-182">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="3346b-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3346b-183">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3346b-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3346b-184">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3346b-184">Create an Azure AD test user</span></span>

<span data-ttu-id="3346b-185">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="3346b-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="3346b-187">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3346b-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3346b-188">No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3346b-188">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-filecloud-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="3346b-190">Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="3346b-190">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-filecloud-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="3346b-192">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.</span><span class="sxs-lookup"><span data-stu-id="3346b-192">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![O botão Adicionar](./media/active-directory-saas-filecloud-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="3346b-194">Na caixa de diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3346b-194">In the **User** dialog box, perform the following steps:</span></span>

    ![A caixa de diálogo Usuário](./media/active-directory-saas-filecloud-tutorial/create_aaduser_04.png)

    <span data-ttu-id="3346b-196">a.</span><span class="sxs-lookup"><span data-stu-id="3346b-196">a.</span></span> <span data-ttu-id="3346b-197">Na caixa **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="3346b-197">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3346b-198">b.</span><span class="sxs-lookup"><span data-stu-id="3346b-198">b.</span></span> <span data-ttu-id="3346b-199">Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="3346b-199">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="3346b-200">c.</span><span class="sxs-lookup"><span data-stu-id="3346b-200">c.</span></span> <span data-ttu-id="3346b-201">Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.</span><span class="sxs-lookup"><span data-stu-id="3346b-201">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="3346b-202">d.</span><span class="sxs-lookup"><span data-stu-id="3346b-202">d.</span></span> <span data-ttu-id="3346b-203">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3346b-203">Click **Create**.</span></span>
 
### <a name="create-a-filecloud-test-user"></a><span data-ttu-id="3346b-204">Criar um usuário de teste do FileCloud</span><span class="sxs-lookup"><span data-stu-id="3346b-204">Create a FileCloud test user</span></span>

<span data-ttu-id="3346b-205">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no FileCloud.</span><span class="sxs-lookup"><span data-stu-id="3346b-205">The objective of this section is to create a user called Britta Simon in FileCloud.</span></span> <span data-ttu-id="3346b-206">O FileCloud dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="3346b-206">FileCloud supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="3346b-207">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="3346b-207">There is no action item for you in this section.</span></span> <span data-ttu-id="3346b-208">Um novo usuário é criado durante uma tentativa de acessar o FileCloud, caso ele ainda não exista.</span><span class="sxs-lookup"><span data-stu-id="3346b-208">A new user is created during an attempt to access FileCloud if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="3346b-209">Se você precisar criar um usuário manualmente, contate a [equipe de suporte ao Cliente do FileCloud](mailto:support@codelathe.com).</span><span class="sxs-lookup"><span data-stu-id="3346b-209">If you need to create a user manually, you need to contact the [FileCloud Client support team](mailto:support@codelathe.com).</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="3346b-210">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3346b-210">Assign the Azure AD test user</span></span>

<span data-ttu-id="3346b-211">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao FileCloud.</span><span class="sxs-lookup"><span data-stu-id="3346b-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to FileCloud.</span></span>

![Atribuir a função de usuário][200] 

<span data-ttu-id="3346b-213">**Para atribuir Brenda Fernandes ao FileCloud, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3346b-213">**To assign Britta Simon to FileCloud, perform the following steps:**</span></span>

1. <span data-ttu-id="3346b-214">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3346b-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="3346b-216">Na lista de aplicativos, escolha **FileCloud**.</span><span class="sxs-lookup"><span data-stu-id="3346b-216">In the applications list, select **FileCloud**.</span></span>

    ![O link do FileCloud na lista de aplicativos](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_app.png)  

3. <span data-ttu-id="3346b-218">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="3346b-218">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202]

4. <span data-ttu-id="3346b-220">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="3346b-220">Click **Add** button.</span></span> <span data-ttu-id="3346b-221">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3346b-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="3346b-223">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="3346b-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3346b-224">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3346b-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3346b-225">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3346b-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="3346b-226">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="3346b-226">Test single sign-on</span></span>

<span data-ttu-id="3346b-227">O objetivo desta seção é testar sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="3346b-227">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="3346b-228">Ao clicar no bloco FileCloud no Painel de Acesso, você deve entrar automaticamente no aplicativo FileCloud.</span><span class="sxs-lookup"><span data-stu-id="3346b-228">When you click the FileCloud tile in the Access Panel, you should get automatically signed-on to your FileCloud application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3346b-229">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="3346b-229">Additional resources</span></span>

* [<span data-ttu-id="3346b-230">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="3346b-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3346b-231">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3346b-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_203.png

