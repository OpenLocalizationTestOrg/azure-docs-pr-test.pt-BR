---
title: "Tutorial: Integração do Azure Active Directory ao SAP Business ByDesign | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o SAP Business ByDesign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 82938920-33ba-47cb-b141-511b46d19e66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: ab76a0ac1ef954efd3c66e6f565514b889ed9444
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-bydesign"></a><span data-ttu-id="a3399-103">Tutorial: integração do Azure Active Directory ao SAP Business ByDesign</span><span class="sxs-lookup"><span data-stu-id="a3399-103">Tutorial: Azure Active Directory integration with SAP Business ByDesign</span></span>

<span data-ttu-id="a3399-104">Neste tutorial, você aprenderá a integrar o SAP Business ByDesign ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="a3399-104">In this tutorial, you learn how to integrate SAP Business ByDesign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a3399-105">A integração do SAP Business ByDesign ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="a3399-105">Integrating SAP Business ByDesign with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a3399-106">No Azure AD, é possível controlar quem tem acesso ao SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="a3399-106">You can control in Azure AD who has access to SAP Business ByDesign.</span></span>
- <span data-ttu-id="a3399-107">Você pode permitir que os usuários façam logon automaticamente no SAP Business ByDesign (Logon Único) com as respectivas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a3399-107">You can enable your users to automatically get signed-on to SAP Business ByDesign (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="a3399-108">Você pode gerenciar suas contas em um único local central – o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a3399-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="a3399-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a3399-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3399-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a3399-110">Prerequisites</span></span>

<span data-ttu-id="a3399-111">Para configurar a integração do Azure AD ao SAP Business ByDesign, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="a3399-111">To configure Azure AD integration with SAP Business ByDesign, you need the following items:</span></span>

