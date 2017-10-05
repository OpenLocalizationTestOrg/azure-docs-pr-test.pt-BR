---
title: "Tutorial: Integração do Azure Active Directory ao ScaleX Enterprise | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o ScaleX Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2379a8d-a659-45f1-87db-9ba156d83183
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: 0ebed0c2605862426384c0e219e52c9d626b6246
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scalex-enterprise"></a><span data-ttu-id="449e4-103">Tutorial: Integração do Azure Active Directory ao ScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="449e4-103">Tutorial: Azure Active Directory integration with ScaleX Enterprise</span></span>

<span data-ttu-id="449e4-104">Neste tutorial, você aprende a integrar o ScaleX Enterprise ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="449e4-104">In this tutorial, you learn how to integrate ScaleX Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="449e4-105">A integração do ScaleX Enterprise ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="449e4-105">Integrating ScaleX Enterprise with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="449e4-106">No Azure AD, é possível controlar quem tem acesso ao ScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="449e4-106">You can control in Azure AD who has access to ScaleX Enterprise</span></span>
- <span data-ttu-id="449e4-107">É possível permitir que os usuários sejam automaticamente conectados ao ScaleX Enterprise (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="449e4-107">You can enable your users to automatically get signed-on to ScaleX Enterprise (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="449e4-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="449e4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="449e4-109">Se você quiser saber mais detalhes sobre a integração de aplicativos SaaS com o Azure AD, consulte.</span><span class="sxs-lookup"><span data-stu-id="449e4-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="449e4-110">O que é o acesso a aplicativos e logon único com o [Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="449e4-110">What is application access and single sign-on with [Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="449e4-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="449e4-111">Prerequisites</span></span>

<span data-ttu-id="449e4-112">Para configurar a integração do Azure AD ao ScaleX Enterprise, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="449e4-112">To configure Azure AD integration with ScaleX Enterprise, you need the following items:</span></span>

- <span data-ttu-id="449e4-113">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="449e4-113">An Azure AD subscription</span></span>
- <span data-ttu-id="449e4-114">Uma assinatura do ScaleX Enterprise habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="449e4-114">A ScaleX Enterprise single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="449e4-115">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="449e4-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="449e4-116">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="449e4-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="449e4-117">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="449e4-117">Do not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="449e4-118">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="449e4-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="449e4-119">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="449e4-119">Scenario description</span></span>
<span data-ttu-id="449e4-120">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="449e4-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="449e4-121">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="449e4-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="449e4-122">Adicionando o ScaleX Enterprise por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="449e4-122">Adding ScaleX Enterprise from the gallery</span></span>
2. <span data-ttu-id="449e4-123">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="449e4-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-scalex-enterprise-from-the-gallery"></a><span data-ttu-id="449e4-124">Adicionando o ScaleX Enterprise por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="449e4-124">Adding ScaleX Enterprise from the gallery</span></span>
<span data-ttu-id="449e4-125">Para configurar a integração do ScaleX Enterprise ao Azure AD, você precisa adicionar o ScaleX Enterprise à lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="449e4-125">To configure the integration of ScaleX Enterprise in to Azure AD, you need to add ScaleX Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="449e4-126">**Para adicionar o ScaleX Enterprise por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="449e4-126">**To add ScaleX Enterprise from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="449e4-127">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="449e4-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="449e4-129">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="449e4-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="449e4-130">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="449e4-130">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="449e4-132">Clique em **adicionar** botão na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="449e4-132">Click **Add** button on the top of the dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="449e4-134">Na caixa de pesquisa, digite **ScaleX Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="449e4-134">In the search box, type **ScaleX Enterprise**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_search.png)

5. <span data-ttu-id="449e4-136">No painel de resultados, selecione **ScaleX Enterprise** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="449e4-136">In the results panel, select **ScaleX Enterprise**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="449e4-138">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="449e4-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="449e4-139">Nesta seção, você configura e testa o logon único do Azure AD com o ScaleX Enterprise, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="449e4-139">In this section, you configure and test Azure AD single sign-on with ScaleX Enterprise based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="449e4-140">Para que o logon único funcione, o Azure AD precisa saber qual usuário do ScaleX Enterprise é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="449e4-140">For single sign-on to work, Azure AD needs to know what the counterpart user in ScaleX Enterprise is to a user in Azure AD.</span></span> <span data-ttu-id="449e4-141">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="449e4-141">In other words, a link relationship between an Azure AD user and the related user in ScaleX Enterprise needs to be established.</span></span>

<span data-ttu-id="449e4-142">Essa relação de vínculo é estabelecida atribuindo o valor de **nome de usuário** no Azure AD ao valor de **Nome de usuário** no ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="449e4-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ScaleX Enterprise.</span></span>

<span data-ttu-id="449e4-143">Para configurar e testar o logon único do Azure AD com o ScaleX Enterprise, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="449e4-143">To configure and test Azure AD single sign-on with ScaleX Enterprise, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="449e4-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="449e4-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="449e4-145">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="449e4-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="449e4-146">**[Criar um usuário de teste do ScaleX Enterprise](#creating-a-scalex-enterprise-test-user)** – para ter um equivalente de Brenda Fernandes no ScaleX Enterprise que está vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="449e4-146">**[Creating a ScaleX Enterprise test user](#creating-a-scalex-enterprise-test-user)** - to have a counterpart of Britta Simon in ScaleX Enterprise that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="449e4-147">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="449e4-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="449e4-148">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="449e4-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="449e4-149">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="449e4-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="449e4-150">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único em seu aplicativo ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="449e4-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ScaleX Enterprise application.</span></span>

<span data-ttu-id="449e4-151">**Para configurar o logon único do Azure AD com o ScaleX Enterprise, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="449e4-151">**To configure Azure AD single sign-on with ScaleX Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="449e4-152">No portal do Azure, na página de integração de aplicativos do **ScaleX Enterprise**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="449e4-152">In the Azure portal, on the **ScaleX Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="449e4-154">Na caixa de diálogo **Logon único**, como **Modo**, selecione **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="449e4-154">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_samlbase.png)

