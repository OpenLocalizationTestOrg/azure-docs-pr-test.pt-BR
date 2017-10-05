---
title: "Tutorial: Integração do Azure Active Directory com a SAP HANA Cloud Platform | Autenticação de Identidade | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e a Autenticação de Identidade da SAP HANA Cloud Platform."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c1320d1-7ba4-4b5f-926f-4996b44d9b5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 7799bf03cc6705f805a48f329a265a3d84bed55f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform-identity-authentication"></a><span data-ttu-id="6ad04-103">Tutorial: Integração do Azure Active Directory com a SAP HANA Cloud Platform | Autenticação de Identidade</span><span class="sxs-lookup"><span data-stu-id="6ad04-103">Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform Identity Authentication</span></span>

<span data-ttu-id="6ad04-104">Neste tutorial, você aprenderá a integrar a Autenticação de Identidade da SAP HANA Cloud Platform ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="6ad04-104">In this tutorial, you learn how to integrate SAP HANA Cloud Platform Identity Authentication with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="6ad04-105">A Autenticação de Identidade da SAP HANA Cloud Platform é usada como um proxy IdP para acessar aplicativos SAP usando o Azure AD como o IdP principal.</span><span class="sxs-lookup"><span data-stu-id="6ad04-105">SAP HANA Cloud Platform Identity Authentication is used as a proxy IdP to access SAP applications using Azure AD as the main IdP.</span></span>

<span data-ttu-id="6ad04-106">Integrar a Autenticação de Identidade da SAP HANA Cloud Platform ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="6ad04-106">Integrating SAP HANA Cloud Platform Identity Authentication with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6ad04-107">Você pode controlar no Azure AD que tem acesso ao aplicativo SAP</span><span class="sxs-lookup"><span data-stu-id="6ad04-107">You can control in Azure AD who has access to SAP application</span></span>
- <span data-ttu-id="6ad04-108">Você pode permitir que os usuários se conectem automaticamente ao SSO (logon único) de aplicativos SAP com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6ad04-108">You can enable your users to automatically get signed-on to SAP applications single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="6ad04-109">Gerenciar suas contas em um único local: o Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="6ad04-109">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="6ad04-110">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6ad04-110">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="6ad04-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6ad04-111">Prerequisites</span></span>

<span data-ttu-id="6ad04-112">Para configurar a integração do Azure AD com Autenticação de Identidade da SAP HANA Cloud Platform, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="6ad04-112">To configure Azure AD integration with SAP HANA Cloud Platform Identity Authentication, you need the following items:</span></span>

- <span data-ttu-id="6ad04-113">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6ad04-113">An Azure AD subscription</span></span>
- <span data-ttu-id="6ad04-114">Uma assinatura da **Autenticação de Identidade da SAP HANA Cloud Platform** habilitada para SSO</span><span class="sxs-lookup"><span data-stu-id="6ad04-114">A **SAP HANA Cloud Platform Identity Authentication** SSO enabled subscription</span></span>


>[!NOTE] 
><span data-ttu-id="6ad04-115">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="6ad04-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="6ad04-116">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="6ad04-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6ad04-117">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="6ad04-117">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="6ad04-118">Se não tiver um ambiente de avaliação do Azure AD, você pode obter uma [versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6ad04-118">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6ad04-119">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="6ad04-119">Scenario description</span></span>
<span data-ttu-id="6ad04-120">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="6ad04-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="6ad04-121">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="6ad04-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6ad04-122">Adicionando autenticação de identidade de plataforma de nuvem do SAP HANA da galeria</span><span class="sxs-lookup"><span data-stu-id="6ad04-122">Adding SAP HANA Cloud Platform Identity Authentication from the gallery</span></span>
2. <span data-ttu-id="6ad04-123">Configurar e testar o SSO do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6ad04-123">Configuring and testing Azure AD SSO</span></span>

