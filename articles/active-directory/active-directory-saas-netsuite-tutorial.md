---
title: "Tutorial: Integração do Azure Active Directory com o NetSuite | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Netsuite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dafa0864-aef2-4f5e-9eac-770504688ef4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 4a19ab310212b93a53495a6fc6c25c77dfb82e79
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netsuite"></a><span data-ttu-id="939f6-103">Tutorial: Integração do Azure Active Directory com o Netsuite</span><span class="sxs-lookup"><span data-stu-id="939f6-103">Tutorial: Azure Active Directory integration with Netsuite</span></span>

<span data-ttu-id="939f6-104">Neste tutorial, você aprende a integrar o Netsuite ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="939f6-104">In this tutorial, you learn how to integrate Netsuite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="939f6-105">A integração do Netsuite ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="939f6-105">Integrating Netsuite with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="939f6-106">No Azure AD, é possível controlar quem tem acesso ao Netsuite</span><span class="sxs-lookup"><span data-stu-id="939f6-106">You can control in Azure AD who has access to Netsuite</span></span>
- <span data-ttu-id="939f6-107">É possível permitir que os usuários se conectem automaticamente ao Netsuite (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="939f6-107">You can enable your users to automatically get signed-on to Netsuite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="939f6-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="939f6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="939f6-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="939f6-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="939f6-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="939f6-110">Prerequisites</span></span>

<span data-ttu-id="939f6-111">Para configurar a integração do Azure AD ao Netsuite, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="939f6-111">To configure Azure AD integration with Netsuite, you need the following items:</span></span>

- <span data-ttu-id="939f6-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="939f6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="939f6-113">Uma assinatura habilitada para logon único do Netsuite</span><span class="sxs-lookup"><span data-stu-id="939f6-113">A Netsuite single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="939f6-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="939f6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="939f6-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="939f6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="939f6-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="939f6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="939f6-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="939f6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="939f6-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="939f6-118">Scenario description</span></span>
<span data-ttu-id="939f6-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="939f6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="939f6-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="939f6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="939f6-121">Adicionando o Netsuite por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="939f6-121">Adding Netsuite from the gallery</span></span>
2. <span data-ttu-id="939f6-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="939f6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netsuite-from-the-gallery"></a><span data-ttu-id="939f6-123">Adicionando o Netsuite por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="939f6-123">Adding Netsuite from the gallery</span></span>
<span data-ttu-id="939f6-124">Para configurar a integração do Netsuite ao Azure AD, é necessário adicionar o Netsuite à lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="939f6-124">To configure the integration of Netsuite into Azure AD, you need to add Netsuite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="939f6-125">**Para adicionar o Netsuite por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="939f6-125">**To add Netsuite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="939f6-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="939f6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="939f6-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="939f6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="939f6-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="939f6-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="939f6-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="939f6-131">Click **New application** button on the top of the dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="939f6-133">Na caixa de pesquisa, digite **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="939f6-133">In the search box, type **Netsuite**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_search.png)

5. <span data-ttu-id="939f6-135">No painel de resultados, selecione **Netsuite** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="939f6-135">In the results panel, select **Netsuite**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="939f6-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="939f6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="939f6-138">Nesta seção, você configura e testa o logon único do Azure AD com o Netsuite, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="939f6-138">In this section, you configure and test Azure AD single sign-on with Netsuite based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="939f6-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Netsuite é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="939f6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Netsuite is to a user in Azure AD.</span></span> <span data-ttu-id="939f6-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Netsuite.</span><span class="sxs-lookup"><span data-stu-id="939f6-140">In other words, a link relationship between an Azure AD user and the related user in Netsuite needs to be established.</span></span>

<span data-ttu-id="939f6-141">Essa relação de vínculo é estabelecida com a atribuição do valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** no Netsuite.</span><span class="sxs-lookup"><span data-stu-id="939f6-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Netsuite.</span></span>

<span data-ttu-id="939f6-142">Para configurar e testar o logon único do Azure AD com o Netsuite, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="939f6-142">To configure and test Azure AD single sign-on with Netsuite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="939f6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="939f6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="939f6-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="939f6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="939f6-145">**[Criando um usuário de teste do Netsuite](#creating-a-netsuite-test-user)** – para ter um equivalente de Brenda Fernandes no Netsuite que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="939f6-145">**[Creating a Netsuite test user](#creating-a-netsuite-test-user)** - to have a counterpart of Britta Simon in Netsuite that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="939f6-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="939f6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="939f6-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="939f6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="939f6-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="939f6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="939f6-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Netsuite.</span><span class="sxs-lookup"><span data-stu-id="939f6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Netsuite application.</span></span>

<span data-ttu-id="939f6-150">**Para configurar o logon único do Azure AD com o Netsuite, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="939f6-150">**To configure Azure AD single sign-on with Netsuite, perform the following steps:**</span></span>

1. <span data-ttu-id="939f6-151">No portal do Azure, na página de integração do aplicativo **Netsuite**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="939f6-151">In the Azure portal, on the **Netsuite** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="939f6-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="939f6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_samlbase.png)

3. <span data-ttu-id="939f6-155">Na seção **Domínio e URLs do Netsuite**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="939f6-155">On the **Netsuite Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_url.png)

    <span data-ttu-id="939f6-157">Na caixa de texto **URL de Resposta**, digite uma URL usando o seguinte padrão: `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span><span class="sxs-lookup"><span data-stu-id="939f6-157">In the **Reply URL** textbox, type a URL using the following pattern:   `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="939f6-158">Esse valor não é o valor real.</span><span class="sxs-lookup"><span data-stu-id="939f6-158">This value is not real value.</span></span> <span data-ttu-id="939f6-159">Atualize o valor com a URL de Resposta real.</span><span class="sxs-lookup"><span data-stu-id="939f6-159">Update the value with the actual Reply URL.</span></span> <span data-ttu-id="939f6-160">Contate a [equipe de suporte do Netsuite](http://www.netsuite.com/portal/services/support.shtml) para obter esse valor.</span><span class="sxs-lookup"><span data-stu-id="939f6-160">Contact [Netsuite support team](http://www.netsuite.com/portal/services/support.shtml) to get this value.</span></span>
 
4. <span data-ttu-id="939f6-161">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo XML em seu computador.</span><span class="sxs-lookup"><span data-stu-id="939f6-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_certificate.png) 

5. <span data-ttu-id="939f6-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="939f6-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-netsuite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="939f6-165">Na seção **Configuração do Netsuite**, clique em **Configurar o Netsuite** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="939f6-165">On the **Netsuite Configuration** section, click **Configure Netsuite** to open **Configure sign-on** window.</span></span> <span data-ttu-id="939f6-166">Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="939f6-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_configure.png) 

7. <span data-ttu-id="939f6-168">Abra uma nova guia no navegador e entre no site Netsuite de sua empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="939f6-168">Open a new tab in your browser, and sign into your Netsuite company site as an administrator.</span></span>

8. <span data-ttu-id="939f6-169">Na barra de ferramentas na parte superior da página, clique em **Instalação** e depois em **Gerenciador de Instalação**.</span><span class="sxs-lookup"><span data-stu-id="939f6-169">In the toolbar at the top of the page, click **Setup**, then click **Setup Manager**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

9. <span data-ttu-id="939f6-171">Na lista **Tarefas de Instalação**, selecione **Integração**.</span><span class="sxs-lookup"><span data-stu-id="939f6-171">From the **Setup Tasks** list, select **Integration**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-integration.png)

