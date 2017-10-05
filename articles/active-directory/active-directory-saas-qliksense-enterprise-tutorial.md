---
title: "Tutorial: Integração do Azure Active Directory com o Qlik Sense Enterprise | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Qlik Sense Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8c27e340-2b25-47b6-bf1f-438be4c14f93
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 4964634cd5aaf0dbb98c766f5e12700c4d118750
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qlik-sense-enterprise"></a><span data-ttu-id="473c5-103">Tutorial: integração do Azure Active Directory ao Qlik Sense Enterprise</span><span class="sxs-lookup"><span data-stu-id="473c5-103">Tutorial: Azure Active Directory integration with Qlik Sense Enterprise</span></span>

<span data-ttu-id="473c5-104">Neste tutorial, você aprenderá como integrar o Qlik Sense Enterprise ao Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="473c5-104">In this tutorial, you learn how to integrate Qlik Sense Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="473c5-105">Integrar o Qlik Sense Enterprise ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="473c5-105">Integrating Qlik Sense Enterprise with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="473c5-106">Você pode controlar no Azure AD que tenha acesso ao Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="473c5-106">You can control in Azure AD who has access to Qlik Sense Enterprise.</span></span>
- <span data-ttu-id="473c5-107">Você pode habilitar seus usuários a fazerem logon automaticamente no Qlik Sense Enterprise (logon único) com suas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="473c5-107">You can enable your users to automatically get signed-on to Qlik Sense Enterprise (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="473c5-108">Você pode gerenciar suas contas em um único local central – o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="473c5-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="473c5-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="473c5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="473c5-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="473c5-110">Prerequisites</span></span>

<span data-ttu-id="473c5-111">Para configurar a integração do Azure AD ao Qlik Sense Enterprise, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="473c5-111">To configure Azure AD integration with Qlik Sense Enterprise, you need the following items:</span></span>

- <span data-ttu-id="473c5-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="473c5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="473c5-113">Uma assinatura do Qlik Sense Enterprise habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="473c5-113">A Qlik Sense Enterprise single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="473c5-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="473c5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="473c5-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="473c5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="473c5-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="473c5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="473c5-117">Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="473c5-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="473c5-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="473c5-118">Scenario description</span></span>
<span data-ttu-id="473c5-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="473c5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="473c5-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="473c5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="473c5-121">Adicionar Qlik Sense Enterprise da galeria</span><span class="sxs-lookup"><span data-stu-id="473c5-121">Adding Qlik Sense Enterprise from the gallery</span></span>
2. <span data-ttu-id="473c5-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="473c5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-qlik-sense-enterprise-from-the-gallery"></a><span data-ttu-id="473c5-123">Adicionar Qlik Sense Enterprise da galeria</span><span class="sxs-lookup"><span data-stu-id="473c5-123">Adding Qlik Sense Enterprise from the gallery</span></span>
<span data-ttu-id="473c5-124">Para configurar a integração do Qlik Sense Enterprise com o Azure AD, você precisará adicionar o Qlik Sense Enterprise à sua lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="473c5-124">To configure the integration of Qlik Sense Enterprise into Azure AD, you need to add Qlik Sense Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="473c5-125">**Para adicionar o Qlik Sense Enterprise por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="473c5-125">**To add Qlik Sense Enterprise from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="473c5-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="473c5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="473c5-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="473c5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="473c5-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="473c5-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="473c5-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="473c5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="473c5-133">Na caixa de pesquisa, digite **Qlik Sense Enterprise**, selecione **Qlik Sense Enterprise** no painel de resultados e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="473c5-133">In the search box, type **Qlik Sense Enterprise**, select **Qlik Sense Enterprise** from result panel then click **Add** button to add the application.</span></span>

    ![Qlik Sense Enterprise na lista de resultados](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="473c5-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="473c5-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="473c5-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Qlik Sense Enterprise, com base em uma usuária de teste chamada "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="473c5-136">In this section, you configure and test Azure AD single sign-on with Qlik Sense Enterprise based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="473c5-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Qlik Sense Enterprise é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="473c5-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Qlik Sense Enterprise is to a user in Azure AD.</span></span> <span data-ttu-id="473c5-138">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="473c5-138">In other words, a link relationship between an Azure AD user and the related user in Qlik Sense Enterprise needs to be established.</span></span>

<span data-ttu-id="473c5-139">No Qlik Sense Enterprise, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="473c5-139">In Qlik Sense Enterprise, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="473c5-140">Para configurar e testar o logon único do Azure AD com o Qlik Sense Enterprise, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="473c5-140">To configure and test Azure AD single sign-on with Qlik Sense Enterprise, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="473c5-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="473c5-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="473c5-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="473c5-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="473c5-143">**[Criar de um usuário de teste do Qlik Sense Enterprise](#create-a-qlik-sense-enterprise-test-user)**: para ter um equivalente de Brenda Fernandes no Qlik Sense Enterprise que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="473c5-143">**[Create a Qlik Sense Enterprise test user](#create-a-qlik-sense-enterprise-test-user)** - to have a counterpart of Britta Simon in Qlik Sense Enterprise that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="473c5-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="473c5-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="473c5-145">**[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="473c5-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="473c5-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="473c5-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="473c5-147">Nesta seção, você habilitará o logon único do Azure AD no portal do Azure e configurará o logon único em seu aplicativo Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="473c5-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Qlik Sense Enterprise application.</span></span>

<span data-ttu-id="473c5-148">**Para configurar o logon único do Azure AD com Qlik Sense Enterprise, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="473c5-148">**To configure Azure AD single sign-on with Qlik Sense Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="473c5-149">No portal do Azure, na página de integração de aplicativos do **Qlik Sense Enterprise**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="473c5-149">In the Azure portal, on the **Qlik Sense Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="473c5-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="473c5-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_samlbase.png)

3. <span data-ttu-id="473c5-153">Na seção **URLs e Domínio do Qlik Sense Enterprise**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="473c5-153">On the **Qlik Sense Enterprise Domain and URLs** section, perform the following steps:</span></span>

    ![Informações de logon único em Domínio e URLs do Qlik Sense Enterprise](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_url.png)

    <span data-ttu-id="473c5-155">a.</span><span class="sxs-lookup"><span data-stu-id="473c5-155">a.</span></span> <span data-ttu-id="473c5-156">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`</span><span class="sxs-lookup"><span data-stu-id="473c5-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="473c5-157">Observe a barra à direita no fim desse URI.</span><span class="sxs-lookup"><span data-stu-id="473c5-157">Note the trailing slash at the end of this URI.</span></span> <span data-ttu-id="473c5-158">Ela é necessária.</span><span class="sxs-lookup"><span data-stu-id="473c5-158">It is required.</span></span>
    
    <span data-ttu-id="473c5-159">b.</span><span class="sxs-lookup"><span data-stu-id="473c5-159">b.</span></span> <span data-ttu-id="473c5-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="473c5-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qlikpoc.com`|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qliksense.com`|

    > [!NOTE] 
    > <span data-ttu-id="473c5-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="473c5-161">These values are not real.</span></span> <span data-ttu-id="473c5-162">Atualize esses valores com a URL de Logon e o Identificador, explicados adiante no tutorial, ou entre em contato com a [equipe de suporte do Cliente do Qlik Sense Enterprise](https://www.qlik.com/us/services/support) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="473c5-162">Update these values with the actual Sign-On URL and Identifier, Which are explained later in this tutorial or contact [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) to get these values.</span></span> 

4. <span data-ttu-id="473c5-163">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="473c5-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_certificate.png) 

5. <span data-ttu-id="473c5-165">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="473c5-165">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="473c5-167">Prepare o arquivo XML de Metadados de Federação para que você possa carregar no servidor Qlik Sense.</span><span class="sxs-lookup"><span data-stu-id="473c5-167">Prepare the Federation Metadata XML file so that you can upload that to Qlik Sense server.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="473c5-168">Antes de carregar os metadados IdP para o servidor Qlik Sense, o arquivo precisa ser editado para remover as informações e garantir a operação correta entre o Azure AD e o servidor Qlik Sense.</span><span class="sxs-lookup"><span data-stu-id="473c5-168">Before uploading the IdP metadata to the Qlik Sense server, the file needs to be edited to remove information to ensure proper operation between Azure AD and Qlik Sense server.</span></span>
    
    ![QlikSense][qs24]
   
    <span data-ttu-id="473c5-170">a.</span><span class="sxs-lookup"><span data-stu-id="473c5-170">a.</span></span> <span data-ttu-id="473c5-171">Abra o arquivo FederationMetaData.xml baixado do portal do Azure em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="473c5-171">Open the FederationMetaData.xml file, which you have downloaded from Azure portal in a text editor.</span></span>
   
    <span data-ttu-id="473c5-172">b.</span><span class="sxs-lookup"><span data-stu-id="473c5-172">b.</span></span> <span data-ttu-id="473c5-173">Procure o valor **RoleDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="473c5-173">Search for the value **RoleDescriptor**.</span></span>  <span data-ttu-id="473c5-174">Há quatro entradas (dois pares de marcas de elemento de abertura e fechamento).</span><span class="sxs-lookup"><span data-stu-id="473c5-174">There are four entries (two pairs of opening and closing element tags).</span></span>
   
    <span data-ttu-id="473c5-175">c.</span><span class="sxs-lookup"><span data-stu-id="473c5-175">c.</span></span> <span data-ttu-id="473c5-176">Exclua todas as informações e as marcas RoleDescriptor do arquivo.</span><span class="sxs-lookup"><span data-stu-id="473c5-176">Delete the RoleDescriptor tags and all information in between from the file.</span></span>
   
    <span data-ttu-id="473c5-177">d.</span><span class="sxs-lookup"><span data-stu-id="473c5-177">d.</span></span> <span data-ttu-id="473c5-178">Salve o arquivo e mantenha-o à mão para uso posterior neste documento.</span><span class="sxs-lookup"><span data-stu-id="473c5-178">Save the file and keep it nearby for use later in this document.</span></span>

7. <span data-ttu-id="473c5-179">Navegue para o QMC (Qlik Sense Qlik Management Console) como um usuário que pode criar configurações de proxy virtual.</span><span class="sxs-lookup"><span data-stu-id="473c5-179">Navigate to the Qlik Sense Qlik Management Console (QMC) as a user who can create virtual proxy configurations.</span></span>

8. <span data-ttu-id="473c5-180">No QMC, clique no item de menu **Virtual Proxies**.</span><span class="sxs-lookup"><span data-stu-id="473c5-180">In the QMC, click on the **Virtual Proxies** menu item.</span></span>
   
    ![QlikSense][qs6] 

9. <span data-ttu-id="473c5-182">Na parte inferior da tela, clique no botão **Criar novo**.</span><span class="sxs-lookup"><span data-stu-id="473c5-182">At the bottom of the screen, click the **Create new** button.</span></span>
   
    ![QlikSense][qs7]

10. <span data-ttu-id="473c5-184">A tela de Edição de proxy virtual é exibida.</span><span class="sxs-lookup"><span data-stu-id="473c5-184">The Virtual proxy edit screen appears.</span></span>  <span data-ttu-id="473c5-185">No lado direito da tela, há um menu para tornar as opções de configuração visíveis.</span><span class="sxs-lookup"><span data-stu-id="473c5-185">On the right side of the screen is a menu for making configuration options visible.</span></span>
   
    ![QlikSense][qs9]

11. <span data-ttu-id="473c5-187">Com a opção de menu identificação marcada, insira as informações de identificação para a configuração de proxy virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="473c5-187">With the Identification menu option checked, enter the identifying information for the Azure virtual proxy configuration.</span></span>
    
    ![QlikSense][qs8]  
    
    <span data-ttu-id="473c5-189">a.</span><span class="sxs-lookup"><span data-stu-id="473c5-189">a.</span></span> <span data-ttu-id="473c5-190">O campo **Descrição** é um nome amigável para a configuração do proxy virtual.</span><span class="sxs-lookup"><span data-stu-id="473c5-190">The **Description** field is a friendly name for the virtual proxy configuration.</span></span>  <span data-ttu-id="473c5-191">Insira um valor para uma descrição.</span><span class="sxs-lookup"><span data-stu-id="473c5-191">Enter a value for a description.</span></span>
    
    <span data-ttu-id="473c5-192">b.</span><span class="sxs-lookup"><span data-stu-id="473c5-192">b.</span></span> <span data-ttu-id="473c5-193">O campo **Prefixo** identifica o ponto de extremidade do proxy virtual para se conectar ao Qlik Sense com o Logon Único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="473c5-193">The **Prefix** field identifies the virtual proxy endpoint for connecting to Qlik Sense with Azure AD Single Sign-On.</span></span>  <span data-ttu-id="473c5-194">Insira um nome de prefixo exclusivo para esse proxy virtual.</span><span class="sxs-lookup"><span data-stu-id="473c5-194">Enter a unique prefix name for this virtual proxy.</span></span>
    
    <span data-ttu-id="473c5-195">c.</span><span class="sxs-lookup"><span data-stu-id="473c5-195">c.</span></span> <span data-ttu-id="473c5-196">**Tempo limite de inatividade de sessão (minutos)** é o tempo limite para conexões por meio desse proxy virtual.</span><span class="sxs-lookup"><span data-stu-id="473c5-196">**Session inactivity timeout (minutes)** is the timeout for connections through this virtual proxy.</span></span>
    
    <span data-ttu-id="473c5-197">d.</span><span class="sxs-lookup"><span data-stu-id="473c5-197">d.</span></span> <span data-ttu-id="473c5-198">O **Nome de cabeçalho de cookie de sessão** é o nome do cookie que armazena o identificador de sessão para a sessão do Qlik Sense que um usuário recebe após uma autenticação bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="473c5-198">The **Session cookie header name** is the cookie name storing the session identifier for the Qlik Sense session a user receives after successful authentication.</span></span>  <span data-ttu-id="473c5-199">Esse nome deve ser exclusivo.</span><span class="sxs-lookup"><span data-stu-id="473c5-199">This name must be unique.</span></span>

12. <span data-ttu-id="473c5-200">Clique na opção de menu de autenticação para torná-la visível.</span><span class="sxs-lookup"><span data-stu-id="473c5-200">Click on the Authentication menu option to make it visible.</span></span>  <span data-ttu-id="473c5-201">Aparece a tela de autenticação.</span><span class="sxs-lookup"><span data-stu-id="473c5-201">The Authentication screen appears.</span></span>
    
    ![QlikSense][qs10]
    
    <span data-ttu-id="473c5-203">a.</span><span class="sxs-lookup"><span data-stu-id="473c5-203">a.</span></span> <span data-ttu-id="473c5-204">O menu suspenso **Modo de acesso anônimo** determina se os usuários anônimos podem acessar o Qlik Sense por meio do proxy virtual.</span><span class="sxs-lookup"><span data-stu-id="473c5-204">The **Anonymous access mode** drop down determines if anonymous users may access Qlik Sense through the virtual proxy.</span></span>  <span data-ttu-id="473c5-205">A opção padrão é Nenhum usuário anônimo.</span><span class="sxs-lookup"><span data-stu-id="473c5-205">The default option is No anonymous user.</span></span>
    
    <span data-ttu-id="473c5-206">b.</span><span class="sxs-lookup"><span data-stu-id="473c5-206">b.</span></span> <span data-ttu-id="473c5-207">O menu suspenso **Método de autenticação** determina o esquema de autenticação que o proxy virtual usará.</span><span class="sxs-lookup"><span data-stu-id="473c5-207">The **Authentication method** drop-down determines the authentication scheme the virtual proxy will use.</span></span>  <span data-ttu-id="473c5-208">Selecione SAML na lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="473c5-208">Select SAML from the drop-down list.</span></span>  <span data-ttu-id="473c5-209">Mais opções são exibidas como resultado.</span><span class="sxs-lookup"><span data-stu-id="473c5-209">More options appear as a result.</span></span>
    
    <span data-ttu-id="473c5-210">c.</span><span class="sxs-lookup"><span data-stu-id="473c5-210">c.</span></span> <span data-ttu-id="473c5-211">No **campo URI de host SAML**, insira o nome de host que os usuários precisam usar para acessar o Qlik Sense por meio desse proxy virtual SAML.</span><span class="sxs-lookup"><span data-stu-id="473c5-211">In the **SAML host URI field**, input the hostname users enter to access Qlik Sense through this SAML virtual proxy.</span></span>  <span data-ttu-id="473c5-212">O nome do host é o uri do servidor Qlik Sense.</span><span class="sxs-lookup"><span data-stu-id="473c5-212">The hostname is the uri of the Qlik Sense server.</span></span>
    
    <span data-ttu-id="473c5-213">d.</span><span class="sxs-lookup"><span data-stu-id="473c5-213">d.</span></span> <span data-ttu-id="473c5-214">Na **ID da entidade SAML**, insira o mesmo valor inserido para o campo URI de host SAML.</span><span class="sxs-lookup"><span data-stu-id="473c5-214">In the **SAML entity ID**, enter the same value entered for the SAML host URI field.</span></span>
    
    <span data-ttu-id="473c5-215">e.</span><span class="sxs-lookup"><span data-stu-id="473c5-215">e.</span></span> <span data-ttu-id="473c5-216">**Metadados IdP SAML** é o arquivo editado anteriormente na seção **Editar metadados de federação de configuração do Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="473c5-216">The **SAML IdP metadata** is the file edited earlier in the **Edit Federation Metadata from Azure AD Configuration** section.</span></span>  <span data-ttu-id="473c5-217">**Antes de carregar os metadados IdP, o arquivo precisa ser editado** para remover as informações e garantir a operação correta entre o Azure AD e servidor Qlik Sense.</span><span class="sxs-lookup"><span data-stu-id="473c5-217">**Before uploading the IdP metadata, the file needs to be edited** to remove information to ensure proper operation between Azure AD and Qlik Sense server.</span></span>  <span data-ttu-id="473c5-218">**Veja as instruções acima se o arquivo ainda precisar ser editado.**</span><span class="sxs-lookup"><span data-stu-id="473c5-218">**Please refer to the instructions above if the file has yet to be edited.**</span></span>  <span data-ttu-id="473c5-219">Se o arquivo foi editado, clique no botão Procurar e selecione o arquivo de metadados editado para carregá-lo para a configuração do proxy virtual.</span><span class="sxs-lookup"><span data-stu-id="473c5-219">If the file has been edited click on the Browse button and select the edited metadata file to upload it to the virtual proxy configuration.</span></span>
    
    <span data-ttu-id="473c5-220">f.</span><span class="sxs-lookup"><span data-stu-id="473c5-220">f.</span></span> <span data-ttu-id="473c5-221">Insira a referência de nome ou o esquema de atributo para o atributo SAML que representa o **UserID** que o Azure AD envia ao servidor Qlik Sense.</span><span class="sxs-lookup"><span data-stu-id="473c5-221">Enter the attribute name or schema reference for the SAML attribute representing the **UserID** Azure AD sends to the Qlik Sense server.</span></span>  <span data-ttu-id="473c5-222">Informações de referência de esquema estão disponíveis na configuração de postagem de telas do aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="473c5-222">Schema reference information is available in the Azure app screens post configuration.</span></span>  <span data-ttu-id="473c5-223">Para usar o atributo de nome, insira `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="473c5-223">To use the name attribute, enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
    
    <span data-ttu-id="473c5-224">g.</span><span class="sxs-lookup"><span data-stu-id="473c5-224">g.</span></span> <span data-ttu-id="473c5-225">Insira o valor para o **diretório de usuário** que será anexado aos usuários quando eles se autenticarem no servidor Qlik Sense por meio do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="473c5-225">Enter the value for the **user directory** that will be attached to users when they authenticate to Qlik Sense server through Azure AD.</span></span>  <span data-ttu-id="473c5-226">Valores embutidos em código devem estar entre **colchetes []**.</span><span class="sxs-lookup"><span data-stu-id="473c5-226">Hardcoded values must be surrounded by **square brackets []**.</span></span>  <span data-ttu-id="473c5-227">Para usar um atributo enviado na asserção SAML do Azure AD, digite o nome do atributo na caixa de texto **sem** colchetes.</span><span class="sxs-lookup"><span data-stu-id="473c5-227">To use an attribute sent in the Azure AD SAML assertion, enter the name of the attribute in this text box **without** square brackets.</span></span>
    
    <span data-ttu-id="473c5-228">h.</span><span class="sxs-lookup"><span data-stu-id="473c5-228">h.</span></span> <span data-ttu-id="473c5-229">O **algoritmo de assinatura SAML** define o certificado de provedor (nesse caso, o servidor Qlik Sense) do serviço de assinatura para a configuração de proxy virtual.</span><span class="sxs-lookup"><span data-stu-id="473c5-229">The **SAML signing algorithm** sets the service provider (in this case Qlik Sense server) certificate signing for the virtual proxy configuration.</span></span>  <span data-ttu-id="473c5-230">Se o servidor Qlik Sense usar um certificado confiável gerado usando o Microsoft Enhanced RSA e o Provedor de Criptografia AES, altere o algoritmo de assinatura de SAML para **SHA-256**.</span><span class="sxs-lookup"><span data-stu-id="473c5-230">If Qlik Sense server uses a trusted certificate generated using Microsoft Enhanced RSA and AES Cryptographic Provider, change the SAML signing algorithm to **SHA-256**.</span></span>
    
    <span data-ttu-id="473c5-231">i.</span><span class="sxs-lookup"><span data-stu-id="473c5-231">i.</span></span> <span data-ttu-id="473c5-232">A seção de mapeamento de atributo SAML permite que atributos adicionais como grupos sejam enviados ao Qlik Sense para uso em regras de segurança.</span><span class="sxs-lookup"><span data-stu-id="473c5-232">The SAML attribute mapping section allows for additional attributes like groups to be sent to Qlik Sense for use in security rules.</span></span>

13. <span data-ttu-id="473c5-233">Clique na opção de menu **BALANCEAMENTO DE CARGA** para torná-la visível.</span><span class="sxs-lookup"><span data-stu-id="473c5-233">Click on the **LOAD BALANCING** menu option to make it visible.</span></span>  <span data-ttu-id="473c5-234">Aparece a tela Balanceamento de Carga.</span><span class="sxs-lookup"><span data-stu-id="473c5-234">The Load Balancing screen appears.</span></span>
    
    ![QlikSense][qs11]

14. <span data-ttu-id="473c5-236">Clique no botão **Adicionar novo nó de servidor**, selecione o(s) nó(s) de mecanismo aos quais o Qlik Sense enviará sessões para fins de balanceamento de carga e clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="473c5-236">Click on the **Add new server node** button, select engine node or nodes Qlik Sense will send sessions to for load balancing purposes, and click the **Add** button.</span></span>
    
    ![QlikSense][qs12]

15. <span data-ttu-id="473c5-238">Clique na opção de menu Avançado para torná-la visível.</span><span class="sxs-lookup"><span data-stu-id="473c5-238">Click on the Advanced menu option to make it visible.</span></span> <span data-ttu-id="473c5-239">Aparece a tela Avançado.</span><span class="sxs-lookup"><span data-stu-id="473c5-239">The Advanced screen appears.</span></span>
    
    ![QlikSense][qs13]
    
    <span data-ttu-id="473c5-241">A lista de permissões de Host identifica os nomes de host que são aceitos durante a conexão com o servidor Qlik Sense.</span><span class="sxs-lookup"><span data-stu-id="473c5-241">The Host white list identifies hostnames that are accepted when connecting to the Qlik Sense server.</span></span>  <span data-ttu-id="473c5-242">**Insira o nome do host que os usuários especificarão ao se conectar ao servidor Qlik Sense.**</span><span class="sxs-lookup"><span data-stu-id="473c5-242">**Enter the hostname users will specify when connecting to Qlik Sense server.**</span></span> <span data-ttu-id="473c5-243">O nome do host é o mesmo valor que o uri de host SAML, sem https://.</span><span class="sxs-lookup"><span data-stu-id="473c5-243">The hostname is the same value as the SAML host uri without the https://.</span></span>

16. <span data-ttu-id="473c5-244">Clique no botão **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="473c5-244">Click the **Apply** button.</span></span>
    
    ![QlikSense][qs14]

17. <span data-ttu-id="473c5-246">Clique em OK para aceitar a mensagem de aviso informando que proxies vinculados ao proxy virtual serão reiniciados.</span><span class="sxs-lookup"><span data-stu-id="473c5-246">Click OK to accept the warning message that states proxies linked to the virtual proxy will be restarted.</span></span>
    
    ![QlikSense][qs15]

18. <span data-ttu-id="473c5-248">No lado direito da tela, o menu Itens Associados é exibido.</span><span class="sxs-lookup"><span data-stu-id="473c5-248">On the right side of the screen, the Associated items menu appears.</span></span>  <span data-ttu-id="473c5-249">Clique na opção de menu **Proxies**.</span><span class="sxs-lookup"><span data-stu-id="473c5-249">Click on the **Proxies** menu option.</span></span>
    
    ![QlikSense][qs16]

19. <span data-ttu-id="473c5-251">Aparece a tela de proxy.</span><span class="sxs-lookup"><span data-stu-id="473c5-251">The proxy screen appears.</span></span>  <span data-ttu-id="473c5-252">Clique no botão **Vincular** na parte inferior para vincular um proxy ao proxy virtual.</span><span class="sxs-lookup"><span data-stu-id="473c5-252">Click the **Link** button at the bottom to link a proxy to the virtual proxy.</span></span>
    
    ![QlikSense][qs17]

20. <span data-ttu-id="473c5-254">Selecione o nó de proxy que dará suporte a essa conexão de proxy virtual e clique no botão **Vincular**.</span><span class="sxs-lookup"><span data-stu-id="473c5-254">Select the proxy node that will support this virtual proxy connection and click the **Link** button.</span></span>  <span data-ttu-id="473c5-255">Depois da vinculação, o proxy será listado nos proxies associados.</span><span class="sxs-lookup"><span data-stu-id="473c5-255">After linking, the proxy will be listed under associated proxies.</span></span>
    
    ![QlikSense][qs18]
  
    ![QlikSense][qs19]

21. <span data-ttu-id="473c5-258">Após cerca de cinco a dez segundos, será exibida a mensagem Atualizar QMC.</span><span class="sxs-lookup"><span data-stu-id="473c5-258">After about five to ten seconds, the Refresh QMC message will appear.</span></span>  <span data-ttu-id="473c5-259">Clique no botão **Atualizar QMC**.</span><span class="sxs-lookup"><span data-stu-id="473c5-259">Click the **Refresh QMC** button.</span></span>
    
    ![QlikSense][qs20]

22. <span data-ttu-id="473c5-261">Quando o QMC for atualizado, clique no item de menu **Virtual proxies**.</span><span class="sxs-lookup"><span data-stu-id="473c5-261">When the QMC refreshes, click on the **Virtual proxies** menu item.</span></span> <span data-ttu-id="473c5-262">A nova entrada de proxy virtual SAML é listada na tabela na tela.</span><span class="sxs-lookup"><span data-stu-id="473c5-262">The new SAML virtual proxy entry is listed in the table on the screen.</span></span>  <span data-ttu-id="473c5-263">Clique na entrada de proxy virtual.</span><span class="sxs-lookup"><span data-stu-id="473c5-263">Single click on the virtual proxy entry.</span></span>
    
    ![QlikSense][qs51]

23. <span data-ttu-id="473c5-265">Na parte inferior da tela, o botão Baixar metadados SP será ativado.</span><span class="sxs-lookup"><span data-stu-id="473c5-265">At the bottom of the screen, the Download SP metadata button will activate.</span></span>  <span data-ttu-id="473c5-266">Clique no botão **Baixar metadados SP** para salvar os metadados em um arquivo.</span><span class="sxs-lookup"><span data-stu-id="473c5-266">Click the **Download SP metadata** button to save the metadata to a file.</span></span>
    
    ![QlikSense][qs52]

24. <span data-ttu-id="473c5-268">Abra o arquivo de metadados sp.</span><span class="sxs-lookup"><span data-stu-id="473c5-268">Open the sp metadata file.</span></span>  <span data-ttu-id="473c5-269">Observe a entrada **entityID** e a entrada **AssertionConsumerService**.</span><span class="sxs-lookup"><span data-stu-id="473c5-269">Observe the **entityID** entry and the **AssertionConsumerService** entry.</span></span>  <span data-ttu-id="473c5-270">Esses valores são equivalentes ao **Identificador** e à **URL de logon** na configuração do aplicativo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="473c5-270">These values are equivalent to the **Identifier** and the **Sign on URL** in the Azure AD application configuration.</span></span> <span data-ttu-id="473c5-271">Cole esses valores na seção **Domínio e URLs do Qlik Sense Enterprise** na configuração do aplicativo do Azure AD se não forem correspondentes e, em seguida, você deverá substituí-los no assistente de configuração de aplicativo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="473c5-271">Paste these values in the **Qlik Sense Enterprise Domain and URLs** section in the Azure AD application configuration if they are not matching, then you should replace them in the Azure AD App configuration wizard.</span></span>
    
    ![QlikSense][qs53]

> [!TIP]
> <span data-ttu-id="473c5-273">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="473c5-273">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="473c5-274">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="473c5-274">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="473c5-275">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="473c5-275">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="473c5-276">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="473c5-276">Create an Azure AD test user</span></span>
<span data-ttu-id="473c5-277">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="473c5-277">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="473c5-279">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="473c5-279">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="473c5-280">No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="473c5-280">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

   ![O botão Azure Active Directory](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="473c5-282">Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="473c5-282">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

   ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="473c5-284">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.</span><span class="sxs-lookup"><span data-stu-id="473c5-284">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

   ![O botão Adicionar](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="473c5-286">Na caixa de diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="473c5-286">In the **User** dialog box, perform the following steps:</span></span>

   ![A caixa de diálogo Usuário](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_04.png)

   <span data-ttu-id="473c5-288">a.</span><span class="sxs-lookup"><span data-stu-id="473c5-288">a.</span></span> <span data-ttu-id="473c5-289">Na caixa **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="473c5-289">In the **Name** box, type **BrittaSimon**.</span></span>

   <span data-ttu-id="473c5-290">b.</span><span class="sxs-lookup"><span data-stu-id="473c5-290">b.</span></span> <span data-ttu-id="473c5-291">Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="473c5-291">In the **User name** box, type the email address of user Britta Simon.</span></span>

   <span data-ttu-id="473c5-292">c.</span><span class="sxs-lookup"><span data-stu-id="473c5-292">c.</span></span> <span data-ttu-id="473c5-293">Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.</span><span class="sxs-lookup"><span data-stu-id="473c5-293">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

   <span data-ttu-id="473c5-294">d.</span><span class="sxs-lookup"><span data-stu-id="473c5-294">d.</span></span> <span data-ttu-id="473c5-295">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="473c5-295">Click **Create**.</span></span>
 
### <a name="create-a-qlik-sense-enterprise-test-user"></a><span data-ttu-id="473c5-296">Criar um usuário de teste do Qlik Sense Enterprise</span><span class="sxs-lookup"><span data-stu-id="473c5-296">Create a Qlik Sense Enterprise test user</span></span>

<span data-ttu-id="473c5-297">Nesta seção, você deve criar uma usuária chamada Brenda Fernandes no Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="473c5-297">In this section, you create a user called Britta Simon in Qlik Sense Enterprise.</span></span> <span data-ttu-id="473c5-298">Trabalhe com a [equipe de suporte do Cliente do Qlik Sense Enterprise](https://www.qlik.com/us/services/support) para adicionar os usuários na plataforma Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="473c5-298">Work with [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) to add the users in the Qlik Sense Enterprise platform.</span></span> <span data-ttu-id="473c5-299">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="473c5-299">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="473c5-300">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="473c5-300">Assign the Azure AD test user</span></span>

<span data-ttu-id="473c5-301">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo acesso ao Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="473c5-301">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Qlik Sense Enterprise.</span></span>

![Atribuir a função de usuário][200] 

<span data-ttu-id="473c5-303">**Para atribuir Brenda Fernandes ao Qlik Sense Enterprise, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="473c5-303">**To assign Britta Simon to Qlik Sense Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="473c5-304">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="473c5-304">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="473c5-306">Na lista de aplicativos, selecione **Qlik Sense Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="473c5-306">In the applications list, select **Qlik Sense Enterprise**.</span></span>

    ![O link do Qlik Sense Enterprise na lista de Aplicativos](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_app.png)  

3. <span data-ttu-id="473c5-308">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="473c5-308">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202]

4. <span data-ttu-id="473c5-310">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="473c5-310">Click **Add** button.</span></span> <span data-ttu-id="473c5-311">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="473c5-311">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="473c5-313">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="473c5-313">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="473c5-314">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="473c5-314">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="473c5-315">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="473c5-315">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="473c5-316">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="473c5-316">Test single sign-on</span></span>

<span data-ttu-id="473c5-317">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="473c5-317">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="473c5-318">Ao clicar no bloco do Qlik Sense Enterprise no Painel de Acesso, você deverá ser conectado automaticamente a seu aplicativo Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="473c5-318">When you click the Qlik Sense Enterprise tile in the Access Panel, you should get automatically signed-on to your Qlik Sense Enterprise application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="473c5-319">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="473c5-319">Additional resources</span></span>

* [<span data-ttu-id="473c5-320">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="473c5-320">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="473c5-321">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="473c5-321">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_203.png

[qs6]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_06.png
[qs7]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_07.png
[qs8]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_08.png
[qs9]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_09.png
[qs10]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_10.png
[qs11]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_11.png
[qs12]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_12.png
[qs13]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_13.png
[qs14]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_14.png
[qs15]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_15.png
[qs16]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_16.png
[qs17]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_17.png
[qs18]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_18.png
[qs19]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_19.png
[qs20]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_20.png
[qs24]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_24.png
[qs51]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_51.png
[qs52]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_52.png
[qs53]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_53.png

