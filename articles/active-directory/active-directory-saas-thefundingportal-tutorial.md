---
title: "Tutorial: Integração do Azure Active Directory com o The Funding Portal | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Drectory e o The Funding Portal."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4663cc8a-976a-4c6c-b3b4-1e5df9b66744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: d0bfc793bb26c551f85706eaec857962a3415e1f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-the-funding-portal"></a><span data-ttu-id="42ef6-103">Tutorial: Integração do Azure Active Directory ao The Funding Portal</span><span class="sxs-lookup"><span data-stu-id="42ef6-103">Tutorial: Azure Active Directory integration with The Funding Portal</span></span>

<span data-ttu-id="42ef6-104">Neste tutorial, você aprenderá a integrar o The Funding Portal ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="42ef6-104">In this tutorial, you learn how to integrate The Funding Portal with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="42ef6-105">A integração do The Funding Portal ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="42ef6-105">Integrating The Funding Portal with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="42ef6-106">Você pode controlar no Azure AD quem tem acesso ao The Funding Portal</span><span class="sxs-lookup"><span data-stu-id="42ef6-106">You can control in Azure AD who has access to The Funding Portal</span></span>
- <span data-ttu-id="42ef6-107">Você pode permitir que os usuários entrem automaticamente no The Funding Portal (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="42ef6-107">You can enable your users to automatically get signed-on to The Funding Portal (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="42ef6-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="42ef6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="42ef6-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="42ef6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42ef6-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="42ef6-110">Prerequisites</span></span>

<span data-ttu-id="42ef6-111">Para configurar a integração do Azure AD com o The Funding Portal, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="42ef6-111">To configure Azure AD integration with The Funding Portal, you need the following items:</span></span>

- <span data-ttu-id="42ef6-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="42ef6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="42ef6-113">Uma assinatura do The Funding Portal habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="42ef6-113">A The Funding Portal single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="42ef6-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="42ef6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="42ef6-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="42ef6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="42ef6-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="42ef6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="42ef6-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="42ef6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="42ef6-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="42ef6-118">Scenario description</span></span>
<span data-ttu-id="42ef6-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="42ef6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="42ef6-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="42ef6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="42ef6-121">Adição do The Funding Portal da galeria</span><span class="sxs-lookup"><span data-stu-id="42ef6-121">Adding The Funding Portal from the gallery</span></span>
2. <span data-ttu-id="42ef6-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="42ef6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-the-funding-portal-from-the-gallery"></a><span data-ttu-id="42ef6-123">Adição do The Funding Portal da galeria</span><span class="sxs-lookup"><span data-stu-id="42ef6-123">Adding The Funding Portal from the gallery</span></span>
<span data-ttu-id="42ef6-124">Para configurar a integração do The Funding Portal ao Azure AD, você precisa adicionar o The Funding Portal por meio da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="42ef6-124">To configure the integration of The Funding Portal into Azure AD, you need to add The Funding Portal from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="42ef6-125">**Para adicionar o The Funding Portal da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="42ef6-125">**To add The Funding Portal from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="42ef6-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="42ef6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="42ef6-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="42ef6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="42ef6-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="42ef6-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="42ef6-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="42ef6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="42ef6-133">Na caixa de pesquisa, digite **The Funding Portal**.</span><span class="sxs-lookup"><span data-stu-id="42ef6-133">In the search box, type **The Funding Portal**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_search.png)

5. <span data-ttu-id="42ef6-135">No painel de resultados, selecione **The Funding Portal** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="42ef6-135">In the results panel, select **The Funding Portal**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="42ef6-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="42ef6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="42ef6-138">Nesta seção, você configurará e testará o logon único do Azure AD com o The Funding Portal, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="42ef6-138">In this section, you configure and test Azure AD single sign-on with The Funding Portal based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="42ef6-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do The Funding Portal é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42ef6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in The Funding Portal is to a user in Azure AD.</span></span> <span data-ttu-id="42ef6-140">Em outras palavras, é necessário estabelecer uma relação de vinculação entre um usuário do Azure AD e o usuário relacionado do The Funding Portal.</span><span class="sxs-lookup"><span data-stu-id="42ef6-140">In other words, a link relationship between an Azure AD user and the related user in The Funding Portal needs to be established.</span></span>

<span data-ttu-id="42ef6-141">No The Funding Portal, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="42ef6-141">In The Funding Portal, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="42ef6-142">Para configurar e testar o logon único do Azure AD com o The Funding Portal, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="42ef6-142">To configure and test Azure AD single sign-on with The Funding Portal, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="42ef6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="42ef6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="42ef6-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="42ef6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="42ef6-145">**[Criação do usuário de teste do The Funding Portal](#creating-the-funding-portal-test-user)** – para ter um equivalente de Brenda Fernandes no The Funding Portal que esteja vinculado à representação de usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42ef6-145">**[Creating The Funding Portal test user](#creating-the-funding-portal-test-user)** - to have a counterpart of Britta Simon in The Funding Portal that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="42ef6-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="42ef6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="42ef6-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="42ef6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="42ef6-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="42ef6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="42ef6-149">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo The Funding Portal.</span><span class="sxs-lookup"><span data-stu-id="42ef6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your The Funding Portal application.</span></span>

<span data-ttu-id="42ef6-150">**Para configurar o logon único do Azure AD com o The Funding Portal, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="42ef6-150">**To configure Azure AD single sign-on with The Funding Portal, perform the following steps:**</span></span>

1. <span data-ttu-id="42ef6-151">No Portal do Azure, na página de integração de aplicativos do **The Funding Portal**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="42ef6-151">In the Azure portal, on the **The Funding Portal** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="42ef6-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="42ef6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_samlbase.png)

3. <span data-ttu-id="42ef6-155">Na seção **URLs e Domínio do The Funding Portal**, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="42ef6-155">On the **The Funding Portal Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_url.png)

    <span data-ttu-id="42ef6-157">a.</span><span class="sxs-lookup"><span data-stu-id="42ef6-157">a.</span></span> <span data-ttu-id="42ef6-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<subdomain>.regenteducation.net/`</span><span class="sxs-lookup"><span data-stu-id="42ef6-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.regenteducation.net/`</span></span>

    <span data-ttu-id="42ef6-159">b.</span><span class="sxs-lookup"><span data-stu-id="42ef6-159">b.</span></span> <span data-ttu-id="42ef6-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<subdomain>.regenteducation.net`</span><span class="sxs-lookup"><span data-stu-id="42ef6-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.regenteducation.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="42ef6-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="42ef6-161">These values are not real.</span></span> <span data-ttu-id="42ef6-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="42ef6-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="42ef6-163">Contate a [equipe de suporte ao cliente do The Funding Portal](mailto:info@regenteducation.com) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="42ef6-163">Contact [The Funding Portal Client support team](mailto:info@regenteducation.com) to get these values.</span></span> 

