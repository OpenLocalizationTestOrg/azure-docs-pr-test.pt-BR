---
title: "Tutorial: integração do Azure Active Directory ao UserEcho | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Active Directory do Azure e o UserEcho."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bedd916b-8f69-4b50-9b8d-56f4ee3bd3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 2d824d8d5eb8a25db128397b908a126bd87213ea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-userecho"></a><span data-ttu-id="e5513-103">Tutorial: Integração do Active Directory do Azure com o UserEcho</span><span class="sxs-lookup"><span data-stu-id="e5513-103">Tutorial: Azure Active Directory integration with UserEcho</span></span>

<span data-ttu-id="e5513-104">Neste tutorial, você aprenderá como integrar o UserEcho ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="e5513-104">In this tutorial, you learn how to integrate UserEcho with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e5513-105">A integração do UserEcho ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="e5513-105">Integrating UserEcho with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e5513-106">No AD do Azure, você pode controlar quem tem acesso ao UserEcho</span><span class="sxs-lookup"><span data-stu-id="e5513-106">You can control in Azure AD who has access to UserEcho</span></span>
- <span data-ttu-id="e5513-107">Você pode permitir que seus usuários façam logon automaticamente no UserEcho (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e5513-107">You can enable your users to automatically get signed-on to UserEcho (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e5513-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e5513-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e5513-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e5513-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e5513-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e5513-110">Prerequisites</span></span>

<span data-ttu-id="e5513-111">Para configurar a integração do AD do Azure ao UserEcho, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="e5513-111">To configure Azure AD integration with UserEcho, you need the following items:</span></span>

- <span data-ttu-id="e5513-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e5513-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e5513-113">Uma assinatura do UserEcho habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="e5513-113">A UserEcho single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e5513-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="e5513-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e5513-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="e5513-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e5513-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="e5513-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e5513-117">Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e5513-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e5513-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="e5513-118">Scenario description</span></span>
<span data-ttu-id="e5513-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="e5513-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e5513-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="e5513-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e5513-121">Adicionando o UserEcho da galeria</span><span class="sxs-lookup"><span data-stu-id="e5513-121">Adding UserEcho from the gallery</span></span>
2. <span data-ttu-id="e5513-122">configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e5513-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-userecho-from-the-gallery"></a><span data-ttu-id="e5513-123">Adicionando o UserEcho da galeria</span><span class="sxs-lookup"><span data-stu-id="e5513-123">Adding UserEcho from the gallery</span></span>
<span data-ttu-id="e5513-124">Para configurar a integração do UserEcho ao AD do Azure, você precisará adicionar o UserEcho da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="e5513-124">To configure the integration of UserEcho into Azure AD, you need to add UserEcho from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e5513-125">**Para adicionar o UserEcho da galeria, execute as etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="e5513-125">**To add UserEcho from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e5513-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e5513-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e5513-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="e5513-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e5513-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e5513-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="e5513-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e5513-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="e5513-133">Na caixa de pesquisa, digite **UserEcho**.</span><span class="sxs-lookup"><span data-stu-id="e5513-133">In the search box, type **UserEcho**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_search.png)

5. <span data-ttu-id="e5513-135">No painel de resultados, selecione **UserEcho** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e5513-135">In the results panel, select **UserEcho**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e5513-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e5513-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e5513-138">Nesta seção, você configurará e testará o logon único do Azure AD com o UserEcho com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="e5513-138">In this section, you configure and test Azure AD single sign-on with UserEcho based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e5513-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do UserEcho é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e5513-139">For single sign-on to work, Azure AD needs to know what the counterpart user in UserEcho is to a user in Azure AD.</span></span> <span data-ttu-id="e5513-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no UserEcho.</span><span class="sxs-lookup"><span data-stu-id="e5513-140">In other words, a link relationship between an Azure AD user and the related user in UserEcho needs to be established.</span></span>

<span data-ttu-id="e5513-141">No UserEcho, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="e5513-141">In UserEcho, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e5513-142">Para configurar e testar o logon único do AD do Azure com o UserEcho, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="e5513-142">To configure and test Azure AD single sign-on with UserEcho, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e5513-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="e5513-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e5513-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e5513-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e5513-145">**[Criação de um usuário de teste do UserEcho](#creating-a-userecho-test-user)** – para ter um equivalente de Brenda Fernandes no UserEcho que esteja vinculado à representação de usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e5513-145">**[Creating a UserEcho test user](#creating-a-userecho-test-user)** - to have a counterpart of Britta Simon in UserEcho that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e5513-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="e5513-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e5513-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="e5513-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e5513-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e5513-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e5513-149">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo UserEcho.</span><span class="sxs-lookup"><span data-stu-id="e5513-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your UserEcho application.</span></span>

<span data-ttu-id="e5513-150">**Para configurar o logon único do AD do Azure com o UserEcho, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e5513-150">**To configure Azure AD single sign-on with UserEcho, perform the following steps:**</span></span>

1. <span data-ttu-id="e5513-151">No Portal do Azure, na página de integração de aplicativos do **UserEcho**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="e5513-151">In the Azure portal, on the **UserEcho** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="e5513-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="e5513-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_samlbase.png)

3. <span data-ttu-id="e5513-155">Na seção **URLs e Domínio do UserEcho**, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="e5513-155">On the **UserEcho Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_url.png)

    <span data-ttu-id="e5513-157">a.</span><span class="sxs-lookup"><span data-stu-id="e5513-157">a.</span></span> <span data-ttu-id="e5513-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<companyname>.userecho.com/`</span><span class="sxs-lookup"><span data-stu-id="e5513-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.userecho.com/`</span></span>

    <span data-ttu-id="e5513-159">b.</span><span class="sxs-lookup"><span data-stu-id="e5513-159">b.</span></span> <span data-ttu-id="e5513-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<companyname>.userecho.com/saml/metadata/`</span><span class="sxs-lookup"><span data-stu-id="e5513-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.userecho.com/saml/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e5513-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="e5513-161">These values are not real.</span></span> <span data-ttu-id="e5513-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="e5513-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e5513-163">Contate a [equipe de suporte ao cliente do UserEcho](https://feedback.userecho.com/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="e5513-163">Contact [UserEcho Client support team](https://feedback.userecho.com/) to get these values.</span></span> 

4. <span data-ttu-id="e5513-164">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="e5513-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_certificate.png) 

5. <span data-ttu-id="e5513-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="e5513-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e5513-168">Na seção **Configuração do UserEcho**, clique em **Configurar UserEcho** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="e5513-168">On the **UserEcho Configuration** section, click **Configure UserEcho** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e5513-169">Copie a **URL do serviço de logon único do SAML e a URL de logoff** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="e5513-169">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_configure.png) 

