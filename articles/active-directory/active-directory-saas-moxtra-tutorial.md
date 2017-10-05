---
title: "Tutorial: Integração do Azure Active Directory com o Moxtra | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Active Directory do Azure e o Moxtra."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2aed2d4b-1dcd-4839-8fed-9419d107c61c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: db2f041a44b6771b0a4f734e58d899298ef0847b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moxtra"></a><span data-ttu-id="c80f6-103">Tutorial: integração do Active Directory do Azure ao Moxtra</span><span class="sxs-lookup"><span data-stu-id="c80f6-103">Tutorial: Azure Active Directory integration with Moxtra</span></span>

<span data-ttu-id="c80f6-104">Neste tutorial, você aprenderá a integrar o Moxtra ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="c80f6-104">In this tutorial, you learn how to integrate Moxtra with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c80f6-105">A integração do Moxtra ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="c80f6-105">Integrating Moxtra with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c80f6-106">No Azure AD, você pode controlar quem tem acesso ao Moxtra</span><span class="sxs-lookup"><span data-stu-id="c80f6-106">You can control in Azure AD who has access to Moxtra</span></span>
- <span data-ttu-id="c80f6-107">Você pode permitir que os usuários façam logon automaticamente no Moxtra (Logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c80f6-107">You can enable your users to automatically get signed-on to Moxtra (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c80f6-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c80f6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c80f6-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c80f6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c80f6-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c80f6-110">Prerequisites</span></span>

<span data-ttu-id="c80f6-111">Para configurar a integração do Azure AD ao Moxtra, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="c80f6-111">To configure Azure AD integration with Moxtra, you need the following items:</span></span>

- <span data-ttu-id="c80f6-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c80f6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c80f6-113">Uma assinatura habilitada para logon único do Moxtra</span><span class="sxs-lookup"><span data-stu-id="c80f6-113">A Moxtra single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c80f6-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="c80f6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c80f6-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="c80f6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c80f6-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="c80f6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c80f6-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c80f6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c80f6-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="c80f6-118">Scenario description</span></span>
<span data-ttu-id="c80f6-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="c80f6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c80f6-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="c80f6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c80f6-121">Adicionando Moxtra da galeria</span><span class="sxs-lookup"><span data-stu-id="c80f6-121">Adding Moxtra from the gallery</span></span>
2. <span data-ttu-id="c80f6-122">configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c80f6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moxtra-from-the-gallery"></a><span data-ttu-id="c80f6-123">Adicionando Moxtra da galeria</span><span class="sxs-lookup"><span data-stu-id="c80f6-123">Adding Moxtra from the gallery</span></span>
<span data-ttu-id="c80f6-124">Para configurar a integração do Moxtra ao Azure AD, você precisará adicionar o Moxtra da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="c80f6-124">To configure the integration of Moxtra into Azure AD, you need to add Moxtra from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c80f6-125">**Para adicionar o Moxtra a partir da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c80f6-125">**To add Moxtra from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c80f6-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c80f6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c80f6-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="c80f6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c80f6-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c80f6-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="c80f6-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c80f6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="c80f6-133">Na caixa de pesquisa, digite **Moxtra**.</span><span class="sxs-lookup"><span data-stu-id="c80f6-133">In the search box, type **Moxtra**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_search.png)

5. <span data-ttu-id="c80f6-135">No painel de resultados, selecione **Moxtra** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c80f6-135">In the results panel, select **Moxtra**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c80f6-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c80f6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c80f6-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Moxtra, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="c80f6-138">In this section, you configure and test Azure AD single sign-on with Moxtra based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c80f6-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Moxtra é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c80f6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Moxtra is to a user in Azure AD.</span></span> <span data-ttu-id="c80f6-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Moxtra.</span><span class="sxs-lookup"><span data-stu-id="c80f6-140">In other words, a link relationship between an Azure AD user and the related user in Moxtra needs to be established.</span></span>

