---
title: "Tutorial: integração do Azure Active Directory ao SAP Business Object Cloud | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o SAP Business Object Cloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 6c5e44f0-4e52-463f-b879-834d80a55cdf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: 6d517c5e302ac36e5bba2053998c75f8f4d42683
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-object-cloud"></a><span data-ttu-id="49de6-103">Tutorial: integração do Azure Active Directory ao SAP Business Object Cloud</span><span class="sxs-lookup"><span data-stu-id="49de6-103">Tutorial: Azure Active Directory integration with SAP Business Object Cloud</span></span>

<span data-ttu-id="49de6-104">Neste tutorial, você aprenderá a integrar o SAP Business Object Cloud ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="49de6-104">In this tutorial, you learn how to integrate SAP Business Object Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="49de6-105">Você obtém os seguintes benefícios quando integra o SAP Business Object Cloud ao Azure AD:</span><span class="sxs-lookup"><span data-stu-id="49de6-105">You get the following benefits when you integrate SAP Business Object Cloud with Azure AD:</span></span>

- <span data-ttu-id="49de6-106">No Azure AD, você pode controlar quem tem acesso ao SAP Business Object Cloud.</span><span class="sxs-lookup"><span data-stu-id="49de6-106">In Azure AD, you can control who has access to SAP Business Object Cloud.</span></span>
- <span data-ttu-id="49de6-107">Você pode conectar automaticamente seus usuários ao SAP Business Object Cloud usando o logon único e a conta do Azure AD de um usuário.</span><span class="sxs-lookup"><span data-stu-id="49de6-107">You can automatically sign in your users to SAP Business Object Cloud by using single sign-on and a user's Azure AD account.</span></span>
- <span data-ttu-id="49de6-108">É possível gerenciar suas contas em uma, um local central e no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="49de6-108">You can manage your accounts in one, central location, the Azure portal.</span></span>