7. <span data-ttu-id="e5513-171">Em outra janela do navegador, entre em seu site de empresa do UserEcho como administrador.</span><span class="sxs-lookup"><span data-stu-id="e5513-171">In another browser window, sign on to your UserEcho company site as an administrator.</span></span>

8. <span data-ttu-id="e5513-172">Na barra de ferramentas na parte superior, clique em seu nome de usuário para expandir o menu e clique em **Instalação**.</span><span class="sxs-lookup"><span data-stu-id="e5513-172">In the toolbar on the top, click your user name to expand the menu, and then click **Setup**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_06.png) 

9. <span data-ttu-id="e5513-174">Clique em **Integrações**.</span><span class="sxs-lookup"><span data-stu-id="e5513-174">Click **Integrations**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_07.png) 

10. <span data-ttu-id="e5513-176">Clique em **site** e em **Logon único (SAML2)**.</span><span class="sxs-lookup"><span data-stu-id="e5513-176">Click **Website**, and then click **Single sign-on (SAML2)**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_08.png) 

11. <span data-ttu-id="e5513-178">Na página **Logon Único (SAML)** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e5513-178">On the **Single sign-on (SAML)** page, perform the following steps:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_09.png)
    
    <span data-ttu-id="e5513-180">a.</span><span class="sxs-lookup"><span data-stu-id="e5513-180">a.</span></span> <span data-ttu-id="e5513-181">Para **Habilitado para SAML**, selecione **Sim**.</span><span class="sxs-lookup"><span data-stu-id="e5513-181">As **SAML-enabled**, select **Yes**.</span></span>
    
    <span data-ttu-id="e5513-182">b.</span><span class="sxs-lookup"><span data-stu-id="e5513-182">b.</span></span> <span data-ttu-id="e5513-183">Cole a **URL do Serviço de Logon Único SAML** copiada do Portal do Azure na caixa de texto **URL de SSO de SAML**.</span><span class="sxs-lookup"><span data-stu-id="e5513-183">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **SAML SSO URL** textbox.</span></span>
    
    <span data-ttu-id="e5513-184">c.</span><span class="sxs-lookup"><span data-stu-id="e5513-184">c.</span></span> <span data-ttu-id="e5513-185">Cole a **URL de Saída** copiada no Portal do Azure para a caixa de texto **URL de Logoff remoto**.</span><span class="sxs-lookup"><span data-stu-id="e5513-185">Paste **Sign-Out URL**, which you have copied from the Azure portal into the **Remote logoout URL** textbox.</span></span>
    
    <span data-ttu-id="e5513-186">d.</span><span class="sxs-lookup"><span data-stu-id="e5513-186">d.</span></span> <span data-ttu-id="e5513-187">Abra o certificado baixado no Bloco de Notas, copie o conteúdo e cole-o na caixa de texto **Certificado X.509** .</span><span class="sxs-lookup"><span data-stu-id="e5513-187">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **X.509 Certificate** textbox.</span></span>
    
    <span data-ttu-id="e5513-188">e.</span><span class="sxs-lookup"><span data-stu-id="e5513-188">e.</span></span> <span data-ttu-id="e5513-189">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="e5513-189">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="e5513-190">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="e5513-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e5513-191">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="e5513-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e5513-192">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e5513-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e5513-193">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e5513-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="e5513-194">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e5513-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="e5513-196">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e5513-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e5513-197">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e5513-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-userecho-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e5513-199">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="e5513-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-userecho-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e5513-201">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e5513-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-userecho-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e5513-203">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e5513-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-userecho-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e5513-205">a.</span><span class="sxs-lookup"><span data-stu-id="e5513-205">a.</span></span> <span data-ttu-id="e5513-206">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="e5513-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e5513-207">b.</span><span class="sxs-lookup"><span data-stu-id="e5513-207">b.</span></span> <span data-ttu-id="e5513-208">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e5513-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e5513-209">c.</span><span class="sxs-lookup"><span data-stu-id="e5513-209">c.</span></span> <span data-ttu-id="e5513-210">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="e5513-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e5513-211">d.</span><span class="sxs-lookup"><span data-stu-id="e5513-211">d.</span></span> <span data-ttu-id="e5513-212">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e5513-212">Click **Create**.</span></span>
 
