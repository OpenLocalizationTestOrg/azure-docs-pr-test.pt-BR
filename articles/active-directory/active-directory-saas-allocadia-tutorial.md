---
title: "Tutorial: Integração do Azure Active Directory com o Allocadia | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Allocadia."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c415fc55-6dc1-49f2-a8a2-2fc6e3790d65
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: jeedes
ms.openlocfilehash: 8e97c365383ecdb72cc1cd449b522b75875fc1db
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-allocadia"></a><span data-ttu-id="2bd68-103">Tutorial: Integração do Azure Active Directory ao Allocadia</span><span class="sxs-lookup"><span data-stu-id="2bd68-103">Tutorial: Azure Active Directory integration with Allocadia</span></span>

<span data-ttu-id="2bd68-104">Neste tutorial, você aprenderá a integrar o Allocadia ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="2bd68-104">In this tutorial, you learn how to integrate Allocadia with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2bd68-105">A integração do Allocadia ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="2bd68-105">Integrating Allocadia with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2bd68-106">É possível controlar no Azure AD quem tem acesso ao Allocadia</span><span class="sxs-lookup"><span data-stu-id="2bd68-106">You can control in Azure AD who has access to Allocadia</span></span>
- <span data-ttu-id="2bd68-107">Você pode permitir que seus usuários façam logon automaticamente no Allocadia (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2bd68-107">You can enable your users to automatically get signed-on to Allocadia (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2bd68-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2bd68-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2bd68-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2bd68-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2bd68-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2bd68-110">Prerequisites</span></span>

<span data-ttu-id="2bd68-111">Para configurar a integração do Azure AD ao Allocadia, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="2bd68-111">To configure Azure AD integration with Allocadia, you need the following items:</span></span>

- <span data-ttu-id="2bd68-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2bd68-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2bd68-113">Uma assinatura habilitada para logon único do Allocadia</span><span class="sxs-lookup"><span data-stu-id="2bd68-113">An Allocadia single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2bd68-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="2bd68-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2bd68-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="2bd68-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2bd68-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="2bd68-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2bd68-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2bd68-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2bd68-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="2bd68-118">Scenario description</span></span>
<span data-ttu-id="2bd68-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="2bd68-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2bd68-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="2bd68-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2bd68-121">Adicionar o Allocadia da galeria</span><span class="sxs-lookup"><span data-stu-id="2bd68-121">Adding Allocadia from the gallery</span></span>
2. <span data-ttu-id="2bd68-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2bd68-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-allocadia-from-the-gallery"></a><span data-ttu-id="2bd68-123">Adicionar o Allocadia da galeria</span><span class="sxs-lookup"><span data-stu-id="2bd68-123">Adding Allocadia from the gallery</span></span>
<span data-ttu-id="2bd68-124">Para configurar a integração do Allocadia ao Azure AD, você precisará adicionar o Allocadia da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="2bd68-124">To configure the integration of Allocadia into Azure AD, you need to add Allocadia from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2bd68-125">**Para adicionar o Allocadia da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="2bd68-125">**To add Allocadia from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2bd68-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2bd68-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2bd68-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="2bd68-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2bd68-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="2bd68-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="2bd68-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2bd68-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="2bd68-133">Na caixa de pesquisa, digite **Allocadia**.</span><span class="sxs-lookup"><span data-stu-id="2bd68-133">In the search box, type **Allocadia**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_search.png)

5. <span data-ttu-id="2bd68-135">No painel de resultados, selecione **Allocadia** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2bd68-135">In the results panel, select **Allocadia**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2bd68-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2bd68-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2bd68-138">Nesta seção, você configura e testa o logon único do Azure AD com o Allocadia, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="2bd68-138">In this section, you configure and test Azure AD single sign-on with Allocadia based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2bd68-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Allocadia é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2bd68-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Allocadia is to a user in Azure AD.</span></span> <span data-ttu-id="2bd68-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Allocadia.</span><span class="sxs-lookup"><span data-stu-id="2bd68-140">In other words, a link relationship between an Azure AD user and the related user in Allocadia needs to be established.</span></span>

<span data-ttu-id="2bd68-141">No Allocadia, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="2bd68-141">In Allocadia, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2bd68-142">Para configurar e testar o logon único do Azure AD com o Allocadia, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="2bd68-142">To configure and test Azure AD single sign-on with Allocadia, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2bd68-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="2bd68-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2bd68-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="2bd68-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2bd68-145">**[Criando um usuário de teste do Allocadia](#creating-an-allocadia-test-user)** – para ter um equivalente de Brenda Fernandes no Allocadia que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2bd68-145">**[Creating an Allocadia test user](#creating-an-allocadia-test-user)** - to have a counterpart of Britta Simon in Allocadia that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2bd68-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="2bd68-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2bd68-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="2bd68-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2bd68-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2bd68-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2bd68-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Allocadia.</span><span class="sxs-lookup"><span data-stu-id="2bd68-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Allocadia application.</span></span>

<span data-ttu-id="2bd68-150">**Para configurar o logon único do Azure AD com o Allocadia, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="2bd68-150">**To configure Azure AD single sign-on with Allocadia, perform the following steps:**</span></span>

1. <span data-ttu-id="2bd68-151">No portal do Azure, na página de integração do aplicativo do **Allocadia**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="2bd68-151">In the Azure portal, on the **Allocadia** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="2bd68-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="2bd68-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_samlbase.png)

