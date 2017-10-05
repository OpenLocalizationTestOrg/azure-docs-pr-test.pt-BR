---
title: "Tutorial: integração do Azure Active Directory ao SAP Cloud for Customer | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o SAP Cloud for Customer."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 90154dab-eba2-4563-bcf0-f2acc797ea97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: e4d945525a45704f34e1d9e742220928a516f341
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-cloud-for-customer"></a><span data-ttu-id="1fb29-103">Tutorial: integração do Azure Active Directory ao SAP Cloud for Customer</span><span class="sxs-lookup"><span data-stu-id="1fb29-103">Tutorial: Azure Active Directory integration with SAP Cloud for Customer</span></span>

<span data-ttu-id="1fb29-104">Neste tutorial, você aprenderá a integrar o SAP Cloud for Customer ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="1fb29-104">In this tutorial, you learn how to integrate SAP Cloud for Customer with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1fb29-105">A integração do SAP Cloud for Customer ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="1fb29-105">Integrating SAP Cloud for Customer with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1fb29-106">No Azure AD, você pode controlar quem tem acesso ao SAP Cloud for Customer</span><span class="sxs-lookup"><span data-stu-id="1fb29-106">You can control in Azure AD who has access to SAP Cloud for Customer</span></span>
- <span data-ttu-id="1fb29-107">Você pode habilitar os usuários a fazer logon automaticamente no SAP Cloud for Customer (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1fb29-107">You can enable your users to automatically get signed-on to SAP Cloud for Customer (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1fb29-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="1fb29-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1fb29-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1fb29-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1fb29-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1fb29-110">Prerequisites</span></span>

<span data-ttu-id="1fb29-111">Para configurar a integração do Azure AD ao SAP Cloud for Customer, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="1fb29-111">To configure Azure AD integration with SAP Cloud for Customer, you need the following items:</span></span>

- <span data-ttu-id="1fb29-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1fb29-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1fb29-113">Uma assinatura habilitada para logon único do SAP Cloud for Customer</span><span class="sxs-lookup"><span data-stu-id="1fb29-113">A SAP Cloud for Customer single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1fb29-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="1fb29-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1fb29-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="1fb29-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1fb29-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="1fb29-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1fb29-117">Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1fb29-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1fb29-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="1fb29-118">Scenario description</span></span>
<span data-ttu-id="1fb29-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="1fb29-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1fb29-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="1fb29-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1fb29-121">Adição do SAP Cloud for Customer da galeria</span><span class="sxs-lookup"><span data-stu-id="1fb29-121">Adding SAP Cloud for Customer from the gallery</span></span>
2. <span data-ttu-id="1fb29-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1fb29-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-cloud-for-customer-from-the-gallery"></a><span data-ttu-id="1fb29-123">Adição do SAP Cloud for Customer da galeria</span><span class="sxs-lookup"><span data-stu-id="1fb29-123">Adding SAP Cloud for Customer from the gallery</span></span>
<span data-ttu-id="1fb29-124">Para configurar a integração do SAP Cloud for Customer ao Azure AD, você precisará adicionar o SAP Cloud for Customer da galeria à lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="1fb29-124">To configure the integration of SAP Cloud for Customer into Azure AD, you need to add SAP Cloud for Customer from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1fb29-125">**Para adicionar o SAP Cloud for Customer da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="1fb29-125">**To add SAP Cloud for Customer from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1fb29-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1fb29-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1fb29-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="1fb29-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1fb29-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="1fb29-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="1fb29-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1fb29-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="1fb29-133">Na caixa de pesquisa, digite **SAP Cloud for Customer**.</span><span class="sxs-lookup"><span data-stu-id="1fb29-133">In the search box, type **SAP Cloud for Customer**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_search.png)

5. <span data-ttu-id="1fb29-135">No painel de resultados, selecione **SAP Cloud for Customer** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1fb29-135">In the results panel, select **SAP Cloud for Customer**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1fb29-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1fb29-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1fb29-138">Nesta seção, você configurará e testará o logon único do Azure AD com o SAP Cloud for Customer, com base em uma usuária de teste chamada "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="1fb29-138">In this section, you configure and test Azure AD single sign-on with SAP Cloud for Customer based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1fb29-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do SAP Cloud for Customer é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1fb29-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP Cloud for Customer is to a user in Azure AD.</span></span> <span data-ttu-id="1fb29-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do AD do Azure e o usuário relacionado do SAP Cloud for Customer.</span><span class="sxs-lookup"><span data-stu-id="1fb29-140">In other words, a link relationship between an Azure AD user and the related user in SAP Cloud for Customer needs to be established.</span></span>