4. <span data-ttu-id="42ef6-164">O aplicativo The Funding Portal espera que as asserções de SAML contenham um atributo chamado "externalId1".</span><span class="sxs-lookup"><span data-stu-id="42ef6-164">The Funding Portal application expects the SAML assertions to contain an attribute named "externalId1".</span></span> <span data-ttu-id="42ef6-165">O valor de "externalId1" deve ser uma studentID reconhecida.</span><span class="sxs-lookup"><span data-stu-id="42ef6-165">The value of "externalId1" should be a recognized studentID.</span></span> <span data-ttu-id="42ef6-166">Configure a declaração "externalId1" para esse aplicativo.</span><span class="sxs-lookup"><span data-stu-id="42ef6-166">Configure the "externalId1" claim for this application.</span></span> <span data-ttu-id="42ef6-167">É possível gerenciar os valores desses atributos na em **Atributos de Usuário** do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="42ef6-167">You can manage the values of these attributes from the **User Attributes** of the application.</span></span> <span data-ttu-id="42ef6-168">A captura de tela a seguir mostra um exemplo disso.</span><span class="sxs-lookup"><span data-stu-id="42ef6-168">The following screenshot shows an example for this.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_attribute.png)

5. <span data-ttu-id="42ef6-170">Na seção **Atributos do Usuário**, na caixa de diálogo **Logon único**, configure o atributo do token SAML como mostra a imagem e execute as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="42ef6-170">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>

    | <span data-ttu-id="42ef6-171">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="42ef6-171">Attribute Name</span></span> | <span data-ttu-id="42ef6-172">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="42ef6-172">Attribute Value</span></span> |
    | ------------------- | ---------------- |
    | <span data-ttu-id="42ef6-173">externalId1</span><span class="sxs-lookup"><span data-stu-id="42ef6-173">externalId1</span></span> | <span data-ttu-id="42ef6-174">user.extensionattribute1</span><span class="sxs-lookup"><span data-stu-id="42ef6-174">user.extensionattribute1</span></span> |

    <span data-ttu-id="42ef6-175">a.</span><span class="sxs-lookup"><span data-stu-id="42ef6-175">a.</span></span> <span data-ttu-id="42ef6-176">Clique em **Adicionar atributo** para abrir o diálogo **Adicionar Atributo**.</span><span class="sxs-lookup"><span data-stu-id="42ef6-176">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-thefundingportal-tutorial/tutorial_attribute_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-thefundingportal-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="42ef6-179">b.</span><span class="sxs-lookup"><span data-stu-id="42ef6-179">b.</span></span> <span data-ttu-id="42ef6-180">Na caixa de texto **Nome** , digite o nome do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="42ef6-180">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="42ef6-181">c.</span><span class="sxs-lookup"><span data-stu-id="42ef6-181">c.</span></span> <span data-ttu-id="42ef6-182">Na lista **Valor do Atributo** , selecione o atributo que você deseja usar na sua implementação.</span><span class="sxs-lookup"><span data-stu-id="42ef6-182">From the **Attribute Value** list, select the attribute you want to use for your implementation.</span></span> <span data-ttu-id="42ef6-183">Por exemplo, se você tiver armazenado o valor de StudentID em ExtensionAttribute1, então selecione user.extensionattribute1.</span><span class="sxs-lookup"><span data-stu-id="42ef6-183">For example, if you have stored the StudentID value in the ExtensionAttribute1, then select user.extensionattribute1.</span></span>
    
    <span data-ttu-id="42ef6-184">d.</span><span class="sxs-lookup"><span data-stu-id="42ef6-184">d.</span></span> <span data-ttu-id="42ef6-185">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="42ef6-185">Click **Ok**.</span></span>
 