3. <span data-ttu-id="2bd68-155">Na seção **Domínio e URLs do Allocadia**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="2bd68-155">On the **Allocadia Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_url.png)

    <span data-ttu-id="2bd68-157">a.</span><span class="sxs-lookup"><span data-stu-id="2bd68-157">a.</span></span> <span data-ttu-id="2bd68-158">Na caixa de texto **Identificador**, digite uma URL usando os seguintes padrões:</span><span class="sxs-lookup"><span data-stu-id="2bd68-158">In the **Identifier** textbox, type a URL using the following patterns:</span></span> 
       
     <span data-ttu-id="2bd68-159">Para o ambiente de teste – `https://na2standby.allocadia.com`</span><span class="sxs-lookup"><span data-stu-id="2bd68-159">For test environment -  `https://na2standby.allocadia.com`</span></span>
    
     <span data-ttu-id="2bd68-160">Para o ambiente de produção – `https://na2.allocadia.com`</span><span class="sxs-lookup"><span data-stu-id="2bd68-160">For production environment - `https://na2.allocadia.com`</span></span>

    <span data-ttu-id="2bd68-161">b.</span><span class="sxs-lookup"><span data-stu-id="2bd68-161">b.</span></span> <span data-ttu-id="2bd68-162">Na caixa de texto **URL de Resposta** , digite uma URL nos seguintes padrões:</span><span class="sxs-lookup"><span data-stu-id="2bd68-162">In the **Reply URL** textbox, type a URL using the following patterns:</span></span> 
    
     <span data-ttu-id="2bd68-163">Para o ambiente de teste – `https://na2standby.allocadia.com/allocadia/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="2bd68-163">For test environment - `https://na2standby.allocadia.com/allocadia/saml/SSO`</span></span>
    
     <span data-ttu-id="2bd68-164">Para o ambiente de produção – `https://na2.allocadia.com/allocadia/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="2bd68-164">For production environment - `https://na2.allocadia.com/allocadia/saml/SSO`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2bd68-165">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="2bd68-165">These values are not real.</span></span> <span data-ttu-id="2bd68-166">Atualize esses valores com o Identificador e a URL de Resposta reais.</span><span class="sxs-lookup"><span data-stu-id="2bd68-166">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="2bd68-167">Contate a [equipe de suporte do Allocadia](mailTo:support@allocadia.com) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="2bd68-167">Contact [Allocadia support team](mailTo:support@allocadia.com) to get these values.</span></span>

4. <span data-ttu-id="2bd68-168">O aplicativo Allocadia espera que as declarações SAML estejam em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="2bd68-168">Allocadia application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="2bd68-169">Configure as declarações a seguir para este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2bd68-169">Configure the following claims for this application.</span></span> <span data-ttu-id="2bd68-170">Você pode gerenciar os valores desses atributos da seção "**Atributos de Usuário**" na página de integração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2bd68-170">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="2bd68-171">A captura de tela a seguir mostra um exemplo dessa configuração.</span><span class="sxs-lookup"><span data-stu-id="2bd68-171">The following screenshot shows an example for this configuration.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_attributes.png)
    
5. <span data-ttu-id="2bd68-173">Na seção **Atributos do Usuário**, na caixa de diálogo **Logon único**, configure o atributo do token SAML como mostra a imagem e execute as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="2bd68-173">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="2bd68-174">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="2bd68-174">Attribute Name</span></span> | <span data-ttu-id="2bd68-175">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="2bd68-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="2bd68-176">nome</span><span class="sxs-lookup"><span data-stu-id="2bd68-176">firstname</span></span> | <span data-ttu-id="2bd68-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="2bd68-177">user.givenname</span></span> |
    | <span data-ttu-id="2bd68-178">sobrenome</span><span class="sxs-lookup"><span data-stu-id="2bd68-178">lastname</span></span> | <span data-ttu-id="2bd68-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="2bd68-179">user.surname</span></span> |
    | <span data-ttu-id="2bd68-180">email</span><span class="sxs-lookup"><span data-stu-id="2bd68-180">email</span></span> | <span data-ttu-id="2bd68-181">user.mail</span><span class="sxs-lookup"><span data-stu-id="2bd68-181">user.mail</span></span> |
    
    <span data-ttu-id="2bd68-182">a.</span><span class="sxs-lookup"><span data-stu-id="2bd68-182">a.</span></span> <span data-ttu-id="2bd68-183">Clique em **Adicionar atributo** para abrir o diálogo **Adicionar Atributo**.</span><span class="sxs-lookup"><span data-stu-id="2bd68-183">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-allocadia-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="2bd68-185">b.</span><span class="sxs-lookup"><span data-stu-id="2bd68-185">b.</span></span> <span data-ttu-id="2bd68-186">Na caixa de texto **Nome** , digite o nome do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="2bd68-186">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-allocadia-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="2bd68-188">c.</span><span class="sxs-lookup"><span data-stu-id="2bd68-188">c.</span></span> <span data-ttu-id="2bd68-189">Na lista **Valor**, digite o valor do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="2bd68-189">From the **Value** list, type the attribute value shown for that row.</span></span>
 
    <span data-ttu-id="2bd68-190">d.</span><span class="sxs-lookup"><span data-stu-id="2bd68-190">d.</span></span> <span data-ttu-id="2bd68-191">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="2bd68-191">Click **Ok**.</span></span>



