---
title: "Tutorial: integração do Azure Active Directory ao LinkedInSalesNavigator | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o LinkedInSalesNavigator."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7a9fa8f3-d611-4ffe-8d50-04e9586b24da
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: ef26a16e79d9c9b0654634960b57dc59827b2c24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-sales-navigator"></a><span data-ttu-id="a0637-103">Tutorial: integração do Azure Active Directory com o LinkedIn Sales Navigator</span><span class="sxs-lookup"><span data-stu-id="a0637-103">Tutorial: Azure Active Directory integration with LinkedIn Sales Navigator</span></span>

<span data-ttu-id="a0637-104">Neste tutorial, você aprenderá a integrar o LinkedIn Sales Navigator ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="a0637-104">In this tutorial, you learn how to integrate LinkedIn Sales Navigator with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a0637-105">A integração do LinkedIn Sales Navigator com o Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="a0637-105">Integrating LinkedIn Sales Navigator with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a0637-106">É possível controlar, no Azure AD, quem tem acesso ao LinkedIn Sales Navigator</span><span class="sxs-lookup"><span data-stu-id="a0637-106">You can control in Azure AD who has access to LinkedIn Sales Navigator</span></span>
- <span data-ttu-id="a0637-107">É possível permitir que seus usuários façam logon automaticamente no LinkedIn Sales Navigator (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0637-107">You can enable your users to automatically get signed-on to LinkedIn Sales Navigator (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a0637-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a0637-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a0637-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, procure [O que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a0637-109">If you want to know more details about SaaS app integration with Azure AD, browse [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a0637-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a0637-110">Prerequisites</span></span>

<span data-ttu-id="a0637-111">Para configurar a integração do Azure AD com o LinkedIn Sales Navigator, serão necessários os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="a0637-111">To configure Azure AD integration with LinkedIn Sales Navigator, you need the following items:</span></span>

- <span data-ttu-id="a0637-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a0637-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a0637-113">Uma assinatura do LinkedIn Sales Navigator com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="a0637-113">A LinkedIn Sales Navigator single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a0637-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="a0637-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a0637-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="a0637-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a0637-116">Evite usar o ambiente de produção a menos que necessário.</span><span class="sxs-lookup"><span data-stu-id="a0637-116">Avoid using your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a0637-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a0637-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a0637-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="a0637-118">Scenario description</span></span>
<span data-ttu-id="a0637-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="a0637-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a0637-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="a0637-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a0637-121">Adicionar LinkedIn Sales Navigator da galeria</span><span class="sxs-lookup"><span data-stu-id="a0637-121">Adding LinkedIn Sales Navigator from the gallery</span></span>
2. <span data-ttu-id="a0637-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a0637-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-sales-navigator-from-the-gallery"></a><span data-ttu-id="a0637-123">Adicionar LinkedIn Sales Navigator da galeria</span><span class="sxs-lookup"><span data-stu-id="a0637-123">Adding LinkedIn Sales Navigator from the gallery</span></span>
<span data-ttu-id="a0637-124">Para configurar a integração do LinkedIn Sales Navigator com o Azure AD, é necessário adicionar o LinkedIn Sales Navigator da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="a0637-124">To configure the integration of LinkedIn Sales Navigator into Azure AD, you need to add LinkedIn Sales Navigator from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a0637-125">**Para adicionar o LinkedIn Sales Navigator da galeria, siga as etapas abaixo:**</span><span class="sxs-lookup"><span data-stu-id="a0637-125">**To add LinkedIn Sales Navigator from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a0637-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a0637-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a0637-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="a0637-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a0637-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a0637-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="a0637-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a0637-131">Click **New application** button on the top of the dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="a0637-133">Na caixa de pesquisa, digite **LinkedIn Sales Navigator**.</span><span class="sxs-lookup"><span data-stu-id="a0637-133">In the search box, type **LinkedIn Sales Navigator**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_search.png)

5. <span data-ttu-id="a0637-135">No painel de resultados, selecione **LinkedIn Sales Navigator** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a0637-135">In the results panel, select **LinkedIn Sales Navigator**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a0637-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a0637-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a0637-138">Nesta seção, você configurará e testará o logon único do Azure AD com o LinkedIn Sales Navigator, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="a0637-138">In this section, you configure and test Azure AD single sign-on with LinkedIn Sales Navigator based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a0637-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do LinkedIn Sales Navigator é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a0637-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LinkedIn Sales Navigator is to a user in Azure AD.</span></span> <span data-ttu-id="a0637-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do LinkedIn Sales Navigator.</span><span class="sxs-lookup"><span data-stu-id="a0637-140">In other words, a link relationship between an Azure AD user and the related user in LinkedIn Sales Navigator needs to be established.</span></span>

<span data-ttu-id="a0637-141">Essa relação de vínculo é estabelecida atribuindo o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** no LinkedIn Sales Navigator.</span><span class="sxs-lookup"><span data-stu-id="a0637-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LinkedIn Sales Navigator.</span></span>

<span data-ttu-id="a0637-142">Para configurar e testar o logon único do Azure AD com o LinkedIn Sales Navigator, é necessário concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="a0637-142">To configure and test Azure AD single sign-on with LinkedIn Sales Navigator, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a0637-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="a0637-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a0637-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="a0637-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a0637-145">**[Criar um usuário de teste do LinkedIn Sales Navigator](#creating-a-linkedin-sales-navigator-test-user)** – para ter um equivalente de Brenda Fernandes no LinkedIn Sales Navigator que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a0637-145">**[Creating a LinkedIn Sales Navigator test user](#creating-a-linkedin-sales-navigator-test-user)** - to have a counterpart of Britta Simon in LinkedIn Sales Navigator that is linked to the Azure AD representation of the user.</span></span>
4. <span data-ttu-id="a0637-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** - para habilitar Britta Simon a usar o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="a0637-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a0637-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="a0637-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a0637-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0637-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a0637-149">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único em seu aplicativo LinkedIn Sales Navigator.</span><span class="sxs-lookup"><span data-stu-id="a0637-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LinkedIn Sales Navigator application.</span></span>

<span data-ttu-id="a0637-150">**Para configurar o logon único do Azure AD com o LinkedIn Sales Navigator, siga as etapas abaixo:**</span><span class="sxs-lookup"><span data-stu-id="a0637-150">**To configure Azure AD single sign-on with LinkedIn Sales Navigator, perform the following steps:**</span></span>

1. <span data-ttu-id="a0637-151">No Portal do Azure, na página de integração de aplicativos do **LinkedIn Sales Navigator**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="a0637-151">In the Azure portal, on the **LinkedIn Sales Navigator** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="a0637-153">Na caixa de diálogo **Logon único**, em **Modo**, selecione **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="a0637-153">On the **Single sign-on** dialog, in **Mode** select **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_samlbase.png)

3. <span data-ttu-id="a0637-155">Em uma janela diferente do navegador da Web, faça logon em seu site do **LinkedIn Sales Navigator** como administrador.</span><span class="sxs-lookup"><span data-stu-id="a0637-155">In a different web browser window, sign-on to your **LinkedIn Sales Navigator** website as an administrator.</span></span>

4. <span data-ttu-id="a0637-156">Em **Centro de Contas**, clique em **Configurações Globais** em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="a0637-156">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="a0637-157">Além disso, selecione **Sales Navigator** na lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="a0637-157">Also, select **Sales Navigator** from the dropdown list.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="a0637-159">Clique em **OU clique aqui para carregar e copiar campos individuais do formulário** e copie a **ID da Entidade** e a **URL ACS (acesso do consumidor de declaração)**.</span><span class="sxs-lookup"><span data-stu-id="a0637-159">Click **OR Click Here to load and copy individual fields from the form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_031.png)

