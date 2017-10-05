---
title: "Tutorial: integração do Azure Active Directory com o BeeLine | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o BeeLine."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0726859d-1dac-44a0-810b-da56d89039ee
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 93acbd90bbe5f0a40bf3f56edb766a0fdd30f68f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-beeline"></a><span data-ttu-id="db8b3-103">Tutorial: Integração do Azure Active Directory ao Beeline</span><span class="sxs-lookup"><span data-stu-id="db8b3-103">Tutorial: Azure Active Directory integration with BeeLine</span></span>

<span data-ttu-id="db8b3-104">Neste tutorial, você aprenderá a integrar o BeeLine ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="db8b3-104">In this tutorial, you learn how to integrate BeeLine with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="db8b3-105">A integração do BeeLine ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="db8b3-105">Integrating BeeLine with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="db8b3-106">Você pode controlar no Azure AD quem tem acesso ao BeeLine</span><span class="sxs-lookup"><span data-stu-id="db8b3-106">You can control in Azure AD who has access to BeeLine</span></span>
- <span data-ttu-id="db8b3-107">Você pode permitir que os usuários façam logon automaticamente no BeeLine (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="db8b3-107">You can enable your users to automatically get signed-on to BeeLine (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="db8b3-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="db8b3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="db8b3-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="db8b3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="db8b3-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="db8b3-110">Prerequisites</span></span>

<span data-ttu-id="db8b3-111">Para configurar a integração do Azure AD com o BeeLine, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="db8b3-111">To configure Azure AD integration with BeeLine, you need the following items:</span></span>

- <span data-ttu-id="db8b3-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="db8b3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="db8b3-113">Uma assinatura habilitada para logon único do BeeLine</span><span class="sxs-lookup"><span data-stu-id="db8b3-113">A BeeLine single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="db8b3-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="db8b3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="db8b3-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="db8b3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="db8b3-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="db8b3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="db8b3-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="db8b3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="db8b3-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="db8b3-118">Scenario description</span></span>
<span data-ttu-id="db8b3-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="db8b3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="db8b3-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="db8b3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="db8b3-121">Como adicionar o BeeLine por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="db8b3-121">Adding BeeLine from the gallery</span></span>
2. <span data-ttu-id="db8b3-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="db8b3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-beeline-from-the-gallery"></a><span data-ttu-id="db8b3-123">Como adicionar o BeeLine por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="db8b3-123">Adding BeeLine from the gallery</span></span>
<span data-ttu-id="db8b3-124">Para configurar a integração do BeeLine ao Azure AD, você precisará adicionar o BeeLine à sua lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="db8b3-124">To configure the integration of BeeLine into Azure AD, you need to add BeeLine from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="db8b3-125">**Para adicionar o BeeLine por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="db8b3-125">**To add BeeLine from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="db8b3-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="db8b3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="db8b3-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="db8b3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="db8b3-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="db8b3-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="db8b3-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="db8b3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="db8b3-133">Na caixa de pesquisa, digite **BeeLine**.</span><span class="sxs-lookup"><span data-stu-id="db8b3-133">In the search box, type **BeeLine**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_search.png)

5. <span data-ttu-id="db8b3-135">No painel de resultados, selecione **BeeLine** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="db8b3-135">In the results panel, select **BeeLine**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="db8b3-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="db8b3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="db8b3-138">Nesta seção, você configurará e testará o logon único do Azure AD com o BeeLine, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="db8b3-138">In this section, you configure and test Azure AD single sign-on with BeeLine based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="db8b3-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do BeeLine é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="db8b3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BeeLine is to a user in Azure AD.</span></span> <span data-ttu-id="db8b3-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do BeeLine.</span><span class="sxs-lookup"><span data-stu-id="db8b3-140">In other words, a link relationship between an Azure AD user and the related user in BeeLine needs to be established.</span></span>

<span data-ttu-id="db8b3-141">No BeeLine, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="db8b3-141">In BeeLine, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="db8b3-142">Para configurar e testar o logon único do Azure AD com o BeeLine, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="db8b3-142">To configure and test Azure AD single sign-on with BeeLine, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="db8b3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="db8b3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="db8b3-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="db8b3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="db8b3-145">**[Criação de um usuário de teste do BeeLine](#creating-a-beeline-test-user)**: para ter um equivalente de Brenda Fernandes no BeeLine que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="db8b3-145">**[Creating a BeeLine test user](#creating-a-beeline-test-user)** - to have a counterpart of Britta Simon in BeeLine that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="db8b3-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="db8b3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="db8b3-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="db8b3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="db8b3-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="db8b3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="db8b3-149">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único em seu aplicativo BeeLine.</span><span class="sxs-lookup"><span data-stu-id="db8b3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BeeLine application.</span></span>

<span data-ttu-id="db8b3-150">**Para configurar o logon único do Azure AD com o BeeLine, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="db8b3-150">**To configure Azure AD single sign-on with BeeLine, perform the following steps:**</span></span>

1. <span data-ttu-id="db8b3-151">No Portal do Azure, na página de integração de aplicativos do **BeeLine**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="db8b3-151">In the Azure portal, on the **BeeLine** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="db8b3-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="db8b3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_samlbase.png)

3. <span data-ttu-id="db8b3-155">Na seção **URLs e Domínio do BeeLine**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="db8b3-155">On the **BeeLine Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_url.png)

    <span data-ttu-id="db8b3-157">a.</span><span class="sxs-lookup"><span data-stu-id="db8b3-157">a.</span></span> <span data-ttu-id="db8b3-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://projects.beeline.net/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="db8b3-158">In the **Identifier** textbox, type a URL using the following pattern: `https://projects.beeline.net/<instancename>`</span></span>

    <span data-ttu-id="db8b3-159">b.</span><span class="sxs-lookup"><span data-stu-id="db8b3-159">b.</span></span> <span data-ttu-id="db8b3-160">Na caixa de texto **URL de resposta** , digite uma URL no seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="db8b3-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://projects.beeline.net/<instancename>/SSO_External.ashx`|
    | `https://projects.beeline.net/<companyname>/SSO_External.ashx` |

    > [!NOTE] 
    > <span data-ttu-id="db8b3-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="db8b3-161">These values are not real.</span></span> <span data-ttu-id="db8b3-162">Atualize esses valores com o Identificador e a URL de Resposta reais.</span><span class="sxs-lookup"><span data-stu-id="db8b3-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="db8b3-163">Entre em contato com a [equipe de suporte do BeeLine](https://www.beeline.com/contact-us/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="db8b3-163">Contact [BeeLine support team](https://www.beeline.com/contact-us/) to get these values.</span></span>
 
4. <span data-ttu-id="db8b3-164">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="db8b3-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_certificate.png) 

5. <span data-ttu-id="db8b3-166">O aplicativo Beeline espera que as declarações SAML estejam em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="db8b3-166">Your Beeline application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="db8b3-167">Trabalhe com a [equipe de suporte do BeeLine](https://www.beeline.com/contact-us/) primeiro para verificar o identificador de usuário correto que será mapeado no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="db8b3-167">Please work with [BeeLine support team](https://www.beeline.com/contact-us/) first to identify the correct user identifier which will be mapped into the application.</span></span> <span data-ttu-id="db8b3-168">Também siga as diretrizes da [equipe de suporte do BeeLine](https://www.beeline.com/contact-us/) sobre o atributo que deseja usar para mapeamento.</span><span class="sxs-lookup"><span data-stu-id="db8b3-168">Also please take the guidance from [BeeLine support team](https://www.beeline.com/contact-us/) about the attribute which they want to use for this mapping.</span></span> <span data-ttu-id="db8b3-169">Você pode gerenciar o valor desse atributo na guia **Atributos do Usuário** do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="db8b3-169">You can manage the value of this attribute from the **User Attributes** tab of the application.</span></span> <span data-ttu-id="db8b3-170">A captura de tela a seguir mostra um exemplo disso.</span><span class="sxs-lookup"><span data-stu-id="db8b3-170">The following screenshot shows an example for this.</span></span> <span data-ttu-id="db8b3-171">Aqui mapeamos a declaração do **Identificador de Usuário** com o atributo **userprincipalname**, que fornece uma ID de usuário único, que será enviada para o aplicativo BeeLine em cada resposta SAML com êxito.</span><span class="sxs-lookup"><span data-stu-id="db8b3-171">Here we have mapped the **User Identifier** claim with the **userprincipalname** attribute, which provides unique user ID, which will be sent to the Beeline application in the every successful SAML Response.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-beeline-tutorial/tutorial_attribute.png)  

6. <span data-ttu-id="db8b3-173">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="db8b3-173">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-beeline-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="db8b3-175">Na seção **Configuração do BeeLine**, clique em **Configurar BeeLine** para abrir a janela **Configuração de logon**.</span><span class="sxs-lookup"><span data-stu-id="db8b3-175">On the **BeeLine Configuration** section, click **Configure BeeLine** to open **Configure sign-on** window.</span></span> <span data-ttu-id="db8b3-176">Copie a **URL de Logoff** e a **ID da Entidade do SAML** da **seção Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="db8b3-176">Copy the **Sign-Out URL** and **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_configure.png) 

8. <span data-ttu-id="db8b3-178">Para configurar logon único no lado do **BeeLine**, é necessário enviar o **XML de Metadados**, a **ID da Entidade SAML** e a **URL de Saída** baixados para a [equipe de suporte do BeeLine](https://www.beeline.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="db8b3-178">To configure single sign-on on **BeeLine** side, you need to send the downloaded **Metadata XML** and **SAML Entity ID**, **Sign-Out URL** to [BeeLine support team](https://www.beeline.com/contact-us/).</span></span>

> [!TIP]
> <span data-ttu-id="db8b3-179">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="db8b3-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="db8b3-180">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="db8b3-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="db8b3-181">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="db8b3-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="db8b3-182">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="db8b3-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="db8b3-183">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="db8b3-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="db8b3-185">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="db8b3-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="db8b3-186">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="db8b3-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-beeline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="db8b3-188">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="db8b3-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-beeline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="db8b3-190">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="db8b3-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-beeline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="db8b3-192">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="db8b3-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-beeline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="db8b3-194">a.</span><span class="sxs-lookup"><span data-stu-id="db8b3-194">a.</span></span> <span data-ttu-id="db8b3-195">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="db8b3-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="db8b3-196">b.</span><span class="sxs-lookup"><span data-stu-id="db8b3-196">b.</span></span> <span data-ttu-id="db8b3-197">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="db8b3-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="db8b3-198">c.</span><span class="sxs-lookup"><span data-stu-id="db8b3-198">c.</span></span> <span data-ttu-id="db8b3-199">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="db8b3-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="db8b3-200">d.</span><span class="sxs-lookup"><span data-stu-id="db8b3-200">d.</span></span> <span data-ttu-id="db8b3-201">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="db8b3-201">Click **Create**.</span></span>
 
### <a name="creating-a-beeline-test-user"></a><span data-ttu-id="db8b3-202">Criação de um usuário de teste do BeeLine</span><span class="sxs-lookup"><span data-stu-id="db8b3-202">Creating a BeeLine test user</span></span>

<span data-ttu-id="db8b3-203">Nesta seção, você criará um usuário chamado Brenda Fernandes no Beeline.</span><span class="sxs-lookup"><span data-stu-id="db8b3-203">In this section, you create a user called Britta Simon in Beeline.</span></span> <span data-ttu-id="db8b3-204">O aplicativo BeeLine precisa que todos os usuários sejam provisionados no aplicativo antes de fazer o Logon Único.</span><span class="sxs-lookup"><span data-stu-id="db8b3-204">Beeline application needs all the users to be provisioned in the application before doing Single Sign On.</span></span> <span data-ttu-id="db8b3-205">Então trabalhe com a [equipe de suporte do BeeLine](https://www.beeline.com/contact-us/) para provisionar todos esses usuários no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="db8b3-205">So work with the [BeeLine support team](https://www.beeline.com/contact-us/) to provision all these users into the application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="db8b3-206">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="db8b3-206">Assigning the Azure AD test user</span></span>

<span data-ttu-id="db8b3-207">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure ao conceder acesso ao BeeLine.</span><span class="sxs-lookup"><span data-stu-id="db8b3-207">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BeeLine.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="db8b3-209">**Para atribuir Brenda Fernandes ao BeeLine, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="db8b3-209">**To assign Britta Simon to BeeLine, perform the following steps:**</span></span>

1. <span data-ttu-id="db8b3-210">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="db8b3-210">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="db8b3-212">Na lista de aplicativos, escolha **BeeLine**.</span><span class="sxs-lookup"><span data-stu-id="db8b3-212">In the applications list, select **BeeLine**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_app.png) 

3. <span data-ttu-id="db8b3-214">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="db8b3-214">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="db8b3-216">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="db8b3-216">Click **Add** button.</span></span> <span data-ttu-id="db8b3-217">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="db8b3-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="db8b3-219">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="db8b3-219">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="db8b3-220">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="db8b3-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="db8b3-221">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="db8b3-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="db8b3-222">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="db8b3-222">Testing single sign-on</span></span>

<span data-ttu-id="db8b3-223">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="db8b3-223">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span> <span data-ttu-id="db8b3-224">Ao clicar no bloco Beeline no Painel de Acesso, você deverá ser conectado automaticamente a seu aplicativo Beeline.</span><span class="sxs-lookup"><span data-stu-id="db8b3-224">When you click the Beeline tile in the Access Panel, you should get automatically signed-on to your Beeline application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="db8b3-225">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="db8b3-225">Additional resources</span></span>

* [<span data-ttu-id="db8b3-226">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="db8b3-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="db8b3-227">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="db8b3-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_203.png