6. <span data-ttu-id="42ef6-186">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="42ef6-186">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_certificate.png) 

7. <span data-ttu-id="42ef6-188">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="42ef6-188">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="42ef6-190">Para configurar o logon único no lado do **The Funding Portal**, é necessário enviar o **XML de metadados** baixado para a [equipe de suporte do The Funding Portal](mailto:info@regenteducation.com).</span><span class="sxs-lookup"><span data-stu-id="42ef6-190">To configure single sign-on on **The Funding Portal** side, you need to send the downloaded **Metadata XML** to [The Funding Portal support team](mailto:info@regenteducation.com).</span></span> <span data-ttu-id="42ef6-191">Eles definem essa configuração para ter a conexão de SSO de SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="42ef6-191">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="42ef6-192">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="42ef6-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="42ef6-193">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="42ef6-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="42ef6-194">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="42ef6-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="42ef6-195">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="42ef6-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="42ef6-196">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="42ef6-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="42ef6-198">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="42ef6-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="42ef6-199">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="42ef6-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="42ef6-201">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="42ef6-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="42ef6-203">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="42ef6-203">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="42ef6-205">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="42ef6-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="42ef6-207">a.</span><span class="sxs-lookup"><span data-stu-id="42ef6-207">a.</span></span> <span data-ttu-id="42ef6-208">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="42ef6-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="42ef6-209">b.</span><span class="sxs-lookup"><span data-stu-id="42ef6-209">b.</span></span> <span data-ttu-id="42ef6-210">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="42ef6-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="42ef6-211">c.</span><span class="sxs-lookup"><span data-stu-id="42ef6-211">c.</span></span> <span data-ttu-id="42ef6-212">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="42ef6-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="42ef6-213">d.</span><span class="sxs-lookup"><span data-stu-id="42ef6-213">d.</span></span> <span data-ttu-id="42ef6-214">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="42ef6-214">Click **Create**.</span></span>
 
### <a name="creating-the-funding-portal-test-user"></a><span data-ttu-id="42ef6-215">Criação de um usuário de teste do The Funding Portal</span><span class="sxs-lookup"><span data-stu-id="42ef6-215">Creating The Funding Portal test user</span></span>

<span data-ttu-id="42ef6-216">Nesta seção, você criará uma usuária chamada Brenda Fernandes no The Funding Portal.</span><span class="sxs-lookup"><span data-stu-id="42ef6-216">In this section, you create a user called Britta Simon in The Funding Portal.</span></span> <span data-ttu-id="42ef6-217">Trabalhe com a [equipe de suporte do The Funding Portal](mailto:info@regenteducation.com) para adicionar o usuário de teste e habilitar o SSO.</span><span class="sxs-lookup"><span data-stu-id="42ef6-217">Work with [The Funding Portal support team](mailto:info@regenteducation.com) to add the test user and enable SSO.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="42ef6-218">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="42ef6-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="42ef6-219">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo acesso ao The Funding Portal.</span><span class="sxs-lookup"><span data-stu-id="42ef6-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to The Funding Portal.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="42ef6-221">**Para atribuir Brenda Fernandes ao The Funding Portal, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="42ef6-221">**To assign Britta Simon to The Funding Portal, perform the following steps:**</span></span>

1. <span data-ttu-id="42ef6-222">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="42ef6-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="42ef6-224">Na lista de aplicativos, selecione **The Funding Portal**.</span><span class="sxs-lookup"><span data-stu-id="42ef6-224">In the applications list, select **The Funding Portal**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_app.png) 

3. <span data-ttu-id="42ef6-226">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="42ef6-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="42ef6-228">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="42ef6-228">Click **Add** button.</span></span> <span data-ttu-id="42ef6-229">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="42ef6-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="42ef6-231">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="42ef6-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="42ef6-232">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="42ef6-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="42ef6-233">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="42ef6-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="42ef6-234">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="42ef6-234">Testing single sign-on</span></span>

<span data-ttu-id="42ef6-235">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="42ef6-235">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="42ef6-236">Quando você clicar no bloco do The Funding Portal no Painel de Acesso, deverá entrar automaticamente no seu aplicativo do The Funding Portal.</span><span class="sxs-lookup"><span data-stu-id="42ef6-236">When you click the The Funding Portal tile in the Access Panel, you should get automatically signed-on to your The Funding Portal application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="42ef6-237">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="42ef6-237">Additional resources</span></span>

* [<span data-ttu-id="42ef6-238">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="42ef6-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="42ef6-239">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="42ef6-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_203.png

