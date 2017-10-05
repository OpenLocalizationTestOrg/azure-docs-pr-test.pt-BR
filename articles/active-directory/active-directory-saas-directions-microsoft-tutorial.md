---
title: "Tutorial: integração do Azure Active Directory com o Directions on Microsoft | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Directions on Microsoft."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e0c8986f-2acd-418d-a306-437abc44b640
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: f9c068c71eb00a4c779c91c8ee0f0dc9d6ba85ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-directions-on-microsoft"></a><span data-ttu-id="db195-103">Tutorial: integração do Active Directory do Azure ao Directions on Microsoft</span><span class="sxs-lookup"><span data-stu-id="db195-103">Tutorial: Azure Active Directory integration with Directions on Microsoft</span></span>

<span data-ttu-id="db195-104">Neste tutorial, você aprende a integrar o Directions on Microsoft ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="db195-104">In this tutorial, you learn how to integrate Directions on Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="db195-105">A integração do Directions on Microsoft ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="db195-105">Integrating Directions on Microsoft with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="db195-106">Você pode controlar no Azure AD quem tem acesso ao Directions on Microsoft</span><span class="sxs-lookup"><span data-stu-id="db195-106">You can control in Azure AD who has access to Directions on Microsoft</span></span>
- <span data-ttu-id="db195-107">Você pode permitir que seus usuários façam logon automaticamente no Directions on Microsoft (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="db195-107">You can enable your users to automatically get signed-on to Directions on Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="db195-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="db195-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="db195-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="db195-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="db195-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="db195-110">Prerequisites</span></span>

<span data-ttu-id="db195-111">Para configurar a integração do Azure AD ao Directions on Microsoft, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="db195-111">To configure Azure AD integration with Directions on Microsoft, you need the following items:</span></span>

- <span data-ttu-id="db195-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="db195-112">An Azure AD subscription</span></span>
- <span data-ttu-id="db195-113">Uma assinatura habilitada para logon único do Directions on Microsoft</span><span class="sxs-lookup"><span data-stu-id="db195-113">A Directions on Microsoft single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="db195-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="db195-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="db195-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="db195-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="db195-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="db195-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="db195-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="db195-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="db195-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="db195-118">Scenario description</span></span>
<span data-ttu-id="db195-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="db195-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="db195-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="db195-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="db195-121">Adicionando Directions na Microsoft da galeria</span><span class="sxs-lookup"><span data-stu-id="db195-121">Adding Directions on Microsoft from the gallery</span></span>
2. <span data-ttu-id="db195-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="db195-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-directions-on-microsoft-from-the-gallery"></a><span data-ttu-id="db195-123">Adicionando Directions na Microsoft da galeria</span><span class="sxs-lookup"><span data-stu-id="db195-123">Adding Directions on Microsoft from the gallery</span></span>
<span data-ttu-id="db195-124">Para configurar a integração do Directions on Microsoft no Azure AD, você precisa adicionar o Directions on Microsoft da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="db195-124">To configure the integration of Directions on Microsoft into Azure AD, you need to add Directions on Microsoft from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="db195-125">**Para adicionar Directions on Microsoft da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="db195-125">**To add Directions on Microsoft from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="db195-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="db195-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="db195-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="db195-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="db195-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="db195-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="db195-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="db195-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="db195-133">Na caixa de pesquisa, digite **Directions on Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="db195-133">In the search box, type **Directions on Microsoft**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_search.png)

5. <span data-ttu-id="db195-135">No painel de resultados, selecione **Directions on Microsoft** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="db195-135">In the results panel, select **Directions on Microsoft**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="db195-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="db195-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="db195-138">Nesta seção, você configurará e testará o logon único do Azure AD no Directions on Microsoft com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="db195-138">In this section, you configure and test Azure AD single sign-on with Directions on Microsoft based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="db195-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Directions on Microsoft é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="db195-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Directions on Microsoft is to a user in Azure AD.</span></span> <span data-ttu-id="db195-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Directions on Microsoft.</span><span class="sxs-lookup"><span data-stu-id="db195-140">In other words, a link relationship between an Azure AD user and the related user in Directions on Microsoft needs to be established.</span></span>

