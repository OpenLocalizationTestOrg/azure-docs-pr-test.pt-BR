---
title: "Tutorial: Integração do Azure Active Directory ao myPolicies | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o myPolicies."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bf79e858-1dfb-4ab3-a6df-74b2d5a878d2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: jeedes
ms.openlocfilehash: fcb403041cb3a8bd20ff7b34aa5cc4b7bf0c0a16
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mypolicies"></a><span data-ttu-id="74bc7-103">Tutorial: Integração do Azure Active Directory ao myPolicies</span><span class="sxs-lookup"><span data-stu-id="74bc7-103">Tutorial: Azure Active Directory integration with myPolicies</span></span>

<span data-ttu-id="74bc7-104">Neste tutorial, você aprende a integrar o myPolicies ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="74bc7-104">In this tutorial, you learn how to integrate myPolicies with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="74bc7-105">A integração do myPolicies ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="74bc7-105">Integrating myPolicies with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="74bc7-106">No Azure AD, é possível controlar quem tem acesso ao myPolicies</span><span class="sxs-lookup"><span data-stu-id="74bc7-106">You can control in Azure AD who has access to myPolicies</span></span>
- <span data-ttu-id="74bc7-107">É possível permitir que os usuários se conectem automaticamente ao myPolicies (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="74bc7-107">You can enable your users to automatically get signed-on to myPolicies (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="74bc7-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="74bc7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="74bc7-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="74bc7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="74bc7-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="74bc7-110">Prerequisites</span></span>

<span data-ttu-id="74bc7-111">Para configurar a integração do Azure AD ao myPolicies, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="74bc7-111">To configure Azure AD integration with myPolicies, you need the following items:</span></span>

- <span data-ttu-id="74bc7-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="74bc7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="74bc7-113">Uma assinatura habilitada para logon único do myPolicies</span><span class="sxs-lookup"><span data-stu-id="74bc7-113">A myPolicies single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="74bc7-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="74bc7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="74bc7-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="74bc7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="74bc7-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="74bc7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="74bc7-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="74bc7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="74bc7-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="74bc7-118">Scenario description</span></span>
<span data-ttu-id="74bc7-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="74bc7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="74bc7-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="74bc7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="74bc7-121">Adicionando o myPolicies por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="74bc7-121">Adding myPolicies from the gallery</span></span>
2. <span data-ttu-id="74bc7-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="74bc7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mypolicies-from-the-gallery"></a><span data-ttu-id="74bc7-123">Adicionando o myPolicies por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="74bc7-123">Adding myPolicies from the gallery</span></span>
<span data-ttu-id="74bc7-124">Para configurar a integração do myPolicies ao Azure AD, é necessário adicionar o myPolicies à lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="74bc7-124">To configure the integration of myPolicies into Azure AD, you need to add myPolicies from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="74bc7-125">**Para adicionar o myPolicies por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="74bc7-125">**To add myPolicies from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="74bc7-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="74bc7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="74bc7-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="74bc7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="74bc7-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="74bc7-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="74bc7-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="74bc7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="74bc7-133">Na caixa de pesquisa, digite **myPolicies**.</span><span class="sxs-lookup"><span data-stu-id="74bc7-133">In the search box, type **myPolicies**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_search.png)

5. <span data-ttu-id="74bc7-135">No painel de resultados, selecione **myPolicies** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="74bc7-135">In the results panel, select **myPolicies**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="74bc7-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="74bc7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="74bc7-138">Nesta seção, você configura e testa o logon único do Azure AD com o myPolicies, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="74bc7-138">In this section, you configure and test Azure AD single sign-on with myPolicies based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="74bc7-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do myPolicies é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="74bc7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in myPolicies is to a user in Azure AD.</span></span> <span data-ttu-id="74bc7-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do myPolicies.</span><span class="sxs-lookup"><span data-stu-id="74bc7-140">In other words, a link relationship between an Azure AD user and the related user in myPolicies needs to be established.</span></span>

<span data-ttu-id="74bc7-141">No myPolicies, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="74bc7-141">In myPolicies, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="74bc7-142">Para configurar e testar o logon único do Azure AD com o myPolicies, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="74bc7-142">To configure and test Azure AD single sign-on with myPolicies, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="74bc7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="74bc7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="74bc7-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="74bc7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="74bc7-145">**[Criando um usuário de teste do myPolicies](#creating-a-mypolicies-test-user)** – para ter um equivalente de Brenda Fernandes no myPolicies que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="74bc7-145">**[Creating a myPolicies test user](#creating-a-mypolicies-test-user)** - to have a counterpart of Britta Simon in myPolicies that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="74bc7-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="74bc7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="74bc7-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="74bc7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="74bc7-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="74bc7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="74bc7-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo myPolicies.</span><span class="sxs-lookup"><span data-stu-id="74bc7-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your myPolicies application.</span></span>

<span data-ttu-id="74bc7-150">**Para configurar o logon único do Azure AD com o myPolicies, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="74bc7-150">**To configure Azure AD single sign-on with myPolicies, perform the following steps:**</span></span>

1. <span data-ttu-id="74bc7-151">No portal do Azure, na página de integração do aplicativo **myPolicies**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="74bc7-151">In the Azure portal, on the **myPolicies** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="74bc7-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="74bc7-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_samlbase.png)

3. <span data-ttu-id="74bc7-155">Na seção **Domínio e URLs do myPolicies**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="74bc7-155">On the **myPolicies Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_url.png)

    <span data-ttu-id="74bc7-157">a.</span><span class="sxs-lookup"><span data-stu-id="74bc7-157">a.</span></span> <span data-ttu-id="74bc7-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<tenantname>.mypolicies.com/`</span><span class="sxs-lookup"><span data-stu-id="74bc7-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.mypolicies.com/`</span></span>

    <span data-ttu-id="74bc7-159">b.</span><span class="sxs-lookup"><span data-stu-id="74bc7-159">b.</span></span> <span data-ttu-id="74bc7-160">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<tenantname>.mypolicies.com/users/auth/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="74bc7-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<tenantname>.mypolicies.com/users/auth/saml/callback`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="74bc7-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="74bc7-161">These values are not real.</span></span> <span data-ttu-id="74bc7-162">Atualize esses valores com o Identificador e a URL de Resposta reais.</span><span class="sxs-lookup"><span data-stu-id="74bc7-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="74bc7-163">Contate a [equipe de suporte do myPolicies](mailto:support@mypolicies.com) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="74bc7-163">Contact [myPolicies support team](mailto:support@mypolicies.com) to get these values.</span></span>