10. <span data-ttu-id="939f6-173">Na seção **Gerenciar Autenticação**, clique em **Logon Único do SAML**.</span><span class="sxs-lookup"><span data-stu-id="939f6-173">In the **Manage Authentication** section, click **SAML Single Sign-on**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-saml.png)

11. <span data-ttu-id="939f6-175">Na página **Instalação do SAML** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="939f6-175">On the **SAML Setup** page, perform the following steps:</span></span>
   
    <span data-ttu-id="939f6-176">a.</span><span class="sxs-lookup"><span data-stu-id="939f6-176">a.</span></span> <span data-ttu-id="939f6-177">Copie o valor da **URL do Serviço de Logon Único SAML** da seção **Referência Rápida** de **Configurar logon** e cole-o no campo **Página de Logon do Provedor de Identidade** do Netsuite.</span><span class="sxs-lookup"><span data-stu-id="939f6-177">Copy the **SAML Single Sign-On Service URL** value from **Quick Reference** section of **Configure sign-on** and paste it into the **Identity Provider Login Page** field in Netsuite.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-netsuite-tutorial/ns-saml-setup.png)
  
    <span data-ttu-id="939f6-179">b.</span><span class="sxs-lookup"><span data-stu-id="939f6-179">b.</span></span> <span data-ttu-id="939f6-180">No NetSuite, selecione **Método de Autenticação Primária**.</span><span class="sxs-lookup"><span data-stu-id="939f6-180">In Netsuite, select **Primary Authentication Method**.</span></span>

    <span data-ttu-id="939f6-181">c.</span><span class="sxs-lookup"><span data-stu-id="939f6-181">c.</span></span> <span data-ttu-id="939f6-182">Para o campo **Metadados do Provedor de Identidade SAMLV2**, selecione **Carregar Arquivo de Metadados IDP**.</span><span class="sxs-lookup"><span data-stu-id="939f6-182">For the field labeled **SAMLV2 Identity Provider Metadata**, select **Upload IDP Metadata File**.</span></span> <span data-ttu-id="939f6-183">Em seguida, clique em **Procurar** para carregar o arquivo de metadados baixado no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="939f6-183">Then click **Browse** to upload the metadata file that you downloaded from Azure portal.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-netsuite-tutorial/ns-sso-setup.png)

    <span data-ttu-id="939f6-185">d.</span><span class="sxs-lookup"><span data-stu-id="939f6-185">d.</span></span> <span data-ttu-id="939f6-186">Clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="939f6-186">Click **Submit**.</span></span>