<span data-ttu-id="db195-141">No Directions on Microsoft, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="db195-141">In Directions on Microsoft, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="db195-142">Para configurar e testar o logon único do Azure AD com o Directions on Microsoft, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="db195-142">To configure and test Azure AD single sign-on with Directions on Microsoft, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="db195-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="db195-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="db195-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="db195-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="db195-145">**[Criando um usuário de teste do Directions on Microsoft](#creating-a-directions-on-microsoft-test-user)** – para ter um equivalente de Brenda Fernandes no Directions on Microsoft que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="db195-145">**[Creating a Directions on Microsoft test user](#creating-a-directions-on-microsoft-test-user)** - to have a counterpart of Britta Simon in Directions on Microsoft that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="db195-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="db195-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="db195-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="db195-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="db195-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="db195-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="db195-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Directions on Microsoft.</span><span class="sxs-lookup"><span data-stu-id="db195-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Directions on Microsoft application.</span></span>

<span data-ttu-id="db195-150">**Para configurar o logon único do Azure AD com Directions on Microsoft, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="db195-150">**To configure Azure AD single sign-on with Directions on Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="db195-151">No portal do Azure, na página de integração de aplicativo **Directions on Microsoft**, clique em **Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="db195-151">In the Azure portal, on the **Directions on Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="db195-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="db195-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_samlbase.png)

3. <span data-ttu-id="db195-155">Na seção **Domínio e URLs do Directions on Microsoft**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="db195-155">On the **Directions on Microsoft Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_url.png)

    <span data-ttu-id="db195-157">a.</span><span class="sxs-lookup"><span data-stu-id="db195-157">a.</span></span> <span data-ttu-id="db195-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="db195-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    |  |
    | --- |
    | `https://www.directionsonmicrosoft.com/user/login` |
    | `https://<subdomain>.devcloud.acquia-sites.com/<companyname>` |

    <span data-ttu-id="db195-159">b.</span><span class="sxs-lookup"><span data-stu-id="db195-159">b.</span></span> <span data-ttu-id="db195-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="db195-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    |  |
    | --- |
    | `https://rhelmdirectionsonmicrosoftcomtest.devcloud.acquia-sites.com/simplesaml/<companyname>` |
    | `https://www.directionsonmicrosoft.com/simplesaml/<companyname>` |

    > [!NOTE] 
    > <span data-ttu-id="db195-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="db195-161">These values are not real.</span></span> <span data-ttu-id="db195-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="db195-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="db195-163">Entre em contato com a [equipe de suporte ao Cliente do Directions on Microsoft](mailto:service@DirectionsOnMicrosoft.com) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="db195-163">Contact [Directions on Microsoft Client support team](mailto:service@DirectionsOnMicrosoft.com) to get these values.</span></span> 
 
4. <span data-ttu-id="db195-164">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="db195-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_certificate.png) 