4. <span data-ttu-id="74bc7-164">O aplicativo myPolicies espera que as declarações SAML estejam em um formato específico, o que exige a adição de mapeamentos de atributo personalizados para a configuração de atributos do token SAML.</span><span class="sxs-lookup"><span data-stu-id="74bc7-164">The myPolicies application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="74bc7-165">Configure as declarações a seguir para este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="74bc7-165">Configure the following claims for this application.</span></span> <span data-ttu-id="74bc7-166">Você pode gerenciar os valores desses atributos da seção "**Atributos de Usuário**" na página de integração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="74bc7-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="74bc7-167">A captura de tela a seguir mostra um exemplo disso.</span><span class="sxs-lookup"><span data-stu-id="74bc7-167">The following screenshot shows an example for this.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_attribute.png)

5. <span data-ttu-id="74bc7-169">Clique na caixa de seleção **Exibir e editar todos os outros atributos de usuário** na seção **Atributos de Usuário** para expandir os atributos.</span><span class="sxs-lookup"><span data-stu-id="74bc7-169">Click **View and edit all other user attributes** checkbox in the **User Attributes** section to expand the attributes.</span></span> <span data-ttu-id="74bc7-170">Realize as seguintes etapas em cada um dos atributos exibidos:</span><span class="sxs-lookup"><span data-stu-id="74bc7-170">Perform the following steps on each of the displayed attributes-</span></span>

    | <span data-ttu-id="74bc7-171">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="74bc7-171">Attribute Name</span></span> | <span data-ttu-id="74bc7-172">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="74bc7-172">Attribute Value</span></span> |
    | ------------------- | ---------- |
    | <span data-ttu-id="74bc7-173">givenname</span><span class="sxs-lookup"><span data-stu-id="74bc7-173">givenname</span></span> | <span data-ttu-id="74bc7-174">user.givenname</span><span class="sxs-lookup"><span data-stu-id="74bc7-174">user.givenname</span></span> |
    | <span data-ttu-id="74bc7-175">sobrenome</span><span class="sxs-lookup"><span data-stu-id="74bc7-175">surname</span></span> | <span data-ttu-id="74bc7-176">user.surname</span><span class="sxs-lookup"><span data-stu-id="74bc7-176">user.surname</span></span> |
    | <span data-ttu-id="74bc7-177">emailaddress</span><span class="sxs-lookup"><span data-stu-id="74bc7-177">emailaddress</span></span> | <span data-ttu-id="74bc7-178">user.mail</span><span class="sxs-lookup"><span data-stu-id="74bc7-178">user.mail</span></span> |
    | <span data-ttu-id="74bc7-179">name</span><span class="sxs-lookup"><span data-stu-id="74bc7-179">name</span></span> | <span data-ttu-id="74bc7-180">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="74bc7-180">user.userprincipalname</span></span> |
    
    <span data-ttu-id="74bc7-181">a.</span><span class="sxs-lookup"><span data-stu-id="74bc7-181">a.</span></span> <span data-ttu-id="74bc7-182">Clique no atributo para abrir a caixa de diálogo **Editar Atributo**.</span><span class="sxs-lookup"><span data-stu-id="74bc7-182">Click on the attribute to open the **Edit Attribute** dialog.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-mypolicies-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="74bc7-184">b.</span><span class="sxs-lookup"><span data-stu-id="74bc7-184">b.</span></span> <span data-ttu-id="74bc7-185">Exclua o valor da URL do **Namespace**.</span><span class="sxs-lookup"><span data-stu-id="74bc7-185">Delete the URL value from the **Namespace**.</span></span>
    
    <span data-ttu-id="74bc7-186">c.</span><span class="sxs-lookup"><span data-stu-id="74bc7-186">c.</span></span> <span data-ttu-id="74bc7-187">Clique em **OK** para salvar a configuração.</span><span class="sxs-lookup"><span data-stu-id="74bc7-187">Click **Ok** to save the setting.</span></span>
    
