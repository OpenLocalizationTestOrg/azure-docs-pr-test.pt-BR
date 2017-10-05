---
title: "Tutorial: integração do Azure Active Directory ao Pluralsight | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Pluralsight."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4c3f07d2-4e1f-4ea3-9025-c663f1f2b7b4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 62429643a108665544e42001d264046b5db1ec97
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pluralsight"></a><span data-ttu-id="5c3fd-103">Tutorial: Integração do Azure Active Directory com o Pluralsight</span><span class="sxs-lookup"><span data-stu-id="5c3fd-103">Tutorial: Azure Active Directory integration with Pluralsight</span></span>

<span data-ttu-id="5c3fd-104">Neste tutorial, você aprenderá como integrar o Pluralsight ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="5c3fd-104">In this tutorial, you learn how to integrate Pluralsight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5c3fd-105">A integração do Pluralsight ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="5c3fd-105">Integrating Pluralsight with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5c3fd-106">No AD do Azure, você poderá controlar quem tem acesso ao Pluralsight</span><span class="sxs-lookup"><span data-stu-id="5c3fd-106">You can control in Azure AD who has access to Pluralsight</span></span>
- <span data-ttu-id="5c3fd-107">Você pode permitir que seus usuários façam logon automaticamente no Pluralsight (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5c3fd-107">You can enable your users to automatically get signed-on to Pluralsight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5c3fd-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5c3fd-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5c3fd-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5c3fd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c3fd-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5c3fd-110">Prerequisites</span></span>

<span data-ttu-id="5c3fd-111">Para configurar a integração do AD do Azure com o Pluralsight, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="5c3fd-111">To configure Azure AD integration with Pluralsight, you need the following items:</span></span>

- <span data-ttu-id="5c3fd-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5c3fd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5c3fd-113">Uma assinatura habilitada para logon único do Pluralsight</span><span class="sxs-lookup"><span data-stu-id="5c3fd-113">A Pluralsight single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5c3fd-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5c3fd-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="5c3fd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5c3fd-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5c3fd-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5c3fd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5c3fd-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="5c3fd-118">Scenario description</span></span>
<span data-ttu-id="5c3fd-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5c3fd-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="5c3fd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5c3fd-121">Como adicionar o Pluralsight da galeria</span><span class="sxs-lookup"><span data-stu-id="5c3fd-121">Adding Pluralsight from the gallery</span></span>
2. <span data-ttu-id="5c3fd-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5c3fd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pluralsight-from-the-gallery"></a><span data-ttu-id="5c3fd-123">Como adicionar o Pluralsight da galeria</span><span class="sxs-lookup"><span data-stu-id="5c3fd-123">Adding Pluralsight from the gallery</span></span>
<span data-ttu-id="5c3fd-124">Para configurar a integração do Pluralsight ao AD do Azure, você precisará adicionar o Pluralsight da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-124">To configure the integration of Pluralsight into Azure AD, you need to add Pluralsight from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5c3fd-125">**Para adicionar o Pluralsight por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="5c3fd-125">**To add Pluralsight from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5c3fd-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5c3fd-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5c3fd-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="5c3fd-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="5c3fd-133">Na caixa de pesquisa, digite **Pluralsight**.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-133">In the search box, type **Pluralsight**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_search.png)

5. <span data-ttu-id="5c3fd-135">No painel de resultados, selecione **Pluralsight** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-135">In the results panel, select **Pluralsight**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5c3fd-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5c3fd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5c3fd-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Pluralsight, com base em uma usuária de teste chamada "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="5c3fd-138">In this section, you configure and test Azure AD single sign-on with Pluralsight based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5c3fd-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Pluralsight é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Pluralsight is to a user in Azure AD.</span></span> <span data-ttu-id="5c3fd-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-140">In other words, a link relationship between an Azure AD user and the related user in Pluralsight needs to be established.</span></span>