5. <span data-ttu-id="db195-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="db195-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="db195-168">Para configurar o logon único no lado do **Directions on Microsoft**, você precisa enviar o **XML de Metadados** baixado para a [equipe de suporte do Directions on Microsoft](mailto:service@DirectionsOnMicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="db195-168">To configure single sign-on on **Directions on Microsoft** side, you need to send the downloaded **Metadata XML** to [Directions on Microsoft support team](mailto:service@DirectionsOnMicrosoft.com).</span></span> <span data-ttu-id="db195-169">Para permitir que a equipe de suporte do Directions on Microsoft localize sua associação federado no site, inclua informações da sua empresa em seu email.</span><span class="sxs-lookup"><span data-stu-id="db195-169">To enable the Directions on Microsoft support team to locate your federated site membership, include your company information in your email.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="db195-170">O logon único para o Directions on Microsoft precisa ser habilitado pela [equipe de suporte ao cliente do Directions on Microsoft](mailto:service@DirectionsOnMicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="db195-170">Single sign-on for Directions on Microsoft needs to be enabled by the [Directions on Microsoft Client support team](mailto:service@DirectionsOnMicrosoft.com).</span></span> <span data-ttu-id="db195-171">Você receberá uma notificação quando o logon único for habilitado.</span><span class="sxs-lookup"><span data-stu-id="db195-171">You will receive a notification when single sign-on has been enabled.</span></span>

> [!TIP]
> <span data-ttu-id="db195-172">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="db195-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="db195-173">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="db195-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="db195-174">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="db195-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="db195-175">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="db195-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="db195-176">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="db195-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="db195-178">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="db195-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="db195-179">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="db195-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="db195-181">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="db195-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="db195-183">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="db195-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="db195-185">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="db195-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="db195-187">a.</span><span class="sxs-lookup"><span data-stu-id="db195-187">a.</span></span> <span data-ttu-id="db195-188">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="db195-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="db195-189">b.</span><span class="sxs-lookup"><span data-stu-id="db195-189">b.</span></span> <span data-ttu-id="db195-190">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="db195-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="db195-191">c.</span><span class="sxs-lookup"><span data-stu-id="db195-191">c.</span></span> <span data-ttu-id="db195-192">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="db195-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="db195-193">d.</span><span class="sxs-lookup"><span data-stu-id="db195-193">d.</span></span> <span data-ttu-id="db195-194">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="db195-194">Click **Create**.</span></span>
 
### <a name="creating-a-directions-on-microsoft-test-user"></a><span data-ttu-id="db195-195">Como criar um usuário de teste do Directions on Microsoft</span><span class="sxs-lookup"><span data-stu-id="db195-195">Creating a Directions on Microsoft test user</span></span>

<span data-ttu-id="db195-196">Não há qualquer item de ação para a configuração do provisionamento de usuário para o Directions on Microsoft.</span><span class="sxs-lookup"><span data-stu-id="db195-196">There is no action item for you to configure user provisioning to Directions on Microsoft.</span></span>  

<span data-ttu-id="db195-197">Quando um usuário atribuído tenta fazer logon no Directions on Microsoft usando o painel de acesso, o Directions on Microsoft verifica se o usuário existe.</span><span class="sxs-lookup"><span data-stu-id="db195-197">When an assigned user tries to log in to Directions on Microsoft using the access panel, Directions on Microsoft checks whether the user exists.</span></span> <span data-ttu-id="db195-198">Se ainda não houver uma conta de usuário disponível, ela será automaticamente criada pelo Directions on Microsoft.</span><span class="sxs-lookup"><span data-stu-id="db195-198">If there is no user account available yet, it is automatically created by Directions on Microsoft.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="db195-199">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="db195-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="db195-200">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Directions on Microsoft.</span><span class="sxs-lookup"><span data-stu-id="db195-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Directions on Microsoft.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="db195-202">**Para atribuir Brenda Fernandes ao Directions on Microsoft, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="db195-202">**To assign Britta Simon to Directions on Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="db195-203">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="db195-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="db195-205">Na lista de aplicativos, selecione **Directions on Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="db195-205">In the applications list, select **Directions on Microsoft**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_app.png) 

3. <span data-ttu-id="db195-207">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="db195-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="db195-209">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="db195-209">Click **Add** button.</span></span> <span data-ttu-id="db195-210">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="db195-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="db195-212">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="db195-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="db195-213">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="db195-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="db195-214">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="db195-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="db195-215">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="db195-215">Testing single sign-on</span></span>

<span data-ttu-id="db195-216">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="db195-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
 
<span data-ttu-id="db195-217">Quando você clica no bloco do Directions on Microsoft no Painel de Acesso, você ser automaticamente conectado ao seu aplicativo Directions on Microsoft.</span><span class="sxs-lookup"><span data-stu-id="db195-217">When you click the Directions on Microsoft tile in the Access Panel, you should get automatically signed-on to your Directions on Microsoft application.</span></span>

<span data-ttu-id="db195-218">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="db195-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="db195-219">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="db195-219">Additional resources</span></span>

* [<span data-ttu-id="db195-220">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="db195-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="db195-221">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="db195-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_203.png