3. <span data-ttu-id="449e4-156">Na seção **Domínio e URLs do ScaleX Enterprise**, realize as seguintes etapas se desejar configurar o aplicativo no modo iniciado pelo **IdP**:</span><span class="sxs-lookup"><span data-stu-id="449e4-156">On the **ScaleX Enterprise Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurar o logon único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url1.png)

    <span data-ttu-id="449e4-158">a.</span><span class="sxs-lookup"><span data-stu-id="449e4-158">a.</span></span> <span data-ttu-id="449e4-159">Na caixa de texto **Identificador**, digite o valor usando o seguinte padrão: `https://platform.rescale.com/saml2/<company id>/`</span><span class="sxs-lookup"><span data-stu-id="449e4-159">In the **Identifier** textbox, type the value using the following pattern: `https://platform.rescale.com/saml2/<company id>/`</span></span>

    <span data-ttu-id="449e4-160">b.</span><span class="sxs-lookup"><span data-stu-id="449e4-160">b.</span></span> <span data-ttu-id="449e4-161">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://platform.rescale.com/saml2/<company id>/acs/`</span><span class="sxs-lookup"><span data-stu-id="449e4-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://platform.rescale.com/saml2/<company id>/acs/`</span></span>

4. <span data-ttu-id="449e4-162">Marque **Mostrar configurações avançadas de URL**, se quiser configurar o aplicativo no modo iniciado em **SP**:</span><span class="sxs-lookup"><span data-stu-id="449e4-162">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurar o logon único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url2.png)

    <span data-ttu-id="449e4-164">Na caixa de texto **URL de Logon**, digite o valor usando o seguinte padrão: `https://platform.rescale.com/saml2/<company id>/sso/`</span><span class="sxs-lookup"><span data-stu-id="449e4-164">In the **Sign-on URL** textbox, type the value using the following pattern: `https://platform.rescale.com/saml2/<company id>/sso/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="449e4-165">Esses não são os valores reais.</span><span class="sxs-lookup"><span data-stu-id="449e4-165">These are not the real values.</span></span> <span data-ttu-id="449e4-166">Atualize esses valores com o Identificador, a URL de Resposta ou a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="449e4-166">Update these values with the actual Identifier, Reply URL or Sign-On URL.</span></span> <span data-ttu-id="449e4-167">Contate a [equipe de suporte ao Cliente do ScaleX Enterprise](http://info.rescale.com/contact_sales) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="449e4-167">Contact [ScaleX Enterprise Client support team](http://info.rescale.com/contact_sales) to get these values.</span></span> 

5. <span data-ttu-id="449e4-168">O aplicativo ScaleX espera as declarações SAML em um formato específico, o que exige a modificação dos mapeamentos de atributo personalizado para sua configuração de atributos do token SAML.</span><span class="sxs-lookup"><span data-stu-id="449e4-168">Your ScaleX application expects the SAML assertions in a specific format, which requires you to modify custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="449e4-169">Clique na caixa de seleção **Exibir e editar todos os outros atributos de usuário** para abrir as configurações de atributo personalizado.</span><span class="sxs-lookup"><span data-stu-id="449e4-169">Click **View and edit all other user attributes** checkbox to open the custom attributes settings.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-scalexenterprise-tutorial/scalex_attributes.png)
    
    <span data-ttu-id="449e4-171">a.</span><span class="sxs-lookup"><span data-stu-id="449e4-171">a.</span></span> <span data-ttu-id="449e4-172">Clique com o botão direito do mouse no atributo **name** e clique em Excluir.</span><span class="sxs-lookup"><span data-stu-id="449e4-172">Right click the attribute **name** and click delete.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-scalexenterprise-tutorial/delete_attribute_name.png)

    <span data-ttu-id="449e4-174">b.</span><span class="sxs-lookup"><span data-stu-id="449e4-174">b.</span></span> <span data-ttu-id="449e4-175">Clique no atributo **emailaddress** para abrir a janela Editar Atributo.</span><span class="sxs-lookup"><span data-stu-id="449e4-175">Click **emailaddress** attribute to open the Edit Attribute window.</span></span> <span data-ttu-id="449e4-176">Altere o valor de **user.mail** para **user.userprincipalname** e clique em OK.</span><span class="sxs-lookup"><span data-stu-id="449e4-176">Change its value from **user.mail** to **user.userprincipalname** and click Ok.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-scalexenterprise-tutorial/edit_email_attribute.png)   
    
5. <span data-ttu-id="449e4-178">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do Certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="449e4-178">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the Certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_certificate.png) 

6. <span data-ttu-id="449e4-180">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="449e4-180">Click **Save** button.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="449e4-182">Na seção **Configuração do ScaleX Enterprise**, clique em **Configurar ScaleX Enterprise** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="449e4-182">On the **ScaleX Enterprise Configuration** section, click **Configure ScaleX Enterprise** to open **Configure sign-on** window.</span></span> <span data-ttu-id="449e4-183">Copie a **ID da Entidade SAML** e a **URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="449e4-183">Copy the **SAML Entity ID** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_configure.png) 

8. <span data-ttu-id="449e4-185">Para configurar o logon único no **ScaleX Enterprise**, faça logon no site da empresa ScaleX Enterprise como administrador.</span><span class="sxs-lookup"><span data-stu-id="449e4-185">To configure single sign-on on **ScaleX Enterprise** side, login to the ScaleX Enterprise company website as an administrator.</span></span>

9. <span data-ttu-id="449e4-186">Clique no menu na parte superior direita e selecione **Administração do Contoso**.</span><span class="sxs-lookup"><span data-stu-id="449e4-186">Click the menu in the upper right and select **Contoso Administration**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="449e4-187">Contoso é apenas um exemplo.</span><span class="sxs-lookup"><span data-stu-id="449e4-187">Contoso is just an example.</span></span> <span data-ttu-id="449e4-188">Esse deve ser o Nome real de sua Empresa.</span><span class="sxs-lookup"><span data-stu-id="449e4-188">This should be your actual Company Name.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-scalexenterprise-tutorial/Test_Admin.png) 

10. <span data-ttu-id="449e4-190">Selecione **Integrações** no menu superior e, em seguida, **Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="449e4-190">Select **Integrations** from the top menu and select **Single Sign-On**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-scalexenterprise-tutorial/admin_sso.png) 

11. <span data-ttu-id="449e4-192">Preencha o formulário da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="449e4-192">Complete the form as follows:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-scalexenterprise-tutorial/scalex_admin_save.png) 
    
    <span data-ttu-id="449e4-194">a.</span><span class="sxs-lookup"><span data-stu-id="449e4-194">a.</span></span> <span data-ttu-id="449e4-195">Selecione **“Criar qualquer usuário que pode se autenticar com o SSO”.**</span><span class="sxs-lookup"><span data-stu-id="449e4-195">Select **“Create any user who can authenticate with SSO.”**</span></span>

    <span data-ttu-id="449e4-196">b.</span><span class="sxs-lookup"><span data-stu-id="449e4-196">b.</span></span> <span data-ttu-id="449e4-197">**SAML do Provedor de Serviços**: cole o valor ***urn:oasis:names:tc:SAML:2.0:nameid-format:persistent***</span><span class="sxs-lookup"><span data-stu-id="449e4-197">**Service Provider saml**: Paste the value ***urn:oasis:names:tc:SAML:2.0:nameid-format:persistent***</span></span>

    <span data-ttu-id="449e4-198">c.</span><span class="sxs-lookup"><span data-stu-id="449e4-198">c.</span></span> <span data-ttu-id="449e4-199">**Nome do campo de email do Provedor de Identidade na resposta do ACS**: cole o valor `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span><span class="sxs-lookup"><span data-stu-id="449e4-199">**Name of Identity Provider email field in ACS response**: Paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span></span>

    <span data-ttu-id="449e4-200">d.</span><span class="sxs-lookup"><span data-stu-id="449e4-200">d.</span></span> <span data-ttu-id="449e4-201">**ID de Entidade do EntityDescriptor do Provedor de Identidade:** cole o valor de **ID de Entidade SAML** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="449e4-201">**Identity Provider EntityDescriptor Entity ID:** Paste the **SAML Entity ID** value copied from the Azure portal.</span></span>

    <span data-ttu-id="449e4-202">e.</span><span class="sxs-lookup"><span data-stu-id="449e4-202">e.</span></span> <span data-ttu-id="449e4-203">**URL do SingleSignOnService do Provedor de Identidade:** cole a **URL de Serviço de Logon Único do SAML** do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="449e4-203">**Identity Provider SingleSignOnService URL:** Paste the **SAML Single Sign-On Service URL** from the Azure portal.</span></span>

    <span data-ttu-id="449e4-204">f.</span><span class="sxs-lookup"><span data-stu-id="449e4-204">f.</span></span> <span data-ttu-id="449e4-205">**Certificado X509 público do Provedor de Identidade:** abra o certificado X509 baixado do Azure no bloco de notas e cole o conteúdo nesta caixa.</span><span class="sxs-lookup"><span data-stu-id="449e4-205">**Identity Provider public X509 certificate:** Open the X509 certificate downloaded from the Azure in notepad and paste the contents in this box.</span></span> <span data-ttu-id="449e4-206">Verifique se não há quebras de linha no meio do conteúdo do certificado.</span><span class="sxs-lookup"><span data-stu-id="449e4-206">Ensure there are no line breaks in the middle of the certificate contents.</span></span>
    
    <span data-ttu-id="449e4-207">g.</span><span class="sxs-lookup"><span data-stu-id="449e4-207">g.</span></span> <span data-ttu-id="449e4-208">Marque as seguintes caixas de seleção: **Habilitado, Criptografar NameID e Assinar AuthnRequests.**</span><span class="sxs-lookup"><span data-stu-id="449e4-208">Check the following checkboxes: **Enabled, Encrypt NameID and Sign AuthnRequests.**</span></span>

    <span data-ttu-id="449e4-209">h.</span><span class="sxs-lookup"><span data-stu-id="449e4-209">h.</span></span> <span data-ttu-id="449e4-210">Clique em **Atualizar Configurações de SSO** para salvar as configurações.</span><span class="sxs-lookup"><span data-stu-id="449e4-210">Click **Update SSO Settings** to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="449e4-211">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="449e4-211">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="449e4-212">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="449e4-212">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="449e4-213">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="449e4-213">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="449e4-214">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="449e4-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="449e4-215">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="449e4-215">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="449e4-217">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="449e4-217">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="449e4-218">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="449e4-218">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="449e4-220">Vá para **usuários e grupos** e clique em **todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="449e4-220">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="449e4-222">Na parte superior da caixa de diálogo, clique em **Adicionar** para abrir a caixa de diálogo **Usuário**.</span><span class="sxs-lookup"><span data-stu-id="449e4-222">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="449e4-224">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="449e4-224">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="449e4-226">a.</span><span class="sxs-lookup"><span data-stu-id="449e4-226">a.</span></span> <span data-ttu-id="449e4-227">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="449e4-227">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="449e4-228">b.</span><span class="sxs-lookup"><span data-stu-id="449e4-228">b.</span></span> <span data-ttu-id="449e4-229">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="449e4-229">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="449e4-230">c.</span><span class="sxs-lookup"><span data-stu-id="449e4-230">c.</span></span> <span data-ttu-id="449e4-231">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="449e4-231">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="449e4-232">d.</span><span class="sxs-lookup"><span data-stu-id="449e4-232">d.</span></span> <span data-ttu-id="449e4-233">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="449e4-233">Click **Create**.</span></span>
 
