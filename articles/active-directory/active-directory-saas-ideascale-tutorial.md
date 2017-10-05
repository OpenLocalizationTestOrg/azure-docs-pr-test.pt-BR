---
title: "Tutorial: Integração do Azure Active Directory ao IdeaScale | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o IdeaScale."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e16dda6b-fdf9-43cc-9bbb-a523f085a8af
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 88099e942319f16dd721da83e4e69b8fcb836c0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ideascale"></a><span data-ttu-id="66de1-103">Tutorial: integração do Active Directory do Azure ao IdeaScale</span><span class="sxs-lookup"><span data-stu-id="66de1-103">Tutorial: Azure Active Directory integration with IdeaScale</span></span>

<span data-ttu-id="66de1-104">Neste tutorial, você aprenderá a integrar o IdeaScale ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="66de1-104">In this tutorial, you learn how to integrate IdeaScale with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="66de1-105">A integração do IdeaScale ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="66de1-105">Integrating IdeaScale with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="66de1-106">Você pode controlar no Azure AD quem terá acesso ao IdeaScale</span><span class="sxs-lookup"><span data-stu-id="66de1-106">You can control in Azure AD who has access to IdeaScale</span></span>
- <span data-ttu-id="66de1-107">Você pode permitir que seus usuários façam logon automaticamente no IdeaScale (Logon Único) com as contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="66de1-107">You can enable your users to automatically get signed-on to IdeaScale (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="66de1-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="66de1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="66de1-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="66de1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66de1-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="66de1-110">Prerequisites</span></span>

<span data-ttu-id="66de1-111">Para configurar a integração do Azure AD ao IdeaScale, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="66de1-111">To configure Azure AD integration with IdeaScale, you need the following items:</span></span>

- <span data-ttu-id="66de1-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="66de1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="66de1-113">Uma assinatura habilitada para logon único do IdeaScale</span><span class="sxs-lookup"><span data-stu-id="66de1-113">An IdeaScale single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="66de1-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="66de1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="66de1-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="66de1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="66de1-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="66de1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="66de1-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="66de1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="66de1-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="66de1-118">Scenario description</span></span>
<span data-ttu-id="66de1-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="66de1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="66de1-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="66de1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="66de1-121">Adicionando IdeaScale da galeria</span><span class="sxs-lookup"><span data-stu-id="66de1-121">Adding IdeaScale from the gallery</span></span>
2. <span data-ttu-id="66de1-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="66de1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ideascale-from-the-gallery"></a><span data-ttu-id="66de1-123">Adicionando IdeaScale da galeria</span><span class="sxs-lookup"><span data-stu-id="66de1-123">Adding IdeaScale from the gallery</span></span>
<span data-ttu-id="66de1-124">Para configurar a integração do IdeaScale ao Azure AD, você precisará adicioná-lo da galeria à sua lista de aplicativos de SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="66de1-124">To configure the integration of IdeaScale into Azure AD, you need to add IdeaScale from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="66de1-125">**Para adicionar o IdeaScale da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="66de1-125">**To add IdeaScale from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="66de1-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="66de1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="66de1-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="66de1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="66de1-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="66de1-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="66de1-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="66de1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="66de1-133">Na caixa de pesquisa, digite **IdeaScale**.</span><span class="sxs-lookup"><span data-stu-id="66de1-133">In the search box, type **IdeaScale**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_search.png)

5. <span data-ttu-id="66de1-135">No painel de resultados, selecione **IdeaScale** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="66de1-135">In the results panel, select **IdeaScale**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="66de1-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="66de1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="66de1-138">Nesta seção, você configurará e testará o logon único do Azure AD com o IdeaScale com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="66de1-138">In this section, you configure and test Azure AD single sign-on with IdeaScale based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="66de1-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do IdeaScale é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="66de1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in IdeaScale is to a user in Azure AD.</span></span> <span data-ttu-id="66de1-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="66de1-140">In other words, a link relationship between an Azure AD user and the related user in IdeaScale needs to be established.</span></span>