<span data-ttu-id="6ad04-124">Antes de nos aprofundarmos nos detalhes técnicos, é essencial entender os conceitos que serão examinados.</span><span class="sxs-lookup"><span data-stu-id="6ad04-124">Before diving into the technical details, it is vital to understand the concepts you're going to look at.</span></span> <span data-ttu-id="6ad04-125">A federação da Autenticação de Identidade da SAP HANA Cloud Platform e do Azure Active Directory permite que você implemente o SSO em aplicativos ou serviços protegidos pelo AAD (como um IdP) com aplicativos SAP e serviços protegidos pela Autenticação de Identidade da SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="6ad04-125">The SAP HANA Cloud Platform Identity Authentication and Azure Active Directory federation enables you to implement SSO across applications or services protected by AAD (as an IdP) with SAP applications and services protected by SAP HANA Cloud Platform Identity Authentication.</span></span>

<span data-ttu-id="6ad04-126">Atualmente, a Autenticação de Identidade da SAP HANA Cloud Platform atua como um provedor de identidade de proxy para aplicativos SAP.</span><span class="sxs-lookup"><span data-stu-id="6ad04-126">Currently, SAP HANA Cloud Platform Identity Authentication acts as a Proxy Identity Provider to SAP-applications.</span></span> <span data-ttu-id="6ad04-127">O Azure Active Directory por sua vez atua como o principal provedor de identidade nessa configuração.</span><span class="sxs-lookup"><span data-stu-id="6ad04-127">Azure Active Directory in turn acts as the leading Identity Provider in this setup.</span></span> 

<span data-ttu-id="6ad04-128">O seguinte diagrama ilustra isso:</span><span class="sxs-lookup"><span data-stu-id="6ad04-128">The following diagram illustrates this:</span></span>    

![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/architecture-01.png)

<span data-ttu-id="6ad04-130">Com essa configuração, seu locatário de Autenticação de Identidade da SAP HANA Cloud Platform será configurado como um aplicativo confiável no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6ad04-130">With this setup, your SAP HANA Cloud Platform Identity Authentication tenant will be configured as a trusted application in Azure Active Directory.</span></span> 

<span data-ttu-id="6ad04-131">Todos os serviços e aplicativos SAP que você deseja proteger dessa maneira são posteriormente configurados no console de gerenciamento de Autenticação de Identidade da SAP HANA Cloud Platform!</span><span class="sxs-lookup"><span data-stu-id="6ad04-131">All SAP applications and services you want to protect through this way are subsequently configured in the SAP HANA Cloud Platform Identity Authentication management console!</span></span>

