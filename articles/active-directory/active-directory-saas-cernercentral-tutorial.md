---
title: "Tutorial: integração do Azure Active Directory ao Cerner Central | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Cerner Central."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2bc549d-d286-4679-854e-bb67c62b0475
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 77b5fb94cdfa5722081198aabc59fbf86229c2b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cerner-central"></a><span data-ttu-id="a042a-103">Tutorial: integração do Azure Active Directory ao Cerner Central</span><span class="sxs-lookup"><span data-stu-id="a042a-103">Tutorial: Azure Active Directory integration with Cerner Central</span></span>

<span data-ttu-id="a042a-104">Neste tutorial, você aprenderá a integrar o Cerner Central ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="a042a-104">In this tutorial, you learn how to integrate Cerner Central with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a042a-105">A integração do Cerner Central ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="a042a-105">Integrating Cerner Central with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a042a-106">No Azure AD, é possível controlar quem tem acesso ao Cerner Central</span><span class="sxs-lookup"><span data-stu-id="a042a-106">You can control in Azure AD who has access to Cerner Central</span></span>
- <span data-ttu-id="a042a-107">Permitir que seus usuários façam logon automaticamente no Cerner Central (logon único) com as respectivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a042a-107">You can enable your users to automatically get signed-on to Cerner Central (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a042a-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a042a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a042a-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a042a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a042a-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a042a-110">Prerequisites</span></span>

<span data-ttu-id="a042a-111">Para configurar a integração do Azure AD ao Cerner Central, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="a042a-111">To configure Azure AD integration with Cerner Central, you need the following items:</span></span>

- <span data-ttu-id="a042a-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a042a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a042a-113">Uma Conta Sistema aprovada do Cerner Central</span><span class="sxs-lookup"><span data-stu-id="a042a-113">An approved Cerner Central System Account</span></span>

> [!NOTE]
> <span data-ttu-id="a042a-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="a042a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a042a-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="a042a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a042a-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="a042a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a042a-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a042a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a042a-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="a042a-118">Scenario description</span></span>
<span data-ttu-id="a042a-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="a042a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a042a-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="a042a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a042a-121">Adicionar o Cerner Central da galeria</span><span class="sxs-lookup"><span data-stu-id="a042a-121">Adding Cerner Central from the gallery</span></span>
2. <span data-ttu-id="a042a-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a042a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cerner-central-from-the-gallery"></a><span data-ttu-id="a042a-123">Adicionar o Cerner Central da galeria</span><span class="sxs-lookup"><span data-stu-id="a042a-123">Adding Cerner Central from the gallery</span></span>
<span data-ttu-id="a042a-124">Para configurar a integração do Cerner Central ao Azure AD, você precisa adicionar o Cerner Central à sua lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="a042a-124">To configure the integration of Cerner Central into Azure AD, you need to add Cerner Central from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a042a-125">**Para adicionar o Cerner Central da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a042a-125">**To add Cerner Central from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a042a-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a042a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a042a-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="a042a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a042a-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a042a-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="a042a-131">Para adicionar o novo aplicativo, clique no botão **Novo aplicativo** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a042a-131">To add new application, click **New application** button on top of the dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="a042a-133">Na caixa de pesquisa, digite **Cerner Central**.</span><span class="sxs-lookup"><span data-stu-id="a042a-133">In the search box, type **Cerner Central**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_search.png)

5. <span data-ttu-id="a042a-135">No painel de resultados, selecione **Cerner Central** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a042a-135">In the results panel, select **Cerner Central**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a042a-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a042a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a042a-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Cerner Central, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="a042a-138">In this section, you configure and test Azure AD single sign-on with Cerner Central based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a042a-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Cerner Central é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a042a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cerner Central is to a user in Azure AD.</span></span> <span data-ttu-id="a042a-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="a042a-140">In other words, a link relationship between an Azure AD user and the related user in Cerner Central needs to be established.</span></span>

