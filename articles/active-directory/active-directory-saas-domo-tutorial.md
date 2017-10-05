---
title: "Tutorial: integração do Azure Active Directory ao Domo | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Domo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 058626e4-73b3-4dc2-86ca-b060d002d70a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/11/2017
ms.author: jeedes
ms.openlocfilehash: 919d2262cf9f14159a13370037301005b5b69da2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-domo"></a><span data-ttu-id="46641-103">Tutorial: Integração do Azure Active Directory ao Domo</span><span class="sxs-lookup"><span data-stu-id="46641-103">Tutorial: Azure Active Directory integration with Domo</span></span>

<span data-ttu-id="46641-104">Neste tutorial, você aprende a integrar o Domo ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="46641-104">In this tutorial, you learn how to integrate Domo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="46641-105">A integração do Domo ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="46641-105">Integrating Domo with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="46641-106">No Azure AD, é possível controlar quem tem acesso ao Domo</span><span class="sxs-lookup"><span data-stu-id="46641-106">You can control in Azure AD who has access to Domo</span></span>
- <span data-ttu-id="46641-107">Você pode permitir que usuários façam logon automaticamente no Domo (Logon Único) com as respectivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="46641-107">You can enable your users to automatically get signed-on to Domo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="46641-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="46641-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="46641-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="46641-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="46641-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="46641-110">Prerequisites</span></span>

<span data-ttu-id="46641-111">Para configurar a integração do Azure AD ao Domo, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="46641-111">To configure Azure AD integration with Domo, you need the following items:</span></span>

- <span data-ttu-id="46641-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="46641-112">An Azure AD subscription</span></span>
- <span data-ttu-id="46641-113">Uma assinatura habilitada para logon único do Domo</span><span class="sxs-lookup"><span data-stu-id="46641-113">A Domo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="46641-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="46641-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="46641-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="46641-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="46641-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="46641-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="46641-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="46641-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="46641-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="46641-118">Scenario description</span></span>
<span data-ttu-id="46641-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="46641-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="46641-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="46641-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="46641-121">Adição do Domo a partir da galeria</span><span class="sxs-lookup"><span data-stu-id="46641-121">Adding Domo from the gallery</span></span>
2. <span data-ttu-id="46641-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="46641-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-domo-from-the-gallery"></a><span data-ttu-id="46641-123">Adição do Domo a partir da galeria</span><span class="sxs-lookup"><span data-stu-id="46641-123">Adding Domo from the gallery</span></span>
<span data-ttu-id="46641-124">Para configurar a integração do Domo ao Azure AD, você precisará adicionar o Domo da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="46641-124">To configure the integration of Domo into Azure AD, you need to add Domo from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="46641-125">**Para adicionar o Domo da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="46641-125">**To add Domo from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="46641-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="46641-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="46641-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="46641-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="46641-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="46641-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="46641-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46641-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="46641-133">Na caixa de pesquisa, digite **Domo**.</span><span class="sxs-lookup"><span data-stu-id="46641-133">In the search box, type **Domo**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-domo-tutorial/tutorial_domo_search.png)

5. <span data-ttu-id="46641-135">No painel de resultados, selecione **Domo** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46641-135">In the results panel, select **Domo**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-domo-tutorial/tutorial_domo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="46641-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="46641-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="46641-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Domo com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="46641-138">In this section, you configure and test Azure AD single sign-on with Domo based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="46641-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Domo é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="46641-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Domo is to a user in Azure AD.</span></span> <span data-ttu-id="46641-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Domo.</span><span class="sxs-lookup"><span data-stu-id="46641-140">In other words, a link relationship between an Azure AD user and the related user in Domo needs to be established.</span></span>

<span data-ttu-id="46641-141">No Domo, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="46641-141">In Domo, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="46641-142">Para configurar e testar o logon único do Azure AD com o Domo, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="46641-142">To configure and test Azure AD single sign-on with Domo, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="46641-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="46641-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="46641-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="46641-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="46641-145">**[Criação de um usuário de teste do Domo](#creating-a-domo-test-user)** – para ter um equivalente de Brenda Fernandes no Domo que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="46641-145">**[Creating a Domo test user](#creating-a-domo-test-user)** - to have a counterpart of Britta Simon in Domo that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="46641-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="46641-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="46641-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="46641-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="46641-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="46641-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="46641-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Domo.</span><span class="sxs-lookup"><span data-stu-id="46641-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Domo application.</span></span>

<span data-ttu-id="46641-150">**Para configurar o logon único do Azure AD com o Domo, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="46641-150">**To configure Azure AD single sign-on with Domo, perform the following steps:**</span></span>

1. <span data-ttu-id="46641-151">No portal do Azure, na página de integração de aplicativos do **Domo**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="46641-151">In the Azure portal, on the **Domo** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="46641-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="46641-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-domo-tutorial/tutorial_domo_samlbase.png)