<span data-ttu-id="6ad04-132">Isso significa que a autorização para conceder acesso aos serviços e aplicativos SAP precisa ocorrer na Autenticação de Identidade da SAP HANA Cloud Platform para uma configuração como essa (em vez de configurar a autorização no Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="6ad04-132">This means that authorization for granting access to SAP applications and services needs to take place in SAP HANA Cloud Platform Identity Authentication for such a setup (as opposed to configuring authorization in Azure Active Directory).</span></span>

<span data-ttu-id="6ad04-133">Configurando a Autenticação de Identidade da SAP HANA Cloud Platform como um aplicativo por meio do Azure Active Directory Marketplace, você não precisa cuidar da configuração de declarações individuais/transformações e asserções SAML necessárias para gerar um token de autenticação válido para aplicativos SAP.</span><span class="sxs-lookup"><span data-stu-id="6ad04-133">By configuring SAP HANA Cloud Platform Identity Authentication as an application through the Azure Active Directory Marketplace, you don't need to take care of configuring needed individual claims / SAML assertions and transformations needed to produce a valid authentication token for SAP applications.</span></span>

>[!NOTE] 
><span data-ttu-id="6ad04-134">Atualmente, o SSO da Web foi testado somente por ambas as partes.</span><span class="sxs-lookup"><span data-stu-id="6ad04-134">Currently Web SSO has been tested by both parties, only.</span></span> <span data-ttu-id="6ad04-135">Fluxos necessários para a comunicação de aplicativo a API ou de API para API devem funcionar, mas ainda não foram testados.</span><span class="sxs-lookup"><span data-stu-id="6ad04-135">Flows needed for App-to-API or API-to-API communication should work but have not been tested, yet.</span></span> <span data-ttu-id="6ad04-136">Eles serão testados como parte das atividades subsequentes.</span><span class="sxs-lookup"><span data-stu-id="6ad04-136">They will be tested as part of subsequent activities.</span></span>
>

## <a name="add-sap-hana-cloud-platform-identity-authentication-from-the-gallery"></a><span data-ttu-id="6ad04-137">Adicionar a Autenticação de Identidade da SAP HANA Cloud Platform por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="6ad04-137">Add SAP HANA Cloud Platform Identity Authentication from the gallery</span></span>
<span data-ttu-id="6ad04-138">Para configurar a integração da Autenticação de Identidade da SAP HANA Cloud Platform no Azure AD, você precisa adicionar a Autenticação de Identidade da SAP HANA Cloud Platform da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="6ad04-138">To configure the integration of SAP HANA Cloud Platform Identity Authentication into Azure AD, you need to add SAP HANA Cloud Platform Identity Authentication from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6ad04-139">**Para adicionar a Autenticação de Identidade da SAP HANA Cloud Platform da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="6ad04-139">**To add SAP HANA Cloud Platform Identity Authentication from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6ad04-140">No [**Portal de Gerenciamento do Azure**](https://portal.azure.com), no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6ad04-140">In the [**Azure Management portal**](https://portal.azure.com), on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6ad04-142">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="6ad04-142">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6ad04-143">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="6ad04-143">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="6ad04-145">Clique em **adicionar** botão na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6ad04-145">Click **Add** button on the top of the dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="6ad04-147">Na caixa de pesquisa, digite **Autenticação de Identidade da SAP HANA Cloud Platform**.</span><span class="sxs-lookup"><span data-stu-id="6ad04-147">In the search box, type **SAP HANA Cloud Platform Identity Authentication**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_01.png)

5. <span data-ttu-id="6ad04-149">No painel resultados, selecione **Autenticação de Identidade da SAP HANA Cloud Platform** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6ad04-149">In the results panel, select **SAP HANA Cloud Platform Identity Authentication**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_02.png)


##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6ad04-151">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6ad04-151">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="6ad04-152">Nesta seção, você configura e testa o SSO do Azure AD com a Autenticação de Identidade da SAP HANA Cloud Platform com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="6ad04-152">In this section, you configure and test Azure AD SSO with SAP HANA Cloud Platform Identity Authentication based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6ad04-153">Para que o SSO funcione, o Azure AD precisa saber qual usuário da Autenticação de Identidade da SAP HANA Cloud Platform é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6ad04-153">For SSO to work, Azure AD needs to know what the counterpart user in SAP HANA Cloud Platform Identity Authentication is to a user in Azure AD.</span></span> <span data-ttu-id="6ad04-154">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado da Autenticação de Identidade da SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="6ad04-154">In other words, a link relationship between an Azure AD user and the related user in SAP HANA Cloud Platform Identity Authentication needs to be established.</span></span>

<span data-ttu-id="6ad04-155">Essa relação de vínculo é estabelecida atribuindo o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** na Autenticação de Identidade da SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="6ad04-155">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SAP HANA Cloud Platform Identity Authentication.</span></span>

<span data-ttu-id="6ad04-156">Para configurar e testar o SSO do Azure AD com a Autenticação de Identidade da SAP HANA Cloud Platform, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="6ad04-156">To configure and test Azure AD SSO with SAP HANA Cloud Platform Identity Authentication, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6ad04-157">**[Configurar logon único do Azure AD](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="6ad04-157">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6ad04-158">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="6ad04-158">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6ad04-159">**[Criar um usuário de teste de Autenticação de Identidade da SAP HANA Cloud Platform](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)** – para ter um equivalente de Brenda Fernandes na Autenticação de Identidade da SAP HANA Cloud Platform que é vinculado à representação dela no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6ad04-159">**[Creating a SAP HANA Cloud Platform Identity Authentication test user](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)** - to have a counterpart of Britta Simon in SAP HANA Cloud Platform Identity Authentication that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="6ad04-160">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ad04-160">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6ad04-161">**[Teste do logon único](#testing-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="6ad04-161">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="6ad04-162">Configurar o SSO do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6ad04-162">Configuring Azure AD SSO</span></span>

<span data-ttu-id="6ad04-163">Nesta seção, você habilita o SSO do Azure AD no portal de Gerenciamento do Azure e configura o logon único no aplicativo da Autenticação de Identidade da SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="6ad04-163">In this section, you enable Azure AD SSO in the Azure Management portal and configure single sign-on in your SAP HANA Cloud Platform Identity Authentication application.</span></span>

<span data-ttu-id="6ad04-164">O aplicativo de Autenticação de Identidade da SAP HANA Cloud Platform espera as asserções SAML em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="6ad04-164">SAP HANA Cloud Platform Identity Authentication application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="6ad04-165">Você pode gerenciar os valores desses atributos da seção "**Atributos de Usuário**" na página de integração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6ad04-165">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="6ad04-166">A captura de tela a seguir mostra um exemplo disso.</span><span class="sxs-lookup"><span data-stu-id="6ad04-166">The following screenshot shows an example for this.</span></span>

![Configurar o logon único](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_03.png)

<span data-ttu-id="6ad04-168">**Para configurar o SSO do Azure AD com a Autenticação de Identidade da SAP HANA Cloud Platform, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="6ad04-168">**To configure Azure AD SSO with SAP HANA Cloud Platform Identity Authentication, perform the following steps:**</span></span>

1. <span data-ttu-id="6ad04-169">No Portal de Gerenciamento do Azure, na página de integração de aplicativos **Autenticação de Identidade da SAP HANA Cloud Platform**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="6ad04-169">In the Azure Management portal, on the **SAP HANA Cloud Platform Identity Authentication** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="6ad04-171">Na caixa de diálogo **Logon único**, como **Modo**, selecione **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="6ad04-171">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurar Logon Único][5]

3. <span data-ttu-id="6ad04-173">Na seção **Atributos de Usuário** da caixa de diálogo **Logon único**, se seu aplicativo SAP espera um atributo, por exemplo "firstName".</span><span class="sxs-lookup"><span data-stu-id="6ad04-173">In the **User Attributes** section on the **Single sign-on** dialog, if your SAP application expects an attribute for example "firstName".</span></span> <span data-ttu-id="6ad04-174">No diálogo de atributos de token SAML, adicione o atributo "firstName".</span><span class="sxs-lookup"><span data-stu-id="6ad04-174">On the SAML token attributes dialog, add the "firstName" attribute.</span></span>
 1. <span data-ttu-id="6ad04-175">Clique em **Adicionar atributo** para abrir o diálogo **Adicionar Atributo**.</span><span class="sxs-lookup"><span data-stu-id="6ad04-175">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>
 
    ![Configurar o logon único][6]

    ![Configurar Logon Único](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_05.png)
 2. <span data-ttu-id="6ad04-178">Na caixa de texto **Nome do Atributo**, digite o nome do atributo "firstName".</span><span class="sxs-lookup"><span data-stu-id="6ad04-178">In the **Attribute Name** textbox, type the attribute name "firstName".</span></span>
 3. <span data-ttu-id="6ad04-179">Na lista **Valor do Atributo**, selecione o valor do atributo "user.givenname".</span><span class="sxs-lookup"><span data-stu-id="6ad04-179">From the **Attribute Value** list, select the attribute value "user.givenname".</span></span>
 4. <span data-ttu-id="6ad04-180">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="6ad04-180">Click **Ok**.</span></span>

4. <span data-ttu-id="6ad04-181">Na seção **Domínio e URLs da Autenticação de Identidade da SAP HANA Cloud Platform**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="6ad04-181">On the **SAP HANA Cloud Platform Identity Authentication Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_06.png)
 1. <span data-ttu-id="6ad04-183">Na caixa de texto **URL de logon**, digite a URL de logon do aplicativo SAP.</span><span class="sxs-lookup"><span data-stu-id="6ad04-183">In the **Sign On URL** textbox, type the sign on URL for the SAP application.</span></span>
 2. <span data-ttu-id="6ad04-184">Na caixa de texto **Identificador**, digite o valor no seguinte padrão: `<entity-id>.accounts.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="6ad04-184">In the **Identifier** textbox, type the value following pattern: `<entity-id>.accounts.ondemand.com`</span></span> 
    * <span data-ttu-id="6ad04-185">Se você não souber esse valor, siga a documentação da Autenticação de Identidade da SAP HANA Cloud Platform em [Configuração do SAML 2.0 do Locatário](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).</span><span class="sxs-lookup"><span data-stu-id="6ad04-185">If you don't know this value, please follow the SAP HANA Cloud Platform Identity Authentication documentation on [Tenant SAML 2.0 Configuration](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).</span></span>

5. <span data-ttu-id="6ad04-186">Na seção **Configuração da Autenticação de Identidade da SAP HANA Cloud Platform**, clique em **Configurar Autenticação de Identidade da SAP HANA Cloud Platform** para abrir a caixa de diálogo **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="6ad04-186">On the **SAP HANA Cloud Platform Identity Authentication Configuration** section, click **Configure SAP HANA Cloud Platform Identity Authentication** to open **Configure sign-on** dialog.</span></span> <span data-ttu-id="6ad04-187">Em seguida, clique em **Metadados XML SAML** e salve o arquivo no computador.</span><span class="sxs-lookup"><span data-stu-id="6ad04-187">Then, click on **SAML XML Metadata** and save the file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_07.png) 

    ![Configurar Logon Único](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_08.png)

6. <span data-ttu-id="6ad04-190">Para configurar o SSO para o seu aplicativo, vá para o Console de administração da Autenticação de Identidade da SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="6ad04-190">To get SSO configured for your application, go to SAP HANA Cloud Platform Identity Authentication Administration Console.</span></span> <span data-ttu-id="6ad04-191">A URL tem o seguinte padrão: `https://<tenant-id>.accounts.ondemand.com/admin`</span><span class="sxs-lookup"><span data-stu-id="6ad04-191">The URL has the following pattern: `https://<tenant-id>.accounts.ondemand.com/admin`</span></span>
 * <span data-ttu-id="6ad04-192">Depois, siga a documentação sobre a Autenticação de Identidade da SAP HANA Cloud Platform para [Configurar o Microsoft Azure AD como provedor de identidade corporativa na Autenticação de Identidade da SAP HANA Cloud Platform](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html).</span><span class="sxs-lookup"><span data-stu-id="6ad04-192">Then, follow the documentation on SAP HANA Cloud Platform Identity Authentication to [Configure Microsoft Azure AD as Corporate Identity Provider at SAP HANA Cloud Platform Identity Authentication](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html).</span></span> 

7. <span data-ttu-id="6ad04-193">No Portal de Gerenciamento do Azure, clique no botão **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="6ad04-193">In the Azure Management portal, click **Save** button.</span></span>
8. <span data-ttu-id="6ad04-194">Continue as etapas a seguir somente se você quiser adicionar e habilitar o SSO para outro aplicativo SAP.</span><span class="sxs-lookup"><span data-stu-id="6ad04-194">Continue the following steps only if you want to add and enable SSO for another SAP application.</span></span> <span data-ttu-id="6ad04-195">Repita as etapas na seção "Adicionar autenticação de identidade de plataforma de nuvem do SAP HANA da galeria" para adicionar outra instância de Autenticação de identidade de plataforma de nuvem do SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="6ad04-195">Repeat steps under the section “Adding SAP HANA Cloud Platform Identity Authentication from the gallery” to add another instance of SAP HANA Cloud Platform Identity Authentication.</span></span>
9. <span data-ttu-id="6ad04-196">No portal de Gerenciamento do Azure, na página de integração de aplicativos **Autenticação de Identidade da SAP HANA Cloud Platform**, clique em **Logon Vinculado**.</span><span class="sxs-lookup"><span data-stu-id="6ad04-196">In the Azure Management portal, on the **SAP HANA Cloud Platform Identity Authentication** application integration page, click **Linked Sign-on**.</span></span>

    ![Configurar o logon vinculado](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/linked_sign_on.png)
10. <span data-ttu-id="6ad04-198">Depois, salve a configuração.</span><span class="sxs-lookup"><span data-stu-id="6ad04-198">Then, save the configuration.</span></span>

>[!NOTE] 
><span data-ttu-id="6ad04-199">O novo aplicativo aproveitará a configuração de SSO para o aplicativo SAP anterior.</span><span class="sxs-lookup"><span data-stu-id="6ad04-199">The new application will leverage the SSO configuration for the previous SAP application.</span></span> <span data-ttu-id="6ad04-200">Use os mesmos Provedores de identidade corporativa no Console de Administração de autenticação de identidade de plataforma de nuvem do SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="6ad04-200">Please make sure you use the same Corporate Identity Providers in the SAP HANA Cloud Platform Identity Authentication Administration Console.</span></span>
>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6ad04-201">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6ad04-201">Create an Azure AD test user</span></span>
<span data-ttu-id="6ad04-202">O objetivo desta seção é criar um usuário de teste no novo portal chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="6ad04-202">The objective of this section is to create a test user in the new portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="6ad04-204">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="6ad04-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6ad04-205">No **portal de Gerenciamento do Azure**, no painel navegação à esquerda, clique em **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6ad04-205">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6ad04-207">Vá para **usuários e grupos** e clique em **todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="6ad04-207">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6ad04-209">Na parte superior da caixa de diálogo clique **adicionar** para abrir o **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6ad04-209">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6ad04-211">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="6ad04-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_04.png) 
  1. <span data-ttu-id="6ad04-213">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="6ad04-213">In the **Name** textbox, type **BrittaSimon**.</span></span>
  2. <span data-ttu-id="6ad04-214">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="6ad04-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>
  3. <span data-ttu-id="6ad04-215">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="6ad04-215">Select **Show Password** and write down the value of the **Password**.</span></span>
  4. <span data-ttu-id="6ad04-216">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="6ad04-216">Click **Create**.</span></span> 