<span data-ttu-id="a042a-141">Para configurar e testar o logon único do Azure AD com o Cerner Central, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="a042a-141">To configure and test Azure AD single sign-on with Cerner Central, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a042a-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="a042a-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a042a-143">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="a042a-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a042a-144">**[Criação de um usuário de teste do Cerner Central](#creating-a-cerner-central-test-user)** – para ter um equivalente de Brenda Fernandes no Cerner Central que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a042a-144">**[Creating a Cerner Central test user](#creating-a-cerner-central-test-user)** - to have a counterpart of Britta Simon in Cerner Central that is linked to the Azure AD representation of the user.</span></span>
4. <span data-ttu-id="a042a-145">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="a042a-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a042a-146">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="a042a-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a042a-147">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a042a-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a042a-148">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único em seu aplicativo Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="a042a-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cerner Central application.</span></span>

<span data-ttu-id="a042a-149">**Para configurar o logon único do Azure AD com o Cerner Central, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a042a-149">**To configure Azure AD single sign-on with Cerner Central, perform the following steps:**</span></span>

1. <span data-ttu-id="a042a-150">No Portal do Azure, na página de integração do aplicativo **Cerner Central**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="a042a-150">In the Azure portal, on the **Cerner Central** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="a042a-152">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="a042a-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_samlbase.png)

3. <span data-ttu-id="a042a-154">Na seção **URLs e Domínio do Cerner Central**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="a042a-154">On the **Cerner Central Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_url.png)

    <span data-ttu-id="a042a-156">a.</span><span class="sxs-lookup"><span data-stu-id="a042a-156">a.</span></span> <span data-ttu-id="a042a-157">Na caixa de texto **Identificador**, digite o valor usando os seguintes padrões:</span><span class="sxs-lookup"><span data-stu-id="a042a-157">In the **Identifier** textbox, type the value using the following patterns:</span></span>
    
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcerner.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |

    <span data-ttu-id="a042a-158">b.</span><span class="sxs-lookup"><span data-stu-id="a042a-158">b.</span></span> <span data-ttu-id="a042a-159">Na caixa de texto **URL de Resposta** , digite uma URL nos seguintes padrões:</span><span class="sxs-lookup"><span data-stu-id="a042a-159">In the **Reply URL** textbox, type a URL using the following patterns:</span></span> 
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/sso` |
    | `https://cernercentral.com/<instasncename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://<subdomain>.sandboxcernercentral.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="a042a-160">Esses não são os valores reais.</span><span class="sxs-lookup"><span data-stu-id="a042a-160">These values are not the real.</span></span> <span data-ttu-id="a042a-161">Atualize esses valores com o Identificador e a URL de Resposta reais.</span><span class="sxs-lookup"><span data-stu-id="a042a-161">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="a042a-162">Entre em contato com a [equipe de suporte do Cerner Central](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="a042a-162">Contact [Cerner Central support team](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations) to get these values.</span></span>
 
4. <span data-ttu-id="a042a-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="a042a-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cernercentral-tutorial/tutorial_general_400.png)

5. <span data-ttu-id="a042a-165">Para gerar a URL de **Metadados**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="a042a-165">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="a042a-166">a.</span><span class="sxs-lookup"><span data-stu-id="a042a-166">a.</span></span> <span data-ttu-id="a042a-167">Clique em **Registros do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="a042a-167">Click **App registrations**.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appregistrations.png)
   
    <span data-ttu-id="a042a-169">b.</span><span class="sxs-lookup"><span data-stu-id="a042a-169">b.</span></span> <span data-ttu-id="a042a-170">Clique em **Pontos de extremidade** para abrir a caixa de diálogo **Pontos de extremidade**.</span><span class="sxs-lookup"><span data-stu-id="a042a-170">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![Configurar Logon Único](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpointicon.png)

    <span data-ttu-id="a042a-172">c.</span><span class="sxs-lookup"><span data-stu-id="a042a-172">c.</span></span> <span data-ttu-id="a042a-173">Clique no botão copiar para copiar a URL **DOCUMENTO DE METADADOS DE FEDERAÇÃO** e cole-a no bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="a042a-173">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpoint.png)
     
    <span data-ttu-id="a042a-175">d.</span><span class="sxs-lookup"><span data-stu-id="a042a-175">d.</span></span> <span data-ttu-id="a042a-176">Agora, vá para a página de propriedades do **Cerner Central** e copie a **ID do aplicativo** usando o botão **Copiar** e cole-a no bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="a042a-176">Now go to the property page of **Cerner Central** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appid.png)

    <span data-ttu-id="a042a-178">e.</span><span class="sxs-lookup"><span data-stu-id="a042a-178">e.</span></span> <span data-ttu-id="a042a-179">Gere a **URL de Metadados** usando o padrão a seguir: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="a042a-179">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