<span data-ttu-id="66de1-141">No IdeaScale, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="66de1-141">In IdeaScale, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="66de1-142">Para configurar e testar o logon único do Azure AD com o IdeaScale, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="66de1-142">To configure and test Azure AD single sign-on with IdeaScale, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="66de1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="66de1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="66de1-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="66de1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="66de1-145">**[Como criar um usuário de teste do IdeaScale](#creating-an-ideascale-test-user)** – para ter um equivalente de Brenda Fernandes no IdeaScale que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="66de1-145">**[Creating an IdeaScale test user](#creating-an-ideascale-test-user)** - to have a counterpart of Britta Simon in IdeaScale that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="66de1-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="66de1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="66de1-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="66de1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="66de1-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="66de1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="66de1-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="66de1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your IdeaScale application.</span></span>

<span data-ttu-id="66de1-150">**Para configurar o logon único do Azure AD com o IdeaScale, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="66de1-150">**To configure Azure AD single sign-on with IdeaScale, perform the following steps:**</span></span>

1. <span data-ttu-id="66de1-151">No portal do Azure, na página de integração de aplicativos do **IdeaScale**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="66de1-151">In the Azure portal, on the **IdeaScale** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="66de1-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="66de1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_samlbase.png)

3. <span data-ttu-id="66de1-155">Na seção **URLs e Domínio do IdeaScale**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="66de1-155">On the **IdeaScale Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_url.png)

    <span data-ttu-id="66de1-157">a.</span><span class="sxs-lookup"><span data-stu-id="66de1-157">a.</span></span> <span data-ttu-id="66de1-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<companyname>.ideascale.com`</span><span class="sxs-lookup"><span data-stu-id="66de1-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.ideascale.com`</span></span>

    <span data-ttu-id="66de1-159">b.</span><span class="sxs-lookup"><span data-stu-id="66de1-159">b.</span></span> <span data-ttu-id="66de1-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="66de1-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `http://<companyname>.ideascale.com`  |
    | `https://<companyname>.ideascale.com` |

    > [!NOTE] 
    > <span data-ttu-id="66de1-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="66de1-161">These values are not real.</span></span> <span data-ttu-id="66de1-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="66de1-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="66de1-163">Entre em contato com a [equipe de suporte do cliente do IdeaScale](http://support.ideascale.com/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="66de1-163">Contact [IdeaScale Client support team](http://support.ideascale.com/) to get these values.</span></span> 
 
4. <span data-ttu-id="66de1-164">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="66de1-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_certificate.png) 

5. <span data-ttu-id="66de1-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="66de1-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ideascale-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="66de1-168">Na seção **Configuração do IdeaScale**, clique em **Configurar IdeaScale** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="66de1-168">On the **IdeaScale Configuration** section, click **Configure IdeaScale** to open **Configure sign-on** window.</span></span> <span data-ttu-id="66de1-169">Copie o **URL de logout e a ID da Entidade do SAML** da **seção de Referência Rápida**.</span><span class="sxs-lookup"><span data-stu-id="66de1-169">Copy the **Sign-Out URL, and SAML Entity ID** from the **Quick Reference section**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_configure.png) 

7. <span data-ttu-id="66de1-171">Em outra janela do navegador da Web, faça logon no site da empresa do IdeaScale como administrador.</span><span class="sxs-lookup"><span data-stu-id="66de1-171">In a different web browser window, log in to your IdeaScale company site as an administrator.</span></span>

8. <span data-ttu-id="66de1-172">Vá para **Configurações da Comunidade**.</span><span class="sxs-lookup"><span data-stu-id="66de1-172">Go to **Community Settings**.</span></span>
   
    <span data-ttu-id="66de1-173">![Configurações da Comunidade](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Configurações da Comunidade")</span><span class="sxs-lookup"><span data-stu-id="66de1-173">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span></span>

9. <span data-ttu-id="66de1-174">Vá para **Segurança \> Configurações de Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="66de1-174">Go to **Security \> Single Signon Settings**.</span></span>
   
    <span data-ttu-id="66de1-175">![Configurações de Logon Único](./media/active-directory-saas-ideascale-tutorial/ic790848.png "Configurações de Logon Único")</span><span class="sxs-lookup"><span data-stu-id="66de1-175">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790848.png "Single Signon Settings")</span></span>

10. <span data-ttu-id="66de1-176">Para **Tipo de Logon Único**, selecione **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="66de1-176">As **Single-Signon Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="66de1-177">![Tipo de Logon Único](./media/active-directory-saas-ideascale-tutorial/ic790849.png "Tipo de Logon Único")</span><span class="sxs-lookup"><span data-stu-id="66de1-177">![Single Signon Type](./media/active-directory-saas-ideascale-tutorial/ic790849.png "Single Signon Type")</span></span>

