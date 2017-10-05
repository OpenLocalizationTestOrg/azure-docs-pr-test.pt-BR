---
title: "Tutorial: Integração do Azure Active Directory ao Blackboard Learn | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Blackboard Learn."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0b8ca505-61ea-487c-9a3e-fa50c936df0c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jeedes
ms.openlocfilehash: c2b7638e99fa46ff41a7f2202bdf0e7a2b017c19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-blackboard-learn"></a><span data-ttu-id="a78c1-103">Tutorial: integração do Azure Active Directory ao Blackboard Learn</span><span class="sxs-lookup"><span data-stu-id="a78c1-103">Tutorial: Azure Active Directory integration with Blackboard Learn</span></span>

<span data-ttu-id="a78c1-104">Neste tutorial, você aprenderá a integrar o Blackboard Learn ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="a78c1-104">In this tutorial, you learn how to integrate Blackboard Learn with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a78c1-105">A integração do Blackboard Learn ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="a78c1-105">Integrating Blackboard Learn with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a78c1-106">Você pode controlar no Azure AD quem tem acesso ao Blackboard Learn</span><span class="sxs-lookup"><span data-stu-id="a78c1-106">You can control in Azure AD who has access to Blackboard Learn</span></span>
- <span data-ttu-id="a78c1-107">Você pode permitir que seus usuários façam logon automaticamente no Blackboard Learn (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a78c1-107">You can enable your users to automatically get signed-on to Blackboard Learn (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a78c1-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a78c1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a78c1-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a78c1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a78c1-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a78c1-110">Prerequisites</span></span>

<span data-ttu-id="a78c1-111">Para configurar a integração do Azure AD ao Blackboard Learn, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="a78c1-111">To configure Azure AD integration with Blackboard Learn, you need the following items:</span></span>

- <span data-ttu-id="a78c1-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a78c1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a78c1-113">Uma assinatura habilitada para logon único do Blackboard Learn</span><span class="sxs-lookup"><span data-stu-id="a78c1-113">A Blackboard Learn single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a78c1-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="a78c1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a78c1-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="a78c1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a78c1-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="a78c1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a78c1-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a78c1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a78c1-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="a78c1-118">Scenario description</span></span>
<span data-ttu-id="a78c1-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="a78c1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a78c1-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="a78c1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a78c1-121">Adicionando o Blackboard Learn da galeria</span><span class="sxs-lookup"><span data-stu-id="a78c1-121">Adding Blackboard Learn from the gallery</span></span>
2. <span data-ttu-id="a78c1-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a78c1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-blackboard-learn-from-the-gallery"></a><span data-ttu-id="a78c1-123">Adicionando o Blackboard Learn da galeria</span><span class="sxs-lookup"><span data-stu-id="a78c1-123">Adding Blackboard Learn from the gallery</span></span>
<span data-ttu-id="a78c1-124">Para configurar a integração do Blackboard Learn ao Azure AD, você precisará adicionar o Blackboard Learn da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="a78c1-124">To configure the integration of Blackboard Learn into Azure AD, you need to add Blackboard Learn from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a78c1-125">**Para adicionar o Blackboard Learn por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a78c1-125">**To add Blackboard Learn from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a78c1-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a78c1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a78c1-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="a78c1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a78c1-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a78c1-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="a78c1-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a78c1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="a78c1-133">Na caixa de pesquisa, digite **Blackboard Learn**.</span><span class="sxs-lookup"><span data-stu-id="a78c1-133">In the search box, type **Blackboard Learn**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_search.png)

5. <span data-ttu-id="a78c1-135">No painel de resultados, selecione **Blackboard Learn** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a78c1-135">In the results panel, select **Blackboard Learn**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a78c1-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a78c1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a78c1-138">Nesta seção, você configura e testa o logon único do Azure AD com o Blackboard Learn, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="a78c1-138">In this section, you configure and test Azure AD single sign-on with Blackboard Learn based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a78c1-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Blackboard Learn é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a78c1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Blackboard Learn is to a user in Azure AD.</span></span> <span data-ttu-id="a78c1-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="a78c1-140">In other words, a link relationship between an Azure AD user and the related user in Blackboard Learn needs to be established.</span></span>

<span data-ttu-id="a78c1-141">Essa relação de vínculo é estabelecida atribuindo o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** no Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="a78c1-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Blackboard Learn.</span></span>