### <a name="creating-a-userecho-test-user"></a><span data-ttu-id="e5513-213">Criando um usuário de teste do UserEcho</span><span class="sxs-lookup"><span data-stu-id="e5513-213">Creating a UserEcho test user</span></span>

<span data-ttu-id="e5513-214">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no UserEcho.</span><span class="sxs-lookup"><span data-stu-id="e5513-214">The objective of this section is to create a user called Britta Simon in UserEcho.</span></span>

<span data-ttu-id="e5513-215">**Para criar um usuário chamado Brenda Fernandes no UserEcho, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e5513-215">**To create a user called Britta Simon in UserEcho, perform the following steps:**</span></span>

1. <span data-ttu-id="e5513-216">Faça logon no site da empresa do UserEcho como um administrador.</span><span class="sxs-lookup"><span data-stu-id="e5513-216">Sign-on to your UserEcho company site as an administrator.</span></span>

2. <span data-ttu-id="e5513-217">Na barra de ferramentas na parte superior, clique em seu nome de usuário para expandir o menu e clique em **Instalação**.</span><span class="sxs-lookup"><span data-stu-id="e5513-217">In the toolbar on the top, click your user name to expand the menu, and then click **Setup**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_06.png)

3. <span data-ttu-id="e5513-219">Clique em **Usuários** para expandir a seção **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="e5513-219">Click **Users**, to expand the **Users** section.</span></span>
   
    ![Configurar o logon único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_10.png)