### <a name="create-a-sap-hana-cloud-platform-identity-authentication-test-user"></a><span data-ttu-id="6ad04-217">Criar um usuário de teste da Autenticação de Identidade da SAP HANA Cloud Platform</span><span class="sxs-lookup"><span data-stu-id="6ad04-217">Create a SAP HANA Cloud Platform Identity Authentication test user</span></span>

<span data-ttu-id="6ad04-218">Você não precisa criar um usuário na Autenticação de Identidade da SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="6ad04-218">You don't need to create an user on SAP HANA Cloud Platform Identity Authentication.</span></span> <span data-ttu-id="6ad04-219">Os usuários que estão no repositório de usuários do Azure AD podem usar a funcionalidade de SSO.</span><span class="sxs-lookup"><span data-stu-id="6ad04-219">Users who are in the Azure AD user store can use the SSO functionality.</span></span>

<span data-ttu-id="6ad04-220">A Autenticação de Identidade da SAP HANA Cloud Platform dá suporte à opção de Federação de Identidades.</span><span class="sxs-lookup"><span data-stu-id="6ad04-220">SAP HANA Cloud Platform Identity Authentication supports the Identity Federation option.</span></span> <span data-ttu-id="6ad04-221">Essa opção permite que o aplicativo verifique se os usuários autenticados pelo provedor de identidade corporativa existem no repositório de usuários da Autenticação de Identidade da SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="6ad04-221">This option allows the application to check if the users authenticated by the corporate identity provider exist in the user store of SAP HANA Cloud Platform Identity Authentication.</span></span> 