- <span data-ttu-id="a3399-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a3399-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a3399-113">Uma assinatura do SAP Business ByDesign habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="a3399-113">An SAP Business ByDesign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a3399-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="a3399-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a3399-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="a3399-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a3399-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="a3399-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a3399-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a3399-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a3399-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="a3399-118">Scenario description</span></span>
<span data-ttu-id="a3399-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="a3399-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a3399-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="a3399-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a3399-121">Adicionar o SAP Business ByDesign da galeria</span><span class="sxs-lookup"><span data-stu-id="a3399-121">Adding SAP Business ByDesign from the gallery</span></span>
2. <span data-ttu-id="a3399-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a3399-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-business-bydesign-from-the-gallery"></a><span data-ttu-id="a3399-123">Adicionar o SAP Business ByDesign da galeria</span><span class="sxs-lookup"><span data-stu-id="a3399-123">Adding SAP Business ByDesign from the gallery</span></span>
<span data-ttu-id="a3399-124">Para configurar a integração do SAP Business ByDesign ao Azure AD, você precisará adicionar o SAP Business ByDesign da galeria à lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="a3399-124">To configure the integration of SAP Business ByDesign into Azure AD, you need to add SAP Business ByDesign from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a3399-125">**Para adicionar o SAP Business ByDesign da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a3399-125">**To add SAP Business ByDesign from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a3399-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a3399-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="a3399-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="a3399-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a3399-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a3399-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="a3399-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a3399-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="a3399-133">Na caixa de pesquisa, digite **SAP Business ByDesign**, selecione **SAP Business ByDesign** no painel de resultados e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a3399-133">In the search box, type **SAP Business ByDesign**, select **SAP Business ByDesign** from result panel then click **Add** button to add the application.</span></span>

    ![SAP Business ByDesign na lista de resultados](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a3399-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3399-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="a3399-136">Nesta seção, você configurará e testará o logon único do Azure AD com o SAP Business ByDesign, com base em uma usuária de teste chamada "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="a3399-136">In this section, you configure and test Azure AD single sign-on with SAP Business ByDesign based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a3399-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do SAP Business ByDesign é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a3399-137">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP Business ByDesign is to a user in Azure AD.</span></span> <span data-ttu-id="a3399-138">Em outras palavras, é necessário estabelecer uma relação de vinculação entre um usuário do Azure AD e o usuário relacionado no SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="a3399-138">In other words, a link relationship between an Azure AD user and the related user in SAP Business ByDesign needs to be established.</span></span>

<span data-ttu-id="a3399-139">No SAP Business ByDesign, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="a3399-139">In SAP Business ByDesign, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a3399-140">Para configurar e testar o logon único do Azure AD com o SAP Business ByDesign, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="a3399-140">To configure and test Azure AD single sign-on with SAP Business ByDesign, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a3399-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="a3399-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a3399-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="a3399-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a3399-143">**[Criar um usuário de teste do SAP Business ByDesign](#create-an-sap-business-bydesign-test-user)** – para ter um equivalente de Brenda Fernandes no SAP Business ByDesign vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a3399-143">**[Create an SAP Business ByDesign test user](#create-an-sap-business-bydesign-test-user)** - to have a counterpart of Britta Simon in SAP Business ByDesign that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a3399-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a3399-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a3399-145">**[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="a3399-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a3399-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3399-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a3399-147">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="a3399-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAP Business ByDesign application.</span></span>

<span data-ttu-id="a3399-148">**Para configurar o logon único do Azure AD com o SAP Business ByDesign, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a3399-148">**To configure Azure AD single sign-on with SAP Business ByDesign, perform the following steps:**</span></span>

1. <span data-ttu-id="a3399-149">No Portal do Azure, na página de integração de aplicativos do **SAP Business ByDesign**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="a3399-149">In the Azure portal, on the **SAP Business ByDesign** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="a3399-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="a3399-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_samlbase.png)

3. <span data-ttu-id="a3399-153">Na seção **Domínio e URLs do SAP Business ByDesign**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="a3399-153">On the **SAP Business ByDesign Domain and URLs** section, perform the following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_url.png)

    <span data-ttu-id="a3399-155">a.</span><span class="sxs-lookup"><span data-stu-id="a3399-155">a.</span></span> <span data-ttu-id="a3399-156">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<servername>.sapbydesign.com`</span><span class="sxs-lookup"><span data-stu-id="a3399-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<servername>.sapbydesign.com`</span></span>

    <span data-ttu-id="a3399-157">b.</span><span class="sxs-lookup"><span data-stu-id="a3399-157">b.</span></span> <span data-ttu-id="a3399-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<servername>.sapbydesign.com`</span><span class="sxs-lookup"><span data-stu-id="a3399-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<servername>.sapbydesign.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a3399-159">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="a3399-159">These values are not real.</span></span> <span data-ttu-id="a3399-160">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="a3399-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a3399-161">Contate a [equipe de suporte ao cliente do SAP Business ByDesign](https://www.sap.com/products/cloud-analytics.support.html) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="a3399-161">Contact [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) to get these values.</span></span>

4. <span data-ttu-id="a3399-162">Na seção **Atributos de Usuário**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="a3399-162">On the **User Attributes** section, perform the following steps:</span></span>

    ![Seção Atributo do SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_attribute.png)
    
    <span data-ttu-id="a3399-164">a.</span><span class="sxs-lookup"><span data-stu-id="a3399-164">a.</span></span> <span data-ttu-id="a3399-165">Na lista **Identificador de Usuário**, selecione a função **ExtractMailPrefix()**.</span><span class="sxs-lookup"><span data-stu-id="a3399-165">In **User Identifier** list, select the **ExtractMailPrefix()** function.</span></span>
    
    <span data-ttu-id="a3399-166">b.</span><span class="sxs-lookup"><span data-stu-id="a3399-166">b.</span></span> <span data-ttu-id="a3399-167">Na lista de **Email** , selecione o atributo de usuário que você deseja usar na implementação.</span><span class="sxs-lookup"><span data-stu-id="a3399-167">From the **Mail** list, select the user attribute you want to use for your implementation.</span></span> <span data-ttu-id="a3399-168">Por exemplo, se você quiser usar EmployeeID como identificador exclusivo de usuário e tiver armazenado o valor do atributo em ExtensionAttribute2, selecione user.extensionattribute2.</span><span class="sxs-lookup"><span data-stu-id="a3399-168">For example, if you want to use the EmployeeID as unique user identifier and you have stored the attribute value in the ExtensionAttribute2, then select user.extensionattribute2.</span></span>     