11. <span data-ttu-id="66de1-178">No diálogo **Configurações de Logon Único** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="66de1-178">On the **Single Signon Settings** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="66de1-179">![Configurações de Logon Único](./media/active-directory-saas-ideascale-tutorial/ic790850.png "Configurações de Logon Único")</span><span class="sxs-lookup"><span data-stu-id="66de1-179">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790850.png "Single Signon Settings")</span></span>
   
    <span data-ttu-id="66de1-180">a.</span><span class="sxs-lookup"><span data-stu-id="66de1-180">a.</span></span> <span data-ttu-id="66de1-181">Na caixa de texto **ID da Entidade do IdP do SAML**, cole o valor da **ID da Entidade do SAML** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="66de1-181">In **SAML IdP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="66de1-182">b.</span><span class="sxs-lookup"><span data-stu-id="66de1-182">b.</span></span> <span data-ttu-id="66de1-183">Copie o conteúdo do arquivo de metadados baixado do portal do Azure e cole-o na caixa de texto **Metadados do IdP do SAML**.</span><span class="sxs-lookup"><span data-stu-id="66de1-183">Copy the content of your downloaded metadata file from Azure portal, and paste it into the **SAML IdP Metadata** textbox.</span></span>

    <span data-ttu-id="66de1-184">c.</span><span class="sxs-lookup"><span data-stu-id="66de1-184">c.</span></span> <span data-ttu-id="66de1-185">Na caixa de texto **URL de Sucesso do Logoff**, cole o valor da **URL de Logoff** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="66de1-185">In **Logout Success URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="66de1-186">d.</span><span class="sxs-lookup"><span data-stu-id="66de1-186">d.</span></span> <span data-ttu-id="66de1-187">Clique em **Salvar Alterações**.</span><span class="sxs-lookup"><span data-stu-id="66de1-187">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="66de1-188">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="66de1-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="66de1-189">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="66de1-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="66de1-190">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="66de1-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="66de1-191">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="66de1-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="66de1-192">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="66de1-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="66de1-194">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="66de1-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="66de1-195">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="66de1-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ideascale-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="66de1-197">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="66de1-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ideascale-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="66de1-199">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="66de1-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ideascale-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="66de1-201">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="66de1-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ideascale-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="66de1-203">a.</span><span class="sxs-lookup"><span data-stu-id="66de1-203">a.</span></span> <span data-ttu-id="66de1-204">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="66de1-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="66de1-205">b.</span><span class="sxs-lookup"><span data-stu-id="66de1-205">b.</span></span> <span data-ttu-id="66de1-206">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="66de1-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="66de1-207">c.</span><span class="sxs-lookup"><span data-stu-id="66de1-207">c.</span></span> <span data-ttu-id="66de1-208">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="66de1-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="66de1-209">d.</span><span class="sxs-lookup"><span data-stu-id="66de1-209">d.</span></span> <span data-ttu-id="66de1-210">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="66de1-210">Click **Create**.</span></span>
 
### <a name="creating-an-ideascale-test-user"></a><span data-ttu-id="66de1-211">Como criar um usuário de teste do IdeaScale</span><span class="sxs-lookup"><span data-stu-id="66de1-211">Creating an IdeaScale test user</span></span>

<span data-ttu-id="66de1-212">Para permitir que os usuários do Azure AD façam logon no IdeaScale, eles deverão ser provisionados no IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="66de1-212">To enable Azure AD users to log into IdeaScale, they must be provisioned in to IdeaScale.</span></span> <span data-ttu-id="66de1-213">No caso do IdeaScale, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="66de1-213">In the case of IdeaScale, provisioning is a manual task.</span></span>

<span data-ttu-id="66de1-214">**Para configurar o provisionamento de usuários, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="66de1-214">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="66de1-215">Faça logon em seu site de empresa do **IdeaScale** como administrador.</span><span class="sxs-lookup"><span data-stu-id="66de1-215">Log in to your **IdeaScale** company site as administrator.</span></span>