6. <span data-ttu-id="a0637-161">No portal do Azure, em **Domínio e URLs do LinkedIn Sales Navigator**, siga as etapas abaixo se você desejar configurar o aplicativo em modo iniciado por **IDP**.</span><span class="sxs-lookup"><span data-stu-id="a0637-161">On Azure portal, under **LinkedIn Sales Navigator Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_url1.png)

    <span data-ttu-id="a0637-163">a.</span><span class="sxs-lookup"><span data-stu-id="a0637-163">a.</span></span> <span data-ttu-id="a0637-164">Na caixa de texto **Identificador**, insira a **ID da Entidade** copiada do Portal do LinkedIn</span><span class="sxs-lookup"><span data-stu-id="a0637-164">In the **Identifier** textbox, enter the **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="a0637-165">b.</span><span class="sxs-lookup"><span data-stu-id="a0637-165">b.</span></span> <span data-ttu-id="a0637-166">Na caixa de texto **URL de Resposta**, insira a **URL ACS (acesso do consumidor de declaração)** copiada do Portal do LinkedIn</span><span class="sxs-lookup"><span data-stu-id="a0637-166">In the **Reply URL** textbox, enter the **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="a0637-167">Marque **Mostrar configurações avançadas de URL** se quiser configurar o aplicativo no modo iniciado em **SP**.</span><span class="sxs-lookup"><span data-stu-id="a0637-167">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_url2.png)

    <span data-ttu-id="a0637-169">Na caixa de texto **URL de Logon**, digite o valor usando o seguinte padrão: `https://www.linkedin.com/checkpoint/enterprise/login/<account id>?application=salesNavigator`</span><span class="sxs-lookup"><span data-stu-id="a0637-169">In the **Sign-on URL** textbox, type the value using the following pattern: `https://www.linkedin.com/checkpoint/enterprise/login/<account id>?application=salesNavigator`</span></span>