12. <span data-ttu-id="939f6-187">No Azure AD, clique na caixa de seleção **Exibir e editar todos os outros atributos de usuário** e adicione um atributo.</span><span class="sxs-lookup"><span data-stu-id="939f6-187">In Azure AD, Click on **View and edit all other user attributes** check-box and add attribute.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-attributes.png)

13. <span data-ttu-id="939f6-189">Para o campo **Nome do Atributo**, digite `account`.</span><span class="sxs-lookup"><span data-stu-id="939f6-189">For the **Attribute Name** field, type in `account`.</span></span> <span data-ttu-id="939f6-190">No campo **Valor do Atributo**, digite sua ID de conta do Netsuite. Esse valor é constante e muda com a conta.</span><span class="sxs-lookup"><span data-stu-id="939f6-190">For the **Attribute Value** field, type in your Netsuite account ID.This value is constant and change with account.</span></span> <span data-ttu-id="939f6-191">Instruções sobre como localizar a ID de conta estão abaixo:</span><span class="sxs-lookup"><span data-stu-id="939f6-191">Instructions on how to find your account ID are included below:</span></span>

      ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-add-attribute.png)

    <span data-ttu-id="939f6-193">a.</span><span class="sxs-lookup"><span data-stu-id="939f6-193">a.</span></span> <span data-ttu-id="939f6-194">No Netsuite, clique em **Instalação** no menu de navegação superior.</span><span class="sxs-lookup"><span data-stu-id="939f6-194">In Netsuite, click **Setup** from the top navigation menu.</span></span>

    <span data-ttu-id="939f6-195">b.</span><span class="sxs-lookup"><span data-stu-id="939f6-195">b.</span></span> <span data-ttu-id="939f6-196">Em seguida, clique na seção **Tarefas de Instalação** no menu de navegação à esquerda, selecione a seção **Integração** e clique em **Preferências de Serviços Web**.</span><span class="sxs-lookup"><span data-stu-id="939f6-196">Then click under the **Setup Tasks** section of the left navigation menu, select the **Integration** section, and click **Web Services Preferences**.</span></span>

    <span data-ttu-id="939f6-197">c.</span><span class="sxs-lookup"><span data-stu-id="939f6-197">c.</span></span> <span data-ttu-id="939f6-198">Copie a ID de conta do NetSuite e cole-a no campo **Valor do Atributo** no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="939f6-198">Copy your Netsuite Account ID and paste it into the **Attribute Value** field in Azure AD.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-account-id.png)

