---
title: "Tutorial: integração do Azure Active Directory com o LinkedIn Elevate | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o LinkedIn Elevate."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ad9941b-c574-42c3-bd0f-5d6ec68537ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeedes
ms.openlocfilehash: 5336543e06d60be555722a615568b12048c2aa2f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-elevate"></a><span data-ttu-id="cb45d-103">Tutorial: integração do Azure Active Directory com o LinkedIn Elevate</span><span class="sxs-lookup"><span data-stu-id="cb45d-103">Tutorial: Azure Active Directory integration with LinkedIn Elevate</span></span>

<span data-ttu-id="cb45d-104">Neste tutorial, você aprenderá a integrar o LinkedIn Elevate ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="cb45d-104">In this tutorial, you learn how to integrate LinkedIn Elevate with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cb45d-105">A integração do LinkedIn Elevate com o Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="cb45d-105">Integrating LinkedIn Elevate with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cb45d-106">É possível controlar, no Azure AD, quem tem acesso ao LinkedIn Elevate</span><span class="sxs-lookup"><span data-stu-id="cb45d-106">You can control in Azure AD who has access to LinkedIn Elevate</span></span>
- <span data-ttu-id="cb45d-107">É possível permitir que seus usuários façam logon automaticamente no LinkedIn Elevate (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb45d-107">You can enable your users to automatically get signed-on to LinkedIn Elevate (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cb45d-108">Você pode gerenciar suas contas em um único local - o portal de Gerenciamento do Azure</span><span class="sxs-lookup"><span data-stu-id="cb45d-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="cb45d-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cb45d-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb45d-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cb45d-110">Prerequisites</span></span>

<span data-ttu-id="cb45d-111">Para configurar a integração do Azure AD com o LinkedIn Elevate, são necessários os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="cb45d-111">To configure Azure AD integration with LinkedIn Elevate, you need the following items:</span></span>

- <span data-ttu-id="cb45d-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cb45d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cb45d-113">Uma assinatura do LinkedIn Elevate habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="cb45d-113">A LinkedIn Elevate single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cb45d-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="cb45d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cb45d-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="cb45d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cb45d-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="cb45d-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="cb45d-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cb45d-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cb45d-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="cb45d-118">Scenario description</span></span>
<span data-ttu-id="cb45d-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="cb45d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cb45d-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="cb45d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cb45d-121">Adicionando o LinkedIn da galeria</span><span class="sxs-lookup"><span data-stu-id="cb45d-121">Adding LinkedIn Elevate from the gallery</span></span>
2. <span data-ttu-id="cb45d-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cb45d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-elevate-from-the-gallery"></a><span data-ttu-id="cb45d-123">Adicionando o LinkedIn da galeria</span><span class="sxs-lookup"><span data-stu-id="cb45d-123">Adding LinkedIn Elevate from the gallery</span></span>
<span data-ttu-id="cb45d-124">Para configurar a integração do LinkedIn Elevate ao Azure AD, é necessário adicionar o LinkedIn Elevate por meio da galeria à lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="cb45d-124">To configure the integration of LinkedIn Elevate into Azure AD, you need to add LinkedIn Elevate from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cb45d-125">**Para adicionar o LinkedIn Elevate da galeria, siga as etapas abaixo:**</span><span class="sxs-lookup"><span data-stu-id="cb45d-125">**To add LinkedIn Elevate from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cb45d-126">No **[Portal de Gerenciamento do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cb45d-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cb45d-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="cb45d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cb45d-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="cb45d-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="cb45d-131">Clique em **adicionar** botão na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cb45d-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="cb45d-133">Na caixa de pesquisa, digite **LinkedIn Elevate**.</span><span class="sxs-lookup"><span data-stu-id="cb45d-133">In the search box, type **LinkedIn Elevate**.</span></span> <span data-ttu-id="cb45d-134">No painel de resultados, clique em **LinkedIn Elevate** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cb45d-134">From results panel, click **LinkedIn Elevate** to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cb45d-136">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cb45d-136">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cb45d-137">Nesta seção, você configurará e testará o logon único do Azure AD com o LinkedIn Elevate, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="cb45d-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Elevate based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cb45d-138">Para que o logon único funcione, o Azure AD precisa saber qual usuário do LinkedIn Elevate é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cb45d-138">For single sign-on to work, Azure AD needs to know what the counterpart user in LinkedIn Elevate is to a user in Azure AD.</span></span> <span data-ttu-id="cb45d-139">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no LinkedIn Elevate.</span><span class="sxs-lookup"><span data-stu-id="cb45d-139">In other words, a link relationship between an Azure AD user and the related user in LinkedIn Elevate needs to be established.</span></span>

<span data-ttu-id="cb45d-140">Essa relação de vínculo é estabelecida por meio da atribuição do valor de **nome de usuário** no Azure AD como o valor de **Nome de Usuário** no LinkedIn Elevate.</span><span class="sxs-lookup"><span data-stu-id="cb45d-140">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LinkedIn Elevate.</span></span>

<span data-ttu-id="cb45d-141">Para configurar e testar o logon único do Azure AD com o LinkedIn Elevate, é necessário concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="cb45d-141">To configure and test Azure AD single sign-on with LinkedIn Elevate, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cb45d-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="cb45d-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="cb45d-143">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="cb45d-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cb45d-144">**[Criando um usuário de teste do LinkedIn Elevate](#creating-a-linkedin-elevate-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="cb45d-144">**[Creating a LinkedIn Elevate test user](#creating-a-linkedin-elevate-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="cb45d-145">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb45d-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cb45d-146">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="cb45d-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cb45d-147">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb45d-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cb45d-148">Nesta seção, você habilitará o logon único do Azure AD no portal de Gerenciamento do Azure e configurará o logon único em seu aplicativo LinkedIn Elevate.</span><span class="sxs-lookup"><span data-stu-id="cb45d-148">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your LinkedIn Elevate application.</span></span>

<span data-ttu-id="cb45d-149">**Para configurar o logon único do Azure AD com o LinkedIn Elevate, siga as etapas abaixo:**</span><span class="sxs-lookup"><span data-stu-id="cb45d-149">**To configure Azure AD single sign-on with LinkedIn Elevate, perform the following steps:**</span></span>

1. <span data-ttu-id="cb45d-150">No portal de Gerenciamento do Azure, na página de integração de aplicativos do **LinkedIn Elevate**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="cb45d-150">In the Azure Management portal, on the **LinkedIn Elevate** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="cb45d-152">Na caixa de diálogo **Logon único**, como **Modo**, selecione **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="cb45d-152">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedin_01.png)

3. <span data-ttu-id="cb45d-154">Em uma janela diferente do navegador da Web, faça logon em seu locatário do LinkedIn Elevate como um administrador.</span><span class="sxs-lookup"><span data-stu-id="cb45d-154">In a different web browser window, sign-on to your LinkedIn Elevate tenant as an administrator.</span></span>

4. <span data-ttu-id="cb45d-155">Em **Centro de Contas**, clique em **Configurações Globais** em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="cb45d-155">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="cb45d-156">Além disso, selecione **Elevar – Elevar teste do AAD** na lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="cb45d-156">Also, select **Elevate - Elevate AAD Test** from the dropdown list.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="cb45d-158">Clique em **OU Clique aqui para carregar e copiar campos individuais do formulário** e copie a **ID da entidade** e **URL ACS (acesso do consumidor de declaração)**</span><span class="sxs-lookup"><span data-stu-id="cb45d-158">Click on **OR Click Here to load and copy individual fields from the form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_03.png)