4. <span data-ttu-id="e5513-221">Clique em **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="e5513-221">Click **Users**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_11.png)

5. <span data-ttu-id="e5513-223">Clique em **Convidar um novo usuário**.</span><span class="sxs-lookup"><span data-stu-id="e5513-223">Click **Invite a new user**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_12.png)

6. <span data-ttu-id="e5513-225">Na caixa de diálogo **Convidar novo usuário** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e5513-225">On the **Invite a new user** dialog, perform the following steps:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_13.png)

    <span data-ttu-id="e5513-227">a.</span><span class="sxs-lookup"><span data-stu-id="e5513-227">a.</span></span> <span data-ttu-id="e5513-228">Na caixa de texto **Nome**, digite o nome do usuário como Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e5513-228">In the **Name** textbox, type name of the user like Britta Simon.</span></span>
    
    <span data-ttu-id="e5513-229">b.</span><span class="sxs-lookup"><span data-stu-id="e5513-229">b.</span></span>  <span data-ttu-id="e5513-230">Na caixa de texto **Email**, digite o endereço de email do usuário, como Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="e5513-230">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="e5513-231">c.</span><span class="sxs-lookup"><span data-stu-id="e5513-231">c.</span></span> <span data-ttu-id="e5513-232">Clique em **Convidar**.</span><span class="sxs-lookup"><span data-stu-id="e5513-232">Click **Invite**.</span></span>

<span data-ttu-id="e5513-233">Um convite é enviado para Brenda, que permite que ela começar a usar o UserEcho.</span><span class="sxs-lookup"><span data-stu-id="e5513-233">An invitation is sent to Britta, which enables her to start using UserEcho.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e5513-234">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e5513-234">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e5513-235">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo acesso ao UserEcho.</span><span class="sxs-lookup"><span data-stu-id="e5513-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to UserEcho.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="e5513-237">**Para atribuir Brenda Fernandes ao UserEcho, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e5513-237">**To assign Britta Simon to UserEcho, perform the following steps:**</span></span>

1. <span data-ttu-id="e5513-238">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e5513-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="e5513-240">Na lista de aplicativos, selecione **UserEcho**.</span><span class="sxs-lookup"><span data-stu-id="e5513-240">In the applications list, select **UserEcho**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_app.png) 

3. <span data-ttu-id="e5513-242">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="e5513-242">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="e5513-244">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e5513-244">Click **Add** button.</span></span> <span data-ttu-id="e5513-245">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e5513-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="e5513-247">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="e5513-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e5513-248">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e5513-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e5513-249">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e5513-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e5513-250">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="e5513-250">Testing single sign-on</span></span>

<span data-ttu-id="e5513-251">O objetivo desta seção é testar sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="e5513-251">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="e5513-252">Quando você clicar no bloco UserEcho no Painel de Acesso, deverá ser conectado automaticamente ao seu aplicativo UserEcho.</span><span class="sxs-lookup"><span data-stu-id="e5513-252">When you click the UserEcho tile in the Access Panel, you should get automatically signed-on to your UserEcho application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e5513-253">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="e5513-253">Additional resources</span></span>

* [<span data-ttu-id="e5513-254">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="e5513-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e5513-255">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e5513-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_203.png