<span data-ttu-id="c80f6-141">No Moxtra, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="c80f6-141">In Moxtra, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c80f6-142">Para configurar e testar o logon único do Azure AD com o Moxtra, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="c80f6-142">To configure and test Azure AD single sign-on with Moxtra, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c80f6-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="c80f6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c80f6-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="c80f6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c80f6-145">**[Criação de um usuário de teste Moxtra](#creating-a-moxtra-test-user)**: para ter um equivalente de Brenda Fernandes no Moxtra que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c80f6-145">**[Creating a Moxtra test user](#creating-a-moxtra-test-user)** - to have a counterpart of Britta Simon in Moxtra that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c80f6-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c80f6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c80f6-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="c80f6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c80f6-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c80f6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c80f6-149">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo Moxtra.</span><span class="sxs-lookup"><span data-stu-id="c80f6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Moxtra application.</span></span>

<span data-ttu-id="c80f6-150">**Para configurar o logon único do Azure AD com o Moxtra, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c80f6-150">**To configure Azure AD single sign-on with Moxtra, perform the following steps:**</span></span>

1. <span data-ttu-id="c80f6-151">No Portal do Azure, na página de integração de aplicativos do **Moxtra**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="c80f6-151">In the Azure portal, on the **Moxtra** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="c80f6-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="c80f6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_samlbase.png)

3. <span data-ttu-id="c80f6-155">Na seção **URLs e Domínio do Moxtra**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c80f6-155">On the **Moxtra Domain and URLs** section, perform the following step:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_url.png)

    <span data-ttu-id="c80f6-157">Na caixa de texto **URL de Logon**, digite uma URL como: `https://www.moxtra.com/service/#login`</span><span class="sxs-lookup"><span data-stu-id="c80f6-157">In the **Sign-on URL** textbox, type a URL as: `https://www.moxtra.com/service/#login`</span></span>

4. <span data-ttu-id="c80f6-158">O aplicativo Moxtra espera que as declarações SAML estejam em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="c80f6-158">Moxtra application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="c80f6-159">Configure as declarações a seguir para este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c80f6-159">Configure the following claims for this application.</span></span> <span data-ttu-id="c80f6-160">Você pode gerenciar os valores desses atributos da seção "**Atributos de Usuário**" na página de integração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c80f6-160">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="c80f6-161">A captura de tela a seguir mostra um exemplo dessa configuração.</span><span class="sxs-lookup"><span data-stu-id="c80f6-161">The following screenshot shows an example for this configuration.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_attributes.png)
    
5. <span data-ttu-id="c80f6-163">Na seção **Atributos do Usuário**, na caixa de diálogo **Logon único**, configure o atributo do token SAML como mostra a imagem e execute as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c80f6-163">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="c80f6-164">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="c80f6-164">Attribute Name</span></span> | <span data-ttu-id="c80f6-165">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="c80f6-165">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="c80f6-166">nome</span><span class="sxs-lookup"><span data-stu-id="c80f6-166">firstname</span></span> | <span data-ttu-id="c80f6-167">user.givenname</span><span class="sxs-lookup"><span data-stu-id="c80f6-167">user.givenname</span></span> |
    | <span data-ttu-id="c80f6-168">sobrenome</span><span class="sxs-lookup"><span data-stu-id="c80f6-168">lastname</span></span> | <span data-ttu-id="c80f6-169">user.surname</span><span class="sxs-lookup"><span data-stu-id="c80f6-169">user.surname</span></span> |
    | <span data-ttu-id="c80f6-170">idpid</span><span class="sxs-lookup"><span data-stu-id="c80f6-170">idpid</span></span>    | <span data-ttu-id="c80f6-171"><ID da Entidade SAML></span><span class="sxs-lookup"><span data-stu-id="c80f6-171">< SAML Entity ID ></span></span> 

    > [!Note]
    > <span data-ttu-id="c80f6-172">O valor do atributo **idpid** não é real.</span><span class="sxs-lookup"><span data-stu-id="c80f6-172">The value of **idpid** attribute is not real.</span></span> <span data-ttu-id="c80f6-173">Você pode obter o valor real da seção **Referência rápida** na **Configuração Moxtra**.</span><span class="sxs-lookup"><span data-stu-id="c80f6-173">You can get the actual value from **Quick reference** section under **Moxtra Configuration**.</span></span>
    
    <span data-ttu-id="c80f6-174">a.</span><span class="sxs-lookup"><span data-stu-id="c80f6-174">a.</span></span> <span data-ttu-id="c80f6-175">Clique em **Adicionar atributo** para abrir o diálogo **Adicionar Atributo**.</span><span class="sxs-lookup"><span data-stu-id="c80f6-175">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="c80f6-177">b.</span><span class="sxs-lookup"><span data-stu-id="c80f6-177">b.</span></span> <span data-ttu-id="c80f6-178">Na caixa de texto **Nome** , digite o nome do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="c80f6-178">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="c80f6-180">c.</span><span class="sxs-lookup"><span data-stu-id="c80f6-180">c.</span></span> <span data-ttu-id="c80f6-181">Na lista **Valor**, digite o valor do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="c80f6-181">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="c80f6-182">d.</span><span class="sxs-lookup"><span data-stu-id="c80f6-182">d.</span></span> <span data-ttu-id="c80f6-183">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="c80f6-183">Click **Ok**.</span></span>
    
