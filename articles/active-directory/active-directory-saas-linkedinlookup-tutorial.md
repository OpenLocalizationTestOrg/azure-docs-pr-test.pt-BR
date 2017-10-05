---
title: "Tutorial: Integração do Azure Active Directory ao LinkedIn Lookup | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o LinkedIn Lookup."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a2757a39-1ead-4a3e-91e4-270be3055683
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: e296431866a8611b30e72f286884890adf0f7e50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-lookup"></a><span data-ttu-id="c7afd-103">Tutorial: Integração do Azure Active Directory ao LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="c7afd-103">Tutorial: Azure Active Directory integration with LinkedIn Lookup</span></span>

<span data-ttu-id="c7afd-104">Neste tutorial, você aprenderá a integrar o LinkedIn Lookup ao Azure AD (Active Directory).</span><span class="sxs-lookup"><span data-stu-id="c7afd-104">In this tutorial, you learn how to integrate LinkedIn Lookup with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c7afd-105">A integração do LinkedIn Lookup ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="c7afd-105">Integrating LinkedIn Lookup with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c7afd-106">No Azure AD, você pode controlar quem tem acesso ao LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="c7afd-106">You can control in Azure AD who has access to LinkedIn Lookup</span></span>
- <span data-ttu-id="c7afd-107">É possível permitir que seus usuários entrem automaticamente no LinkedIn Lookup (Logon Único) com as respectivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7afd-107">You can enable your users to automatically get signed-on to LinkedIn Lookup (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c7afd-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c7afd-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c7afd-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c7afd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7afd-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c7afd-110">Prerequisites</span></span>

<span data-ttu-id="c7afd-111">Para configurar a integração do Azure AD ao LinkedIn Lookup, são necessários os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="c7afd-111">To configure Azure AD integration with LinkedIn Lookup, you need the following items:</span></span>

- <span data-ttu-id="c7afd-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7afd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c7afd-113">Uma assinatura habilitada para logon único do LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="c7afd-113">An LinkedIn Lookup single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c7afd-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="c7afd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c7afd-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="c7afd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c7afd-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="c7afd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c7afd-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c7afd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c7afd-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="c7afd-118">Scenario description</span></span>
<span data-ttu-id="c7afd-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="c7afd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c7afd-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="c7afd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c7afd-121">Adicionando o LinkedIn Lookup usando a galeria</span><span class="sxs-lookup"><span data-stu-id="c7afd-121">Adding LinkedIn Lookup from the gallery</span></span>
2. <span data-ttu-id="c7afd-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7afd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-lookup-from-the-gallery"></a><span data-ttu-id="c7afd-123">Adicionando o LinkedIn Lookup usando a galeria</span><span class="sxs-lookup"><span data-stu-id="c7afd-123">Adding LinkedIn Lookup from the gallery</span></span>
<span data-ttu-id="c7afd-124">Para configurar a integração do LinkedIn Lookup ao Azure AD, é necessário adicionar o LinkedIn Lookup da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="c7afd-124">To configure the integration of LinkedIn Lookup into Azure AD, you need to add LinkedIn Lookup from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c7afd-125">**Para adicionar o LinkedIn Lookup da galeria, siga as etapas abaixo:**</span><span class="sxs-lookup"><span data-stu-id="c7afd-125">**To add LinkedIn Lookup from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c7afd-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c7afd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c7afd-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="c7afd-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c7afd-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c7afd-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="c7afd-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c7afd-131">Click **New application** button on the top of the dialog to add new application.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="c7afd-133">Na caixa de pesquisa, digite **LinkedIn Lookup**.</span><span class="sxs-lookup"><span data-stu-id="c7afd-133">In the search box, type **LinkedIn Lookup**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_search.png)

5. <span data-ttu-id="c7afd-135">No painel de resultados, selecione **LinkedIn Lookup** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c7afd-135">In the results panel, select **LinkedIn Lookup**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c7afd-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7afd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c7afd-138">Nesta seção, você vai configurar e testar o logon único do Azure AD com o LinkedIn Lookup, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="c7afd-138">In this section, you configure and test Azure AD single sign-on with LinkedIn Lookup based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c7afd-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do LinkedIn Lookup é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7afd-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LinkedIn Lookup is to a user in Azure AD.</span></span> <span data-ttu-id="c7afd-140">Em outras palavras, é necessário estabelecer uma relação de vinculação entre um usuário do Azure AD e o usuário relacionado no LinkedIn Lookup.</span><span class="sxs-lookup"><span data-stu-id="c7afd-140">In other words, a link relationship between an Azure AD user and the related user in LinkedIn Lookup needs to be established.</span></span>