<span data-ttu-id="a78c1-142">Para configurar e testar o logon único do Azure AD o com Blackboard Learn, você precisará realizar as seguintes tarefas básicas:</span><span class="sxs-lookup"><span data-stu-id="a78c1-142">To configure and test Azure AD single sign-on with Blackboard Learn, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a78c1-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="a78c1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a78c1-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="a78c1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a78c1-145">**[Criando um usuário de teste do Blackboard Learn](#creating-a-blackboard-learn-test-user)** – para ter um equivalente de Brenda Fernandes no Blackboard Learn que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a78c1-145">**[Creating a Blackboard Learn test user](#creating-a-blackboard-learn-test-user)** - to have a counterpart of Britta Simon in Blackboard Learn that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a78c1-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="a78c1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a78c1-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="a78c1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a78c1-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a78c1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a78c1-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="a78c1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Blackboard Learn application.</span></span>

<span data-ttu-id="a78c1-150">**Para configurar o logon único do Azure AD com o Blackboard Learn, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a78c1-150">**To configure Azure AD single sign-on with Blackboard Learn, perform the following steps:**</span></span>

1. <span data-ttu-id="a78c1-151">No portal do Azure, na página de integração do aplicativo do **Blackboard Learn**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="a78c1-151">In the Azure portal, on the **Blackboard Learn** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="a78c1-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="a78c1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_samlbase.png)

