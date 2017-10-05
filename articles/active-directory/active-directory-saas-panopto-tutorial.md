---
title: "Tutorial: Integração do Azure Active Directory com o Panopto | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Panopto."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 89c88e23-93ce-4970-9baa-1104c4e8fe4a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 725fba1227cfc9c4850f9e2d6fd0b13e88eafa20
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-panopto"></a><span data-ttu-id="7163e-103">Tutorial: Integração do Active Directory do Azure com o Panopto</span><span class="sxs-lookup"><span data-stu-id="7163e-103">Tutorial: Azure Active Directory integration with Panopto</span></span>

<span data-ttu-id="7163e-104">Neste tutorial, você aprenderá a integrar o Panopto ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="7163e-104">In this tutorial, you learn how to integrate Panopto with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7163e-105">A integração do Panopto ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="7163e-105">Integrating Panopto with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7163e-106">Você pode controlar no Azure AD quem tem acesso ao Panopto</span><span class="sxs-lookup"><span data-stu-id="7163e-106">You can control in Azure AD who has access to Panopto</span></span>
- <span data-ttu-id="7163e-107">Você pode permitir que usuários façam logon automaticamente no Panopto (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7163e-107">You can enable your users to automatically get signed-on to Panopto (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7163e-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7163e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7163e-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7163e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7163e-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7163e-110">Prerequisites</span></span>

<span data-ttu-id="7163e-111">Para configurar a integração do Azure AD ao Panopto, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="7163e-111">To configure Azure AD integration with Panopto, you need the following items:</span></span>

- <span data-ttu-id="7163e-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7163e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7163e-113">Uma assinatura do Panopto habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="7163e-113">A Panopto single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7163e-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="7163e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7163e-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="7163e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7163e-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="7163e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7163e-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7163e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7163e-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="7163e-118">Scenario description</span></span>
<span data-ttu-id="7163e-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="7163e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7163e-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="7163e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7163e-121">Adicionar o Panopto da galeria</span><span class="sxs-lookup"><span data-stu-id="7163e-121">Adding Panopto from the gallery</span></span>
2. <span data-ttu-id="7163e-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7163e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-panopto-from-the-gallery"></a><span data-ttu-id="7163e-123">Adicionar o Panopto da galeria</span><span class="sxs-lookup"><span data-stu-id="7163e-123">Adding Panopto from the gallery</span></span>
<span data-ttu-id="7163e-124">Para configurar a integração do Panopto ao Azure AD, você precisa adicionar o Panopto por meio da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="7163e-124">To configure the integration of Panopto into Azure AD, you need to add Panopto from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7163e-125">**Para adicionar o Panopto da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7163e-125">**To add Panopto from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7163e-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7163e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7163e-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="7163e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7163e-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7163e-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="7163e-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7163e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="7163e-133">Na caixa de pesquisa, digite **Panopto**.</span><span class="sxs-lookup"><span data-stu-id="7163e-133">In the search box, type **Panopto**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_search.png)

5. <span data-ttu-id="7163e-135">No painel de resultados, selecione **Panopto** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7163e-135">In the results panel, select **Panopto**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7163e-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7163e-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="7163e-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Panopto com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="7163e-138">In this section, you configure and test Azure AD single sign-on with Panopto based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7163e-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Panopto é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7163e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Panopto is to a user in Azure AD.</span></span> <span data-ttu-id="7163e-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Panopto.</span><span class="sxs-lookup"><span data-stu-id="7163e-140">In other words, a link relationship between an Azure AD user and the related user in Panopto needs to be established.</span></span>

<span data-ttu-id="7163e-141">No Panopto, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="7163e-141">In Panopto, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7163e-142">Para configurar e testar o logon único do Azure AD com o Panopto, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="7163e-142">To configure and test Azure AD single sign-on with Panopto, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7163e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="7163e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7163e-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="7163e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7163e-145">**[Criação de um usuário de teste do Panopto](#creating-a-panopto-test-user)** – para ter um equivalente de Brenda Fernandes no Panopto que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7163e-145">**[Creating a Panopto test user](#creating-a-panopto-test-user)** - to have a counterpart of Britta Simon in Panopto that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7163e-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="7163e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7163e-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="7163e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7163e-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7163e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7163e-149">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único em seu aplicativo Panopto.</span><span class="sxs-lookup"><span data-stu-id="7163e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Panopto application.</span></span>

<span data-ttu-id="7163e-150">**Para configurar o logon único do Azure AD com o Panopto, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7163e-150">**To configure Azure AD single sign-on with Panopto, perform the following steps:**</span></span>

1. <span data-ttu-id="7163e-151">No Portal do Azure, na página de integração de aplicativos do **Panopto**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="7163e-151">In the Azure portal, on the **Panopto** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="7163e-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="7163e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_samlbase.png)