<span data-ttu-id="1fb29-141">No SAP Cloud for Customer, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="1fb29-141">In SAP Cloud for Customer, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1fb29-142">Para configurar e testar o logon único do Azure AD com o SAP Cloud for Customer, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="1fb29-142">To configure and test Azure AD single sign-on with SAP Cloud for Customer, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1fb29-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="1fb29-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1fb29-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="1fb29-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1fb29-145">**[Criando um usuário de teste do SAP Cloud for Customer](#creating-a-sap-cloud-for-customer-test-user)** – para ter um equivalente de Brenda Fernandes no SAP Cloud for Customer que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1fb29-145">**[Creating a SAP Cloud for Customer test user](#creating-a-sap-cloud-for-customer-test-user)** - to have a counterpart of Britta Simon in SAP Cloud for Customer that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1fb29-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="1fb29-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1fb29-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="1fb29-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1fb29-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1fb29-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1fb29-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo SAP Cloud for Customer.</span><span class="sxs-lookup"><span data-stu-id="1fb29-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAP Cloud for Customer application.</span></span>

<span data-ttu-id="1fb29-150">**Para configurar o logon único do Azure AD com o SAP Cloud for Customer, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="1fb29-150">**To configure Azure AD single sign-on with SAP Cloud for Customer, perform the following steps:**</span></span>

1. <span data-ttu-id="1fb29-151">No portal do Azure, na página de integração do aplicativo **SAP Cloud for Customer**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="1fb29-151">In the Azure portal, on the **SAP Cloud for Customer** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="1fb29-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="1fb29-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_samlbase.png)