3. <span data-ttu-id="a78c1-155">Na seção **Domínio e URLs do Blackboard Learn**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="a78c1-155">On the **Blackboard Learn Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_url.png)

    <span data-ttu-id="a78c1-157">a.</span><span class="sxs-lookup"><span data-stu-id="a78c1-157">a.</span></span> <span data-ttu-id="a78c1-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<subdomain>.blackboard.com/`</span><span class="sxs-lookup"><span data-stu-id="a78c1-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.blackboard.com/`</span></span>

    <span data-ttu-id="a78c1-159">b.</span><span class="sxs-lookup"><span data-stu-id="a78c1-159">b.</span></span> <span data-ttu-id="a78c1-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span><span class="sxs-lookup"><span data-stu-id="a78c1-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="a78c1-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="a78c1-161">These values are not real.</span></span> <span data-ttu-id="a78c1-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="a78c1-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a78c1-163">Contate a [equipe de suporte ao Cliente do Blackboard Learn](https://www.blackboard.com/support/index.aspx) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="a78c1-163">Contact [Blackboard Learn Client support team](https://www.blackboard.com/support/index.aspx) to get these values.</span></span> 

4. <span data-ttu-id="a78c1-164">O aplicativo Blackboard Learn espera que as declarações SAML estejam em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="a78c1-164">Blackboard Learn application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="a78c1-165">Configure as declarações a seguir para este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a78c1-165">Configure the following claims for this application.</span></span> <span data-ttu-id="a78c1-166">Você pode gerenciar os valores desses atributos da seção **Atributos de Usuário** na página de integração de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="a78c1-166">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span>
 <span data-ttu-id="a78c1-167">A captura de tela a seguir mostra um exemplo disso.</span><span class="sxs-lookup"><span data-stu-id="a78c1-167">The following screenshot shows an example about it.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute.png)

5. <span data-ttu-id="a78c1-169">Na seção **Atributos de Usuário** da caixa de diálogo **Logon único**, configure o atributo do token SAML, conforme mostrado na imagem e realize as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="a78c1-169">In the **User Attributes** section on **Single sign-on** dialog, configure SAML token attributes as shown in the image and perform the following steps.</span></span> <span data-ttu-id="a78c1-170">Mapeamos o Userprincipalname como o atributo de usuário único aqui, mas você pode mapeá-la para o valor apropriado, que distingue exclusivamente o usuário na organização e que é mapeado para o campo de nome de usuário do Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="a78c1-170">We have mapped the Userprincipalname as the unique user attribute here but you can map it to the appropriate value, which uniquely distinguishes the user in the organization and that maps to Blackboard Learn username field.</span></span>
           
    | <span data-ttu-id="a78c1-171">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="a78c1-171">Attribute Name</span></span> | <span data-ttu-id="a78c1-172">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="a78c1-172">Attribute Value</span></span> |   
    | ---------------| ----------------|
    | <span data-ttu-id="a78c1-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span><span class="sxs-lookup"><span data-stu-id="a78c1-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span></span> |<span data-ttu-id="a78c1-174">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="a78c1-174">user.userprincipalname</span></span> |

    <span data-ttu-id="a78c1-175">a.</span><span class="sxs-lookup"><span data-stu-id="a78c1-175">a.</span></span> <span data-ttu-id="a78c1-176">Clique em **Adicionar atributo** para abrir o diálogo **Adicionar Atributo**.</span><span class="sxs-lookup"><span data-stu-id="a78c1-176">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute_04.png)
    
    ![Configurar Logon Único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="a78c1-179">b.</span><span class="sxs-lookup"><span data-stu-id="a78c1-179">b.</span></span> <span data-ttu-id="a78c1-180">Na caixa de texto **Nome** , digite o nome do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="a78c1-180">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="a78c1-181">c.</span><span class="sxs-lookup"><span data-stu-id="a78c1-181">c.</span></span> <span data-ttu-id="a78c1-182">Na lista **Valor**, digite o valor do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="a78c1-182">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="a78c1-183">d.</span><span class="sxs-lookup"><span data-stu-id="a78c1-183">d.</span></span> <span data-ttu-id="a78c1-184">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="a78c1-184">Click **Ok**.</span></span>

4. <span data-ttu-id="a78c1-185">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo XML em seu computador.</span><span class="sxs-lookup"><span data-stu-id="a78c1-185">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_certificate.png)

7. <span data-ttu-id="a78c1-187">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="a78c1-187">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="a78c1-189">Na seção **Configuração do Blackboard Learn**, clique em **Configurar o Blackboard Learn** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="a78c1-189">On the **Blackboard Learn Configuration** section, click **Configure Blackboard Learn** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a78c1-190">Copie a **ID da Entidade SAML** da **seção Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="a78c1-190">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_configure.png) 

9. <span data-ttu-id="a78c1-192">Para configurar o logon único no lado do **Blackboard Learn**, é necessário enviar o **XML de Metadados** baixado e a **ID da Entidade SAML** para o [suporte do Blackboard Learn](https://www.blackboard.com/support/index.aspx).</span><span class="sxs-lookup"><span data-stu-id="a78c1-192">To configure single sign-on on **Blackboard Learn** side, you need to send the downloaded **Metadata XML** and **SAML Entity ID** to [Blackboard Learn support](https://www.blackboard.com/support/index.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="a78c1-193">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="a78c1-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a78c1-194">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="a78c1-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a78c1-195">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a78c1-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a78c1-196">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a78c1-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="a78c1-197">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="a78c1-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="a78c1-199">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a78c1-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a78c1-200">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a78c1-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a78c1-202">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="a78c1-202">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a78c1-204">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a78c1-204">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a78c1-206">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="a78c1-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a78c1-208">a.</span><span class="sxs-lookup"><span data-stu-id="a78c1-208">a.</span></span> <span data-ttu-id="a78c1-209">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="a78c1-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a78c1-210">b.</span><span class="sxs-lookup"><span data-stu-id="a78c1-210">b.</span></span> <span data-ttu-id="a78c1-211">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="a78c1-211">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="a78c1-212">c.</span><span class="sxs-lookup"><span data-stu-id="a78c1-212">c.</span></span> <span data-ttu-id="a78c1-213">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="a78c1-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a78c1-214">d.</span><span class="sxs-lookup"><span data-stu-id="a78c1-214">d.</span></span> <span data-ttu-id="a78c1-215">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a78c1-215">Click **Create**.</span></span>
 
### <a name="creating-a-blackboard-learn-test-user"></a><span data-ttu-id="a78c1-216">Criando um usuário de teste do Blackboard Learn</span><span class="sxs-lookup"><span data-stu-id="a78c1-216">Creating a Blackboard Learn test user</span></span>
<span data-ttu-id="a78c1-217">Nesta seção, você deve criar um usuário chamado Brenda Fernandes no Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="a78c1-217">In this section, you create a user called Britta Simon in Blackboard Learn.</span></span> 

<span data-ttu-id="a78c1-218">O aplicativo Blackboard Learn dá suporte a provisionamento de usuários imediato.</span><span class="sxs-lookup"><span data-stu-id="a78c1-218">Blackboard Learn application support just in time user provisioning.</span></span> <span data-ttu-id="a78c1-219">Configure as declarações, conforme descrito na seção **[Configurando o Logon Único do Azure AD](#configuring-azure-ad-single-sign-on)**</span><span class="sxs-lookup"><span data-stu-id="a78c1-219">Make sure that you have configured the claims as described in the section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**</span></span>
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a78c1-220">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a78c1-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a78c1-221">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="a78c1-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Blackboard Learn.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="a78c1-223">**Para atribuir Brenda Fernandes ao Blackboard Learn, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a78c1-223">**To assign Britta Simon to Blackboard Learn, perform the following steps:**</span></span>

1. <span data-ttu-id="a78c1-224">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a78c1-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="a78c1-226">Na lista de aplicativos, selecione **Blackboard Learn**.</span><span class="sxs-lookup"><span data-stu-id="a78c1-226">In the applications list, select **Blackboard Learn**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_app.png) 

3. <span data-ttu-id="a78c1-228">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="a78c1-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="a78c1-230">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a78c1-230">Click **Add** button.</span></span> <span data-ttu-id="a78c1-231">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a78c1-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="a78c1-233">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="a78c1-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a78c1-234">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a78c1-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a78c1-235">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a78c1-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a78c1-236">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="a78c1-236">Testing single sign-on</span></span>

<span data-ttu-id="a78c1-237">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="a78c1-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a78c1-238">Quando você clicar no bloco Blackboard Learn no Painel de Acesso, deverá ser automaticamente conectado ao aplicativo Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="a78c1-238">When you click the Blackboard Learn tile in the Access Panel, you should get automatically signed-on to your Blackboard Learn application.</span></span> <span data-ttu-id="a78c1-239">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a78c1-239">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a78c1-240">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="a78c1-240">Additional resources</span></span>

* [<span data-ttu-id="a78c1-241">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="a78c1-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a78c1-242">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a78c1-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_203.png