3. <span data-ttu-id="46641-155">Na seção **URLs e Domínio do Domo**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="46641-155">On the **Domo Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-domo-tutorial/tutorial_domo_url.png)

    <span data-ttu-id="46641-157">a.</span><span class="sxs-lookup"><span data-stu-id="46641-157">a.</span></span> <span data-ttu-id="46641-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<companyname>.domo.com`</span><span class="sxs-lookup"><span data-stu-id="46641-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.domo.com`</span></span>

    <span data-ttu-id="46641-159">b.</span><span class="sxs-lookup"><span data-stu-id="46641-159">b.</span></span> <span data-ttu-id="46641-160">Na caixa de texto **Identificador**, digite uma URL usando os seguintes padrões:</span><span class="sxs-lookup"><span data-stu-id="46641-160">In the **Identifier** textbox, type a URL using the following patterns:</span></span>     

    | |
    |--|    
    | `https://<companyname>.domo.com` |
    | `https://<companyname>.beta.domo.com` |
    | `https://<companyname>.demo.domo.com` |
    | `https://<companyname>.dev.domo.com` | 
    | `https://<companyname>.fastage1.domo.com` |       
    | `https://<companyname>.frdev.domo.com` |       
    | `https://<companyname>.gastage.domo.com` |       
    | `https://<companyname>.load.domo.com` |       
    | `https://<companyname>.local.domo.com` |       
    | `https://<companyname>.qa.domo.com` |
    | `https://<companyname>.stage.domo.com` |
    
    > [!NOTE] 
    > <span data-ttu-id="46641-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="46641-161">These values are not real.</span></span> <span data-ttu-id="46641-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="46641-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="46641-163">Contate a [equipe de suporte ao Cliente do Domo](mailto:support@domo.com) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="46641-163">Contact [Domo Client support team](mailto:support@domo.com) to get these values.</span></span>

4. <span data-ttu-id="46641-164">O aplicativo Domo espera que as declarações SAML estejam em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="46641-164">Domo application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="46641-165">Configure as declarações a seguir para este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46641-165">Configure the following claims for this application.</span></span> <span data-ttu-id="46641-166">Você pode gerenciar os valores desses atributos da seção "**Atributos de Usuário**" na página de integração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46641-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="46641-167">A captura de tela a seguir mostra um exemplo dessa configuração.</span><span class="sxs-lookup"><span data-stu-id="46641-167">The following screenshot shows an example for this configuration.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-domo-tutorial/tutorial_domo_attributes.png)
    
5. <span data-ttu-id="46641-169">Na seção **Atributos do Usuário**, na caixa de diálogo **Logon único**, configure o atributo do token SAML como mostra a imagem e execute as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="46641-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="46641-170">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="46641-170">Attribute Name</span></span> | <span data-ttu-id="46641-171">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="46641-171">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="46641-172">name</span><span class="sxs-lookup"><span data-stu-id="46641-172">name</span></span> | <span data-ttu-id="46641-173">user.displayname</span><span class="sxs-lookup"><span data-stu-id="46641-173">user.displayname</span></span> |
    | <span data-ttu-id="46641-174">email</span><span class="sxs-lookup"><span data-stu-id="46641-174">email</span></span> | <span data-ttu-id="46641-175">user.mail</span><span class="sxs-lookup"><span data-stu-id="46641-175">user.mail</span></span> |
    
    <span data-ttu-id="46641-176">a.</span><span class="sxs-lookup"><span data-stu-id="46641-176">a.</span></span> <span data-ttu-id="46641-177">Clique em **Adicionar atributo** para abrir o diálogo **Adicionar Atributo**.</span><span class="sxs-lookup"><span data-stu-id="46641-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-domo-tutorial/tutorial_attribute_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-domo-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="46641-180">b.</span><span class="sxs-lookup"><span data-stu-id="46641-180">b.</span></span> <span data-ttu-id="46641-181">Na caixa de texto **Nome** , digite o nome do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="46641-181">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="46641-182">c.</span><span class="sxs-lookup"><span data-stu-id="46641-182">c.</span></span> <span data-ttu-id="46641-183">Na lista **Valor**, digite o valor do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="46641-183">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="46641-184">d.</span><span class="sxs-lookup"><span data-stu-id="46641-184">d.</span></span> <span data-ttu-id="46641-185">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="46641-185">Click **Ok**.</span></span> 
 
6. <span data-ttu-id="46641-186">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="46641-186">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-domo-tutorial/tutorial_domo_certificate.png) 

7. <span data-ttu-id="46641-188">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="46641-188">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-domo-tutorial/tutorial_general_400.png)