5. <span data-ttu-id="a3399-169">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="a3399-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_certificate.png) 

6. <span data-ttu-id="a3399-171">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="a3399-171">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="a3399-173">Na seção **Configuração do SAP Business ByDesign** do Portal do Azure, clique em **Configurar o SAP Business ByDesign** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="a3399-173">On the **SAP Business ByDesign Configuration** section, click **Configure SAP Business ByDesign** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a3399-174">Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="a3399-174">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuração do SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_configure.png) 

8. <span data-ttu-id="a3399-176">Para que o SSO seja configurado para o aplicativo, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="a3399-176">To get SSO configured for your application, perform the following steps:</span></span>
   
    <span data-ttu-id="a3399-177">a.</span><span class="sxs-lookup"><span data-stu-id="a3399-177">a.</span></span> <span data-ttu-id="a3399-178">Faça logon no portal do SAP Business ByDesign com direitos de administrador.</span><span class="sxs-lookup"><span data-stu-id="a3399-178">Sign on to your SAP Business ByDesign portal with administrator rights.</span></span>
   
    <span data-ttu-id="a3399-179">b.</span><span class="sxs-lookup"><span data-stu-id="a3399-179">b.</span></span> <span data-ttu-id="a3399-180">Navegue até **Tarefa Comum de Gerenciamento de Aplicativos e Usuários** e clique na guia **Provedor de Identidade**.</span><span class="sxs-lookup"><span data-stu-id="a3399-180">Navigate to **Application and User Management Common Task** and click the **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="a3399-181">c.</span><span class="sxs-lookup"><span data-stu-id="a3399-181">c.</span></span> <span data-ttu-id="a3399-182">Clique em **Novo Provedor de Identidade** e selecione o arquivo XML de metadados baixado no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a3399-182">Click **New Identity Provider** and select the metadata XML file that you have downloaded from the Azure portal.</span></span> <span data-ttu-id="a3399-183">Com a importação dos metadados, o sistema carrega automaticamente o certificado de assinatura e o certificado de criptografia necessários.</span><span class="sxs-lookup"><span data-stu-id="a3399-183">By importing the metadata, the system automatically uploads the required signature certificate and encryption certificate.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_54.png)
   
    <span data-ttu-id="a3399-185">d.</span><span class="sxs-lookup"><span data-stu-id="a3399-185">d.</span></span> <span data-ttu-id="a3399-186">Para incluir a **URL de Serviço de Consumidor de Declaração** na solicitação SAML, selecione **Incluir URL de Serviço de Consumidor de Declaração**.</span><span class="sxs-lookup"><span data-stu-id="a3399-186">To include the **Assertion Consumer Service URL** into the SAML request, select **Include Assertion Consumer Service URL**.</span></span>
   
    <span data-ttu-id="a3399-187">e.</span><span class="sxs-lookup"><span data-stu-id="a3399-187">e.</span></span> <span data-ttu-id="a3399-188">Clique em **Ativar Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="a3399-188">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="a3399-189">f.</span><span class="sxs-lookup"><span data-stu-id="a3399-189">f.</span></span> <span data-ttu-id="a3399-190">Salve suas alterações.</span><span class="sxs-lookup"><span data-stu-id="a3399-190">Save your changes.</span></span>
   
    <span data-ttu-id="a3399-191">g.</span><span class="sxs-lookup"><span data-stu-id="a3399-191">g.</span></span> <span data-ttu-id="a3399-192">Clique na guia **Meu Sistema** .</span><span class="sxs-lookup"><span data-stu-id="a3399-192">Click the **My System** tab.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_52.png)
   
    <span data-ttu-id="a3399-194">h.</span><span class="sxs-lookup"><span data-stu-id="a3399-194">h.</span></span> <span data-ttu-id="a3399-195">Cole a **URL do Serviço de Logon Único SAML** copiado do Portal do Azure na caixa de texto **URL de Logon do Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="a3399-195">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal it into the **Azure AD Sign On URL** textbox.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_53.png)
   
    <span data-ttu-id="a3399-197">i.</span><span class="sxs-lookup"><span data-stu-id="a3399-197">i.</span></span> <span data-ttu-id="a3399-198">Especifique se o funcionário pode escolher manualmente entre fazer logon com uma ID de usuário e senha ou SSO, selecionando **Seleção de Provedor de Identidade Manual**.</span><span class="sxs-lookup"><span data-stu-id="a3399-198">Specify whether the employee can manually choose between logging on with user ID and password or SSO by selecting **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="a3399-199">j.</span><span class="sxs-lookup"><span data-stu-id="a3399-199">j.</span></span> <span data-ttu-id="a3399-200">Na seção **URL de SSO** , especifique a URL que deve ser usada pelo funcionário para fazer logon no sistema.</span><span class="sxs-lookup"><span data-stu-id="a3399-200">In the **SSO URL** section, specify the URL that should be used by the employee to logon to the system.</span></span> 
    <span data-ttu-id="a3399-201">Na lista suspensa URL Enviada ao Funcionário, você pode escolher entre as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="a3399-201">In the URL Sent to Employee dropdown list, you can choose between the following options:</span></span>
   
    <span data-ttu-id="a3399-202">**URL não SSO**</span><span class="sxs-lookup"><span data-stu-id="a3399-202">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="a3399-203">O sistema envia apenas a URL normal do sistema ao funcionário.</span><span class="sxs-lookup"><span data-stu-id="a3399-203">The system sends only the normal system URL to the employee.</span></span> <span data-ttu-id="a3399-204">O funcionário não pode fazer logon usando o SSO e deve usar uma senha ou um certificado em vez disso.</span><span class="sxs-lookup"><span data-stu-id="a3399-204">The employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="a3399-205">**URL de SSO**</span><span class="sxs-lookup"><span data-stu-id="a3399-205">**SSO URL**</span></span> 
   
    <span data-ttu-id="a3399-206">O sistema envia apenas a URL de SSO ao funcionário.</span><span class="sxs-lookup"><span data-stu-id="a3399-206">The system sends only the SSO URL to the employee.</span></span> <span data-ttu-id="a3399-207">O funcionário pode fazer logon usando o SSO.</span><span class="sxs-lookup"><span data-stu-id="a3399-207">The employee can log on using SSO.</span></span> <span data-ttu-id="a3399-208">A solicitação de autenticação é redirecionada por meio do IdP.</span><span class="sxs-lookup"><span data-stu-id="a3399-208">Authentication request is redirected through the IdP.</span></span>
   
    <span data-ttu-id="a3399-209">**Seleção Automática**</span><span class="sxs-lookup"><span data-stu-id="a3399-209">**Automatic Selection**</span></span>
   
    <span data-ttu-id="a3399-210">Se o SSO não estiver ativo, o sistema enviará a URL normal do sistema ao funcionário.</span><span class="sxs-lookup"><span data-stu-id="a3399-210">If SSO is not active, the system sends the normal system URL to the employee.</span></span> <span data-ttu-id="a3399-211">Se o SSO estiver ativo, o sistema verificará se o funcionário tem uma senha.</span><span class="sxs-lookup"><span data-stu-id="a3399-211">If SSO is active, the system checks whether the employee has a password.</span></span> <span data-ttu-id="a3399-212">Se uma senha estiver disponível, a URL de SSO e a URL não SSO serão enviadas ao funcionário.</span><span class="sxs-lookup"><span data-stu-id="a3399-212">If a password is available, both SSO URL and Non-SSO URL are sent to the employee.</span></span> <span data-ttu-id="a3399-213">No entanto, se o funcionário não tiver uma senha, apenas a URL de SSO será enviada ao funcionário.</span><span class="sxs-lookup"><span data-stu-id="a3399-213">However, if the employee has no password, only the SSO URL is sent to the employee.</span></span>
   
    <span data-ttu-id="a3399-214">k.</span><span class="sxs-lookup"><span data-stu-id="a3399-214">k.</span></span> <span data-ttu-id="a3399-215">Salve suas alterações.</span><span class="sxs-lookup"><span data-stu-id="a3399-215">Save your changes.</span></span>