14. <span data-ttu-id="939f6-200">Antes que os usuários possam realizar logon único no NetSuite, eles devem primeiro ter as permissões apropriadas no NetSuite.</span><span class="sxs-lookup"><span data-stu-id="939f6-200">Before users can perform single sign-on into Netsuite, they must first be assigned the appropriate permissions in Netsuite.</span></span> <span data-ttu-id="939f6-201">Siga as instruções abaixo para atribuir essas permissões.</span><span class="sxs-lookup"><span data-stu-id="939f6-201">Follow the instructions below to assign these permissions.</span></span>

    <span data-ttu-id="939f6-202">a.</span><span class="sxs-lookup"><span data-stu-id="939f6-202">a.</span></span> <span data-ttu-id="939f6-203">No menu de navegação superior, clique em **Instalação** e depois em **Gerenciador de Instalação**.</span><span class="sxs-lookup"><span data-stu-id="939f6-203">On the top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
      ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="939f6-205">b.</span><span class="sxs-lookup"><span data-stu-id="939f6-205">b.</span></span> <span data-ttu-id="939f6-206">No menu de navegação à esquerda, selecione **Usuários/Funções** e, em seguida, clique em **Gerenciar Funções**.</span><span class="sxs-lookup"><span data-stu-id="939f6-206">On the left navigation menu, select **Users/Roles**, then click **Manage Roles**.</span></span>
      
      ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-manage-roles.png)

    <span data-ttu-id="939f6-208">c.</span><span class="sxs-lookup"><span data-stu-id="939f6-208">c.</span></span> <span data-ttu-id="939f6-209">Clique em **Nova Função**.</span><span class="sxs-lookup"><span data-stu-id="939f6-209">Click **New Role**.</span></span>

    <span data-ttu-id="939f6-210">d.</span><span class="sxs-lookup"><span data-stu-id="939f6-210">d.</span></span> <span data-ttu-id="939f6-211">Digite um **Nome** para a nova função e marque a caixa de seleção **Somente Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="939f6-211">Type in a **Name** for your new role, and select the **Single Sign-On Only** checkbox.</span></span>
      
      ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-new-role.png)

    <span data-ttu-id="939f6-213">e.</span><span class="sxs-lookup"><span data-stu-id="939f6-213">e.</span></span> <span data-ttu-id="939f6-214">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="939f6-214">Click **Save**.</span></span>

    <span data-ttu-id="939f6-215">f.</span><span class="sxs-lookup"><span data-stu-id="939f6-215">f.</span></span> <span data-ttu-id="939f6-216">No menu na parte superior, clique em **Permissões**.</span><span class="sxs-lookup"><span data-stu-id="939f6-216">In the menu on the top, click **Permissions**.</span></span> <span data-ttu-id="939f6-217">Em seguida, clique em **Instalação**.</span><span class="sxs-lookup"><span data-stu-id="939f6-217">Then click **Setup**.</span></span>
      
       ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-sso.png)

    <span data-ttu-id="939f6-219">g.</span><span class="sxs-lookup"><span data-stu-id="939f6-219">g.</span></span> <span data-ttu-id="939f6-220">Selecione **Instalar o Logon Único do SAM** e, em seguida, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="939f6-220">Select **Set Up SAM Single Sign-on**, and then click **Add**.</span></span>

    <span data-ttu-id="939f6-221">h.</span><span class="sxs-lookup"><span data-stu-id="939f6-221">h.</span></span> <span data-ttu-id="939f6-222">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="939f6-222">Click **Save**.</span></span>

    <span data-ttu-id="939f6-223">i.</span><span class="sxs-lookup"><span data-stu-id="939f6-223">i.</span></span> <span data-ttu-id="939f6-224">No menu de navegação superior, clique em **Instalação** e depois em **Gerenciador de Instalação**.</span><span class="sxs-lookup"><span data-stu-id="939f6-224">On the top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
       ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="939f6-226">j.</span><span class="sxs-lookup"><span data-stu-id="939f6-226">j.</span></span> <span data-ttu-id="939f6-227">No menu de navegação à esquerda, selecione **Usuários/Funções** e, em seguida, clique em **Gerenciar Usuários**.</span><span class="sxs-lookup"><span data-stu-id="939f6-227">On the left navigation menu, select **Users/Roles**, then click **Manage Users**.</span></span>
      
       ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-manage-users.png)

    <span data-ttu-id="939f6-229">k.</span><span class="sxs-lookup"><span data-stu-id="939f6-229">k.</span></span> <span data-ttu-id="939f6-230">Selecione um usuário de teste.</span><span class="sxs-lookup"><span data-stu-id="939f6-230">Select a test user.</span></span> <span data-ttu-id="939f6-231">Em seguida, clique em **Editar**.</span><span class="sxs-lookup"><span data-stu-id="939f6-231">Then click **Edit**.</span></span>
      
       ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-edit-user.png)

    <span data-ttu-id="939f6-233">l.</span><span class="sxs-lookup"><span data-stu-id="939f6-233">l.</span></span> <span data-ttu-id="939f6-234">Na caixa de diálogo Funções, selecione a função que você criou e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="939f6-234">On the Roles dialog, select the role that you have created and click **Add**.</span></span>
      
       ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-add-role.png)

    <span data-ttu-id="939f6-236">m.</span><span class="sxs-lookup"><span data-stu-id="939f6-236">m.</span></span> <span data-ttu-id="939f6-237">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="939f6-237">Click **Save**.</span></span>
    