6. <span data-ttu-id="74bc7-188">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="74bc7-188">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_certificate.png) 

7. <span data-ttu-id="74bc7-190">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="74bc7-190">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mypolicies-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="74bc7-192">Na seção **Configuração do myPolicies**, clique em **Configurar o myPolicies** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="74bc7-192">On the **myPolicies Configuration** section, click **Configure myPolicies** to open **Configure sign-on** window.</span></span> <span data-ttu-id="74bc7-193">Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="74bc7-193">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_configure.png) 

9. <span data-ttu-id="74bc7-195">Para configurar o logon único no lado do **myPolicies**, é necessário enviar o **Certificado (Base64)** baixado e a **URL do Serviço de Logon Único SAML** para a [equipe de suporte do myPolicies](mailto:support@mypolicies.com).</span><span class="sxs-lookup"><span data-stu-id="74bc7-195">To configure single sign-on on **myPolicies** side, you need to send the downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** to [myPolicies support team](mailto:support@mypolicies.com).</span></span> 

> [!TIP]
> <span data-ttu-id="74bc7-196">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="74bc7-196">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="74bc7-197">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="74bc7-197">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="74bc7-198">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="74bc7-198">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="74bc7-199">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="74bc7-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="74bc7-200">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="74bc7-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="74bc7-202">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="74bc7-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="74bc7-203">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="74bc7-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="74bc7-205">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="74bc7-205">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="74bc7-207">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="74bc7-207">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="74bc7-209">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="74bc7-209">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="74bc7-211">a.</span><span class="sxs-lookup"><span data-stu-id="74bc7-211">a.</span></span> <span data-ttu-id="74bc7-212">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="74bc7-212">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="74bc7-213">b.</span><span class="sxs-lookup"><span data-stu-id="74bc7-213">b.</span></span> <span data-ttu-id="74bc7-214">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="74bc7-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="74bc7-215">c.</span><span class="sxs-lookup"><span data-stu-id="74bc7-215">c.</span></span> <span data-ttu-id="74bc7-216">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="74bc7-216">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="74bc7-217">d.</span><span class="sxs-lookup"><span data-stu-id="74bc7-217">d.</span></span> <span data-ttu-id="74bc7-218">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="74bc7-218">Click **Create**.</span></span>
 
