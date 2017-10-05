---
title: "Tutorial: integração do Azure Active Directory ao StatusPage | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Active Directory do Azure e o StatusPage."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f6ee8bb3-df43-4c0d-bf84-89f18deac4b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: fa16cdec7b89404c140435fe57d5aa4b08cfa985
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-statuspage"></a><span data-ttu-id="07170-103">Tutorial: Integração do Active Directory do Azure com o StatusPage</span><span class="sxs-lookup"><span data-stu-id="07170-103">Tutorial: Azure Active Directory integration with StatusPage</span></span>

<span data-ttu-id="07170-104">Neste tutorial, você aprende a integrar o StatusPage ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="07170-104">In this tutorial, you learn how to integrate StatusPage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="07170-105">A integração do StatusPage ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="07170-105">Integrating StatusPage with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="07170-106">No AD do Azure, você pode controlar quem tem acesso ao StatusPage</span><span class="sxs-lookup"><span data-stu-id="07170-106">You can control in Azure AD who has access to StatusPage</span></span>
- <span data-ttu-id="07170-107">Você pode habilitar o logon automático de seus usuários no StatusPage (Logon único) com as contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="07170-107">You can enable your users to automatically get signed-on to StatusPage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="07170-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="07170-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="07170-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="07170-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="07170-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="07170-110">Prerequisites</span></span>

<span data-ttu-id="07170-111">Para configurar a integração do AD do Azure com o StatusPage, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="07170-111">To configure Azure AD integration with StatusPage, you need the following items:</span></span>

- <span data-ttu-id="07170-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="07170-112">An Azure AD subscription</span></span>
- <span data-ttu-id="07170-113">Uma assinatura habilitada para logon único do StatusPage</span><span class="sxs-lookup"><span data-stu-id="07170-113">A StatusPage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="07170-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="07170-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="07170-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="07170-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="07170-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="07170-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="07170-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="07170-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="07170-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="07170-118">Scenario description</span></span>
<span data-ttu-id="07170-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="07170-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="07170-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="07170-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="07170-121">Adicionando o StatusPage da galeria</span><span class="sxs-lookup"><span data-stu-id="07170-121">Adding StatusPage from the gallery</span></span>
2. <span data-ttu-id="07170-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="07170-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-statuspage-from-the-gallery"></a><span data-ttu-id="07170-123">Adicionando o StatusPage da galeria</span><span class="sxs-lookup"><span data-stu-id="07170-123">Adding StatusPage from the gallery</span></span>
<span data-ttu-id="07170-124">Para configurar a integração do StatusPage ao AD do Azure, você precisará adicionar o StatusPage da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="07170-124">To configure the integration of StatusPage into Azure AD, you need to add StatusPage from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="07170-125">**Para adicionar o StatusPage da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="07170-125">**To add StatusPage from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="07170-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="07170-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="07170-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="07170-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="07170-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="07170-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="07170-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="07170-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="07170-133">Na caixa de pesquisa, digite **StatusPage**.</span><span class="sxs-lookup"><span data-stu-id="07170-133">In the search box, type **StatusPage**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_search.png)

5. <span data-ttu-id="07170-135">No painel de resultados, selecione **StatusPage** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="07170-135">In the results panel, select **StatusPage**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="07170-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="07170-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="07170-138">Nesta seção, você configura e testa o logon único do Azure AD com o StatusPage, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="07170-138">In this section, you configure and test Azure AD single sign-on with StatusPage based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="07170-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do StatusPage é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07170-139">For single sign-on to work, Azure AD needs to know what the counterpart user in StatusPage is to a user in Azure AD.</span></span> <span data-ttu-id="07170-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no StatusPage.</span><span class="sxs-lookup"><span data-stu-id="07170-140">In other words, a link relationship between an Azure AD user and the related user in StatusPage needs to be established.</span></span>

<span data-ttu-id="07170-141">No StatusPage, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="07170-141">In StatusPage, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="07170-142">Para configurar e testar o logon único do AD do Azure com o StatusPage, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="07170-142">To configure and test Azure AD single sign-on with StatusPage, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="07170-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="07170-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="07170-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="07170-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="07170-145">**[Criando um usuário de teste do StatusPage](#creating-a-statuspage-test-user)** – para ter um equivalente de Brenda Fernandes no StatusPage que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07170-145">**[Creating a StatusPage test user](#creating-a-statuspage-test-user)** - to have a counterpart of Britta Simon in StatusPage that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="07170-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="07170-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="07170-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="07170-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="07170-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="07170-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="07170-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo StatusPage.</span><span class="sxs-lookup"><span data-stu-id="07170-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your StatusPage application.</span></span>

<span data-ttu-id="07170-150">**Para configurar o logon único do AD do Azure com o StatusPage, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="07170-150">**To configure Azure AD single sign-on with StatusPage, perform the following steps:**</span></span>

1. <span data-ttu-id="07170-151">No portal do Azure, na página de integração do aplicativo **StatusPage**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="07170-151">In the Azure portal, on the **StatusPage** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="07170-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="07170-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_samlbase.png)