8. <span data-ttu-id="a0637-170">Seu aplicativo **LinkedIn Sales Navigator** espera as asserções SAML em um formato específico, o que exige que você adicione mapeamentos de atributos personalizados à sua configuração de atributos de token SAML.</span><span class="sxs-lookup"><span data-stu-id="a0637-170">Your **LinkedIn Sales Navigator** application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="a0637-171">A captura de tela a seguir mostra um exemplo.</span><span class="sxs-lookup"><span data-stu-id="a0637-171">The following screenshot shows an example.</span></span> <span data-ttu-id="a0637-172">O valor padrão do **Identificador de Usuário** é **user.userprincipalname**, mas o LinkedIn Sales Navigator espera que isso seja mapeado com o endereço de email do usuário.</span><span class="sxs-lookup"><span data-stu-id="a0637-172">The default value of **User Identifier** is **user.userprincipalname** but LinkedIn Sales Navigator expects it to be mapped with the user's email address.</span></span> <span data-ttu-id="a0637-173">Você pode usar o atributo **user.mail** na lista ou usar o valor do atributo apropriado com base na configuração da sua organização.</span><span class="sxs-lookup"><span data-stu-id="a0637-173">You can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/updateusermail.png)
    
9. <span data-ttu-id="a0637-175">Na seção **Atributos de Usuário**, clique em **Exibir e editar todos os outros atributos de usuário** e defina os atributos.</span><span class="sxs-lookup"><span data-stu-id="a0637-175">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span> <span data-ttu-id="a0637-176">O usuário precisa adicionar quatro declarações denominadas **email**, **departamento**, **nome** e **sobrenome** e o valor deve ser mapeado com **user.mail**, **user.department**, **user.givenname** e **user.surname** respectivamente</span><span class="sxs-lookup"><span data-stu-id="a0637-176">The user needs to add four claims named **email**, **department**, **firstname**, and **lastname** and the value is to be mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="a0637-177">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="a0637-177">Attribute Name</span></span> | <span data-ttu-id="a0637-178">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="a0637-178">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="a0637-179">email</span><span class="sxs-lookup"><span data-stu-id="a0637-179">email</span></span>| <span data-ttu-id="a0637-180">user.mail</span><span class="sxs-lookup"><span data-stu-id="a0637-180">user.mail</span></span> |
    | <span data-ttu-id="a0637-181">department</span><span class="sxs-lookup"><span data-stu-id="a0637-181">department</span></span>| <span data-ttu-id="a0637-182">user.department</span><span class="sxs-lookup"><span data-stu-id="a0637-182">user.department</span></span> |
    | <span data-ttu-id="a0637-183">nome</span><span class="sxs-lookup"><span data-stu-id="a0637-183">firstname</span></span>| <span data-ttu-id="a0637-184">user.givenname</span><span class="sxs-lookup"><span data-stu-id="a0637-184">user.givenname</span></span> |
    | <span data-ttu-id="a0637-185">sobrenome</span><span class="sxs-lookup"><span data-stu-id="a0637-185">lastname</span></span>| <span data-ttu-id="a0637-186">user.surname</span><span class="sxs-lookup"><span data-stu-id="a0637-186">user.surname</span></span> |
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinsalesnavigator-tutorial/userattribute.png)
    
    <span data-ttu-id="a0637-188">a.</span><span class="sxs-lookup"><span data-stu-id="a0637-188">a.</span></span> <span data-ttu-id="a0637-189">Clique em **Adicionar Atributo** para abrir a caixa de diálogo do atributo.</span><span class="sxs-lookup"><span data-stu-id="a0637-189">Click on **Add Attribute** to open the attribute dialog.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_attribute_04.png)
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_attribute_05.png)
   
    <span data-ttu-id="a0637-192">b.</span><span class="sxs-lookup"><span data-stu-id="a0637-192">b.</span></span> <span data-ttu-id="a0637-193">Na caixa de texto **Nome** , digite o nome do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="a0637-193">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="a0637-194">c.</span><span class="sxs-lookup"><span data-stu-id="a0637-194">c.</span></span> <span data-ttu-id="a0637-195">Na lista **Valor**, digite o valor do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="a0637-195">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="a0637-196">d.</span><span class="sxs-lookup"><span data-stu-id="a0637-196">d.</span></span> <span data-ttu-id="a0637-197">Clique em **Ok**</span><span class="sxs-lookup"><span data-stu-id="a0637-197">Click **Ok**</span></span>