<span data-ttu-id="5c3fd-141">No Pluralsight, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-141">In Pluralsight, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5c3fd-142">Para configurar e testar o logon único do AD do Azure com o Pluralsight, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="5c3fd-142">To configure and test Azure AD single sign-on with Pluralsight, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5c3fd-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5c3fd-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5c3fd-145">**[Criação de um usuário de teste do Pluralsight](#creating-a-pluralsight-test-user)** – para ter um equivalente de Brenda Fernandes no Pluralsight que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-145">**[Creating a Pluralsight test user](#creating-a-pluralsight-test-user)** - to have a counterpart of Britta Simon in Pluralsight that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5c3fd-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5c3fd-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5c3fd-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c3fd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5c3fd-149">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único em seu aplicativo Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Pluralsight application.</span></span>

<span data-ttu-id="5c3fd-150">**Para configurar o logon único do AD do Azure com o Pluralsight, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="5c3fd-150">**To configure Azure AD single sign-on with Pluralsight, perform the following steps:**</span></span>

1. <span data-ttu-id="5c3fd-151">No Portal do Azure, na página de integração de aplicativos do **Pluralsight**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-151">In the Azure portal, on the **Pluralsight** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="5c3fd-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_samlbase.png)

3. <span data-ttu-id="5c3fd-155">Na seção **URLs e Domínio do Pluralsight**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="5c3fd-155">On the **Pluralsight Domain and URLs** section, perform the following:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_url.png)

    <span data-ttu-id="5c3fd-157">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<instance name>.pluralsight.com/sso/<company name>`</span><span class="sxs-lookup"><span data-stu-id="5c3fd-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instance name>.pluralsight.com/sso/<company name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5c3fd-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-158">This value is not real.</span></span> <span data-ttu-id="5c3fd-159">Atualize esse valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="5c3fd-160">Entre em contato com a [equipe de suporte ao cliente do Pluralsight](mailto:support@pluralsight.com) para obter esse valor.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-160">Contact [Pluralsight Client support team](mailto:support@pluralsight.com) to get this value.</span></span> 
 


4. <span data-ttu-id="5c3fd-161">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_certificate.png) 

5. <span data-ttu-id="5c3fd-163">O objetivo desta seção é habilitar o logon único do Azure AD no Portal do Azure e configurar o SSO no aplicativo Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-163">The objective of this section is to enable Azure AD single sign-on in the Azure portal and to configure SSO in the Pluralsight application.</span></span>

    <span data-ttu-id="5c3fd-164">O aplicativo Pluralsight espera as declarações do SAML em um formato específico, o que exige que você adicione mapeamentos de atributo personalizados de acordo com a sua configuração de atributos do token SAML.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-164">The Pluralsight application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="5c3fd-165">A captura de tela a seguir mostra um exemplo disso.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-165">The following screenshot shows an example for this.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_attribute.png)

    >[!NOTE]
    ><span data-ttu-id="5c3fd-167">Também é possível adicionar o atributo **“ID Exclusiva”** com o valor apropriado, como EmployeeID, ou algo que se adapte à sua organização.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-167">You can also add the **"Unique ID"** attribute with the appropriate value like EmployeeID or something else which suits for your organization.</span></span> <span data-ttu-id="5c3fd-168">Observe também que esse não é o atributo obrigatório; no entanto, é possível adicioná-lo para identificar o usuário exclusivo.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-168">Also note that this is not the required attribute; however, you can add it to  identify the unique user.</span></span> 

6. <span data-ttu-id="5c3fd-169">Para adicionar os **atributos de token SAML**necessários, para cada linha mostrada na tabela abaixo, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="5c3fd-169">To add the required **SAML token attributes**, for each row shown in the table below, perform the following steps:</span></span>
   
   | <span data-ttu-id="5c3fd-170">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="5c3fd-170">Attribute Name</span></span> | <span data-ttu-id="5c3fd-171">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="5c3fd-171">Attribute Value</span></span> |
   | ---| --- |
   | <span data-ttu-id="5c3fd-172">Nome</span><span class="sxs-lookup"><span data-stu-id="5c3fd-172">First Name</span></span> |<span data-ttu-id="5c3fd-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="5c3fd-173">user.givenname</span></span> |
   | <span data-ttu-id="5c3fd-174">Sobrenome</span><span class="sxs-lookup"><span data-stu-id="5c3fd-174">Last Name</span></span> |<span data-ttu-id="5c3fd-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="5c3fd-175">user.surname</span></span> |
   | <span data-ttu-id="5c3fd-176">Email</span><span class="sxs-lookup"><span data-stu-id="5c3fd-176">Email</span></span> |<span data-ttu-id="5c3fd-177">user.mail</span><span class="sxs-lookup"><span data-stu-id="5c3fd-177">user.mail</span></span> |
   
   <span data-ttu-id="5c3fd-178">a.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-178">a.</span></span> <span data-ttu-id="5c3fd-179">Clique em **adicionar atributo de usuário** para abrir a caixa de diálogo **Adicionar Atributo de Usuário**.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-179">Click **add user attribute** to open the **Add User Attribure** dialog.</span></span>
    
     ![Configurar Logon Único](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_addattribute.png)
  
   <span data-ttu-id="5c3fd-181">b.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-181">b.</span></span> <span data-ttu-id="5c3fd-182">Na caixa de texto **Nome do Atributo** , digite o nome do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-182">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
  
   <span data-ttu-id="5c3fd-183">c.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-183">c.</span></span> <span data-ttu-id="5c3fd-184">Na lista **Valor do Atributo** , selecione o valor do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-184">From the **Attribute Value** list, select the attribute value shown for that row.</span></span>
  
   <span data-ttu-id="5c3fd-185">d.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-185">d.</span></span> <span data-ttu-id="5c3fd-186">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-186">Click **Ok**.</span></span>    

7. <span data-ttu-id="5c3fd-187">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="5c3fd-187">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-pluralsight-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="5c3fd-189">Para configurar o SSO para seu aplicativo, entre em contato com a equipe de [Serviços Profissionais do Pluralsight](mailTo:professionalservices@pluralsight.com) e forneça o arquivo de metadados baixado.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-189">To get SSO configured for your application, contact [Pluralsight Professional Services](mailTo:professionalservices@pluralsight.com) team and provide the downloaded metadata file.</span></span>

> [!TIP]
> <span data-ttu-id="5c3fd-190">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="5c3fd-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5c3fd-191">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5c3fd-192">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5c3fd-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5c3fd-193">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5c3fd-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="5c3fd-194">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="5c3fd-196">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="5c3fd-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5c3fd-197">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5c3fd-199">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5c3fd-201">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5c3fd-203">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="5c3fd-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5c3fd-205">a.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-205">a.</span></span> <span data-ttu-id="5c3fd-206">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5c3fd-207">b.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-207">b.</span></span> <span data-ttu-id="5c3fd-208">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5c3fd-209">c.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-209">c.</span></span> <span data-ttu-id="5c3fd-210">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5c3fd-211">d.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-211">d.</span></span> <span data-ttu-id="5c3fd-212">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-212">Click **Create**.</span></span>
 
### <a name="creating-a-pluralsight-test-user"></a><span data-ttu-id="5c3fd-213">Criar um usuário de teste do Pluralsight</span><span class="sxs-lookup"><span data-stu-id="5c3fd-213">Creating a Pluralsight test user</span></span>

<span data-ttu-id="5c3fd-214">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-214">The objective of this section is to create a user called Britta Simon in Pluralsight.</span></span> <span data-ttu-id="5c3fd-215">Trabalhe com a [equipe de suporte ao cliente do Pluralsight](mailto:support@pluralsight.com) para adicionar usuários à conta do Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-215">Please work with [Pluralsight Client support team](mailto:support@pluralsight.com) to add the users in the Pluralsight account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5c3fd-216">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5c3fd-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5c3fd-217">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo acesso ao Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Pluralsight.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="5c3fd-219">**Para atribuir Brenda Fernandes ao Pluralsight, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="5c3fd-219">**To assign Britta Simon to Pluralsight, perform the following steps:**</span></span>

1. <span data-ttu-id="5c3fd-220">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="5c3fd-222">Na lista de aplicativos, selecione **Pluralsight**.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-222">In the applications list, select **Pluralsight**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_app.png) 

3. <span data-ttu-id="5c3fd-224">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="5c3fd-226">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-226">Click **Add** button.</span></span> <span data-ttu-id="5c3fd-227">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="5c3fd-229">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5c3fd-230">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5c3fd-231">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5c3fd-232">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="5c3fd-232">Testing single sign-on</span></span>

<span data-ttu-id="5c3fd-233">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-233">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5c3fd-234">Ao clicar no bloco Pluralsight no Painel de Acesso, você deve ser conectado automaticamente ao aplicativo Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="5c3fd-234">When you click the Pluralsight tile in the Access Panel, you should get automatically signed-on to your Pluralsight application.</span></span> <span data-ttu-id="5c3fd-235">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5c3fd-235">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5c3fd-236">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="5c3fd-236">Additional resources</span></span>

* [<span data-ttu-id="5c3fd-237">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="5c3fd-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5c3fd-238">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5c3fd-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_203.png

