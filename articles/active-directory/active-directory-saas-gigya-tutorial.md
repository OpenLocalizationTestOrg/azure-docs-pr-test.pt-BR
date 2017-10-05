---
title: "Tutorial: integração do Azure Active Directory ao Gigya | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Gigya."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2c7d200b-9242-44a5-ac8a-ab3214a78e41
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: b65a33989a045a3e0b57fda522a9bc3b0770c7f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-gigya"></a><span data-ttu-id="4af00-103">Tutorial: integração do Active Directory do Azure ao Gigya</span><span class="sxs-lookup"><span data-stu-id="4af00-103">Tutorial: Azure Active Directory integration with Gigya</span></span>

<span data-ttu-id="4af00-104">Neste tutorial, você aprende a integrar o Gigya ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="4af00-104">In this tutorial, you learn how to integrate Gigya with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4af00-105">A integração do Gigya ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="4af00-105">Integrating Gigya with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4af00-106">Você pode controlar no Azure AD quem tem acesso ao Gigya</span><span class="sxs-lookup"><span data-stu-id="4af00-106">You can control in Azure AD who has access to Gigya</span></span>
- <span data-ttu-id="4af00-107">Você pode permitir que seus usuários entrem automaticamente no Gigya (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4af00-107">You can enable your users to automatically get signed-on to Gigya (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4af00-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4af00-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4af00-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4af00-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4af00-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4af00-110">Prerequisites</span></span>

<span data-ttu-id="4af00-111">Para configurar a integração do Azure AD ao Gigya, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="4af00-111">To configure Azure AD integration with Gigya, you need the following items:</span></span>

- <span data-ttu-id="4af00-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4af00-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4af00-113">Uma assinatura habilitada para logon único do Gigya</span><span class="sxs-lookup"><span data-stu-id="4af00-113">A Gigya single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4af00-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="4af00-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4af00-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="4af00-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4af00-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="4af00-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4af00-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4af00-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4af00-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="4af00-118">Scenario description</span></span>
<span data-ttu-id="4af00-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="4af00-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4af00-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="4af00-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4af00-121">Adicionando Gigya da galeria</span><span class="sxs-lookup"><span data-stu-id="4af00-121">Adding Gigya from the gallery</span></span>
2. <span data-ttu-id="4af00-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4af00-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-gigya-from-the-gallery"></a><span data-ttu-id="4af00-123">Adicionando Gigya da galeria</span><span class="sxs-lookup"><span data-stu-id="4af00-123">Adding Gigya from the gallery</span></span>
<span data-ttu-id="4af00-124">Para configurar a integração do Gigya ao Azure AD, você precisa adicionar o Gigya da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="4af00-124">To configure the integration of Gigya into Azure AD, you need to add Gigya from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4af00-125">**Para adicionar o Gigya da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4af00-125">**To add Gigya from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4af00-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4af00-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4af00-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="4af00-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4af00-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4af00-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="4af00-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4af00-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="4af00-133">Na caixa de pesquisa, digite **Gigya**.</span><span class="sxs-lookup"><span data-stu-id="4af00-133">In the search box, type **Gigya**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_search.png)

5. <span data-ttu-id="4af00-135">No painel de resultados, selecione **Gigya** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4af00-135">In the results panel, select **Gigya**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4af00-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4af00-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4af00-138">Nesta seção, você configura e testa o logon único do Azure AD com o Gigya com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="4af00-138">In this section, you configure and test Azure AD single sign-on with Gigya based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4af00-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Gigya é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4af00-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Gigya is to a user in Azure AD.</span></span> <span data-ttu-id="4af00-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Gigya.</span><span class="sxs-lookup"><span data-stu-id="4af00-140">In other words, a link relationship between an Azure AD user and the related user in Gigya needs to be established.</span></span>