8. <span data-ttu-id="46641-190">Na seção **Configuração do Domo**, clique em **Configurar Domo** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="46641-190">On the **Domo Configuration** section, click **Configure Domo** to open **Configure sign-on** window.</span></span> <span data-ttu-id="46641-191">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="46641-191">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>   

   ![Configurar Logon Único](./media/active-directory-saas-domo-tutorial/tutorial_domo_configure.png) 

9. <span data-ttu-id="46641-193">Para configurar o logon único no lado do **Domo**, é necessário enviar o **Certificado** baixado, a **ID da Entidade do SAML**, a **URL de Serviço de Logon Único do SAML** e a **URL de Logoff** à [equipe de suporte do Domo](mailto:support@domo.com).</span><span class="sxs-lookup"><span data-stu-id="46641-193">To configure single sign-on on **Domo** side, you need to send the downloaded **Certificate**, **SAML Entity ID**, the **SAML Single Sign-On Service URL** and the **Sign-Out URL** to [Domo support team](mailto:support@domo.com).</span></span> <span data-ttu-id="46641-194">Eles definem essa configuração para ter a conexão de SSO do SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="46641-194">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="46641-195">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="46641-195">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="46641-196">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="46641-196">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="46641-197">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="46641-197">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="46641-198">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="46641-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="46641-199">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="46641-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="46641-201">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="46641-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="46641-202">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="46641-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-domo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="46641-204">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="46641-204">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-domo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="46641-206">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="46641-206">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-domo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="46641-208">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="46641-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-domo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="46641-210">a.</span><span class="sxs-lookup"><span data-stu-id="46641-210">a.</span></span> <span data-ttu-id="46641-211">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="46641-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="46641-212">b.</span><span class="sxs-lookup"><span data-stu-id="46641-212">b.</span></span> <span data-ttu-id="46641-213">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="46641-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="46641-214">c.</span><span class="sxs-lookup"><span data-stu-id="46641-214">c.</span></span> <span data-ttu-id="46641-215">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="46641-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="46641-216">d.</span><span class="sxs-lookup"><span data-stu-id="46641-216">d.</span></span> <span data-ttu-id="46641-217">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="46641-217">Click **Create**.</span></span>
 
### <a name="creating-a-domo-test-user"></a><span data-ttu-id="46641-218">Criação de um usuário de teste do Domo</span><span class="sxs-lookup"><span data-stu-id="46641-218">Creating a Domo test user</span></span>

<span data-ttu-id="46641-219">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no Domo.</span><span class="sxs-lookup"><span data-stu-id="46641-219">The objective of this section is to create a user called Britta Simon in Domo.</span></span> <span data-ttu-id="46641-220">O Domo dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="46641-220">Domo supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="46641-221">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="46641-221">There is no action item for you in this section.</span></span> <span data-ttu-id="46641-222">Um novo usuário é criado durante uma tentativa de acessar o Domo, caso ele ainda não exista.</span><span class="sxs-lookup"><span data-stu-id="46641-222">A new user is created during an attempt to access Domo if it doesn't exist yet.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="46641-223">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="46641-223">Assigning the Azure AD test user</span></span>

<span data-ttu-id="46641-224">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Domo.</span><span class="sxs-lookup"><span data-stu-id="46641-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Domo.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="46641-226">**Para atribuir Brenda Fernandes ao Domo, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="46641-226">**To assign Britta Simon to Domo, perform the following steps:**</span></span>

1. <span data-ttu-id="46641-227">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="46641-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="46641-229">Na lista de aplicativos, escolha **Domo**.</span><span class="sxs-lookup"><span data-stu-id="46641-229">In the applications list, select **Domo**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-domo-tutorial/tutorial_domo_app.png) 

3. <span data-ttu-id="46641-231">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="46641-231">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="46641-233">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="46641-233">Click **Add** button.</span></span> <span data-ttu-id="46641-234">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="46641-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="46641-236">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="46641-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="46641-237">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="46641-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="46641-238">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="46641-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="46641-239">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="46641-239">Testing single sign-on</span></span>

<span data-ttu-id="46641-240">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="46641-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
<span data-ttu-id="46641-241">Quando você clicar no bloco Domo no Painel de Acesso, deverá fazer logon automaticamente no seu aplicativo Domo.</span><span class="sxs-lookup"><span data-stu-id="46641-241">When you click the Domo tile in the Access Panel, you should get automatically signed-on to your Domo application.</span></span>

<span data-ttu-id="46641-242">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="46641-242">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="46641-243">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="46641-243">Additional resources</span></span>

* [<span data-ttu-id="46641-244">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="46641-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="46641-245">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="46641-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-domo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-domo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-domo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-domo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-domo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-domo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-domo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-domo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-domo-tutorial/tutorial_general_203.png