### <a name="creating-a-mypolicies-test-user"></a><span data-ttu-id="74bc7-219">Criando um usuário de teste do myPolicies</span><span class="sxs-lookup"><span data-stu-id="74bc7-219">Creating a myPolicies test user</span></span>

<span data-ttu-id="74bc7-220">Nesta seção, você cria um usuário chamado Brenda Fernandes no myPolicies.</span><span class="sxs-lookup"><span data-stu-id="74bc7-220">In this section, you create a user called Britta Simon in myPolicies.</span></span> <span data-ttu-id="74bc7-221">Trabalhe com a [equipe de suporte do myPolicies](mailto:support@mypolicies.com) para adicionar os usuários à plataforma myPolicies.</span><span class="sxs-lookup"><span data-stu-id="74bc7-221">Work with [myPolicies support team](mailto:support@mypolicies.com) to add the users in the myPolicies platform.</span></span> <span data-ttu-id="74bc7-222">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="74bc7-222">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="74bc7-223">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="74bc7-223">Assigning the Azure AD test user</span></span>

<span data-ttu-id="74bc7-224">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao myPolicies.</span><span class="sxs-lookup"><span data-stu-id="74bc7-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to myPolicies.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="74bc7-226">**Para atribuir Brenda Fernandes ao myPolicies, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="74bc7-226">**To assign Britta Simon to myPolicies, perform the following steps:**</span></span>

1. <span data-ttu-id="74bc7-227">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="74bc7-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="74bc7-229">Na lista de aplicativos, selecione **myPolicies**.</span><span class="sxs-lookup"><span data-stu-id="74bc7-229">In the applications list, select **myPolicies**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_app.png) 

3. <span data-ttu-id="74bc7-231">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="74bc7-231">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="74bc7-233">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="74bc7-233">Click **Add** button.</span></span> <span data-ttu-id="74bc7-234">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="74bc7-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="74bc7-236">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="74bc7-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="74bc7-237">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="74bc7-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="74bc7-238">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="74bc7-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="74bc7-239">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="74bc7-239">Testing single sign-on</span></span>

<span data-ttu-id="74bc7-240">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="74bc7-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="74bc7-241">Quando você clicar no bloco do myPolicies no Painel de Acesso, deverá ser conectado automaticamente ao aplicativo myPolicies.</span><span class="sxs-lookup"><span data-stu-id="74bc7-241">When you click the myPolicies tile in the Access Panel, you should get automatically signed-on to your myPolicies application.</span></span>
<span data-ttu-id="74bc7-242">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="74bc7-242">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="74bc7-243">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="74bc7-243">Additional resources</span></span>

* [<span data-ttu-id="74bc7-244">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="74bc7-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="74bc7-245">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="74bc7-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_203.png