<span data-ttu-id="c7afd-141">Essa relação de vinculação é estabelecida por meio da atribuição do valor de **nome de usuário** no Azure AD como o valor de **Nome de Usuário** no LinkedIn Lookup.</span><span class="sxs-lookup"><span data-stu-id="c7afd-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LinkedIn Lookup.</span></span>

<span data-ttu-id="c7afd-142">Para configurar e testar o logon único do Azure AD com o LinkedIn Lookup, é necessário concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="c7afd-142">To configure and test Azure AD single sign-on with LinkedIn Lookup, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c7afd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="c7afd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c7afd-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="c7afd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c7afd-145">**[Criação de um usuário de teste do LinkedIn Lookup](#creating-an-linkedin-lookup-test-user)**: para ter um equivalente de Brenda Fernandes no LinkedIn Lookup que esteja vinculado à representação dela no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7afd-145">**[Creating an LinkedIn Lookup test user](#creating-an-linkedin-lookup-test-user)** - to have a counterpart of Britta Simon in LinkedIn Lookup that is linked to the Azure AD representation.</span></span>
4. <span data-ttu-id="c7afd-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** - para habilitar Britta Simon a usar o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7afd-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c7afd-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="c7afd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c7afd-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7afd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c7afd-149">Nesta seção, você vai habilitar o logon único do Azure AD no Portal do Azure e configurar o logon único em seu aplicativo LinkedIn Lookup.</span><span class="sxs-lookup"><span data-stu-id="c7afd-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LinkedIn Lookup application.</span></span>

<span data-ttu-id="c7afd-150">**Para configurar o logon único do Azure AD com o LinkedIn Lookup, siga as etapas abaixo:**</span><span class="sxs-lookup"><span data-stu-id="c7afd-150">**To configure Azure AD single sign-on with LinkedIn Lookup, perform the following steps:**</span></span>

1. <span data-ttu-id="c7afd-151">No Portal do Azure, na página de integração de aplicativos do **LinkedIn Lookup**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="c7afd-151">In the Azure portal, on the **LinkedIn Lookup** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="c7afd-153">Na caixa de diálogo **Logon único**, em **Modo**, selecione **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="c7afd-153">On the **Single sign-on** dialog, in **Mode** select **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_samlbase.png)

3. <span data-ttu-id="c7afd-155">Em uma janela diferente do navegador da Web, faça logon no site do seu **LinkedIn Lookup** como administrador.</span><span class="sxs-lookup"><span data-stu-id="c7afd-155">In a different web browser window, sign-on to your **LinkedIn Lookup** website as an administrator.</span></span>

4. <span data-ttu-id="c7afd-156">Em **Centro de Contas**, clique em **Configurações Globais** em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="c7afd-156">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="c7afd-157">Além disso, selecione **Lookup** na lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="c7afd-157">Also, select **Lookup** from the dropdown list.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_011.png)

5. <span data-ttu-id="c7afd-159">Clique em **OU clique aqui para carregar e copiar campos individuais do formulário** e copie a **ID da Entidade** e a **URL do ACS (Serviço do Consumidor de Declaração)**</span><span class="sxs-lookup"><span data-stu-id="c7afd-159">Click **OR Click Here to load and copy individual fields from the form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_032.png)

