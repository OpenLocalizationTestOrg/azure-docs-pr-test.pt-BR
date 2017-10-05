---
title: "Tutorial: integração do Azure Active Directory com o LinkedIn Learning | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o LinkedIn Learning."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d5857070-bf79-4bd3-9a2a-4c1919a74946
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: jeedes
ms.openlocfilehash: 6ad28cb3adaa63ddc3d3769a650d26ca6a7e2695
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-learning"></a><span data-ttu-id="a7718-103">Tutorial: integração do Azure Active Directory com o LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="a7718-103">Tutorial: Azure Active Directory integration with LinkedIn Learning</span></span>

<span data-ttu-id="a7718-104">Neste tutorial, você aprenderá a integrar o LinkedIn Learning ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="a7718-104">In this tutorial, you learn how to integrate LinkedIn Learning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a7718-105">A integração do LinkedIn Learning com o Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="a7718-105">Integrating LinkedIn Learning with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a7718-106">É possível controlar, no Azure AD, quem tem acesso ao LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="a7718-106">You can control in Azure AD who has access to LinkedIn Learning</span></span>
- <span data-ttu-id="a7718-107">É possível permitir que seus usuários façam logon automaticamente no LinkedIn Learning (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7718-107">You can enable your users to automatically get signed-on to LinkedIn Learning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a7718-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a7718-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a7718-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a7718-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7718-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a7718-110">Prerequisites</span></span>

<span data-ttu-id="a7718-111">Para configurar a integração do Azure AD com o LinkedIn Learning, serão necessários os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="a7718-111">To configure Azure AD integration with LinkedIn Learning, you need the following items:</span></span>

- <span data-ttu-id="a7718-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a7718-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a7718-113">Uma assinatura do LinkedIn Learning habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="a7718-113">A LinkedIn Learning single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a7718-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="a7718-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a7718-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="a7718-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a7718-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="a7718-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a7718-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a7718-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a7718-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="a7718-118">Scenario description</span></span>
<span data-ttu-id="a7718-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="a7718-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a7718-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="a7718-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a7718-121">Adicionando o LinkedIn Learning da galeria</span><span class="sxs-lookup"><span data-stu-id="a7718-121">Adding LinkedIn Learning from the gallery</span></span>
2. <span data-ttu-id="a7718-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a7718-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-learning-from-the-gallery"></a><span data-ttu-id="a7718-123">Adicionando o LinkedIn Learning da galeria</span><span class="sxs-lookup"><span data-stu-id="a7718-123">Adding LinkedIn Learning from the gallery</span></span>
<span data-ttu-id="a7718-124">Para configurar a integração do LinkedIn Learning com o Azure AD, é necessário adicionar o LinkedIn Learning da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="a7718-124">To configure the integration of LinkedIn Learning into Azure AD, you need to add LinkedIn Learning from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a7718-125">**Para adicionar o LinkedIn Learning da galeria, siga as etapas abaixo:**</span><span class="sxs-lookup"><span data-stu-id="a7718-125">**To add LinkedIn Learning from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a7718-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a7718-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a7718-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="a7718-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a7718-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a7718-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="a7718-131">Clique em **adicionar** botão na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a7718-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="a7718-133">Na caixa de pesquisa, digite **LinkedIn Learning**.</span><span class="sxs-lookup"><span data-stu-id="a7718-133">In the search box, type **LinkedIn Learning**.</span></span> <span data-ttu-id="a7718-134">No painel de resultados, clique em **LinkedIn Learning** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a7718-134">From results panel, click **LinkedIn Learning** to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a7718-136">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a7718-136">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a7718-137">Nesta seção, você configurará e testará o logon único do Azure AD com o LinkedIn Learning, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="a7718-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Learning based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a7718-138">Para que o logon único funcione, o Azure AD precisa saber qual usuário do LinkedIn Learning é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7718-138">For single sign-on to work, Azure AD needs to know what the counterpart user in LinkedIn Learning is to a user in Azure AD.</span></span> <span data-ttu-id="a7718-139">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="a7718-139">In other words, a link relationship between an Azure AD user and the related user in LinkedIn Learning needs to be established.</span></span>

<span data-ttu-id="a7718-140">Essa relação de vínculo é estabelecida atribuindo o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** no LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="a7718-140">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LinkedIn Learning.</span></span>

<span data-ttu-id="a7718-141">Para configurar e testar o logon único do Azure AD com o LinkedIn Learning, é necessário concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="a7718-141">To configure and test Azure AD single sign-on with LinkedIn Learning, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a7718-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="a7718-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a7718-143">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="a7718-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a7718-144">**[Criando um usuário de teste do LinkedIn Learning](#creating-a-linkedin-learning-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="a7718-144">**[Creating a LinkedIn Learning test user](#creating-a-linkedin-learning-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="a7718-145">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="a7718-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a7718-146">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="a7718-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a7718-147">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7718-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a7718-148">Nesta seção, você vai habilitar o logon único do Azure AD no portal do Azure e configurar o logon único em seu aplicativo LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="a7718-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LinkedIn Learning application.</span></span>

<span data-ttu-id="a7718-149">**Para configurar o logon único do Azure AD com o LinkedIn Learning, siga as etapas abaixo:**</span><span class="sxs-lookup"><span data-stu-id="a7718-149">**To configure Azure AD single sign-on with LinkedIn Learning, perform the following steps:**</span></span>

1. <span data-ttu-id="a7718-150">No Portal do Azure, na página de integração de aplicativos do **LinkedIn Learning**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="a7718-150">In the Azure portal, on the **LinkedIn Learning** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="a7718-152">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="a7718-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedin_01.png)

3. <span data-ttu-id="a7718-154">Em uma janela diferente do navegador da Web, faça logon em seu locatário do LinkedIn Learning como administrador.</span><span class="sxs-lookup"><span data-stu-id="a7718-154">In a different web browser window, sign-on to your LinkedIn Learning tenant as an administrator.</span></span>

4. <span data-ttu-id="a7718-155">Em **Centro de Contas**, clique em **Configurações Globais** em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="a7718-155">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="a7718-156">Além disso, selecione **Learning – Padrão** na lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="a7718-156">Also, select **Learning - Default** from the dropdown list.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="a7718-158">Clique em **OU clique aqui para carregar e copiar campos individuais do formulário** e copie a **ID da Entidade** e a **URL do ACS (Serviço do Consumidor de Declaração)**</span><span class="sxs-lookup"><span data-stu-id="a7718-158">Click **OR Click Here to load and copy individual fields from the form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_03.png)

6. <span data-ttu-id="a7718-160">No portal do Azure, em **URLs e Domínio do LinkedIn Learning**, siga as etapas abaixo para configurar o SSO no modo **iniciado pelo IdP**</span><span class="sxs-lookup"><span data-stu-id="a7718-160">On Azure portal, under **LinkedIn Learning Domain and URLs**, perform the following steps if you want to configure SSO in **IdP Initiated** mode</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_01.png)

    <span data-ttu-id="a7718-162">a.</span><span class="sxs-lookup"><span data-stu-id="a7718-162">a.</span></span> <span data-ttu-id="a7718-163">Na caixa de texto **Identificador**, insira a **ID da Entidade** copiada do Portal do LinkedIn</span><span class="sxs-lookup"><span data-stu-id="a7718-163">In the **Identifier** textbox, enter the **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="a7718-164">b.</span><span class="sxs-lookup"><span data-stu-id="a7718-164">b.</span></span> <span data-ttu-id="a7718-165">Na caixa de texto **URL de resposta**, insira a **URL ACS (acesso do consumidor de declaração)** copiada do Portal do LinkedIn</span><span class="sxs-lookup"><span data-stu-id="a7718-165">In the **Reply URL** textbox, enter the **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="a7718-166">Se você desejar configurar o SSO em **Iniciado pelo SP**, clique na opção Mostrar Configurações Avançadas de URL na seção de configuração e configure o logon na URL com o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="a7718-166">If you want to configure SSO in **SP Initiated**, then click Show Advanced URL setting option in the configuration section and configure the sign-on URL with the following pattern:</span></span>

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=learning&applicationInstanceId=<InstanceId>`

    ![Configurar Logon Único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_02.png)   
    
8. <span data-ttu-id="a7718-168">Seu aplicativo LinkedIn Learning espera as asserções SAML em um formato específico, o que exige que você adicione mapeamentos de atributos personalizados à sua configuração de atributos de token SAML.</span><span class="sxs-lookup"><span data-stu-id="a7718-168">Your LinkedIn Learning application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="a7718-169">A captura de tela a seguir mostra um exemplo disso.</span><span class="sxs-lookup"><span data-stu-id="a7718-169">The following screenshot shows an example for this.</span></span> <span data-ttu-id="a7718-170">O valor padrão do **identificador de usuário** é **user.userprincipalname**, mas o LinkedIn Learning espera que isso seja mapeado com o endereço de email do usuário.</span><span class="sxs-lookup"><span data-stu-id="a7718-170">The default value of **User Identifier** is **user.userprincipalname** but LinkedIn Learning expects this to be mapped with the user's email address.</span></span> <span data-ttu-id="a7718-171">Para que você possa usar o atributo **user. mail** na lista ou usar o valor do atributo apropriado com base na configuração da sua organização.</span><span class="sxs-lookup"><span data-stu-id="a7718-171">For that you can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-linkedinlearning-tutorial/updateusermail.png)
    
9. <span data-ttu-id="a7718-173">Na seção **Atributos de Usuário**, clique em **Exibir e editar todos os outros atributos de usuário** e defina os atributos.</span><span class="sxs-lookup"><span data-stu-id="a7718-173">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span> <span data-ttu-id="a7718-174">O usuário precisa adicionar quatro declarações denominadas **email**, **departamento**, **nome** e **sobrenome** e o valor deve ser mapeado com **user.mail**, **user.department**, **user.givenname** e **user.surname** respectivamente</span><span class="sxs-lookup"><span data-stu-id="a7718-174">The user needs to add four claims named **email**, **department**, **firstname**, and **lastname** and the value is to be mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="a7718-175">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="a7718-175">Attribute Name</span></span> | <span data-ttu-id="a7718-176">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="a7718-176">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="a7718-177">email</span><span class="sxs-lookup"><span data-stu-id="a7718-177">email</span></span>| <span data-ttu-id="a7718-178">user.mail</span><span class="sxs-lookup"><span data-stu-id="a7718-178">user.mail</span></span> |    
    | <span data-ttu-id="a7718-179">department</span><span class="sxs-lookup"><span data-stu-id="a7718-179">department</span></span>| <span data-ttu-id="a7718-180">user.department</span><span class="sxs-lookup"><span data-stu-id="a7718-180">user.department</span></span> |
    | <span data-ttu-id="a7718-181">nome</span><span class="sxs-lookup"><span data-stu-id="a7718-181">firstname</span></span>| <span data-ttu-id="a7718-182">user.givenname</span><span class="sxs-lookup"><span data-stu-id="a7718-182">user.givenname</span></span> |
    | <span data-ttu-id="a7718-183">sobrenome</span><span class="sxs-lookup"><span data-stu-id="a7718-183">lastname</span></span>| <span data-ttu-id="a7718-184">user.surname</span><span class="sxs-lookup"><span data-stu-id="a7718-184">user.surname</span></span> |
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinlearning-tutorial/userattribute.png)
    
    <span data-ttu-id="a7718-186">a.</span><span class="sxs-lookup"><span data-stu-id="a7718-186">a.</span></span> <span data-ttu-id="a7718-187">Clique em **Adicionar Atributo** para abrir a caixa de diálogo do atributo.</span><span class="sxs-lookup"><span data-stu-id="a7718-187">Click **Add Attribute** to open the attribute dialog.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_04.png)

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="a7718-190">b.</span><span class="sxs-lookup"><span data-stu-id="a7718-190">b.</span></span> <span data-ttu-id="a7718-191">Na caixa de texto **Nome** , digite o nome do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="a7718-191">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="a7718-192">c.</span><span class="sxs-lookup"><span data-stu-id="a7718-192">c.</span></span> <span data-ttu-id="a7718-193">Na lista **Valor**, digite o valor do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="a7718-193">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="a7718-194">d.</span><span class="sxs-lookup"><span data-stu-id="a7718-194">d.</span></span> <span data-ttu-id="a7718-195">Clique em **Ok**</span><span class="sxs-lookup"><span data-stu-id="a7718-195">Click **Ok**</span></span>

10. <span data-ttu-id="a7718-196">Realize as seguintes etapas no atributo **name**-</span><span class="sxs-lookup"><span data-stu-id="a7718-196">Perform the following steps on the **name** attribute-</span></span>

    <span data-ttu-id="a7718-197">a.</span><span class="sxs-lookup"><span data-stu-id="a7718-197">a.</span></span> <span data-ttu-id="a7718-198">Clique no atributo para abrir a janela **Editar Atributo**.</span><span class="sxs-lookup"><span data-stu-id="a7718-198">Click on the attribute to open the **Edit Attribute** window.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinLearning-tutorial/url_update.png)

    <span data-ttu-id="a7718-200">b.</span><span class="sxs-lookup"><span data-stu-id="a7718-200">b.</span></span> <span data-ttu-id="a7718-201">Exclua o valor da URL do **namespace**.</span><span class="sxs-lookup"><span data-stu-id="a7718-201">Delete the URL value from the **namespace**.</span></span>
    
    <span data-ttu-id="a7718-202">c.</span><span class="sxs-lookup"><span data-stu-id="a7718-202">c.</span></span> <span data-ttu-id="a7718-203">Clique em **OK** para salvar a configuração.</span><span class="sxs-lookup"><span data-stu-id="a7718-203">Click **Ok** to save the setting.</span></span>

11. <span data-ttu-id="a7718-204">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo XML em seu computador.</span><span class="sxs-lookup"><span data-stu-id="a7718-204">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_certificate.png) 

12. <span data-ttu-id="a7718-206">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="a7718-206">Click **Save**.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_400.png)

13. <span data-ttu-id="a7718-208">Vá para a seção **Configurações de administração do LinkedIn**.</span><span class="sxs-lookup"><span data-stu-id="a7718-208">Go to **LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="a7718-209">Carregue o arquivo XML que você baixou do portal do Azure clicando na opção Carregar Arquivo XML.</span><span class="sxs-lookup"><span data-stu-id="a7718-209">Upload the XML file you downloaded from the Azure portal by clicking the Upload XML file option.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_metadata_03.png)

14. <span data-ttu-id="a7718-211">Clique em **Ativar** para habilitar o SSO.</span><span class="sxs-lookup"><span data-stu-id="a7718-211">Click **On** to enable SSO.</span></span> <span data-ttu-id="a7718-212">O status do SSO é alterado de **Não Conectado** para **Conectado**</span><span class="sxs-lookup"><span data-stu-id="a7718-212">SSO status changes from **Not Connected** to **Connected**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a7718-214">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a7718-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="a7718-215">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="a7718-215">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="a7718-217">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a7718-217">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a7718-218">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a7718-218">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a7718-220">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="a7718-220">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a7718-222">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a7718-222">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a7718-224">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="a7718-224">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a7718-226">a.</span><span class="sxs-lookup"><span data-stu-id="a7718-226">a.</span></span> <span data-ttu-id="a7718-227">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="a7718-227">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a7718-228">b.</span><span class="sxs-lookup"><span data-stu-id="a7718-228">b.</span></span> <span data-ttu-id="a7718-229">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="a7718-229">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a7718-230">c.</span><span class="sxs-lookup"><span data-stu-id="a7718-230">c.</span></span> <span data-ttu-id="a7718-231">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="a7718-231">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a7718-232">d.</span><span class="sxs-lookup"><span data-stu-id="a7718-232">d.</span></span> <span data-ttu-id="a7718-233">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a7718-233">Click **Create**.</span></span> 

### <a name="creating-a-linkedin-learning-test-user"></a><span data-ttu-id="a7718-234">Criando um usuário de teste do LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="a7718-234">Creating a LinkedIn Learning test user</span></span>

<span data-ttu-id="a7718-235">Com suporte do aplicativo Linked Learning.</span><span class="sxs-lookup"><span data-stu-id="a7718-235">Linked Learning Application supports.</span></span> <span data-ttu-id="a7718-236">Provisionamento de usuário Just-In-Time e, após a autenticação, os usuários são criados no aplicativo automaticamente.</span><span class="sxs-lookup"><span data-stu-id="a7718-236">Just in time user provisioning and after authentication users are created in the application automatically.</span></span> <span data-ttu-id="a7718-237">Na página de configurações de administração no portal do LinkedIn Learning, coloque a opção **Atribuir licenças automaticamente** como ativa para habilitar o provisionamento just-in-time e isso também atribuirá uma licença ao usuário.</span><span class="sxs-lookup"><span data-stu-id="a7718-237">On the admin settings page on the LinkedIn Learning portal flip the switch **Automatically Assign licenses** to active to enable Just in time provisioning and this will also assign a license to the user.</span></span>
   
   ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinLearning-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a7718-239">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a7718-239">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a7718-240">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure ao conceder acesso ao LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="a7718-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LinkedIn Learning.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="a7718-242">**Para atribuir Brenda Fernandes ao LinkedIn Learning, siga as etapas abaixo:**</span><span class="sxs-lookup"><span data-stu-id="a7718-242">**To assign Britta Simon to LinkedIn Learning, perform the following steps:**</span></span>

1. <span data-ttu-id="a7718-243">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a7718-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="a7718-245">Na lista de aplicativos, selecione **LinkedIn Learning**.</span><span class="sxs-lookup"><span data-stu-id="a7718-245">In the applications list, select **LinkedIn Learning**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_0001.png) 

3. <span data-ttu-id="a7718-247">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="a7718-247">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="a7718-249">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a7718-249">Click **Add** button.</span></span> <span data-ttu-id="a7718-250">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a7718-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="a7718-252">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="a7718-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a7718-253">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a7718-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a7718-254">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a7718-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a7718-255">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="a7718-255">Testing single sign-on</span></span>

<span data-ttu-id="a7718-256">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="a7718-256">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a7718-257">Quando você clica no bloco LinkedIn Learning no Painel de Acesso, você deve obter a página de logon do Azure e, após o logon bem-sucedido, você deve entrar em seu aplicativo LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="a7718-257">When you click the LinkedIn Learning tile in the Access Panel, you should get the Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Learning application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a7718-258">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="a7718-258">Additional resources</span></span>

* [<span data-ttu-id="a7718-259">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="a7718-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a7718-260">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a7718-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_203.png