3. <span data-ttu-id="1fb29-155">Na seção **Domínio e URLs do SAP Cloud for Customer**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="1fb29-155">On the **SAP Cloud for Customer Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_url.png)

    <span data-ttu-id="1fb29-157">a.</span><span class="sxs-lookup"><span data-stu-id="1fb29-157">a.</span></span> <span data-ttu-id="1fb29-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<server name>.crm.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="1fb29-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server name>.crm.ondemand.com`</span></span>

    <span data-ttu-id="1fb29-159">b.</span><span class="sxs-lookup"><span data-stu-id="1fb29-159">b.</span></span> <span data-ttu-id="1fb29-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<server name>.crm.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="1fb29-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<server name>.crm.ondemand.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1fb29-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="1fb29-161">These values are not real.</span></span> <span data-ttu-id="1fb29-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="1fb29-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1fb29-163">Contate a [equipe de suporte ao Cliente do SAP Cloud for Customer](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="1fb29-163">Contact [SAP Cloud for Customer Client support team](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) to get these values.</span></span> 

4. <span data-ttu-id="1fb29-164">Na seção **Atributos de Usuário**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="1fb29-164">On the **User Attributes** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_attribute.png)

    <span data-ttu-id="1fb29-166">a.</span><span class="sxs-lookup"><span data-stu-id="1fb29-166">a.</span></span> <span data-ttu-id="1fb29-167">Na lista **Identificador de Usuário**, selecione a função **ExtractMailPrefix()**.</span><span class="sxs-lookup"><span data-stu-id="1fb29-167">In **User Identifier** list, select the **ExtractMailPrefix()** function.</span></span>

    <span data-ttu-id="1fb29-168">b.</span><span class="sxs-lookup"><span data-stu-id="1fb29-168">b.</span></span> <span data-ttu-id="1fb29-169">Na lista de **Email** , selecione o atributo de usuário que você deseja usar na implementação.</span><span class="sxs-lookup"><span data-stu-id="1fb29-169">From the **Mail** list, select the user attribute you want to use for your implementation.</span></span>
    <span data-ttu-id="1fb29-170">Por exemplo, se você quiser usar EmployeeID como identificador exclusivo de usuário e tiver armazenado o valor do atributo em ExtensionAttribute2, selecione user.extensionattribute2.</span><span class="sxs-lookup"><span data-stu-id="1fb29-170">For example, if you want to use the EmployeeID as unique user identifier and you have stored the attribute value in the ExtensionAttribute2, then select user.extensionattribute2.</span></span>  

5. <span data-ttu-id="1fb29-171">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="1fb29-171">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_certificate.png) 

6. <span data-ttu-id="1fb29-173">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="1fb29-173">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="1fb29-175">Na seção **Configuração do SAP Cloud for Customer**, clique em **Configurar o SAP Cloud for Customer** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="1fb29-175">On the **SAP Cloud for Customer Configuration** section, click **Configure SAP Cloud for Customer** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1fb29-176">Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="1fb29-176">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_configure.png) 

8. <span data-ttu-id="1fb29-178">Para que o SSO seja configurado, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="1fb29-178">To get SSO configured, perform the following steps:</span></span>
   
    <span data-ttu-id="1fb29-179">a.</span><span class="sxs-lookup"><span data-stu-id="1fb29-179">a.</span></span> <span data-ttu-id="1fb29-180">Faça logon no portal do SAP Cloud for Customer com direitos de administrador.</span><span class="sxs-lookup"><span data-stu-id="1fb29-180">Login into SAP Cloud for Customer portal with administrator rights.</span></span>
   
    <span data-ttu-id="1fb29-181">b.</span><span class="sxs-lookup"><span data-stu-id="1fb29-181">b.</span></span> <span data-ttu-id="1fb29-182">Navegue até **Tarefa Comum de Gerenciamento de Aplicativos e Usuários** e clique na guia **Provedor de Identidade**.</span><span class="sxs-lookup"><span data-stu-id="1fb29-182">Navigate to the **Application and User Management Common Task** and click the **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="1fb29-183">c.</span><span class="sxs-lookup"><span data-stu-id="1fb29-183">c.</span></span> <span data-ttu-id="1fb29-184">Clique em **Novo Provedor de Identidade** e selecione o arquivo XML de metadados baixado no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1fb29-184">Click **New Identity Provider** and select the metadata XML file you have downloaded from the Azure portal.</span></span> <span data-ttu-id="1fb29-185">Com a importação dos metadados, o sistema carrega automaticamente o certificado de assinatura e o certificado de criptografia necessários.</span><span class="sxs-lookup"><span data-stu-id="1fb29-185">By importing the metadata, the system automatically uploads the required signature certificate and encryption certificate.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_54.png)
   
    <span data-ttu-id="1fb29-187">d.</span><span class="sxs-lookup"><span data-stu-id="1fb29-187">d.</span></span> <span data-ttu-id="1fb29-188">O Azure Active Directory exige a URL do Serviço do Consumidor de Declaração do elemento na solicitação do SAML. Portanto, marque a caixa de seleção **Incluir URL do Serviço do Consumidor de Declaração**.</span><span class="sxs-lookup"><span data-stu-id="1fb29-188">Azure Active Directory requires the element Assertion Consumer Service URL in the SAML request, so select the **Include Assertion Consumer Service URL** checkbox.</span></span>
   
    <span data-ttu-id="1fb29-189">e.</span><span class="sxs-lookup"><span data-stu-id="1fb29-189">e.</span></span> <span data-ttu-id="1fb29-190">Clique em **Ativar Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="1fb29-190">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="1fb29-191">f.</span><span class="sxs-lookup"><span data-stu-id="1fb29-191">f.</span></span> <span data-ttu-id="1fb29-192">Salve suas alterações.</span><span class="sxs-lookup"><span data-stu-id="1fb29-192">Save your changes.</span></span>
   
    <span data-ttu-id="1fb29-193">g.</span><span class="sxs-lookup"><span data-stu-id="1fb29-193">g.</span></span> <span data-ttu-id="1fb29-194">Clique na guia **Meu Sistema** .</span><span class="sxs-lookup"><span data-stu-id="1fb29-194">Click the **My System** tab.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_52.png)
   
    <span data-ttu-id="1fb29-196">h.</span><span class="sxs-lookup"><span data-stu-id="1fb29-196">h.</span></span> <span data-ttu-id="1fb29-197">Na caixa de texto **URL de Logon do Azure AD**, cole a **URL do Serviço de Logon Único SAML** copiada do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1fb29-197">In **Azure AD Sign On URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_53.png)
   
    <span data-ttu-id="1fb29-199">i.</span><span class="sxs-lookup"><span data-stu-id="1fb29-199">i.</span></span> <span data-ttu-id="1fb29-200">Especifique se o funcionário pode escolher manualmente entre fazer logon com uma ID de usuário e senha ou SSO, selecionando a **Seleção de Provedor de Identidade Manual**.</span><span class="sxs-lookup"><span data-stu-id="1fb29-200">Specify whether the employee can manually choose between logging on with user ID and password or SSO by selecting the **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="1fb29-201">j.</span><span class="sxs-lookup"><span data-stu-id="1fb29-201">j.</span></span> <span data-ttu-id="1fb29-202">Na seção **URL de SSO** , especifique a URL que deve ser usada pelos funcionários para fazer logon no sistema.</span><span class="sxs-lookup"><span data-stu-id="1fb29-202">In the **SSO URL** section, specify the URL that should be used by your employees to sign on to the system.</span></span> 
    <span data-ttu-id="1fb29-203">Na lista **URL Enviada ao Funcionário** , você pode escolher entre as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="1fb29-203">In the **URL Sent to Employee** list, you can choose between the following options:</span></span>
   
    <span data-ttu-id="1fb29-204">**URL não SSO**</span><span class="sxs-lookup"><span data-stu-id="1fb29-204">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="1fb29-205">O sistema envia apenas a URL normal do sistema ao funcionário.</span><span class="sxs-lookup"><span data-stu-id="1fb29-205">The system sends only the normal system URL to the employee.</span></span> <span data-ttu-id="1fb29-206">O funcionário não pode fazer logon usando o SSO e deve usar uma senha ou um certificado em vez disso.</span><span class="sxs-lookup"><span data-stu-id="1fb29-206">The employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="1fb29-207">**URL de SSO**</span><span class="sxs-lookup"><span data-stu-id="1fb29-207">**SSO URL**</span></span> 
   
    <span data-ttu-id="1fb29-208">O sistema envia apenas a URL de SSO ao funcionário.</span><span class="sxs-lookup"><span data-stu-id="1fb29-208">The system sends only the SSO URL to the employee.</span></span> <span data-ttu-id="1fb29-209">O funcionário pode fazer logon usando o SSO.</span><span class="sxs-lookup"><span data-stu-id="1fb29-209">The employee can log on using SSO.</span></span> <span data-ttu-id="1fb29-210">A solicitação de autenticação é redirecionada por meio do IdP.</span><span class="sxs-lookup"><span data-stu-id="1fb29-210">Authentication request is redirected through the IdP.</span></span>
   
    <span data-ttu-id="1fb29-211">**Seleção Automática**</span><span class="sxs-lookup"><span data-stu-id="1fb29-211">**Automatic Selection**</span></span>
   
    <span data-ttu-id="1fb29-212">Se o SSO não estiver ativo, o sistema enviará a URL normal do sistema ao funcionário.</span><span class="sxs-lookup"><span data-stu-id="1fb29-212">If SSO is not active, the system sends the normal system URL to the employee.</span></span> <span data-ttu-id="1fb29-213">Se o SSO estiver ativo, o sistema verificará se o funcionário tem uma senha.</span><span class="sxs-lookup"><span data-stu-id="1fb29-213">If SSO is active, the system checks whether the employee has a password.</span></span> <span data-ttu-id="1fb29-214">Se uma senha estiver disponível, a URL de SSO e a URL não SSO serão enviadas ao funcionário.</span><span class="sxs-lookup"><span data-stu-id="1fb29-214">If a password is available, both SSO URL and Non-SSO URL are sent to the employee.</span></span> <span data-ttu-id="1fb29-215">No entanto, se o funcionário não tiver uma senha, apenas a URL de SSO será enviada ao funcionário.</span><span class="sxs-lookup"><span data-stu-id="1fb29-215">However, if the employee has no password, only the SSO URL is sent to the employee.</span></span>
   
    <span data-ttu-id="1fb29-216">k.</span><span class="sxs-lookup"><span data-stu-id="1fb29-216">k.</span></span> <span data-ttu-id="1fb29-217">Salve suas alterações.</span><span class="sxs-lookup"><span data-stu-id="1fb29-217">Save your changes.</span></span>

> [!TIP]
> <span data-ttu-id="1fb29-218">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="1fb29-218">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1fb29-219">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="1fb29-219">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1fb29-220">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1fb29-220">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1fb29-221">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1fb29-221">Creating an Azure AD test user</span></span>
<span data-ttu-id="1fb29-222">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="1fb29-222">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="1fb29-224">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="1fb29-224">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1fb29-225">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1fb29-225">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1fb29-227">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="1fb29-227">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1fb29-229">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1fb29-229">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1fb29-231">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="1fb29-231">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1fb29-233">a.</span><span class="sxs-lookup"><span data-stu-id="1fb29-233">a.</span></span> <span data-ttu-id="1fb29-234">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="1fb29-234">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1fb29-235">b.</span><span class="sxs-lookup"><span data-stu-id="1fb29-235">b.</span></span> <span data-ttu-id="1fb29-236">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="1fb29-236">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1fb29-237">c.</span><span class="sxs-lookup"><span data-stu-id="1fb29-237">c.</span></span> <span data-ttu-id="1fb29-238">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="1fb29-238">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1fb29-239">d.</span><span class="sxs-lookup"><span data-stu-id="1fb29-239">d.</span></span> <span data-ttu-id="1fb29-240">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="1fb29-240">Click **Create**.</span></span>
 
### <a name="creating-a-sap-cloud-for-customer-test-user"></a><span data-ttu-id="1fb29-241">Criando um usuário de teste do SAP Cloud for Customer</span><span class="sxs-lookup"><span data-stu-id="1fb29-241">Creating a SAP Cloud for Customer test user</span></span>

<span data-ttu-id="1fb29-242">Nesta seção, você criará uma usuária chamada Brenda Fernandes no SAP Cloud for Customer.</span><span class="sxs-lookup"><span data-stu-id="1fb29-242">In this section, you create a user called Britta Simon in SAP Cloud for Customer.</span></span> <span data-ttu-id="1fb29-243">Trabalhe com a [equipe de suporte do SAP Cloud for Customer](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) para adicionar os usuários à plataforma SAP Cloud for Customer.</span><span class="sxs-lookup"><span data-stu-id="1fb29-243">Please work with [SAP Cloud for Customer support team](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) to add the users in the SAP Cloud for Customer platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="1fb29-244">Verifique se o valor de NameID corresponde ao campo de nome de usuário na plataforma SAP Cloud for Customer.</span><span class="sxs-lookup"><span data-stu-id="1fb29-244">Please make sure that NameID value should match with the username field in the SAP Cloud for Customer platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1fb29-245">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1fb29-245">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1fb29-246">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao SAP Cloud for Customer.</span><span class="sxs-lookup"><span data-stu-id="1fb29-246">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP Cloud for Customer.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="1fb29-248">**Para atribuir Brenda Fernandes ao SAP Cloud for Customer, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="1fb29-248">**To assign Britta Simon to SAP Cloud for Customer, perform the following steps:**</span></span>

1. <span data-ttu-id="1fb29-249">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="1fb29-249">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="1fb29-251">Na lista de aplicativos, selecione **SAP Cloud for Customer**.</span><span class="sxs-lookup"><span data-stu-id="1fb29-251">In the applications list, select **SAP Cloud for Customer**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_app.png) 

3. <span data-ttu-id="1fb29-253">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="1fb29-253">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="1fb29-255">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1fb29-255">Click **Add** button.</span></span> <span data-ttu-id="1fb29-256">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1fb29-256">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="1fb29-258">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="1fb29-258">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1fb29-259">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1fb29-259">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1fb29-260">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1fb29-260">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1fb29-261">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="1fb29-261">Testing single sign-on</span></span>

<span data-ttu-id="1fb29-262">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="1fb29-262">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1fb29-263">Ao clicar no bloco do SAP Cloud for Customer no Painel de Acesso, você deve ser conectado automaticamente ao aplicativo SAP Cloud for Customer.</span><span class="sxs-lookup"><span data-stu-id="1fb29-263">When you click the SAP Cloud for Customer tile in the Access Panel, you should get automatically signed-on to your SAP Cloud for Customer application.</span></span>
<span data-ttu-id="1fb29-264">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1fb29-264">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1fb29-265">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="1fb29-265">Additional resources</span></span>

* [<span data-ttu-id="1fb29-266">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="1fb29-266">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1fb29-267">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1fb29-267">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_203.png