2. <span data-ttu-id="66de1-216">Vá para **Configurações da Comunidade**.</span><span class="sxs-lookup"><span data-stu-id="66de1-216">Go to **Community Settings**.</span></span>
   
    <span data-ttu-id="66de1-217">![Configurações da Comunidade](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Configurações da Comunidade")</span><span class="sxs-lookup"><span data-stu-id="66de1-217">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span></span>

3. <span data-ttu-id="66de1-218">Vá para **Configurações Básicas \> Gerenciamento de Membros**.</span><span class="sxs-lookup"><span data-stu-id="66de1-218">Go to **Basic Settings \> Member Management**.</span></span>

4. <span data-ttu-id="66de1-219">Clique em **Adicionar Membro**.</span><span class="sxs-lookup"><span data-stu-id="66de1-219">Click **Add Member**.</span></span>
   
    <span data-ttu-id="66de1-220">![Gerenciamento de Membros](./media/active-directory-saas-ideascale-tutorial/ic790852.png "Gerenciamento de Membros")</span><span class="sxs-lookup"><span data-stu-id="66de1-220">![Member Management](./media/active-directory-saas-ideascale-tutorial/ic790852.png "Member Management")</span></span>

5. <span data-ttu-id="66de1-221">Na seção Adicionar Novo Membro, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="66de1-221">In the Add New Member section, perform the following steps:</span></span>
   
    <span data-ttu-id="66de1-222">![Adicionar Novo Membro](./media/active-directory-saas-ideascale-tutorial/ic790853.png "Adicionar Novo Membro")</span><span class="sxs-lookup"><span data-stu-id="66de1-222">![Add New Member](./media/active-directory-saas-ideascale-tutorial/ic790853.png "Add New Member")</span></span>
   
    <span data-ttu-id="66de1-223">a.</span><span class="sxs-lookup"><span data-stu-id="66de1-223">a.</span></span> <span data-ttu-id="66de1-224">Na caixa de texto **Endereços de Email** , digite o endereço de email de uma conta de AAD válida que você deseja provisionar.</span><span class="sxs-lookup"><span data-stu-id="66de1-224">In the **Email Addresses** textbox, type the email address of a valid AAD account you want to provision.</span></span>
   
    <span data-ttu-id="66de1-225">b.</span><span class="sxs-lookup"><span data-stu-id="66de1-225">b.</span></span> <span data-ttu-id="66de1-226">Clique em **Salvar Alterações**.</span><span class="sxs-lookup"><span data-stu-id="66de1-226">Click **Save Changes**.</span></span> 
   
    >[!NOTE]
    ><span data-ttu-id="66de1-227">O titular da conta do Azure Active Directory recebe um email com um link para confirmar a conta antes que ela se torne ativa.</span><span class="sxs-lookup"><span data-stu-id="66de1-227">The Azure Active Directory account holder gets an email with a link to confirm the account before it becomes active.</span></span>
      
>[!NOTE]
><span data-ttu-id="66de1-228">É possível usar qualquer outra ferramenta de criação da conta de usuário do IdeaScale ou as APIs fornecidas pelo IdeaScale para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="66de1-228">You can use any other IdeaScale user account creation tools or APIs provided by IdeaScale to provision AAD user accounts.</span></span>
 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="66de1-229">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="66de1-229">Assigning the Azure AD test user</span></span>

<span data-ttu-id="66de1-230">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="66de1-230">In this section, you enable Britta Simon to use Azure single sign-on by granting access to IdeaScale.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="66de1-232">**Para atribuir Brenda Fernandes ao IdeaScale, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="66de1-232">**To assign Britta Simon to IdeaScale, perform the following steps:**</span></span>

1. <span data-ttu-id="66de1-233">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="66de1-233">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="66de1-235">Na lista de aplicativos, selecione **IdeaScale**.</span><span class="sxs-lookup"><span data-stu-id="66de1-235">In the applications list, select **IdeaScale**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_app.png) 

3. <span data-ttu-id="66de1-237">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="66de1-237">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="66de1-239">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="66de1-239">Click **Add** button.</span></span> <span data-ttu-id="66de1-240">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="66de1-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="66de1-242">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="66de1-242">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="66de1-243">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="66de1-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="66de1-244">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="66de1-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="66de1-245">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="66de1-245">Testing single sign-on</span></span>


<span data-ttu-id="66de1-246">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="66de1-246">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="66de1-247">Ao clicar no bloco do IdeaScale no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="66de1-247">When you click the IdeaScale tile in the Access Panel, you should get automatically signed-on to your IdeaScale application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="66de1-248">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="66de1-248">Additional resources</span></span>

* [<span data-ttu-id="66de1-249">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="66de1-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="66de1-250">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="66de1-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_203.png