6. <span data-ttu-id="a042a-180">Para configurar o logon único no lado do **Cerner Central**, você precisa enviar a **URL de Metadados** para o [suporte do Cerner Central](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).</span><span class="sxs-lookup"><span data-stu-id="a042a-180">To configure single sign-on on **Cerner Central** side, you need to send the **Metadata URL** to [Cerner Central support](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).</span></span> <span data-ttu-id="a042a-181">Eles configuram o SSO no lado do aplicativo para concluir a integração.</span><span class="sxs-lookup"><span data-stu-id="a042a-181">They configure the SSO on application side to complete the integration.</span></span>

> [!TIP]
> <span data-ttu-id="a042a-182">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="a042a-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a042a-183">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="a042a-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a042a-184">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a042a-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a042a-185">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a042a-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="a042a-186">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="a042a-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span> 

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="a042a-188">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a042a-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a042a-189">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a042a-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a042a-191">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="a042a-191">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a042a-193">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a042a-193">To open the **User** dialog, click **Add**.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a042a-195">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="a042a-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a042a-197">a.</span><span class="sxs-lookup"><span data-stu-id="a042a-197">a.</span></span> <span data-ttu-id="a042a-198">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="a042a-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a042a-199">b.</span><span class="sxs-lookup"><span data-stu-id="a042a-199">b.</span></span> <span data-ttu-id="a042a-200">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="a042a-200">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="a042a-201">c.</span><span class="sxs-lookup"><span data-stu-id="a042a-201">c.</span></span> <span data-ttu-id="a042a-202">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="a042a-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a042a-203">d.</span><span class="sxs-lookup"><span data-stu-id="a042a-203">d.</span></span> <span data-ttu-id="a042a-204">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a042a-204">Click **Create**.</span></span>
 
### <a name="creating-a-cerner-central-test-user"></a><span data-ttu-id="a042a-205">Criar um usuário de teste do Cerner Central</span><span class="sxs-lookup"><span data-stu-id="a042a-205">Creating a Cerner Central test user</span></span>

<span data-ttu-id="a042a-206">O aplicativo **Cerner Central** permite a autenticação por meio de qualquer provedor de identidade federada.</span><span class="sxs-lookup"><span data-stu-id="a042a-206">**Cerner Central** application allows authentication from any federated identity provider.</span></span> <span data-ttu-id="a042a-207">Se um usuário conseguir fazer logon na home page do aplicativo, ele será federado e não precisará de nenhum provisionamento manual.</span><span class="sxs-lookup"><span data-stu-id="a042a-207">If a user is able to log in to the application home page, they are federated and have no need for any manual provisioning.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a042a-208">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a042a-208">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a042a-209">Nesta seção, ao conceder a Brenda Fernandes acesso ao Cerner Central, você permite que ela use o logon único do Azure.</span><span class="sxs-lookup"><span data-stu-id="a042a-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cerner Central.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="a042a-211">**Para atribuir Brenda Fernandes ao Cerner Central, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a042a-211">**To assign Britta Simon to Cerner Central, perform the following steps:**</span></span>

1. <span data-ttu-id="a042a-212">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a042a-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="a042a-214">Na lista de aplicativos, selecione **Cerner Central**.</span><span class="sxs-lookup"><span data-stu-id="a042a-214">In the applications list, select **Cerner Central**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_app.png) 

3. <span data-ttu-id="a042a-216">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="a042a-216">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="a042a-218">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a042a-218">Click **Add** button.</span></span> <span data-ttu-id="a042a-219">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a042a-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="a042a-221">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="a042a-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a042a-222">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a042a-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a042a-223">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a042a-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a042a-224">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="a042a-224">Testing single sign-on</span></span>

<span data-ttu-id="a042a-225">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="a042a-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a042a-226">Ao clicar no bloco do Cerner Central no Painel de Acesso, você deverá ser conectado automaticamente a seu aplicativo do Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="a042a-226">When you click the Cerner Central tile in the Access Panel, you should get automatically signed-on to your Cerner Central application.</span></span> <span data-ttu-id="a042a-227">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a042a-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a042a-228">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="a042a-228">Additional resources</span></span>

* [<span data-ttu-id="a042a-229">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="a042a-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a042a-230">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a042a-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_203.png