<span data-ttu-id="4af00-141">No Gigya, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="4af00-141">In Gigya, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4af00-142">Para configurar e testar o logon único do Azure AD com o Gigya, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="4af00-142">To configure and test Azure AD single sign-on with Gigya, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4af00-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="4af00-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4af00-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4af00-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4af00-145">**[Como criar um usuário de teste do Gigya](#creating-a-gigya-test-user)** – para ter um equivalente de Brenda Fernandes no Gigya que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4af00-145">**[Creating a Gigya test user](#creating-a-gigya-test-user)** - to have a counterpart of Britta Simon in Gigya that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4af00-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4af00-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4af00-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="4af00-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4af00-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4af00-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4af00-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Gigya.</span><span class="sxs-lookup"><span data-stu-id="4af00-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Gigya application.</span></span>

<span data-ttu-id="4af00-150">**Para configurar o logon único do Azure AD com o Gigya, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4af00-150">**To configure Azure AD single sign-on with Gigya, perform the following steps:**</span></span>

1. <span data-ttu-id="4af00-151">No portal do Azure, na página de integração do aplicativo **Gigya**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="4af00-151">In the Azure portal, on the **Gigya** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="4af00-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="4af00-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_samlbase.png)

3. <span data-ttu-id="4af00-155">Na seção **URLs e Domínio do Gigya**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4af00-155">On the **Gigya Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_url.png)

    <span data-ttu-id="4af00-157">a.</span><span class="sxs-lookup"><span data-stu-id="4af00-157">a.</span></span> <span data-ttu-id="4af00-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `http://<companyname>.gigya.com`</span><span class="sxs-lookup"><span data-stu-id="4af00-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://<companyname>.gigya.com`</span></span>

    <span data-ttu-id="4af00-159">b.</span><span class="sxs-lookup"><span data-stu-id="4af00-159">b.</span></span> <span data-ttu-id="4af00-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://fidm.gigya.com/saml/v2.0/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="4af00-160">In the **Identifier** textbox, type a URL using the following pattern: `https://fidm.gigya.com/saml/v2.0/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4af00-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="4af00-161">These values are not real.</span></span> <span data-ttu-id="4af00-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="4af00-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4af00-163">Contate a [equipe de suporte ao Cliente do Gigya](https://www.gigya.com/support-policy/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="4af00-163">Contact [Gigya Client support team](https://www.gigya.com/support-policy/) to get these values.</span></span> 
 
4. <span data-ttu-id="4af00-164">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="4af00-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_certificate.png) 

5. <span data-ttu-id="4af00-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="4af00-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-gigya-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4af00-168">Na seção **Configuração do Gigya**, clique em **Configurar o Gigya** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="4af00-168">On the **Gigya Configuration** section, click **Configure Gigya** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4af00-169">Copie a **ID da Entidade SAML e a URL do Serviço de Logon Único do SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="4af00-169">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_configure.png) 

7. <span data-ttu-id="4af00-171">Em outra janela do navegador da Web, faça logon em seu site de empresa do Gigya como administrador.</span><span class="sxs-lookup"><span data-stu-id="4af00-171">In a different web browser window, log into your Gigya company site as an administrator.</span></span>

8. <span data-ttu-id="4af00-172">Vá para **Configurações \> Logon do SAML** e clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4af00-172">Go to **Settings \> SAML Login**, and then click the **Add** button.</span></span>
   
    <span data-ttu-id="4af00-173">![Logon SAML](./media/active-directory-saas-gigya-tutorial/ic789532.png "logon SAML")</span><span class="sxs-lookup"><span data-stu-id="4af00-173">![SAML Login](./media/active-directory-saas-gigya-tutorial/ic789532.png "SAML Login")</span></span>