### <a name="creating-a-scalex-enterprise-test-user"></a><span data-ttu-id="449e4-234">Criando um usuário de teste do ScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="449e4-234">Creating a ScaleX Enterprise test user</span></span>

<span data-ttu-id="449e4-235">Para permitir que os usuários do Azure AD façam logon no ScaleX Enterprise, eles devem ser provisionados no ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="449e4-235">To enable Azure AD users to log in to ScaleX Enterprise, they must be provisioned in to ScaleX Enterprise.</span></span> <span data-ttu-id="449e4-236">No caso do ScaleX Enterprise, o provisionamento é uma tarefa automática e nenhuma etapa manual é necessária.</span><span class="sxs-lookup"><span data-stu-id="449e4-236">In the case of ScaleX Enterprise, provisioning is an automatic task and no manual steps are required.</span></span> <span data-ttu-id="449e4-237">Qualquer usuário que pode se autenticar com êxito com as credenciais de SSO será provisionado automaticamente no ScaleX.</span><span class="sxs-lookup"><span data-stu-id="449e4-237">Any user who can successfully authenticate with SSO credentials will be automatically provisioned on the ScaleX side.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="449e4-238">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="449e4-238">Assigning the Azure AD test user</span></span>

<span data-ttu-id="449e4-239">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso do usuário ao ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="449e4-239">In this section, you enable Britta Simon to use Azure single sign-on by granting user access to ScaleX Enterprise.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="449e4-241">**Para atribuir Brenda Fernandes ao ScaleX Enterprise, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="449e4-241">**To assign Britta Simon to ScaleX Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="449e4-242">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="449e4-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="449e4-244">Na lista de aplicativos, selecione **ScaleX Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="449e4-244">In the applications list, select **ScaleX Enterprise**.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_app.png) 

3. <span data-ttu-id="449e4-246">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="449e4-246">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="449e4-248">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="449e4-248">Click **Add** button.</span></span> <span data-ttu-id="449e4-249">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="449e4-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="449e4-251">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="449e4-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="449e4-252">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="449e4-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="449e4-253">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="449e4-253">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="449e4-254">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="449e4-254">Testing single sign-on</span></span>

<span data-ttu-id="449e4-255">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="449e4-255">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="449e4-256">Clique no bloco ScaleX Enterprise no Painel de Acesso e você será automaticamente conectado ao aplicativo ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="449e4-256">Click the ScaleX Enterprise tile in the Access Panel, you will get automatically signed-on to your ScaleX Enterprise application.</span></span> <span data-ttu-id="449e4-257">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="449e4-257">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="449e4-258">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="449e4-258">Additional resources</span></span>

* [<span data-ttu-id="449e4-259">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="449e4-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="449e4-260">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="449e4-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_203.png