> [!TIP]
> <span data-ttu-id="939f6-238">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="939f6-238">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="939f6-239">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="939f6-239">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="939f6-240">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="939f6-240">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="939f6-241">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="939f6-241">Creating an Azure AD test user</span></span>
<span data-ttu-id="939f6-242">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="939f6-242">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="939f6-244">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="939f6-244">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="939f6-245">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="939f6-245">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-netsuite-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="939f6-247">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="939f6-247">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-netsuite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="939f6-249">Na parte superior da caixa de diálogo, clique em **Adicionar** para abrir a caixa de diálogo **Usuário**.</span><span class="sxs-lookup"><span data-stu-id="939f6-249">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-netsuite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="939f6-251">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="939f6-251">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-netsuite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="939f6-253">a.</span><span class="sxs-lookup"><span data-stu-id="939f6-253">a.</span></span> <span data-ttu-id="939f6-254">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="939f6-254">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="939f6-255">b.</span><span class="sxs-lookup"><span data-stu-id="939f6-255">b.</span></span> <span data-ttu-id="939f6-256">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="939f6-256">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="939f6-257">c.</span><span class="sxs-lookup"><span data-stu-id="939f6-257">c.</span></span> <span data-ttu-id="939f6-258">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="939f6-258">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="939f6-259">d.</span><span class="sxs-lookup"><span data-stu-id="939f6-259">d.</span></span> <span data-ttu-id="939f6-260">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="939f6-260">Click **Create**.</span></span> 

### <a name="creating-a-netsuite-test-user"></a><span data-ttu-id="939f6-261">Criando um usuário de teste do Netsuite</span><span class="sxs-lookup"><span data-stu-id="939f6-261">Creating a Netsuite test user</span></span>

<span data-ttu-id="939f6-262">Nesta seção, um usuário chamado Brenda Fernandes é criado no Netsuite.</span><span class="sxs-lookup"><span data-stu-id="939f6-262">In this section, a user called Britta Simon is created in Netsuite.</span></span> <span data-ttu-id="939f6-263">O Netsuite dá suporte ao provisionamento Just-In-Time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="939f6-263">Netsuite supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="939f6-264">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="939f6-264">There is no action item for you in this section.</span></span> <span data-ttu-id="939f6-265">Se um usuário ainda não existir no Netsuite, um novo será criado quando você tentar acessar o Netsuite.</span><span class="sxs-lookup"><span data-stu-id="939f6-265">If a user doesn't already exist in Netsuite, a new one is created when you attempt to access Netsuite.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="939f6-266">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="939f6-266">Assigning the Azure AD test user</span></span>

<span data-ttu-id="939f6-267">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Netsuite.</span><span class="sxs-lookup"><span data-stu-id="939f6-267">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Netsuite.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="939f6-269">**Para atribuir Brenda Fernandes ao Netsuite, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="939f6-269">**To assign Britta Simon to Netsuite, perform the following steps:**</span></span>

1. <span data-ttu-id="939f6-270">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="939f6-270">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="939f6-272">Na lista de aplicativos, selecione **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="939f6-272">In the applications list, select **Netsuite**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_app.png) 

3. <span data-ttu-id="939f6-274">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="939f6-274">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="939f6-276">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="939f6-276">Click **Add** button.</span></span> <span data-ttu-id="939f6-277">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="939f6-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="939f6-279">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="939f6-279">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="939f6-280">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="939f6-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="939f6-281">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="939f6-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="939f6-282">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="939f6-282">Testing single sign-on</span></span>

<span data-ttu-id="939f6-283">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="939f6-283">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="939f6-284">Para testar as configurações de logon único, abra o Painel de Acesso em [https://myapps.microsoft.com](https://myapps.microsoft.com/), entre na conta de teste e clique em **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="939f6-284">To test your single sign-on settings, open the Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), sign into the test account, and click **Netsuite**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="939f6-285">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="939f6-285">Additional resources</span></span>

* [<span data-ttu-id="939f6-286">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="939f6-286">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="939f6-287">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="939f6-287">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="939f6-288">Configurar Provisionamento de Usuário</span><span class="sxs-lookup"><span data-stu-id="939f6-288">Configure User Provisioning</span></span>](active-directory-saas-netsuite-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_203.png