<span data-ttu-id="6ad04-222">Na configuração padrão, a opção de Federação de Identidades é desabilitada.</span><span class="sxs-lookup"><span data-stu-id="6ad04-222">In the default setting, the Identity Federation option is disabled.</span></span> <span data-ttu-id="6ad04-223">Se a Federação de Identidades é habilitada, somente os usuários que são importados na Autenticação de Identidade da SAP HANA Cloud Platform são capazes de acessar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6ad04-223">If Identity Federation is enabled, only the users that are imported in SAP HANA Cloud Platform Identity Authentication are able to access the application.</span></span> 

<span data-ttu-id="6ad04-224">Para obter mais informações sobre como habilitar ou desabilitar a Federação de Identidades com a Autenticação de Identidade da SAP HANA Cloud Platform, consulte Habilitar a Federação de Identidades com a Autenticação de Identidade da SAP HANA Cloud Platform em [Configurar a Federação de Identidades com o repositório de usuários da Autenticação de Identidade da SAP HANA Cloud Platform](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).</span><span class="sxs-lookup"><span data-stu-id="6ad04-224">For more information about how to enable or disable Identity Federation with SAP HANA Cloud Platform Identity Authentication, see Enable Identity Federation with SAP HANA Cloud Platform Identity Authentication in [Configure Identity Federation with the User Store of SAP HANA Cloud Platform Identity Authentication.](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="6ad04-225">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6ad04-225">Assign the Azure AD test user</span></span>

<span data-ttu-id="6ad04-226">Nesta seção, você habilitará Brenda Fernandes a usar o logon único do Azure concedendo-lhe acesso à Autenticação de Identidade da SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="6ad04-226">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to SAP HANA Cloud Platform Identity Authentication.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="6ad04-228">**Para atribuir Brenda Fernandes à Autenticação de Identidade da SAP HANA Cloud Platform, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="6ad04-228">**To assign Britta Simon to SAP HANA Cloud Platform Identity Authentication, perform the following steps:**</span></span>

1. <span data-ttu-id="6ad04-229">No Portal de Gerenciamento do Azure, abra a exibição de aplicativos e, em seguida, navegue até o modo de exibição de diretório e vá para **Aplicativos empresariais**, depois clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="6ad04-229">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="6ad04-231">Na lista de aplicativos, selecione **Autenticação de Identidade da SAP HANA Cloud Platform**.</span><span class="sxs-lookup"><span data-stu-id="6ad04-231">In the applications list, select **SAP HANA Cloud Platform Identity Authentication**.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_09.png)

3. <span data-ttu-id="6ad04-233">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="6ad04-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="6ad04-235">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6ad04-235">Click **Add** button.</span></span> <span data-ttu-id="6ad04-236">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6ad04-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="6ad04-238">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="6ad04-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6ad04-239">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6ad04-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6ad04-240">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6ad04-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    

### <a name="test-single-sign-on"></a><span data-ttu-id="6ad04-241">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="6ad04-241">Test single sign-on</span></span>

<span data-ttu-id="6ad04-242">Nesta seção, você testará sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="6ad04-242">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="6ad04-243">Quando você clica no bloco de Autenticação de Identidade da SAP HANA Cloud Platform no Painel de Acesso, seu logon deve ser realizado automaticamente no seu aplicativo de Autenticação de Identidade da SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="6ad04-243">When you click the SAP HANA Cloud Platform Identity Authentication tile in the Access Panel, you should get automatically signed-on to your SAP HANA Cloud Platform Identity Authentication application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="6ad04-244">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="6ad04-244">Additional resources</span></span>

* [<span data-ttu-id="6ad04-245">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="6ad04-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6ad04-246">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6ad04-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_06.png

[100]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_203.png