> [!TIP]
> <span data-ttu-id="a3399-216">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="a3399-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a3399-217">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="a3399-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a3399-218">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a3399-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a3399-219">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3399-219">Create an Azure AD test user</span></span>

<span data-ttu-id="a3399-220">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="a3399-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="a3399-222">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a3399-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a3399-223">No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a3399-223">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="a3399-225">Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="a3399-225">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="a3399-227">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.</span><span class="sxs-lookup"><span data-stu-id="a3399-227">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![O botão Adicionar](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="a3399-229">Na caixa de diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="a3399-229">In the **User** dialog box, perform the following steps:</span></span>

    ![A caixa de diálogo Usuário](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_04.png)

    <span data-ttu-id="a3399-231">a.</span><span class="sxs-lookup"><span data-stu-id="a3399-231">a.</span></span> <span data-ttu-id="a3399-232">Na caixa **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="a3399-232">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a3399-233">b.</span><span class="sxs-lookup"><span data-stu-id="a3399-233">b.</span></span> <span data-ttu-id="a3399-234">Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="a3399-234">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="a3399-235">c.</span><span class="sxs-lookup"><span data-stu-id="a3399-235">c.</span></span> <span data-ttu-id="a3399-236">Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.</span><span class="sxs-lookup"><span data-stu-id="a3399-236">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="a3399-237">d.</span><span class="sxs-lookup"><span data-stu-id="a3399-237">d.</span></span> <span data-ttu-id="a3399-238">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a3399-238">Click **Create**.</span></span>
 