5. <span data-ttu-id="c80f6-184">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="c80f6-184">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_certificate.png) 

6. <span data-ttu-id="c80f6-186">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="c80f6-186">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-moxtra-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="c80f6-188">Na seção **Configuração do Moxtra**, clique em **Configurar o Moxtra** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="c80f6-188">On the **Moxtra Configuration** section, click **Configure Moxtra** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c80f6-189">Copie a **ID da Entidade SAML e a URL do Serviço de Logon Único do SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="c80f6-189">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_configure.png) 

8. <span data-ttu-id="c80f6-191">Em outra janela do navegador, entre em seu site de empresa do Moxtra como administrador.</span><span class="sxs-lookup"><span data-stu-id="c80f6-191">In another browser window, sign on to your Moxtra company site as an administrator.</span></span>

9. <span data-ttu-id="c80f6-192">Na barra de ferramentas à esquerda, clique em **Console do Administrador > Logon Único do SAML** e clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="c80f6-192">In the toolbar on the left, click **Admin Console > SAML Single Sign-on**, and then click **New**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_06.png) 

10. <span data-ttu-id="c80f6-194">Na página **SAML** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c80f6-194">On the **SAML** page, perform the following steps:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_08.png)   
 
    <span data-ttu-id="c80f6-196">a.</span><span class="sxs-lookup"><span data-stu-id="c80f6-196">a.</span></span> <span data-ttu-id="c80f6-197">Na caixa de texto **Nome** , digite um nome para a sua configuração (por exemplo: *SAML*).</span><span class="sxs-lookup"><span data-stu-id="c80f6-197">In the **Name** textbox, type a name for your configuration (e.g.: *SAML*).</span></span> 
  
    <span data-ttu-id="c80f6-198">b.</span><span class="sxs-lookup"><span data-stu-id="c80f6-198">b.</span></span> <span data-ttu-id="c80f6-199">Na caixa de texto **ID da Entidade IdP**, cole o valor da **ID da Entidade SAML** copiado no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c80f6-199">In the **IdP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="c80f6-200">c.</span><span class="sxs-lookup"><span data-stu-id="c80f6-200">c.</span></span> <span data-ttu-id="c80f6-201">Na caixa de texto **URL de Logon**, cole o valor da **URL de Serviço de Logon Único do SAML** que você copiou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c80f6-201">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="c80f6-202">d.</span><span class="sxs-lookup"><span data-stu-id="c80f6-202">d.</span></span> <span data-ttu-id="c80f6-203">Na caixa de texto **AuthnContextClassRef**, digite **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span><span class="sxs-lookup"><span data-stu-id="c80f6-203">In the **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span> 
 
    <span data-ttu-id="c80f6-204">e.</span><span class="sxs-lookup"><span data-stu-id="c80f6-204">e.</span></span> <span data-ttu-id="c80f6-205">Na caixa de texto **Formato da NameID**, digite **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="c80f6-205">In the **NameID Format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span> 
 
    <span data-ttu-id="c80f6-206">f.</span><span class="sxs-lookup"><span data-stu-id="c80f6-206">f.</span></span> <span data-ttu-id="c80f6-207">Abra o certificado baixado no bloco de notas do Portal do Azure, copie o conteúdo e cole-o na caixa de texto **Certificado**.</span><span class="sxs-lookup"><span data-stu-id="c80f6-207">Open certificate which you have downloaded from Azure portal in notepad, copy the content, and then paste it into the **Certificate** textbox.</span></span>    
 
    <span data-ttu-id="c80f6-208">g.</span><span class="sxs-lookup"><span data-stu-id="c80f6-208">g.</span></span> <span data-ttu-id="c80f6-209">Na caixa de texto de domínio de email SAML email, digite seu domínio de email SAML.</span><span class="sxs-lookup"><span data-stu-id="c80f6-209">In the SAML email domain textbox, type your SAML email domain.</span></span>    
  
    >[!NOTE]
    ><span data-ttu-id="c80f6-210">Para ver as etapas de verificação do domínio, clique no “**i**” abaixo.</span><span class="sxs-lookup"><span data-stu-id="c80f6-210">To see the steps to verify the domain, click the "**i**" below.</span></span>

    <span data-ttu-id="c80f6-211">h.</span><span class="sxs-lookup"><span data-stu-id="c80f6-211">h.</span></span> <span data-ttu-id="c80f6-212">Clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="c80f6-212">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="c80f6-213">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="c80f6-213">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c80f6-214">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="c80f6-214">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c80f6-215">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c80f6-215">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c80f6-216">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c80f6-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="c80f6-217">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="c80f6-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="c80f6-219">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c80f6-219">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c80f6-220">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c80f6-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-moxtra-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c80f6-222">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="c80f6-222">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-moxtra-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c80f6-224">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c80f6-224">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-moxtra-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c80f6-226">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c80f6-226">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-moxtra-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c80f6-228">a.</span><span class="sxs-lookup"><span data-stu-id="c80f6-228">a.</span></span> <span data-ttu-id="c80f6-229">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="c80f6-229">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c80f6-230">b.</span><span class="sxs-lookup"><span data-stu-id="c80f6-230">b.</span></span> <span data-ttu-id="c80f6-231">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="c80f6-231">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c80f6-232">c.</span><span class="sxs-lookup"><span data-stu-id="c80f6-232">c.</span></span> <span data-ttu-id="c80f6-233">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="c80f6-233">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c80f6-234">d.</span><span class="sxs-lookup"><span data-stu-id="c80f6-234">d.</span></span> <span data-ttu-id="c80f6-235">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c80f6-235">Click **Create**.</span></span>
 