9. <span data-ttu-id="4af00-174">Na seção **Logon SAML** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4af00-174">In the **SAML Login** section, perform the following steps:</span></span>
   
    <span data-ttu-id="4af00-175">![Configuração SAML](./media/active-directory-saas-gigya-tutorial/ic789533.png "configuração SAML")</span><span class="sxs-lookup"><span data-stu-id="4af00-175">![SAML Configuration](./media/active-directory-saas-gigya-tutorial/ic789533.png "SAML Configuration")</span></span>
   
    <span data-ttu-id="4af00-176">a.</span><span class="sxs-lookup"><span data-stu-id="4af00-176">a.</span></span> <span data-ttu-id="4af00-177">Na caixa de texto **Nome** , digite um nome para a sua configuração.</span><span class="sxs-lookup"><span data-stu-id="4af00-177">In the **Name** textbox, type a name for your configuration.</span></span>
   
    <span data-ttu-id="4af00-178">b.</span><span class="sxs-lookup"><span data-stu-id="4af00-178">b.</span></span> <span data-ttu-id="4af00-179">Na caixa de texto **Emissor**, cole o valor da **ID de Entidade do SAML** que você copiou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4af00-179">In **Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure Portal.</span></span> 
   
    <span data-ttu-id="4af00-180">c.</span><span class="sxs-lookup"><span data-stu-id="4af00-180">c.</span></span> <span data-ttu-id="4af00-181">Na caixa de texto **URL de Serviço de Logon Único**, cole o valor da **URL de Serviço de Logon Único** copiado do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4af00-181">In **Single Sign-On Service URL** textbox, paste the value of **Single Sign-On Service URL** which you have copied from Azure Portal.</span></span>
   
    <span data-ttu-id="4af00-182">d.</span><span class="sxs-lookup"><span data-stu-id="4af00-182">d.</span></span> <span data-ttu-id="4af00-183">Na caixa de texto **Formato de ID de Nome**, cole o valor do **Formato de Nome do Identificador** que você copiou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4af00-183">In **Name ID Format** textbox, paste the value of **Name Identifier Format** which you have copied from Azure Portal.</span></span>
   
    <span data-ttu-id="4af00-184">e.</span><span class="sxs-lookup"><span data-stu-id="4af00-184">e.</span></span> <span data-ttu-id="4af00-185">Abra seu certificado codificado em base 64 no bloco de notas baixado do portal do Azure, copie o conteúdo dele na área de transferência e cole-o na caixa de texto **Certificado X.509**.</span><span class="sxs-lookup"><span data-stu-id="4af00-185">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.</span></span>
   
    <span data-ttu-id="4af00-186">f.</span><span class="sxs-lookup"><span data-stu-id="4af00-186">f.</span></span> <span data-ttu-id="4af00-187">Clique em **Salvar Configurações**.</span><span class="sxs-lookup"><span data-stu-id="4af00-187">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="4af00-188">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="4af00-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4af00-189">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="4af00-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4af00-190">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4af00-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4af00-191">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4af00-191">Creating an Azure AD test user</span></span>

<span data-ttu-id="4af00-192">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4af00-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="4af00-194">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4af00-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4af00-195">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4af00-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-gigya-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4af00-197">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="4af00-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-gigya-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4af00-199">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4af00-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-gigya-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4af00-201">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4af00-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-gigya-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4af00-203">a.</span><span class="sxs-lookup"><span data-stu-id="4af00-203">a.</span></span> <span data-ttu-id="4af00-204">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="4af00-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4af00-205">b.</span><span class="sxs-lookup"><span data-stu-id="4af00-205">b.</span></span> <span data-ttu-id="4af00-206">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4af00-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4af00-207">c.</span><span class="sxs-lookup"><span data-stu-id="4af00-207">c.</span></span> <span data-ttu-id="4af00-208">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="4af00-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4af00-209">d.</span><span class="sxs-lookup"><span data-stu-id="4af00-209">d.</span></span> <span data-ttu-id="4af00-210">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="4af00-210">Click **Create**.</span></span>
 
### <a name="creating-a-gigya-test-user"></a><span data-ttu-id="4af00-211">Como criar um usuário de teste do Gigya</span><span class="sxs-lookup"><span data-stu-id="4af00-211">Creating a Gigya test user</span></span>

<span data-ttu-id="4af00-212">Para permitir que os usuários do Azure AD façam logon no Gigya, eles devem ser provisionados no Gigya.</span><span class="sxs-lookup"><span data-stu-id="4af00-212">In order to enable Azure AD users to log into Gigya, they must be provisioned into Gigya.</span></span>  
<span data-ttu-id="4af00-213">No caso do Gigya, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="4af00-213">In the case of Gigya, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a><span data-ttu-id="4af00-214">Para provisionar contas de usuário, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4af00-214">To provision a user accounts, perform the following steps:</span></span>