10. <span data-ttu-id="a0637-198">Realize as seguintes etapas no atributo **name**-</span><span class="sxs-lookup"><span data-stu-id="a0637-198">Perform the following steps on the **name** attribute-</span></span>

    <span data-ttu-id="a0637-199">a.</span><span class="sxs-lookup"><span data-stu-id="a0637-199">a.</span></span> <span data-ttu-id="a0637-200">Clique no atributo para abrir a janela **Editar Atributo**.</span><span class="sxs-lookup"><span data-stu-id="a0637-200">Click on the attribute to open the **Edit Attribute** window.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/url_update.png)

    <span data-ttu-id="a0637-202">b.</span><span class="sxs-lookup"><span data-stu-id="a0637-202">b.</span></span> <span data-ttu-id="a0637-203">Exclua o valor da URL do **namespace**.</span><span class="sxs-lookup"><span data-stu-id="a0637-203">Delete the URL value from the **namespace**.</span></span>
    
    <span data-ttu-id="a0637-204">c.</span><span class="sxs-lookup"><span data-stu-id="a0637-204">c.</span></span> <span data-ttu-id="a0637-205">Clique em **OK** para salvar a configuração.</span><span class="sxs-lookup"><span data-stu-id="a0637-205">Click **Ok** to save the setting.</span></span>

11. <span data-ttu-id="a0637-206">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo XML em seu computador.</span><span class="sxs-lookup"><span data-stu-id="a0637-206">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_certificate.png) 

12. <span data-ttu-id="a0637-208">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="a0637-208">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_400.png)

13. <span data-ttu-id="a0637-210">Vá para a seção **Configurações de administração do LinkedIn**.</span><span class="sxs-lookup"><span data-stu-id="a0637-210">Go to **LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="a0637-211">Clique em **Carregar arquivo XML** para carregar o arquivo XML de metadados que você baixou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a0637-211">Click **Upload XML file** to upload the Metadata XML file that you have downloaded from the Azure portal.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_metadata_03.png)

14. <span data-ttu-id="a0637-213">Clique em **Ativar** para habilitar o SSO.</span><span class="sxs-lookup"><span data-stu-id="a0637-213">Click **On** to enable SSO.</span></span> <span data-ttu-id="a0637-214">O status do SSO é alterado de **Não Conectado** para **Conectado**</span><span class="sxs-lookup"><span data-stu-id="a0637-214">SSO status changes from **Not Connected** to **Connected**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_05.png)