### <a name="create-an-sap-business-bydesign-test-user"></a><span data-ttu-id="a3399-239">Criar um usuário de teste do SAP Business ByDesign</span><span class="sxs-lookup"><span data-stu-id="a3399-239">Create an SAP Business ByDesign test user</span></span>

<span data-ttu-id="a3399-240">Nesta seção, você criará uma usuária chamada Brenda Fernandes no SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="a3399-240">In this section, you create a user called Britta Simon in SAP Business ByDesign.</span></span> <span data-ttu-id="a3399-241">Trabalhe com a [equipe de suporte ao cliente do SAP Business ByDesign](https://www.sap.com/products/cloud-analytics.support.html) para adicionar os usuários à plataforma SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="a3399-241">Please work with [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) to add the users in the SAP Business ByDesign platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="a3399-242">Verifique se o valor de NameID corresponde ao campo de nome de usuário na plataforma SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="a3399-242">Please make sure that NameID value should match with the username field in the SAP Business ByDesign platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="a3399-243">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3399-243">Assign the Azure AD test user</span></span>

<span data-ttu-id="a3399-244">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="a3399-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP Business ByDesign.</span></span>

![Atribuir a função de usuário][200] 

<span data-ttu-id="a3399-246">**Para atribuir Brenda Fernandes ao SAP Business ByDesign, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a3399-246">**To assign Britta Simon to SAP Business ByDesign, perform the following steps:**</span></span>

1. <span data-ttu-id="a3399-247">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a3399-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="a3399-249">Na lista de aplicativos, selecione **SAP Business ByDesign**.</span><span class="sxs-lookup"><span data-stu-id="a3399-249">In the applications list, select **SAP Business ByDesign**.</span></span>

    ![O link do SAP Business ByDesign na lista de Aplicativos](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_app.png)  

3. <span data-ttu-id="a3399-251">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="a3399-251">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202]

4. <span data-ttu-id="a3399-253">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a3399-253">Click **Add** button.</span></span> <span data-ttu-id="a3399-254">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a3399-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="a3399-256">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="a3399-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a3399-257">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a3399-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a3399-258">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a3399-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a3399-259">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="a3399-259">Test single sign-on</span></span>

<span data-ttu-id="a3399-260">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="a3399-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a3399-261">Ao clicar no bloco do SAP Business ByDesign no Painel de Acesso, você deve ser conectado automaticamente ao aplicativo SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="a3399-261">When you click the SAP Business ByDesign tile in the Access Panel, you should get automatically signed-on to your SAP Business ByDesign application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a3399-262">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="a3399-262">Additional resources</span></span>

* [<span data-ttu-id="a3399-263">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="a3399-263">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a3399-264">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a3399-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_203.png