<span data-ttu-id="49de6-109">Para saber mais sobre a integração de aplicativos de SaaS (software como serviço) ao Azure AD, confira [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="49de6-109">To learn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="49de6-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="49de6-110">Prerequisites</span></span>

<span data-ttu-id="49de6-111">Para configurar a integração do Azure AD ao SAP Business Object Cloud, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="49de6-111">To set up Azure AD integration with SAP Business Object Cloud, you need the following items:</span></span>

- <span data-ttu-id="49de6-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="49de6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="49de6-113">Um SAP Business Object Cloud, com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="49de6-113">An SAP Business Object Cloud, with single sign-on turned on</span></span>

> [!NOTE]
> <span data-ttu-id="49de6-114">Em caso de testar as etapas deste tutorial, recomendamos não testá-las em um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="49de6-114">If you test the steps in this tutorial, we recommend that you don't test them in a production environment.</span></span>

<span data-ttu-id="49de6-115">Recomendações para testar as etapas deste tutorial:</span><span class="sxs-lookup"><span data-stu-id="49de6-115">Recommendations for testing the steps in this tutorial:</span></span>

- <span data-ttu-id="49de6-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="49de6-116">Do not use your production environment, unless it's necessary.</span></span>
- <span data-ttu-id="49de6-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="49de6-117">If you don't have an Azure AD trial environment, you can [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="49de6-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="49de6-118">Scenario description</span></span>
<span data-ttu-id="49de6-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="49de6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="49de6-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="49de6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="49de6-121">Adicionar o SAP Business Object Cloud da galeria.</span><span class="sxs-lookup"><span data-stu-id="49de6-121">Add SAP Business Object Cloud from the gallery.</span></span>
2. <span data-ttu-id="49de6-122">Configurar e testar o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49de6-122">Set up and test Azure AD single sign-on.</span></span>

## <a name="add-sap-business-object-cloud-from-the-gallery"></a><span data-ttu-id="49de6-123">Adicionar o SAP Business Object Cloud da galeria</span><span class="sxs-lookup"><span data-stu-id="49de6-123">Add SAP Business Object Cloud from the gallery</span></span>
<span data-ttu-id="49de6-124">Para configurar a integração do SAP Business Object Cloud ao Azure AD, na galeria, adicione o SAP Business Object Cloud à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="49de6-124">To set up the integration of SAP Business Object Cloud with Azure AD, in the gallery, add SAP Business Object Cloud to your list of managed SaaS apps.</span></span>

<span data-ttu-id="49de6-125">Para adicionar o SAP Business Object Cloud da galeria:</span><span class="sxs-lookup"><span data-stu-id="49de6-125">To add SAP Business Object Cloud from the gallery:</span></span>

1. <span data-ttu-id="49de6-126">No [portal do Azure](https://portal.azure.com), no menu esquerdo, selecione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="49de6-126">In the [Azure portal](https://portal.azure.com), in the left menu, select **Azure Active Directory**.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="49de6-128">Selecione **Aplicativos empresariais** e, em seguida, selecione **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="49de6-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![A página de aplicativos empresariais][2]
    
3. <span data-ttu-id="49de6-130">Para adicionar um novo aplicativo, selecione **Novo aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="49de6-130">To add a new application, select **New application**.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="49de6-132">Na caixa de pesquisa, insira **SAP Business Object Cloud**.</span><span class="sxs-lookup"><span data-stu-id="49de6-132">In the search box, enter **SAP Business Object Cloud**.</span></span>

    ![A caixa de pesquisa](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_search.png)

5. <span data-ttu-id="49de6-134">No painel de resultados, selecione **SAP Business Object Cloud** e o botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="49de6-134">In the results panel, select **SAP Business Object Cloud**, and then select **Add**.</span></span>

    ![SAP Business Object Cloud na lista de resultados](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_addfromgallery.png)

##  <a name="set-up-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="49de6-136">Configurar e testar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="49de6-136">Set up and test Azure AD single sign-on</span></span>

<span data-ttu-id="49de6-137">Nesta seção, você vai configurar e testar o logon único do Azure AD com o SAP Business Object Cloud, com base em uma usuária de teste chamada *Brenda Fernandes*.</span><span class="sxs-lookup"><span data-stu-id="49de6-137">In this section, you set up and test Azure AD single sign-on with SAP Business Object Cloud based on a test user named *Britta Simon*.</span></span>

<span data-ttu-id="49de6-138">Para que o logon único funcione, o Azure AD precisa conhecer o usuário equivalente do Azure AD no SAP Business Object Cloud.</span><span class="sxs-lookup"><span data-stu-id="49de6-138">For single sign-on to work, Azure AD needs to know the Azure AD counterpart user in SAP Business Object Cloud.</span></span> <span data-ttu-id="49de6-139">É necessário estabelecer uma relação de vinculação entre um usuário do Azure AD e o usuário relacionado no SAP Business Object Cloud.</span><span class="sxs-lookup"><span data-stu-id="49de6-139">A link relationship between an Azure AD user and the related user in SAP Business Object Cloud must be established.</span></span>

<span data-ttu-id="49de6-140">Para estabelecer a relação de vinculação, no SAP Business Object Cloud, para **Nome de usuário**, atribua o valor de **nome de usuário** no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49de6-140">To establish the link relationship, in SAP Business Object Cloud, for **Username**, assign the value of the **user name** in Azure AD.</span></span>

<span data-ttu-id="49de6-141">Para configurar e testar o logon único do Azure AD com o SAP Business Object Cloud, complete as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="49de6-141">To configure and test Azure AD single sign-on with SAP Business Object Cloud, complete the following tasks:</span></span>

1. <span data-ttu-id="49de6-142">[Configurar o logon único do Azure AD](#set-up-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="49de6-142">[Set up Azure AD single sign-on](#set-up-azure-ad-single-sign-on).</span></span> <span data-ttu-id="49de6-143">Configura um usuário para usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="49de6-143">Sets up a user to use this feature.</span></span>
2. <span data-ttu-id="49de6-144">[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="49de6-144">[Create an Azure AD test user](#create-an-azure-ad-test-user).</span></span> <span data-ttu-id="49de6-145">Testa o logon único do Azure AD com a usuária Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="49de6-145">Tests Azure AD single sign-on with the user Britta Simon.</span></span>
3. <span data-ttu-id="49de6-146">[Criar um usuário de teste do SAP Business Object Cloud](#create-an-sap-business-object-cloud-test-user).</span><span class="sxs-lookup"><span data-stu-id="49de6-146">[Create an SAP Business Object Cloud test user](#create-an-sap-business-object-cloud-test-user).</span></span> <span data-ttu-id="49de6-147">Cria um equivalente de Brenda Fernandes no SAP Business Object Cloud que é vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49de6-147">Creates a counterpart of Britta Simon in SAP Business Object Cloud that is linked to the Azure AD representation of the user.</span></span>
4. <span data-ttu-id="49de6-148">[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="49de6-148">[Assign the Azure AD test user](#assign-the-azure-ad-test-user).</span></span> <span data-ttu-id="49de6-149">Configura Brenda Fernandes para usar o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49de6-149">Sets up Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="49de6-150">[Testar o logon único](#test-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="49de6-150">[Test single sign-on](#test-single-sign-on).</span></span> <span data-ttu-id="49de6-151">Verifica se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="49de6-151">Verifies that the configuration works.</span></span>

### <a name="set-up-azure-ad-single-sign-on"></a><span data-ttu-id="49de6-152">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="49de6-152">Set up Azure AD single sign-on</span></span>

<span data-ttu-id="49de6-153">Nesta seção, você ativa o logon único do Azure AD no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="49de6-153">In this section, you turn on Azure AD single sign-on in the Azure portal.</span></span> <span data-ttu-id="49de6-154">Em seguida, configura o logon único no seu aplicativo SAP Business Object Cloud.</span><span class="sxs-lookup"><span data-stu-id="49de6-154">Then, you set up single sign-on in your SAP Business Object Cloud application.</span></span>

<span data-ttu-id="49de6-155">Para configurar o logon único do Azure AD com o SAP Business Object Cloud:</span><span class="sxs-lookup"><span data-stu-id="49de6-155">To set up Azure AD single sign-on with SAP Business Object Cloud:</span></span>

1. <span data-ttu-id="49de6-156">No portal do Azure, na página de integração do aplicativo do **SAP Business Object Cloud**, selecione **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="49de6-156">In the Azure portal, on the **SAP Business Object Cloud** application integration page, select **Single sign-on**.</span></span>

    ![Selecionar Logon Único][4]

2. <span data-ttu-id="49de6-158">Na página **Logon único**, para **Modo**, selecione **Logon com base em SAML**.</span><span class="sxs-lookup"><span data-stu-id="49de6-158">On the **Single sign-on** page, for **Mode**, select **SAML-based Sign-on**.</span></span>
 
    ![Selecionar Logon com base em SAML](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_samlbase.png)

3. <span data-ttu-id="49de6-160">Em **Domínio e URLs do SAP Business Object Cloud**, conclua as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="49de6-160">Under **SAP Business Object Cloud Domain and URLs**, complete the following steps:</span></span>

    1. <span data-ttu-id="49de6-161">Na caixa **URL de Entrada**, digite uma URL com o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="49de6-161">In the **Sign-on URL** box, enter a URL that has the following pattern:</span></span> 
    | |
    |-|-|
    | `https://<sub-domain>.sapanalytics.cloud/` |
    | `https://<sub-domain>.sapbusinessobjects.cloud/` |

    2. <span data-ttu-id="49de6-162">Na caixa **Identificador**, digite uma URL com o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="49de6-162">In the **Identifier** box, enter a URL that has the following pattern:</span></span>
    | |
    |-|-|
    | `<sub-domain>.sapbusinessobjects.cloud` |
    | `<sub-domain>.sapanalytics.cloud` |

    ![URLs da página Domínio e URLs do SAP Business Object Cloud](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_url.png)
 
    > [!NOTE] 
    > <span data-ttu-id="49de6-164">Os valores nessas URLs são apenas para demonstração.</span><span class="sxs-lookup"><span data-stu-id="49de6-164">The values in these URLs are for demonstration only.</span></span> <span data-ttu-id="49de6-165">Atualize os valores com a verdadeira URL de entrada e a URL do identificador.</span><span class="sxs-lookup"><span data-stu-id="49de6-165">Update the values with the actual sign-on URL and identifier URL.</span></span> <span data-ttu-id="49de6-166">Para obter a URL de entrada, entre em contato com a [equipe de Suporte ao cliente do SAP Business Object Cloud](https://www.sap.com/product/analytics/cloud-analytics.support.html).</span><span class="sxs-lookup"><span data-stu-id="49de6-166">To get the sign-on URL, contact the [SAP Business Object Cloud Client support team](https://www.sap.com/product/analytics/cloud-analytics.support.html).</span></span> <span data-ttu-id="49de6-167">Você pode obter a URL do identificador ao baixar os metadados do SAP Business Object Cloud do console do administrador.</span><span class="sxs-lookup"><span data-stu-id="49de6-167">You can get the identifier URL by downloading the SAP Business Object Cloud metadata from the admin console.</span></span> <span data-ttu-id="49de6-168">Isso é explicado mais adiante no tutorial.</span><span class="sxs-lookup"><span data-stu-id="49de6-168">This is explained later in the tutorial.</span></span> 

4. <span data-ttu-id="49de6-169">Em **Certificado de Autenticação SAML**, selecione **XML de Metadados**.</span><span class="sxs-lookup"><span data-stu-id="49de6-169">Under **SAML Signing Certificate**, select **Metadata XML**.</span></span> <span data-ttu-id="49de6-170">Em seguida, salve o arquivo de metadados no computador.</span><span class="sxs-lookup"><span data-stu-id="49de6-170">Then, save the metadata file on your computer.</span></span>

    ![Selecionar XML de Metadados](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_certificate.png) 

5. <span data-ttu-id="49de6-172">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="49de6-172">Select **Save**.</span></span>

    ![Selecionar Salvar](./media/active-directory-saas-sapboc-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="49de6-174">Em outra janela do navegador da Web, entre no site da empresa do seu SAP Business Object Cloud como um administrador.</span><span class="sxs-lookup"><span data-stu-id="49de6-174">In a different web browser window, sign in to your SAP Business Object Cloud company site as an administrator.</span></span>

7. <span data-ttu-id="49de6-175">Selecione **Menu** > **Sistema** > **Administração**.</span><span class="sxs-lookup"><span data-stu-id="49de6-175">Select **Menu** > **System** > **Administration**.</span></span>
    
    ![Selecionar Menu, Sistema e Administração](./media/active-directory-saas-sapboc-tutorial/config1.png)

8. <span data-ttu-id="49de6-177">Na guia **Segurança**, selecione o ícone **Editar** (caneta).</span><span class="sxs-lookup"><span data-stu-id="49de6-177">On the **Security** tab, select the **Edit** (pen) icon.</span></span>
    
    ![Na guia Segurança, selecionar o ícone Editar](./media/active-directory-saas-sapboc-tutorial/config2.png)  

9. <span data-ttu-id="49de6-179">Para **Método de Autenticação**, selecione **SSO (Logon Único) do SAML**.</span><span class="sxs-lookup"><span data-stu-id="49de6-179">For **Authentication Method**, select **SAML Single Sign-On (SSO)**.</span></span>

    ![Selecionar Logon Único do SAML para o método de autenticação](./media/active-directory-saas-sapboc-tutorial/config3.png)  

10. <span data-ttu-id="49de6-181">Para baixar os metadados do provedor de serviços (Etapa 1), selecione **Baixar**.</span><span class="sxs-lookup"><span data-stu-id="49de6-181">To download the service provider metadata (Step 1), select **Download**.</span></span> <span data-ttu-id="49de6-182">No arquivo de metadados, localize e copie o valor **entityID**.</span><span class="sxs-lookup"><span data-stu-id="49de6-182">In the metadata file, find and copy the **entityID** value.</span></span> <span data-ttu-id="49de6-183">No portal do Azure, em **Domínio e URLs do SAP Business Object Cloud**, cole o valor na caixa **Identificador**.</span><span class="sxs-lookup"><span data-stu-id="49de6-183">In the Azure portal, under **SAP Business Object Cloud Domain and URLs**, paste the value in the **Identifier** box.</span></span>

    ![Copiar e colar o valor de entityID](./media/active-directory-saas-sapboc-tutorial/config4.png)  

11. <span data-ttu-id="49de6-185">Para fazer upload dos metadados do provedor de serviços (Etapa 2) no arquivo que você baixou do portal do Azure, em **Fazer upload dos metadados do Provedor de Identidade**, selecione **Fazer Upload**.</span><span class="sxs-lookup"><span data-stu-id="49de6-185">To upload the service provider metadata (Step 2) in the file that you downloaded from the Azure portal, under **Upload Identity Provider metadata**, select **Upload**.</span></span>  

    ![Em Fazer upload dos metadados do Provedor de Identidade, selecionar Fazer Upload](./media/active-directory-saas-sapboc-tutorial/config5.png)

12. <span data-ttu-id="49de6-187">Na lista **Atributo de Usuário**, selecione o atributo de usuário (Etapa 3) que você quer usar na sua implementação.</span><span class="sxs-lookup"><span data-stu-id="49de6-187">In the **User Attribute** list, select the user attribute (Step 3) that you want to use for your implementation.</span></span> <span data-ttu-id="49de6-188">Esse atributo de usuário é mapeado para o provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="49de6-188">This user attribute maps to the identity provider.</span></span> <span data-ttu-id="49de6-189">Para inserir um atributo personalizado na página do usuário, use a opção **Mapeamento de SAML Personalizado**.</span><span class="sxs-lookup"><span data-stu-id="49de6-189">To enter a custom attribute on the user's page, use the **Custom SAML Mapping** option.</span></span> <span data-ttu-id="49de6-190">Ou você pode selecionar o **Email** ou a **ID DE USUÁRIO** como o atributo de usuário.</span><span class="sxs-lookup"><span data-stu-id="49de6-190">Or, you can select either **Email** or **USER ID** as the user attribute.</span></span> <span data-ttu-id="49de6-191">Em nosso exemplo, selecionamos **Email** porque mapeamos a declaração da identificação de usuário com o atributo **userprincipalname** na seção **Atributos de Usuário** do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="49de6-191">In our example, we selected **Email** because we mapped the user identifier claim with the **userprincipalname** attribute in the **User Attributes** section in the Azure portal.</span></span> <span data-ttu-id="49de6-192">Isso fornece um email de usuário exclusivo, que é enviado ao aplicativo SAP Business Object Cloud em cada resposta bem-sucedida de SAML.</span><span class="sxs-lookup"><span data-stu-id="49de6-192">This provides a unique user email, which is sent to the SAP Business Object Cloud application in every successful SAML response.</span></span>

    ![Selecionar Atributo de Usuário](./media/active-directory-saas-sapboc-tutorial/config6.png)

13. <span data-ttu-id="49de6-194">Para verificar a conta com o provedor de identidade (Etapa 4), na caixa **Credencial de Logon (Email)**, insira o endereço de email do usuário.</span><span class="sxs-lookup"><span data-stu-id="49de6-194">To verify the account with the identity provider (Step 4), in the **Login Credential (Email)** box, enter the user's email address.</span></span> <span data-ttu-id="49de6-195">Em seguida, selecione **Verificar Conta**.</span><span class="sxs-lookup"><span data-stu-id="49de6-195">Then, select **Verify Account**.</span></span> <span data-ttu-id="49de6-196">O sistema adiciona credenciais de entrada à conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="49de6-196">The system adds sign-in credentials to the user account.</span></span>

    ![Inserir email e selecionar Verificar Conta](./media/active-directory-saas-sapboc-tutorial/config7.png)

14. <span data-ttu-id="49de6-198">Selecione o ícone **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="49de6-198">Select the **Save** icon.</span></span>

    ![Ícone Salvar](./media/active-directory-saas-sapboc-tutorial/save.png)

> [!TIP]
> <span data-ttu-id="49de6-200">É possível ler uma versão concisa dessas instruções no [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="49de6-200">You can read a concise version of these instructions in the [Azure portal](https://portal.azure.com), while you are setting up your app!</span></span> <span data-ttu-id="49de6-201">Depois de adicionar o aplicativo selecionando **Active Directory** > **Aplicativos Empresariais**, selecione a guia **Logon Único**. Você pode acessar a documentação inserida na seção **Configuração**, na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="49de6-201">After you add the app by selecting **Active Directory** > **Enterprise Applications**, select the **Single Sign-On** tab. You can access the embedded documentation in the **Configuration** section, at the bottom of the page.</span></span> <span data-ttu-id="49de6-202">Para saber mais, confira a [documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="49de6-202">For more information, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="49de6-203">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="49de6-203">Create an Azure AD test user</span></span>
<span data-ttu-id="49de6-204">Nesta seção, você criará uma usuária de teste no portal do Azure chamada Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="49de6-204">In this section, you create a test user named Britta Simon in the Azure portal.</span></span>

<span data-ttu-id="49de6-205">Para criar um usuário de teste no Azure AD:</span><span class="sxs-lookup"><span data-stu-id="49de6-205">To create a test user in Azure AD:</span></span>

1. <span data-ttu-id="49de6-206">No portal do Azure, no menu esquerdo, selecione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="49de6-206">In the Azure portal, in the left menu, select **Azure Active Directory**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sapboc-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="49de6-208">Para exibir a lista de usuários, selecione **Usuários e grupos** e, em seguida, selecione **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="49de6-208">To display the list of users, select **Users and groups**, and then select **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sapboc-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="49de6-210">Para abrir a caixa de diálogo **Usuário**, selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="49de6-210">To open the **User** dialog box, select **Add**.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sapboc-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="49de6-212">Na caixa de diálogo **Usuário**, conclua as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="49de6-212">In the **User** dialog box, complete the following steps:</span></span>
 
    1. <span data-ttu-id="49de6-213">Na caixa **Nome**, insira **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="49de6-213">In the **Name** box, enter **BrittaSimon**.</span></span>

    2. <span data-ttu-id="49de6-214">Na caixa **Nome de usuário**, insira o endereço de email da usuária Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="49de6-214">In the **User name** box, enter the email address of the user Britta Simon.</span></span>

    3. <span data-ttu-id="49de6-215">Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.</span><span class="sxs-lookup"><span data-stu-id="49de6-215">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    4. <span data-ttu-id="49de6-216">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="49de6-216">Select **Create**.</span></span>

        ![A caixa de diálogo Usuário](./media/active-directory-saas-sapboc-tutorial/create_aaduser_04.png) 

    ![Criar um usuário do AD do Azure][100]

### <a name="create-an-sap-business-object-cloud-test-user"></a><span data-ttu-id="49de6-219">Criar um usuário de teste do SAP Business Object Cloud</span><span class="sxs-lookup"><span data-stu-id="49de6-219">Create an SAP Business Object Cloud test user</span></span>

<span data-ttu-id="49de6-220">Os usuários do Azure AD devem ser provisionados no SAP Business Object Cloud para que possam entrar no SAP Business Object Cloud.</span><span class="sxs-lookup"><span data-stu-id="49de6-220">Azure AD users must be provisioned in SAP Business Object Cloud before they can sign in to SAP Business Object Cloud.</span></span> <span data-ttu-id="49de6-221">No SAP Business Object Cloud, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="49de6-221">In SAP Business Object Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="49de6-222">Para provisionar uma conta de usuário:</span><span class="sxs-lookup"><span data-stu-id="49de6-222">To provision a user account:</span></span>

1. <span data-ttu-id="49de6-223">Entre no site da empresa do seu SAP Business Object Cloud como administrador.</span><span class="sxs-lookup"><span data-stu-id="49de6-223">Sign in to your SAP Business Object Cloud company site as an administrator.</span></span>

2. <span data-ttu-id="49de6-224">Selecione **Menu** > **Segurança** > **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="49de6-224">Select **Menu** > **Security** > **Users**.</span></span>

    ![Adicionar Funcionário](./media/active-directory-saas-sapboc-tutorial/user1.png)

3. <span data-ttu-id="49de6-226">Na página **Usuários**, para adicionar detalhes do novo usuário, selecione **+**.</span><span class="sxs-lookup"><span data-stu-id="49de6-226">On the **Users** page, to add new user details, select **+**.</span></span> 

    ![Página Adicionar Usuários](./media/active-directory-saas-sapboc-tutorial/user4.png)

    <span data-ttu-id="49de6-228">Em seguida, conclua as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="49de6-228">Then, complete the following steps:</span></span>

    1. <span data-ttu-id="49de6-229">Na caixa **ID DE USUÁRIO**, insira a ID do usuário, como **Brenda**.</span><span class="sxs-lookup"><span data-stu-id="49de6-229">In the **USER ID** box, enter the user ID of the user, like **Britta**.</span></span>

    2. <span data-ttu-id="49de6-230">Na caixa **NOME**, insira o nome do usuário, como **Brenda**.</span><span class="sxs-lookup"><span data-stu-id="49de6-230">In the **FIRST NAME** box, enter the first name of the user, like **Britta**.</span></span>

    3. <span data-ttu-id="49de6-231">Na caixa **SOBRENOME**, insira o sobrenome do usuário, como **Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="49de6-231">In the **LAST NAME** box, enter the last name of the user, like **Simon**.</span></span>

    4. <span data-ttu-id="49de6-232">Na caixa **NOME DE EXIBIÇÃO**, insira o nome completo do usuário, como **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="49de6-232">In the **DISPLAY NAME** box, enter the full name of the user, like **Britta Simon**.</span></span>

    5. <span data-ttu-id="49de6-233">Na caixa **EMAIL**, insira o endereço de email do usuário, como **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="49de6-233">In the **E-MAIL** box, enter the email address of the user, like **brittasimon@contoso.com**.</span></span>

    6. <span data-ttu-id="49de6-234">Na página **Selecionar Funções**, selecione a função apropriada para o usuário e selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="49de6-234">On the **Select Roles** page, select the appropriate role for the user, and then select **OK**.</span></span>

      ![Escolher função](./media/active-directory-saas-sapboc-tutorial/user3.png)

    7. <span data-ttu-id="49de6-236">Selecione o ícone **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="49de6-236">Select the **Save** icon.</span></span>    


### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="49de6-237">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="49de6-237">Assign the Azure AD test user</span></span>

<span data-ttu-id="49de6-238">Nesta seção, você permitirá que a usuária Brenda Fernandes use o logon único do Azure AD concedendo acesso de conta de usuário ao SAP Business Object Cloud.</span><span class="sxs-lookup"><span data-stu-id="49de6-238">In this section, you allow the user Britta Simon to use Azure AD single sign-on by granting the user account access to SAP Business Object Cloud.</span></span>

<span data-ttu-id="49de6-239">Para atribuir Brenda Fernandes ao SAP Business Object Cloud:</span><span class="sxs-lookup"><span data-stu-id="49de6-239">To assign Britta Simon to SAP Business Object Cloud:</span></span>

1. <span data-ttu-id="49de6-240">No portal do Azure, abra a exibição de aplicativos e vá para a exibição de diretório.</span><span class="sxs-lookup"><span data-stu-id="49de6-240">In the Azure portal, open the applications view, and then go to the directory view.</span></span> <span data-ttu-id="49de6-241">Selecione **Aplicativos empresariais** e, em seguida, selecione **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="49de6-241">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="49de6-243">Na lista de aplicativos, selecione **SAP Business Object Cloud**.</span><span class="sxs-lookup"><span data-stu-id="49de6-243">In the applications list, select **SAP Business Object Cloud**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_app.png) 

3. <span data-ttu-id="49de6-245">No menu esquerdo, selecione **Usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="49de6-245">In the left menu, select **Users and groups**.</span></span>

    ![Selecionar Usuários e grupos][202] 

4. <span data-ttu-id="49de6-247">Selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="49de6-247">Select **Add**.</span></span> <span data-ttu-id="49de6-248">Na página **Adicionar Atribuição**, selecione **Usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="49de6-248">Then, on the **Add Assignment** page, select **Users and groups**.</span></span>

    ![A página Adicionar Atribuição][203]

5. <span data-ttu-id="49de6-250">Na página **Usuários e grupos**, na lista de usuários, selecione **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="49de6-250">On the **Users and groups** page, in the list of users, select **Britta Simon**.</span></span>

6. <span data-ttu-id="49de6-251">Na página **Usuários e grupos**, selecione **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="49de6-251">On the **Users and groups** page, select **Select**.</span></span>

7. <span data-ttu-id="49de6-252">Na página **Adicionar Atribuição**, selecione **Atribuir**.</span><span class="sxs-lookup"><span data-stu-id="49de6-252">On the **Add Assignment** page, select **Assign**.</span></span>

![Atribuir a função de usuário][200] 
    
### <a name="test-single-sign-on"></a><span data-ttu-id="49de6-254">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="49de6-254">Test single sign-on</span></span>

<span data-ttu-id="49de6-255">Nesta seção, você testará sua configuração de logon único do Azure AD usando o painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="49de6-255">In this section, you test your Azure AD single sign-on configuration by using the access panel.</span></span>

<span data-ttu-id="49de6-256">Ao selecionar o bloco do SAP Business Object Cloud no painel de acesso, você deve ser conectado automaticamente ao aplicativo SAP Business Object Cloud.</span><span class="sxs-lookup"><span data-stu-id="49de6-256">When you select the SAP Business Object Cloud tile in the access panel, you should be automatically signed in to your SAP Business Object Cloud application.</span></span>

<span data-ttu-id="49de6-257">Para saber mais sobre o painel de acesso, veja [Introdução ao painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="49de6-257">For more information about the access panel, see [Introduction to the access panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="49de6-258">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="49de6-258">Additional resources</span></span>

* [<span data-ttu-id="49de6-259">Lista de tutoriais sobre como integrar aplicativos SaaS ao Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="49de6-259">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="49de6-260">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="49de6-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_203.png