3. <span data-ttu-id="7163e-155">Na seção **Domínio e URLs do Panopto**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7163e-155">On the **Panopto Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_url.png)

    <span data-ttu-id="7163e-157">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<tenant-name>.panopto.com`</span><span class="sxs-lookup"><span data-stu-id="7163e-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.panopto.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7163e-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="7163e-158">This value is not real.</span></span> <span data-ttu-id="7163e-159">Atualize esse valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="7163e-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="7163e-160">Entre em contato com a [equipe de suporte ao cliente do Panopto](mailto:support@panopto.com‎) para obter esse valor.</span><span class="sxs-lookup"><span data-stu-id="7163e-160">Contact [Panopto Client support team](mailto:support@panopto.com‎) to get this value.</span></span> 
 
4. <span data-ttu-id="7163e-161">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="7163e-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_certificate.png) 

5. <span data-ttu-id="7163e-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="7163e-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-panopto-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7163e-165">Na seção **Configuração do Panopto**, clique em **Configurar o Panopto** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="7163e-165">On the **Panopto Configuration** section, click **Configure Panopto** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7163e-166">Copie a **ID da Entidade SAML e a URL do Serviço de Logon Único do SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="7163e-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_configure.png) 

7. <span data-ttu-id="7163e-168">Em uma janela de navegador da Web diferente, faça logon no site de sua empresa do Panopto como administrador.</span><span class="sxs-lookup"><span data-stu-id="7163e-168">In a different web browser window, log in to your Panopto company site as an administrator.</span></span>

8. <span data-ttu-id="7163e-169">Na barra de ferramentas à esquerda, clique em **Sistema** e, em seguida, clique em **Provedores de Identidade**.</span><span class="sxs-lookup"><span data-stu-id="7163e-169">In the toolbar on the left, click **System**, and then click **Identity Providers**.</span></span>
   
   <span data-ttu-id="7163e-170">![Sistema](./media/active-directory-saas-panopto-tutorial/ic777670.png "Sistema")</span><span class="sxs-lookup"><span data-stu-id="7163e-170">![System](./media/active-directory-saas-panopto-tutorial/ic777670.png "System")</span></span>
9. <span data-ttu-id="7163e-171">Clique em **Adicionar Provedor**.</span><span class="sxs-lookup"><span data-stu-id="7163e-171">Click **Add Provider**.</span></span>
   
   <span data-ttu-id="7163e-172">![Provedores de Identidade](./media/active-directory-saas-panopto-tutorial/ic777671.png "Provedores de Identidade")</span><span class="sxs-lookup"><span data-stu-id="7163e-172">![Identity Providers](./media/active-directory-saas-panopto-tutorial/ic777671.png "Identity Providers")</span></span>
   
10. <span data-ttu-id="7163e-173">Na seção de provedor SAML, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7163e-173">In the SAML provider section, perform the following steps:</span></span>
   
    <span data-ttu-id="7163e-174">![Configuração de SaaS](./media/active-directory-saas-panopto-tutorial/ic777672.png "Configuração de SaaS")</span><span class="sxs-lookup"><span data-stu-id="7163e-174">![SaaS configuration](./media/active-directory-saas-panopto-tutorial/ic777672.png "SaaS configuration")</span></span>
    
    <span data-ttu-id="7163e-175">a.</span><span class="sxs-lookup"><span data-stu-id="7163e-175">a.</span></span> <span data-ttu-id="7163e-176">Na lista **Tipo de Provedor**, selecione **SAML20**.</span><span class="sxs-lookup"><span data-stu-id="7163e-176">From the **Provider Type** list, select **SAML20**.</span></span>    
    
    <span data-ttu-id="7163e-177">b.</span><span class="sxs-lookup"><span data-stu-id="7163e-177">b.</span></span> <span data-ttu-id="7163e-178">Na caixa de texto **Nome da Instância** , digite um nome para a instância.</span><span class="sxs-lookup"><span data-stu-id="7163e-178">In the **Instance Name** textbox, type a name for the instance.</span></span>

    <span data-ttu-id="7163e-179">c.</span><span class="sxs-lookup"><span data-stu-id="7163e-179">c.</span></span> <span data-ttu-id="7163e-180">Na caixa de texto **Descrição Amigável** , digite uma descrição amigável.</span><span class="sxs-lookup"><span data-stu-id="7163e-180">In the **Friendly Description** textbox, type a friendly description.</span></span>
    
    <span data-ttu-id="7163e-181">d.</span><span class="sxs-lookup"><span data-stu-id="7163e-181">d.</span></span> <span data-ttu-id="7163e-182">Na caixa de texto **URL da Página de Devolução**, cole o valor da **URL do Serviço de Logon Único SAML** copiado do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7163e-182">In **Bounce Page Url** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="7163e-183">e.</span><span class="sxs-lookup"><span data-stu-id="7163e-183">e.</span></span> <span data-ttu-id="7163e-184">Na caixa de texto **Emissor**, cole o valor da **ID de Entidade do SAML** que você copiou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7163e-184">In the **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="7163e-185">f.</span><span class="sxs-lookup"><span data-stu-id="7163e-185">f.</span></span> <span data-ttu-id="7163e-186">Abra seu certificado codificado em Base 64, que você baixou do Portal do Azure, copie o conteúdo dele para a área de transferência e cole-o na caixa de texto **Chave Pública**.</span><span class="sxs-lookup"><span data-stu-id="7163e-186">Open your base-64 encoded certificate, which you have downloaded from Azure portal, copy the content of it in to your clipboard, and then paste it to the **Public Key**  textbox.</span></span>

11. <span data-ttu-id="7163e-187">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="7163e-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="7163e-188">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="7163e-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7163e-189">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="7163e-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7163e-190">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7163e-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7163e-191">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7163e-191">Creating an Azure AD test user</span></span>

<span data-ttu-id="7163e-192">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="7163e-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="7163e-194">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7163e-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7163e-195">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7163e-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-panopto-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7163e-197">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="7163e-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-panopto-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7163e-199">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7163e-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-panopto-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7163e-201">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7163e-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-panopto-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7163e-203">a.</span><span class="sxs-lookup"><span data-stu-id="7163e-203">a.</span></span> <span data-ttu-id="7163e-204">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="7163e-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7163e-205">b.</span><span class="sxs-lookup"><span data-stu-id="7163e-205">b.</span></span> <span data-ttu-id="7163e-206">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="7163e-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7163e-207">c.</span><span class="sxs-lookup"><span data-stu-id="7163e-207">c.</span></span> <span data-ttu-id="7163e-208">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="7163e-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7163e-209">d.</span><span class="sxs-lookup"><span data-stu-id="7163e-209">d.</span></span> <span data-ttu-id="7163e-210">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="7163e-210">Click **Create**.</span></span>
 
### <a name="creating-a-panopto-test-user"></a><span data-ttu-id="7163e-211">Criação de um usuário de teste do Panopto</span><span class="sxs-lookup"><span data-stu-id="7163e-211">Creating a Panopto test user</span></span>

<span data-ttu-id="7163e-212">Não há nenhum item de ação para a configuração de provisionamento de usuário para o Panopto.</span><span class="sxs-lookup"><span data-stu-id="7163e-212">There is no action item for you to configure user provisioning to Panopto.</span></span>  
<span data-ttu-id="7163e-213">Quando um usuário atribuído tenta fazer logon no Panopto usando o painel de acesso, o Panopto verifica se o usuário existe.</span><span class="sxs-lookup"><span data-stu-id="7163e-213">When an assigned user tries to log in to Panopto using the access panel, Panopto checks whether the user exists.</span></span>  

<span data-ttu-id="7163e-214">Se ainda não houver nenhuma conta de usuário, ela será criada automaticamente pelo Panopto.</span><span class="sxs-lookup"><span data-stu-id="7163e-214">If there is no user account available yet, it is automatically created by Panopto.</span></span>

>[!NOTE]
><span data-ttu-id="7163e-215">Você pode usar quaisquer outras ferramentas de criação de contas de usuários do Panopto ou APIs fornecidas pela Panopto para provisionar contas de usuário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="7163e-215">You can use any other Panopto user account creation tools or APIs provided by Panopto to provision Azure AD user accounts.</span></span>
>
>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7163e-216">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7163e-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7163e-217">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo acesso ao Panopto.</span><span class="sxs-lookup"><span data-stu-id="7163e-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Panopto.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="7163e-219">**Para atribuir Brenda Fernandes ao Panopto, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7163e-219">**To assign Britta Simon to Panopto, perform the following steps:**</span></span>

1. <span data-ttu-id="7163e-220">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7163e-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="7163e-222">Na lista de aplicativos, selecione **Panopto**.</span><span class="sxs-lookup"><span data-stu-id="7163e-222">In the applications list, select **Panopto**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_app.png) 

3. <span data-ttu-id="7163e-224">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="7163e-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="7163e-226">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="7163e-226">Click **Add** button.</span></span> <span data-ttu-id="7163e-227">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7163e-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="7163e-229">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="7163e-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7163e-230">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7163e-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7163e-231">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7163e-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7163e-232">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="7163e-232">Testing single sign-on</span></span>

<span data-ttu-id="7163e-233">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="7163e-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7163e-234">Ao clicar no bloco Panopto no Painel de Acesso, você deverá ser levado automaticamente à página de logon do aplicativo Panopto.</span><span class="sxs-lookup"><span data-stu-id="7163e-234">When you click the Panopto tile in the Access Panel, you should get automatically login page of Panopto application.</span></span>
<span data-ttu-id="7163e-235">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7163e-235">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7163e-236">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="7163e-236">Additional resources</span></span>

* [<span data-ttu-id="7163e-237">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="7163e-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7163e-238">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7163e-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_203.png