6. <span data-ttu-id="cb45d-160">No Portal do Azure, em **Domínio e URLs do LinkedIn Elevate**, siga as etapas abaixo para configurar o SSO no modo **iniciado pelo IdP**</span><span class="sxs-lookup"><span data-stu-id="cb45d-160">On Azure Portal, under **LinkedIn Elevate Domain and URLs**, perform the following steps if you want to configure SSO in **IdP Initiated** mode</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_01.png)

    <span data-ttu-id="cb45d-162">a.</span><span class="sxs-lookup"><span data-stu-id="cb45d-162">a.</span></span> <span data-ttu-id="cb45d-163">Na caixa de texto **Identificador**, insira a **ID da Entidade** copiada do Portal do LinkedIn</span><span class="sxs-lookup"><span data-stu-id="cb45d-163">In the **Identifier** textbox, enter the **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="cb45d-164">b.</span><span class="sxs-lookup"><span data-stu-id="cb45d-164">b.</span></span> <span data-ttu-id="cb45d-165">Na caixa de texto **URL de resposta**, insira a **URL ACS (acesso do consumidor de declaração)** copiada do Portal do LinkedIn</span><span class="sxs-lookup"><span data-stu-id="cb45d-165">In the **Reply URL** textbox, enter the **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="cb45d-166">Se você desejar configurar o SSO em **Iniciado pelo SP**, clique na opção Mostrar configurações avançadas de URL na seção de configuração e configure o logon na URL com o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="cb45d-166">If you want to configure SSO in **SP Initiated**, then click Show Advanced URL setting option in the configuration section and configure the sign on URL with the following pattern:</span></span>

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=elevate&applicationInstanceId=<InstanceId>` 
    
    ![Configurar Logon Único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_02.png) 
    
8. <span data-ttu-id="cb45d-168">Seu aplicativo LinkedIn Elevate espera as declarações SAML em um formato específico, o que exige que você adicione mapeamentos de atributo personalizados à sua configuração de atributos de token SAML.</span><span class="sxs-lookup"><span data-stu-id="cb45d-168">Your LinkedIn Elevate application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="cb45d-169">A captura de tela a seguir mostra um exemplo disso.</span><span class="sxs-lookup"><span data-stu-id="cb45d-169">The following screenshot shows an example for this.</span></span> <span data-ttu-id="cb45d-170">O valor padrão do **identificador de usuário** é **user.userprincipalname**, mas o LinkedIn Elevate espera que isso seja mapeado com o endereço de email do usuário.</span><span class="sxs-lookup"><span data-stu-id="cb45d-170">The default value of **User Identifier** is **user.userprincipalname** but LinkedIn Elevate expects this to be mapped with the user's email address.</span></span> <span data-ttu-id="cb45d-171">Para que você possa usar o atributo **user. mail** na lista ou usar o valor do atributo apropriado com base na configuração da sua organização.</span><span class="sxs-lookup"><span data-stu-id="cb45d-171">For that you can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-linkedinElevate-tutorial/updateusermail.png)

9. <span data-ttu-id="cb45d-173">Na seção **Atributos de Usuário**, clique em **Exibir e editar todos os outros atributos de usuário** e defina os atributos.</span><span class="sxs-lookup"><span data-stu-id="cb45d-173">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span> <span data-ttu-id="cb45d-174">É necessário adicionar outra declaração denominada **departamento** e o valor deve ser mapeado para **user.department**.</span><span class="sxs-lookup"><span data-stu-id="cb45d-174">You need to add another claim named **department** and the value needs to be mapped to **user.department**.</span></span>

    | <span data-ttu-id="cb45d-175">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="cb45d-175">Attribute Name</span></span> | <span data-ttu-id="cb45d-176">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="cb45d-176">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="cb45d-177">department</span><span class="sxs-lookup"><span data-stu-id="cb45d-177">department</span></span>| <span data-ttu-id="cb45d-178">user.department</span><span class="sxs-lookup"><span data-stu-id="cb45d-178">user.department</span></span> |

      ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinElevate-tutorial/userattribute.png)

      <span data-ttu-id="cb45d-180">a.</span><span class="sxs-lookup"><span data-stu-id="cb45d-180">a.</span></span> <span data-ttu-id="cb45d-181">Clique em Adicionar atributo para abrir a página de detalhes do atributo. Adicione o atributo department conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="cb45d-181">Click on Add attribute to open the attribute details page add the department attribute as shown below-</span></span>

      ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinElevate-tutorial/adduserattribute.png)

      <span data-ttu-id="cb45d-183">b.</span><span class="sxs-lookup"><span data-stu-id="cb45d-183">b.</span></span> <span data-ttu-id="cb45d-184">Clique em **Ok** para salvar o atributo.</span><span class="sxs-lookup"><span data-stu-id="cb45d-184">Click on **Ok** to save the attribute.</span></span>

      <span data-ttu-id="cb45d-185">c.</span><span class="sxs-lookup"><span data-stu-id="cb45d-185">c.</span></span> <span data-ttu-id="cb45d-186">Altere o nome do atributo **emailaddress** para **email**.</span><span class="sxs-lookup"><span data-stu-id="cb45d-186">Change the name of the attribute **emailaddress** to **email**.</span></span>


10. <span data-ttu-id="cb45d-187">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo XML em seu computador.</span><span class="sxs-lookup"><span data-stu-id="cb45d-187">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_certificate.png) 

11. <span data-ttu-id="cb45d-189">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="cb45d-189">Click **Save**.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_400.png)

12. <span data-ttu-id="cb45d-191">Vá para a seção **Configurações de administração do LinkedIn**.</span><span class="sxs-lookup"><span data-stu-id="cb45d-191">Go to **LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="cb45d-192">Carregue o arquivo XML que você acabou de baixar no portal do Azure clicando na opção Carregar arquivo XML.</span><span class="sxs-lookup"><span data-stu-id="cb45d-192">Upload the XML file you just downloaded from the Azure portal by clicking on the Upload XML file option.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_metadata_03.png)

13. <span data-ttu-id="cb45d-194">Clique em **Ativar** para habilitar o SSO.</span><span class="sxs-lookup"><span data-stu-id="cb45d-194">Click **On** to enable SSO.</span></span> <span data-ttu-id="cb45d-195">O status do SSO será alterado de **Não conectado** para **Conectado**</span><span class="sxs-lookup"><span data-stu-id="cb45d-195">SSO status will change from **Not Connected** to **Connected**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cb45d-197">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cb45d-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="cb45d-198">O objetivo desta seção é criar um usuário de teste no Portal de Gerenciamento do Azure chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cb45d-198">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="cb45d-200">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="cb45d-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cb45d-201">No **portal de Gerenciamento do Azure**, no painel navegação à esquerda, clique em **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cb45d-201">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cb45d-203">Vá para **usuários e grupos** e clique em **todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="cb45d-203">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cb45d-205">Na parte superior da caixa de diálogo clique **adicionar** para abrir o **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cb45d-205">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cb45d-207">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="cb45d-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cb45d-209">a.</span><span class="sxs-lookup"><span data-stu-id="cb45d-209">a.</span></span> <span data-ttu-id="cb45d-210">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="cb45d-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cb45d-211">b.</span><span class="sxs-lookup"><span data-stu-id="cb45d-211">b.</span></span> <span data-ttu-id="cb45d-212">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="cb45d-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cb45d-213">c.</span><span class="sxs-lookup"><span data-stu-id="cb45d-213">c.</span></span> <span data-ttu-id="cb45d-214">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="cb45d-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="cb45d-215">d.</span><span class="sxs-lookup"><span data-stu-id="cb45d-215">d.</span></span> <span data-ttu-id="cb45d-216">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="cb45d-216">Click **Create**.</span></span> 

### <a name="creating-a-linkedin-elevate-test-user"></a><span data-ttu-id="cb45d-217">Criando um usuário de teste do LinkedIn Elevate</span><span class="sxs-lookup"><span data-stu-id="cb45d-217">Creating a LinkedIn Elevate test user</span></span>

<span data-ttu-id="cb45d-218">O aplicativo Linked Elevate dá suporte ao provisionamento de usuário just-in-time e, após a autenticação, os usuários serão automaticamente criados no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cb45d-218">Linked Elevate Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span> <span data-ttu-id="cb45d-219">Na página de configurações de administração no portal do LinkedIn Elevate, coloque a opção **Atribuir licenças automaticamente** como ativa para habilitar o provisionamento just-in-time e isso também atribuirá uma licença ao usuário.</span><span class="sxs-lookup"><span data-stu-id="cb45d-219">On the admin settings page on the LinkedIn Elevate portal flip the switch **Automatically Assign licenses** to active to enable Just in time provisioning and this will also assign a license to the user.</span></span>

   ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinElevate-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="cb45d-221">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cb45d-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="cb45d-222">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao LinkedIn Elevate.</span><span class="sxs-lookup"><span data-stu-id="cb45d-222">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to LinkedIn Elevate.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="cb45d-224">**Para atribuir Brenda Fernandes ao LinkedIn Elevate, siga as etapas abaixo:**</span><span class="sxs-lookup"><span data-stu-id="cb45d-224">**To assign Britta Simon to LinkedIn Elevate, perform the following steps:**</span></span>

1. <span data-ttu-id="cb45d-225">No portal de gerenciamento do Azure, abra a exibição de aplicativos e, em seguida, navegue até o modo de exibição de diretório e vá para **aplicativos empresariais** e clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="cb45d-225">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="cb45d-227">Na lista de aplicativos, selecione **LinkedIn Elevate**.</span><span class="sxs-lookup"><span data-stu-id="cb45d-227">In the applications list, select **LinkedIn Elevate**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_0001.png) 

3. <span data-ttu-id="cb45d-229">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="cb45d-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="cb45d-231">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="cb45d-231">Click **Add** button.</span></span> <span data-ttu-id="cb45d-232">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cb45d-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="cb45d-234">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="cb45d-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="cb45d-235">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cb45d-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cb45d-236">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cb45d-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cb45d-237">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="cb45d-237">Testing single sign-on</span></span>

<span data-ttu-id="cb45d-238">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="cb45d-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="cb45d-239">Quando você clica no bloco LinkedIn Elevate no Painel de Acesso, você deve obter a página de logon do Azure e, após o logon bem-sucedido, você deve entrar em seu aplicativo LinkedIn Elevate.</span><span class="sxs-lookup"><span data-stu-id="cb45d-239">When you click the LinkedIn Elevate tile in the Access Panel, you should get the Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Elevate application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cb45d-240">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="cb45d-240">Additional resources</span></span>

* [<span data-ttu-id="cb45d-241">Tutorial: Configurar o LinkedIn Elevate para o provisionamento automático de usuário com o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cb45d-241">Tutorial: Configuring LinkedIn Elevate for automatic user provisioning with Azure Active Directory</span></span>](active-directory-saas-linkedinelevate-provisioning-tutorial.md)
* [<span data-ttu-id="cb45d-242">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="cb45d-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cb45d-243">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cb45d-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_203.png