1. <span data-ttu-id="4af00-215">Faça logon em seu site de empresa do **Gigya** como administrador.</span><span class="sxs-lookup"><span data-stu-id="4af00-215">Log in to your **Gigya** company site as an administrator.</span></span>

2. <span data-ttu-id="4af00-216">Acesse **Administrador \> Gerenciar Usuários** e clique em **Convidar Usuários**.</span><span class="sxs-lookup"><span data-stu-id="4af00-216">Go to **Admin \> Manage Users**, and then click **Invite Users**.</span></span>
   
    <span data-ttu-id="4af00-217">![Gerenciar Usuários](./media/active-directory-saas-gigya-tutorial/ic789535.png "Gerenciar Usuários")</span><span class="sxs-lookup"><span data-stu-id="4af00-217">![Manage Users](./media/active-directory-saas-gigya-tutorial/ic789535.png "Manage Users")</span></span>

3. <span data-ttu-id="4af00-218">Na caixa de diálogo Convidar Usuários, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4af00-218">On the Invite Users dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="4af00-219">![Convidar Usuários](./media/active-directory-saas-gigya-tutorial/ic789536.png "Convidar Usuários")</span><span class="sxs-lookup"><span data-stu-id="4af00-219">![Invite Users](./media/active-directory-saas-gigya-tutorial/ic789536.png "Invite Users")</span></span>
   
    <span data-ttu-id="4af00-220">a.</span><span class="sxs-lookup"><span data-stu-id="4af00-220">a.</span></span> <span data-ttu-id="4af00-221">Na caixa de texto **Email** , digite o alias de email de uma conta válida do Active Directory do Azure que você deseja provisionar.</span><span class="sxs-lookup"><span data-stu-id="4af00-221">In the **Email** textbox, type the email alias of a valid Azure Active Directory account you want to provision.</span></span>
    
    <span data-ttu-id="4af00-222">b.</span><span class="sxs-lookup"><span data-stu-id="4af00-222">b.</span></span> <span data-ttu-id="4af00-223">Clique em **Convidar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="4af00-223">Click **Invite User**.</span></span>
      
    > [!NOTE]
    > <span data-ttu-id="4af00-224">O titular da conta do Active Directory do Azure receberá um email com um link para confirmar a conta antes que ela se torne ativa.</span><span class="sxs-lookup"><span data-stu-id="4af00-224">The Azure Active Directory account holder will receive an email that includes a link to confirm the account before it becomes active.</span></span>
    > 
    

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4af00-225">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4af00-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4af00-226">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Gigya.</span><span class="sxs-lookup"><span data-stu-id="4af00-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Gigya.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="4af00-228">**Para atribuir Brenda Fernandes ao Gigya, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4af00-228">**To assign Britta Simon to Gigya, perform the following steps:**</span></span>

1. <span data-ttu-id="4af00-229">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4af00-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="4af00-231">Na lista de aplicativos, selecione **Gigya**.</span><span class="sxs-lookup"><span data-stu-id="4af00-231">In the applications list, select **Gigya**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_app.png) 

3. <span data-ttu-id="4af00-233">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="4af00-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="4af00-235">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4af00-235">Click **Add** button.</span></span> <span data-ttu-id="4af00-236">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4af00-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="4af00-238">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="4af00-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4af00-239">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4af00-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4af00-240">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4af00-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4af00-241">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="4af00-241">Testing single sign-on</span></span>

<span data-ttu-id="4af00-242">O objetivo desta seção é testar sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="4af00-242">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="4af00-243">Ao clicar no bloco do Gigya no Painel de Acesso, você deve ser conectado automaticamente ao seu aplicativo Gigya.</span><span class="sxs-lookup"><span data-stu-id="4af00-243">When you click the Gigya tile in the Access Panel, you should get automatically signed-on to your Gigya application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4af00-244">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="4af00-244">Additional resources</span></span>

* [<span data-ttu-id="4af00-245">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="4af00-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4af00-246">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4af00-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_203.png