3. <span data-ttu-id="07170-155">Na seção **Domínio e URLs do StatusPage**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="07170-155">On the **StatusPage Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_url.png)

    <span data-ttu-id="07170-157">a.</span><span class="sxs-lookup"><span data-stu-id="07170-157">a.</span></span> <span data-ttu-id="07170-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="07170-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.statuspagestaging.com/` |
    | `https://<subdomain>.statuspage.io/` |

    <span data-ttu-id="07170-159">b.</span><span class="sxs-lookup"><span data-stu-id="07170-159">b.</span></span> <span data-ttu-id="07170-160">Na caixa de texto **URL de resposta** , digite uma URL no seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="07170-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span> 
    | |
    |--|
    | `https://<subdomain>.statuspagestaging.com/sso/saml/consume` |
    | `https://<subdomain>.statuspage.io/sso/saml/consume` |

    > [!NOTE]
    > <span data-ttu-id="07170-161">Entre em contato com a equipe de suporte do StatusPage em [SupportTeam@statuspage.io](mailto:SupportTeam@statuspage.io)para solicitar os metadados necessários para a configuração do logon único.</span><span class="sxs-lookup"><span data-stu-id="07170-161">Contact the StatusPage support team at [SupportTeam@statuspage.io](mailto:SupportTeam@statuspage.io)to request metadata necessary to configure single sign-on.</span></span> 
    >
    ><span data-ttu-id="07170-162">a.</span><span class="sxs-lookup"><span data-stu-id="07170-162">a.</span></span> <span data-ttu-id="07170-163">Nos metadados, copie o valor de Issuer e cole-o na caixa de texto **Identificador** .</span><span class="sxs-lookup"><span data-stu-id="07170-163">From the metadata, copy the Issuer value, and then paste it into the **Identifier** textbox.</span></span>
    >
    ><span data-ttu-id="07170-164">b.</span><span class="sxs-lookup"><span data-stu-id="07170-164">b.</span></span> <span data-ttu-id="07170-165">Nos metadados, copie o valor a URL de Resposta e cole-a na caixa de texto **URL de Resposta** .</span><span class="sxs-lookup"><span data-stu-id="07170-165">From the metadata, copy the Reply URL, and then paste it into the **Reply URL** textbox.</span></span>

4. <span data-ttu-id="07170-166">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="07170-166">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_certificate.png) 

5. <span data-ttu-id="07170-168">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="07170-168">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-statuspage-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="07170-170">Na seção **Configuração do StatusPage**, clique em **Configurar o StatusPage** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="07170-170">On the **StatusPage Configuration** section, click **Configure StatusPage** to open **Configure sign-on** window.</span></span> <span data-ttu-id="07170-171">Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="07170-171">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_configure.png) 

7. <span data-ttu-id="07170-173">Em outra janela do navegador, entre em seu site de empresa do StatusPage como administrador.</span><span class="sxs-lookup"><span data-stu-id="07170-173">In another browser window, sign on to your StatusPage company site as an administrator.</span></span>

8. <span data-ttu-id="07170-174">Na barra de ferramentas principal, clique em **Gerenciar Conta**.</span><span class="sxs-lookup"><span data-stu-id="07170-174">In the main toolbar, click **Manage Account**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_06.png) 

10. <span data-ttu-id="07170-176">Clique na guia **Logon Único** .</span><span class="sxs-lookup"><span data-stu-id="07170-176">Click the **Single Sign-on** tab.</span></span> 
   
    ![Configurar Logon Único](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_07.png) 

11. <span data-ttu-id="07170-178">Na página Instalação do SSO, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="07170-178">On the SSO Setup page, perform the following steps:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_08.png) 

    ![Configurar Logon Único](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_09.png) 
 
    <span data-ttu-id="07170-181">a.</span><span class="sxs-lookup"><span data-stu-id="07170-181">a.</span></span> <span data-ttu-id="07170-182">Na caixa de texto **URL de Destino do SSO**, cole o valor da **URL do Serviço de Logon Único SAML** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="07170-182">In the **SSO Target URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="07170-183">b.</span><span class="sxs-lookup"><span data-stu-id="07170-183">b.</span></span> <span data-ttu-id="07170-184">Abra seu certificado baixado no Bloco de Notas, copie o conteúdo e cole-o na caixa de texto **Certificado** .</span><span class="sxs-lookup"><span data-stu-id="07170-184">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **Certificate** textbox.</span></span> 

    <span data-ttu-id="07170-185">c.</span><span class="sxs-lookup"><span data-stu-id="07170-185">c.</span></span> <span data-ttu-id="07170-186">Clique em **SALVAR CONFIGURAÇÃO**.</span><span class="sxs-lookup"><span data-stu-id="07170-186">Click **SAVE CONFIGURATION**.</span></span>