6. <span data-ttu-id="2bd68-192">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="2bd68-192">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_certificate.png) 


7. <span data-ttu-id="2bd68-194">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="2bd68-194">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-allocadia-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="2bd68-196">Para configurar o logon único no lado do **Allocadia**, é necessário enviar o **XML de Metadados** baixado para a [equipe de suporte do Allocadia](mailTo:support@allocadia.com).</span><span class="sxs-lookup"><span data-stu-id="2bd68-196">To configure single sign-on on **Allocadia** side, you need to send the downloaded **Metadata XML** to [Allocadia support team](mailTo:support@allocadia.com).</span></span> <span data-ttu-id="2bd68-197">Eles definem essa configuração para ter a conexão de SSO do SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="2bd68-197">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="2bd68-198">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="2bd68-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2bd68-199">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="2bd68-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2bd68-200">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2bd68-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2bd68-201">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2bd68-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="2bd68-202">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="2bd68-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="2bd68-204">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="2bd68-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2bd68-205">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2bd68-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-allocadia-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2bd68-207">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="2bd68-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-allocadia-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2bd68-209">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2bd68-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-allocadia-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2bd68-211">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="2bd68-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-allocadia-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2bd68-213">a.</span><span class="sxs-lookup"><span data-stu-id="2bd68-213">a.</span></span> <span data-ttu-id="2bd68-214">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="2bd68-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2bd68-215">b.</span><span class="sxs-lookup"><span data-stu-id="2bd68-215">b.</span></span> <span data-ttu-id="2bd68-216">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="2bd68-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2bd68-217">c.</span><span class="sxs-lookup"><span data-stu-id="2bd68-217">c.</span></span> <span data-ttu-id="2bd68-218">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="2bd68-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2bd68-219">d.</span><span class="sxs-lookup"><span data-stu-id="2bd68-219">d.</span></span> <span data-ttu-id="2bd68-220">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="2bd68-220">Click **Create**.</span></span>
 
### <a name="creating-an-allocadia-test-user"></a><span data-ttu-id="2bd68-221">Criação um usuário de teste do Allocadia</span><span class="sxs-lookup"><span data-stu-id="2bd68-221">Creating an Allocadia test user</span></span>

<span data-ttu-id="2bd68-222">O aplicativo dá suporte ao provisionamento de usuário Just-In-Time.</span><span class="sxs-lookup"><span data-stu-id="2bd68-222">Application supports Just in time user provisioning.</span></span> <span data-ttu-id="2bd68-223">Após a autenticação, os usuários são criados no aplicativo automaticamente.</span><span class="sxs-lookup"><span data-stu-id="2bd68-223">After authentication users are created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2bd68-224">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2bd68-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2bd68-225">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Allocadia.</span><span class="sxs-lookup"><span data-stu-id="2bd68-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Allocadia.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="2bd68-227">**Para atribuir Brenda Fernandes ao Allocadia, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="2bd68-227">**To assign Britta Simon to Allocadia, perform the following steps:**</span></span>

1. <span data-ttu-id="2bd68-228">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="2bd68-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="2bd68-230">Na lista de aplicativos, selecione **Allocadia**.</span><span class="sxs-lookup"><span data-stu-id="2bd68-230">In the applications list, select **Allocadia**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_app.png) 

3. <span data-ttu-id="2bd68-232">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="2bd68-232">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="2bd68-234">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="2bd68-234">Click **Add** button.</span></span> <span data-ttu-id="2bd68-235">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2bd68-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="2bd68-237">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="2bd68-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2bd68-238">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2bd68-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2bd68-239">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2bd68-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2bd68-240">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="2bd68-240">Testing single sign-on</span></span>

<span data-ttu-id="2bd68-241">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="2bd68-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2bd68-242">Ao clicar no bloco Allocadia no Painel de Acesso, você deverá ser conectado automaticamente a seu aplicativo Allocadia.</span><span class="sxs-lookup"><span data-stu-id="2bd68-242">When you click the Allocadia tile in the Access Panel, you should get automatically signed-on to your Allocadia application.</span></span>
<span data-ttu-id="2bd68-243">Para obter mais informações sobre o Painel de Acesso, consulte [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="2bd68-243">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2bd68-244">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="2bd68-244">Additional resources</span></span>

* [<span data-ttu-id="2bd68-245">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="2bd68-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2bd68-246">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2bd68-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_203.png