6. <span data-ttu-id="c7afd-161">No portal do Azure, em **Domínio e URLs do LinkedIn Lookup**, siga as etapas abaixo se quiser configurar o aplicativo em modo iniciado por **IDP**:</span><span class="sxs-lookup"><span data-stu-id="c7afd-161">On Azure portal, under **LinkedIn Lookup Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url.png)

    <span data-ttu-id="c7afd-163">a.</span><span class="sxs-lookup"><span data-stu-id="c7afd-163">a.</span></span> <span data-ttu-id="c7afd-164">Na caixa de texto **Identificador**, insira a **ID da Entidade** copiada do Portal do LinkedIn</span><span class="sxs-lookup"><span data-stu-id="c7afd-164">In the **Identifier** textbox, enter the **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="c7afd-165">b.</span><span class="sxs-lookup"><span data-stu-id="c7afd-165">b.</span></span> <span data-ttu-id="c7afd-166">Na caixa de texto **URL de Resposta**, insira a **URL ACS (acesso do consumidor de declaração)** copiada do Portal do LinkedIn</span><span class="sxs-lookup"><span data-stu-id="c7afd-166">In the **Reply URL** textbox, enter the **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="c7afd-167">Marque **Mostrar configurações avançadas de URL**, se quiser configurar o aplicativo no modo iniciado em **SP**:</span><span class="sxs-lookup"><span data-stu-id="c7afd-167">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url1.png)

    <span data-ttu-id="c7afd-169">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`</span><span class="sxs-lookup"><span data-stu-id="c7afd-169">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="c7afd-170">Isso não é um valor real.</span><span class="sxs-lookup"><span data-stu-id="c7afd-170">This is not real value.</span></span> <span data-ttu-id="c7afd-171">O usuário precisa atualizar esses valores com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="c7afd-171">The user has to update these values with the actual Sign-On URL.</span></span> <span data-ttu-id="c7afd-172">Contate a [equipe de suporte do Cliente LinkedIn Lookup](https://business.LinkedIn.com/lookup) para obter esse valor.</span><span class="sxs-lookup"><span data-stu-id="c7afd-172">Contact [LinkedIn Lookup Client support team](https://business.LinkedIn.com/lookup) to get this value.</span></span>

8. <span data-ttu-id="c7afd-173">Seu aplicativo **LinkedIn Lookup** espera que as declarações SAML estejam em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="c7afd-173">Your **LinkedIn Lookup** application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="c7afd-174">O usuário precisa adicionar mapeamentos de atributos personalizados à configuração de atributos de token SAML.</span><span class="sxs-lookup"><span data-stu-id="c7afd-174">The user has to add custom attribute mappings to the SAML token attributes configuration.</span></span> <span data-ttu-id="c7afd-175">A captura de tela a seguir mostra um exemplo.</span><span class="sxs-lookup"><span data-stu-id="c7afd-175">The following screenshot shows an example.</span></span> <span data-ttu-id="c7afd-176">O valor padrão do **Identificador de Usuário** é **user.userprincipalname**, mas o LinkedIn Lookup espera que isso seja mapeado com o endereço de email do usuário.</span><span class="sxs-lookup"><span data-stu-id="c7afd-176">The default value of **User Identifier** is **user.userprincipalname** but LinkedIn Lookup expects this to be mapped with the user's email address.</span></span> <span data-ttu-id="c7afd-177">Você pode usar o atributo **user.mail** na lista ou usar o valor do atributo apropriado com base na configuração da sua organização.</span><span class="sxs-lookup"><span data-stu-id="c7afd-177">You can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-LinkedInlookup-tutorial/updateusermail.png)
    
9. <span data-ttu-id="c7afd-179">Na seção **Atributos de Usuário**, clique em **Exibir e editar todos os outros atributos de usuário** e defina os atributos.</span><span class="sxs-lookup"><span data-stu-id="c7afd-179">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span> <span data-ttu-id="c7afd-180">O usuário precisa adicionar quatro declarações denominadas **email**, **departamento**, **nome** e **sobrenome** e o valor deve ser mapeado com **user.mail**, **user.department**, **user.givenname** e **user.surname** respectivamente</span><span class="sxs-lookup"><span data-stu-id="c7afd-180">The user needs to add four claims named **email**,  **department**, **firstname**, and **lastname** and the value is to be mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="c7afd-181">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="c7afd-181">Attribute Name</span></span> | <span data-ttu-id="c7afd-182">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="c7afd-182">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="c7afd-183">email</span><span class="sxs-lookup"><span data-stu-id="c7afd-183">email</span></span>| <span data-ttu-id="c7afd-184">user.mail</span><span class="sxs-lookup"><span data-stu-id="c7afd-184">user.mail</span></span> |    
    | <span data-ttu-id="c7afd-185">department</span><span class="sxs-lookup"><span data-stu-id="c7afd-185">department</span></span>| <span data-ttu-id="c7afd-186">user.department</span><span class="sxs-lookup"><span data-stu-id="c7afd-186">user.department</span></span> |
    | <span data-ttu-id="c7afd-187">nome</span><span class="sxs-lookup"><span data-stu-id="c7afd-187">firstname</span></span>| <span data-ttu-id="c7afd-188">user.givenname</span><span class="sxs-lookup"><span data-stu-id="c7afd-188">user.givenname</span></span> |
    | <span data-ttu-id="c7afd-189">sobrenome</span><span class="sxs-lookup"><span data-stu-id="c7afd-189">lastname</span></span>| <span data-ttu-id="c7afd-190">user.surname</span><span class="sxs-lookup"><span data-stu-id="c7afd-190">user.surname</span></span> |

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-LinkedInlookup-tutorial/userattribute.png)

    <span data-ttu-id="c7afd-192">a.</span><span class="sxs-lookup"><span data-stu-id="c7afd-192">a.</span></span> <span data-ttu-id="c7afd-193">Clique em **Adicionar Atributo** para abrir a caixa de diálogo **Adicionar Atributo**.</span><span class="sxs-lookup"><span data-stu-id="c7afd-193">Click **Add Attribute** to open the **Add Attribute** dialog.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-LinkedInlookup-tutorial/4.png)
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-LinkedInlookup-tutorial/5.png)
   
    <span data-ttu-id="c7afd-196">b.</span><span class="sxs-lookup"><span data-stu-id="c7afd-196">b.</span></span> <span data-ttu-id="c7afd-197">Na caixa de texto **Nome** , digite o nome do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="c7afd-197">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="c7afd-198">c.</span><span class="sxs-lookup"><span data-stu-id="c7afd-198">c.</span></span> <span data-ttu-id="c7afd-199">Na lista **Valor**, digite o valor do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="c7afd-199">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="c7afd-200">d.</span><span class="sxs-lookup"><span data-stu-id="c7afd-200">d.</span></span> <span data-ttu-id="c7afd-201">Clique em **Ok**</span><span class="sxs-lookup"><span data-stu-id="c7afd-201">Click **Ok**</span></span>

10. <span data-ttu-id="c7afd-202">Realize as seguintes etapas no atributo **name**-</span><span class="sxs-lookup"><span data-stu-id="c7afd-202">Perform the following steps on the **name** attribute-</span></span>

    <span data-ttu-id="c7afd-203">a.</span><span class="sxs-lookup"><span data-stu-id="c7afd-203">a.</span></span> <span data-ttu-id="c7afd-204">Clique no atributo para abrir a janela **Editar Atributo**.</span><span class="sxs-lookup"><span data-stu-id="c7afd-204">Click on the attribute to open the **Edit Attribute** window.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-LinkedInlookup-tutorial/url_update.png)

    <span data-ttu-id="c7afd-206">b.</span><span class="sxs-lookup"><span data-stu-id="c7afd-206">b.</span></span> <span data-ttu-id="c7afd-207">Exclua o valor da URL do **namespace**.</span><span class="sxs-lookup"><span data-stu-id="c7afd-207">Delete the URL value from the **namespace**.</span></span>
    
    <span data-ttu-id="c7afd-208">c.</span><span class="sxs-lookup"><span data-stu-id="c7afd-208">c.</span></span> <span data-ttu-id="c7afd-209">Clique em **OK** para salvar a configuração.</span><span class="sxs-lookup"><span data-stu-id="c7afd-209">Click **Ok** to save the setting.</span></span>

10. <span data-ttu-id="c7afd-210">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo XML em seu computador.</span><span class="sxs-lookup"><span data-stu-id="c7afd-210">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_certificate.png) 

11. <span data-ttu-id="c7afd-212">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="c7afd-212">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_400.png)

12. <span data-ttu-id="c7afd-214">Vá para a seção **Configurações de administração do LinkedIn**.</span><span class="sxs-lookup"><span data-stu-id="c7afd-214">Go to **LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="c7afd-215">Carregue o arquivo XML que você baixou do Portal do Azure clicando na opção **Carregar o arquivo XML**.</span><span class="sxs-lookup"><span data-stu-id="c7afd-215">Upload the XML file you downloaded from the Azure portal by clicking the **Upload XML file** option.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_metadata_03.png)

13. <span data-ttu-id="c7afd-217">Clique em **Ativar** para habilitar o SSO.</span><span class="sxs-lookup"><span data-stu-id="c7afd-217">Click **On** to enable SSO.</span></span> <span data-ttu-id="c7afd-218">O status do SSO é alterado de **Não Conectado** para **Conectado**</span><span class="sxs-lookup"><span data-stu-id="c7afd-218">SSO status changes from **Not Connected** to **Connected**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_admin_05.png)

> [!TIP]
> <span data-ttu-id="c7afd-220">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="c7afd-220">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c7afd-221">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="c7afd-221">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c7afd-222">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c7afd-222">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c7afd-223">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7afd-223">Creating an Azure AD test user</span></span>
<span data-ttu-id="c7afd-224">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="c7afd-224">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="c7afd-226">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c7afd-226">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c7afd-227">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c7afd-227">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c7afd-229">Clicar em **Usuários e grupos** e **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="c7afd-229">Go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c7afd-231">Clique em **Adicionar** para abrir o diálogo **Usuário**.</span><span class="sxs-lookup"><span data-stu-id="c7afd-231">Click **Add** to open the **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c7afd-233">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c7afd-233">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c7afd-235">a.</span><span class="sxs-lookup"><span data-stu-id="c7afd-235">a.</span></span> <span data-ttu-id="c7afd-236">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="c7afd-236">In the **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="c7afd-237">b.</span><span class="sxs-lookup"><span data-stu-id="c7afd-237">b.</span></span> <span data-ttu-id="c7afd-238">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="c7afd-238">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="c7afd-239">c.</span><span class="sxs-lookup"><span data-stu-id="c7afd-239">c.</span></span> <span data-ttu-id="c7afd-240">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="c7afd-240">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c7afd-241">d.</span><span class="sxs-lookup"><span data-stu-id="c7afd-241">d.</span></span> <span data-ttu-id="c7afd-242">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c7afd-242">Click **Create**.</span></span>
 
### <a name="creating-an-linkedin-lookup-test-user"></a><span data-ttu-id="c7afd-243">Criação de um usuário de teste do LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="c7afd-243">Creating an LinkedIn Lookup test user</span></span>

<span data-ttu-id="c7afd-244">O aplicativo LinkedIn Lookup dá suporte ao provisionamento de usuário JIT (Just-In-Time) e, após a autenticação, os usuários são automaticamente criados no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c7afd-244">Linked Lookup Application supports Just in Time (JIT) user provisioning and after authentication users are created in the application automatically.</span></span> <span data-ttu-id="c7afd-245">Ative **atribuir licenças automaticamente** para atribuir uma licença ao usuário.</span><span class="sxs-lookup"><span data-stu-id="c7afd-245">Activate **Automatically assign licenses** to assign a license to the user.</span></span>
   
   ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedin_admin_license.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c7afd-247">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7afd-247">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c7afd-248">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure ao conceder acesso ao LinkedIn Lookup.</span><span class="sxs-lookup"><span data-stu-id="c7afd-248">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LinkedIn Lookup.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="c7afd-250">**Para atribuir Brenda Fernandes ao LinkedIn Lookup, siga as etapas abaixo:**</span><span class="sxs-lookup"><span data-stu-id="c7afd-250">**To assign Britta Simon to LinkedIn Lookup, perform the following steps:**</span></span>

1. <span data-ttu-id="c7afd-251">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c7afd-251">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="c7afd-253">Na lista de aplicativos, selecione **LinkedIn Lookup**.</span><span class="sxs-lookup"><span data-stu-id="c7afd-253">In the applications list, select **LinkedIn Lookup**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_app.png) 

3. <span data-ttu-id="c7afd-255">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c7afd-255">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="c7afd-257">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c7afd-257">Click **Add** button.</span></span> <span data-ttu-id="c7afd-258">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c7afd-258">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="c7afd-260">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="c7afd-260">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c7afd-261">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c7afd-261">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c7afd-262">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c7afd-262">Click **Assign** button on **Add Assignment** dialog.</span></span>

    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c7afd-263">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="c7afd-263">Testing single sign-on</span></span>

<span data-ttu-id="c7afd-264">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="c7afd-264">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c7afd-265">Ao clicar no bloco LinkedIn Lookup no Painel de Acesso, você deverá ser redirecionado para a página Organizacional, na qual é preciso fornecer os detalhes da sua conta pessoal do LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="c7afd-265">When you click the LinkedIn Lookup tile in the Access Panel, you should be redirected to Organizational page where you have to provide your personal LinkedIn account details.</span></span> <span data-ttu-id="c7afd-266">Ele vincula a sua conta pessoal à sua conta de negócios do LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="c7afd-266">It links your personal account with your LinkedIn business account.</span></span> 

<span data-ttu-id="c7afd-267">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c7afd-267">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c7afd-268">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="c7afd-268">Additional resources</span></span>

* [<span data-ttu-id="c7afd-269">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="c7afd-269">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c7afd-270">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c7afd-270">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_203.png