> [!TIP]
> <span data-ttu-id="07170-187">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="07170-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="07170-188">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="07170-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="07170-189">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="07170-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="07170-190">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="07170-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="07170-191">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="07170-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="07170-193">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="07170-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="07170-194">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="07170-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-statuspage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="07170-196">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="07170-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-statuspage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="07170-198">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="07170-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-statuspage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="07170-200">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="07170-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-statuspage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="07170-202">a.</span><span class="sxs-lookup"><span data-stu-id="07170-202">a.</span></span> <span data-ttu-id="07170-203">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="07170-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="07170-204">b.</span><span class="sxs-lookup"><span data-stu-id="07170-204">b.</span></span> <span data-ttu-id="07170-205">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="07170-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="07170-206">c.</span><span class="sxs-lookup"><span data-stu-id="07170-206">c.</span></span> <span data-ttu-id="07170-207">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="07170-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="07170-208">d.</span><span class="sxs-lookup"><span data-stu-id="07170-208">d.</span></span> <span data-ttu-id="07170-209">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="07170-209">Click **Create**.</span></span>
 
### <a name="creating-a-statuspage-test-user"></a><span data-ttu-id="07170-210">Criando um usuário de teste de StatusPage</span><span class="sxs-lookup"><span data-stu-id="07170-210">Creating a StatusPage test user</span></span>

<span data-ttu-id="07170-211">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no StatusPage.</span><span class="sxs-lookup"><span data-stu-id="07170-211">The objective of this section is to create a user called Britta Simon in StatusPage.</span></span>

<span data-ttu-id="07170-212">O StatusPage dá suporte ao provisionamento de usuário just-in-time.</span><span class="sxs-lookup"><span data-stu-id="07170-212">StatusPage supports just-in-time provisioning.</span></span> <span data-ttu-id="07170-213">Você já habilitou isso em [Configurar o logon único do AD do Azure](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="07170-213">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="07170-214">**Para criar um usuário chamado Brenda Fernandes no StatusPage, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="07170-214">**To create a user called Britta Simon in StatusPage, perform the following steps:**</span></span>

1. <span data-ttu-id="07170-215">Faça logon em seu site de empresa do StatusPage como administrador.</span><span class="sxs-lookup"><span data-stu-id="07170-215">Sign-on to your StatusPage company site as an administrator.</span></span>

2. <span data-ttu-id="07170-216">Na parte superior do menu, clique em **Gerenciar Conta**.</span><span class="sxs-lookup"><span data-stu-id="07170-216">In the menu on the top, click **Manage Account**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_06.png)

3. <span data-ttu-id="07170-218">Clique na guia **Membros da Equipe**.</span><span class="sxs-lookup"><span data-stu-id="07170-218">Click the **Team Members** tab.</span></span> 
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_10.png) 

4. <span data-ttu-id="07170-220">Clique em **ADICIONAR MEMBRO DA EQUIPE**.</span><span class="sxs-lookup"><span data-stu-id="07170-220">Click **ADD TEAM MEMBER**.</span></span> 
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_11.png) 

5. <span data-ttu-id="07170-222">Digite o **Endereço de Email**, o **Nome** e o **Sobrenome** de um usuário válido que você deseja provisionar nas caixas de texto relacionadas.</span><span class="sxs-lookup"><span data-stu-id="07170-222">Type the **Email Address**, **First Name**, and **Sur Name** of a valid user you want to provision into the related textboxes.</span></span> 
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_12.png) 

6. <span data-ttu-id="07170-224">Como **Função**, escolha **Administrador do Cliente**.</span><span class="sxs-lookup"><span data-stu-id="07170-224">As **Role**, choose **Client Administrator**.</span></span>

7. <span data-ttu-id="07170-225">Clique em **CRIAR CONTA**.</span><span class="sxs-lookup"><span data-stu-id="07170-225">Click **CREATE ACCOUNT**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="07170-226">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="07170-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="07170-227">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao StatusPage.</span><span class="sxs-lookup"><span data-stu-id="07170-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to StatusPage.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="07170-229">**Para atribuir Brenda Fernandes ao StatusPage, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="07170-229">**To assign Britta Simon to StatusPage, perform the following steps:**</span></span>

1. <span data-ttu-id="07170-230">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="07170-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="07170-232">Na lista de aplicativos, selecione **StatusPage**.</span><span class="sxs-lookup"><span data-stu-id="07170-232">In the applications list, select **StatusPage**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_app.png) 

3. <span data-ttu-id="07170-234">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="07170-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="07170-236">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="07170-236">Click **Add** button.</span></span> <span data-ttu-id="07170-237">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="07170-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="07170-239">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="07170-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="07170-240">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="07170-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="07170-241">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="07170-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="07170-242">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="07170-242">Testing single sign-on</span></span>

<span data-ttu-id="07170-243">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="07170-243">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="07170-244">Quando você clica no bloco StatusPage no Painel de Acesso, você deve ser conectado automaticamente ao seu aplicativo StatusPage.</span><span class="sxs-lookup"><span data-stu-id="07170-244">When you click the StatusPage tile in the Access Panel, you should get automatically signed-on to your StatusPage application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="07170-245">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="07170-245">Additional resources</span></span>

* [<span data-ttu-id="07170-246">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="07170-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="07170-247">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="07170-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_203.png