> [!TIP]
> <span data-ttu-id="a0637-216">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="a0637-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a0637-217">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="a0637-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a0637-218">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a0637-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a0637-219">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a0637-219">Creating an Azure AD test user</span></span>
<span data-ttu-id="a0637-220">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="a0637-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="a0637-222">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a0637-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a0637-223">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a0637-223">In the **Azure  portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a0637-225">Clicar em **Usuários e grupos** e **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="a0637-225">Go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a0637-227">Na parte superior da caixa de diálogo clique **adicionar** para abrir o **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a0637-227">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a0637-229">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="a0637-229">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a0637-231">a.</span><span class="sxs-lookup"><span data-stu-id="a0637-231">a.</span></span> <span data-ttu-id="a0637-232">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="a0637-232">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a0637-233">b.</span><span class="sxs-lookup"><span data-stu-id="a0637-233">b.</span></span> <span data-ttu-id="a0637-234">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="a0637-234">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a0637-235">c.</span><span class="sxs-lookup"><span data-stu-id="a0637-235">c.</span></span> <span data-ttu-id="a0637-236">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="a0637-236">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a0637-237">d.</span><span class="sxs-lookup"><span data-stu-id="a0637-237">d.</span></span> <span data-ttu-id="a0637-238">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a0637-238">Click **Create**.</span></span>
 
### <a name="creating-a-linkedin-sales-navigator-test-user"></a><span data-ttu-id="a0637-239">Criar um usuário de teste do LinkedIn Sales Navigator</span><span class="sxs-lookup"><span data-stu-id="a0637-239">Creating a LinkedIn Sales Navigator test user</span></span>

<span data-ttu-id="a0637-240">O aplicativo LinkedIn Sales Navigator dá suporte ao provisionamento de usuário JIT (Just-In-Time) e, após a autenticação, os usuários são automaticamente criados no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a0637-240">Linked Sales Navigator Application supports Just in Time (JIT) user provisioning and after authentication users are created in the application automatically.</span></span> <span data-ttu-id="a0637-241">Ative **atribuir licenças automaticamente** para atribuir uma licença ao usuário.</span><span class="sxs-lookup"><span data-stu-id="a0637-241">Activate **Automatically assign licenses** to assign a license to the user.</span></span>
   
   ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinsalesnavigator-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a0637-243">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a0637-243">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a0637-244">Nesta seção, ao conceder acesso ao LinkedIn Sales Navigator a Brenda Fernandes, você permitirá que ela use o logon único do Azure.</span><span class="sxs-lookup"><span data-stu-id="a0637-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LinkedIn Sales Navigator.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="a0637-246">**Para atribuir Brenda Fernandes ao LinkedIn Sales Navigator, siga as etapas abaixo:**</span><span class="sxs-lookup"><span data-stu-id="a0637-246">**To assign Britta Simon to LinkedIn Sales Navigator, perform the following steps:**</span></span>

1. <span data-ttu-id="a0637-247">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a0637-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="a0637-249">Na lista de aplicativos, selecione **LinkedIn Sales Navigator**.</span><span class="sxs-lookup"><span data-stu-id="a0637-249">In the applications list, select **LinkedIn Sales Navigator**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_app.png) 

3. <span data-ttu-id="a0637-251">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="a0637-251">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="a0637-253">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a0637-253">Click **Add** button.</span></span> <span data-ttu-id="a0637-254">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a0637-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="a0637-256">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="a0637-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a0637-257">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a0637-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a0637-258">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a0637-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a0637-259">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="a0637-259">Testing single sign-on</span></span>

<span data-ttu-id="a0637-260">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="a0637-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a0637-261">Quando você clicar no bloco LinkedIn Sales Navigator no painel de acesso, você deverá ser redirecionado à página organizacional em que você precisa fornecer os detalhes da sua conta pessoal do LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="a0637-261">When you click the LinkedIn Sales Navigator tile in the Access Panel, you should be redirected to Organizational page where you have to provide your personal LinkedIn account details.</span></span> <span data-ttu-id="a0637-262">Ele vincula a sua conta pessoal à sua conta de negócios do LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="a0637-262">It links your personal account with your LinkedIn business account.</span></span> <span data-ttu-id="a0637-263">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="a0637-263">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a0637-264">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="a0637-264">Additional resources</span></span>

* [<span data-ttu-id="a0637-265">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="a0637-265">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a0637-266">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a0637-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_203.png