### <a name="creating-a-moxtra-test-user"></a><span data-ttu-id="c80f6-236">Criar um usuário de teste Moxtra</span><span class="sxs-lookup"><span data-stu-id="c80f6-236">Creating a Moxtra test user</span></span>

<span data-ttu-id="c80f6-237">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no Moxtra.</span><span class="sxs-lookup"><span data-stu-id="c80f6-237">The objective of this section is to create a user called Britta Simon in Moxtra.</span></span>

<span data-ttu-id="c80f6-238">**Para criar um usuário chamado Brenda Fernandes no Moxtra, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c80f6-238">**To create a user called Britta Simon in Moxtra, perform the following steps:**</span></span>

1. <span data-ttu-id="c80f6-239">Faça logon em seu site de empresa do Moxtra como administrador.</span><span class="sxs-lookup"><span data-stu-id="c80f6-239">Sign on to your Moxtra company site as an administrator.</span></span>

2. <span data-ttu-id="c80f6-240">Na barra de ferramentas à esquerda, clique em **Console do Administrador > Gerenciamento de Usuário** e em **Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="c80f6-240">In the toolbar on the left, click **Admin Console > User Management**, and then **Add User**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_10.png) 

3. <span data-ttu-id="c80f6-242">No diálogo **Adicionar Usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c80f6-242">On the **Add User** dialog, perform the following steps:</span></span>
  
    <span data-ttu-id="c80f6-243">a.</span><span class="sxs-lookup"><span data-stu-id="c80f6-243">a.</span></span> <span data-ttu-id="c80f6-244">Na caixa de texto **Nome**, digite **Brenda**.</span><span class="sxs-lookup"><span data-stu-id="c80f6-244">In the **First Name** textbox, type **Britta**.</span></span>
  
    <span data-ttu-id="c80f6-245">b.</span><span class="sxs-lookup"><span data-stu-id="c80f6-245">b.</span></span> <span data-ttu-id="c80f6-246">Na caixa de texto **Sobrenome**, digite **Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="c80f6-246">In the **Last Name** textbox, type **Simon**.</span></span>
  
    <span data-ttu-id="c80f6-247">c.</span><span class="sxs-lookup"><span data-stu-id="c80f6-247">c.</span></span> <span data-ttu-id="c80f6-248">Na caixa de texto **Email**, digite o endereço de email de Brenda no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c80f6-248">In the **Email** textbox, type Britta's email address same as on Azure portal.</span></span>
  
    <span data-ttu-id="c80f6-249">d.</span><span class="sxs-lookup"><span data-stu-id="c80f6-249">d.</span></span> <span data-ttu-id="c80f6-250">Na caixa de texto **Divisão**, digite **Dev**.</span><span class="sxs-lookup"><span data-stu-id="c80f6-250">In the **Division** textbox, type **Dev**.</span></span>
  
    <span data-ttu-id="c80f6-251">e.</span><span class="sxs-lookup"><span data-stu-id="c80f6-251">e.</span></span> <span data-ttu-id="c80f6-252">Na caixa de texto **Departamento**, digite **TI**.</span><span class="sxs-lookup"><span data-stu-id="c80f6-252">In the **Department** textbox, type **IT**.</span></span>
  
    <span data-ttu-id="c80f6-253">f.</span><span class="sxs-lookup"><span data-stu-id="c80f6-253">f.</span></span> <span data-ttu-id="c80f6-254">Selecione **Administrator**.</span><span class="sxs-lookup"><span data-stu-id="c80f6-254">Select **Administrator**.</span></span>
  
    <span data-ttu-id="c80f6-255">g.</span><span class="sxs-lookup"><span data-stu-id="c80f6-255">g.</span></span> <span data-ttu-id="c80f6-256">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c80f6-256">Click **Add**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c80f6-257">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c80f6-257">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c80f6-258">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure ao conceder acesso ao Moxtra.</span><span class="sxs-lookup"><span data-stu-id="c80f6-258">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Moxtra.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="c80f6-260">**Para atribuir Brenda Fernandes ao Moxtra, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c80f6-260">**To assign Britta Simon to Moxtra, perform the following steps:**</span></span>

1. <span data-ttu-id="c80f6-261">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c80f6-261">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="c80f6-263">Na lista de aplicativos, selecione **Moxtra**.</span><span class="sxs-lookup"><span data-stu-id="c80f6-263">In the applications list, select **Moxtra**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_app.png) 

3. <span data-ttu-id="c80f6-265">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c80f6-265">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="c80f6-267">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c80f6-267">Click **Add** button.</span></span> <span data-ttu-id="c80f6-268">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c80f6-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="c80f6-270">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="c80f6-270">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c80f6-271">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c80f6-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c80f6-272">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c80f6-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c80f6-273">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="c80f6-273">Testing single sign-on</span></span>

<span data-ttu-id="c80f6-274">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="c80f6-274">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c80f6-275">Ao clicar no bloco do Moxtra no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo do Moxtra.</span><span class="sxs-lookup"><span data-stu-id="c80f6-275">When you click the Moxtra tile in the Access Panel, you should get automatically signed-on to your Moxtra application.</span></span>
<span data-ttu-id="c80f6-276">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c80f6-276">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c80f6-277">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="c80f6-277">Additional resources</span></span>

* [<span data-ttu-id="c80f6-278">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="c80f6-278">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c80f6-279">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c80f6-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_203.png

