---
title: "Tutorial: Integração do Azure Active Directory ao iLMS | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o iLMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d6e11639-6cea-48c9-b008-246cf686e726
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: 22c72020200138e78835ed7dd2661f18b824c785
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ilms"></a><span data-ttu-id="8a187-103">Tutorial: Integração do Azure Active Directory ao iLMS</span><span class="sxs-lookup"><span data-stu-id="8a187-103">Tutorial: Azure Active Directory integration with iLMS</span></span>

<span data-ttu-id="8a187-104">Neste tutorial, você aprende a integrar o iLMS ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="8a187-104">In this tutorial, you learn how to integrate iLMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8a187-105">A integração do iLMS ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="8a187-105">Integrating iLMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8a187-106">No Azure AD, é possível controlar quem tem acesso ao iLMS</span><span class="sxs-lookup"><span data-stu-id="8a187-106">You can control in Azure AD who has access to iLMS</span></span>
- <span data-ttu-id="8a187-107">Você pode permitir que os usuários sejam automaticamente conectados ao iLMS (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a187-107">You can enable your users to automatically get signed-on to iLMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8a187-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8a187-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8a187-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8a187-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a187-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8a187-110">Prerequisites</span></span>

<span data-ttu-id="8a187-111">Para configurar a integração do Azure AD ao iLMS, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="8a187-111">To configure Azure AD integration with iLMS, you need the following items:</span></span>

- <span data-ttu-id="8a187-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8a187-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8a187-113">Uma assinatura do iLMS habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="8a187-113">An iLMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8a187-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="8a187-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8a187-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="8a187-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8a187-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="8a187-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="8a187-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8a187-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8a187-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="8a187-118">Scenario description</span></span>
<span data-ttu-id="8a187-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="8a187-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8a187-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="8a187-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8a187-121">Adicionando o iLMS por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="8a187-121">Adding iLMS from the gallery</span></span>
2. <span data-ttu-id="8a187-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8a187-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ilms-from-the-gallery"></a><span data-ttu-id="8a187-123">Adicionando o iLMS por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="8a187-123">Adding iLMS from the gallery</span></span>
<span data-ttu-id="8a187-124">Para configurar a integração do iLMS ao Azure AD, você precisa adicionar o iLMS à lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="8a187-124">To configure the integration of iLMS into Azure AD, you need to add iLMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8a187-125">**Para adicionar o iLMS por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="8a187-125">**To add iLMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8a187-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8a187-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8a187-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="8a187-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8a187-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="8a187-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="8a187-131">Para adicionar o novo aplicativo, clique no botão **Novo aplicativo** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8a187-131">To add new application, click **New application** button on the top of the dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="8a187-133">Na caixa de pesquisa, digite **iLMS**.</span><span class="sxs-lookup"><span data-stu-id="8a187-133">In the search box, type **iLMS**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_search.png)

5. <span data-ttu-id="8a187-135">No painel de resultados, selecione **iLMS** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8a187-135">In the results panel, select **iLMS**, then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8a187-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8a187-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8a187-138">Nesta seção, você configura e testa o logon único do Azure AD com o iLMS, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="8a187-138">In this section, you configure and test Azure AD single sign-on with iLMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8a187-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do iLMS é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8a187-139">For single sign-on to work, Azure AD needs to know what the counterpart user in iLMS is to a user in Azure AD.</span></span> <span data-ttu-id="8a187-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do iLMS.</span><span class="sxs-lookup"><span data-stu-id="8a187-140">In other words, a link relationship between an Azure AD user and the related user in iLMS needs to be established.</span></span>

<span data-ttu-id="8a187-141">Essa relação de vínculo é estabelecida atribuindo o valor de **nome de usuário** no Azure AD ao valor de **Nome de Usuário** no iLMS.</span><span class="sxs-lookup"><span data-stu-id="8a187-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in iLMS.</span></span>

<span data-ttu-id="8a187-142">Para configurar e testar o logon único do Azure AD com o iLMS, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="8a187-142">To configure and test Azure AD single sign-on with iLMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8a187-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="8a187-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8a187-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="8a187-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8a187-145">**[Criar um usuário de teste do iLMS](#creating-an-ilms-test-user)** – para ter um equivalente de Brenda Fernandes no iLMS que está vinculado à representação dela no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8a187-145">**[Creating an iLMS test user](#creating-an-ilms-test-user)** - to have a counterpart of Britta Simon in iLMS that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="8a187-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="8a187-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8a187-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="8a187-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8a187-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a187-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8a187-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo iLMS.</span><span class="sxs-lookup"><span data-stu-id="8a187-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your iLMS application.</span></span>

<span data-ttu-id="8a187-150">**Para configurar o logon único do Azure AD com o iLMS, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="8a187-150">**To configure Azure AD single sign-on with iLMS, perform the following steps:**</span></span>

1. <span data-ttu-id="8a187-151">No portal do Azure, na página de integração de aplicativos do **iLMS**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="8a187-151">In the Azure portal, on the **iLMS** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="8a187-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="8a187-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_samlbase.png)

3. <span data-ttu-id="8a187-155">Na seção **Domínio e URLs do iLMS**, realize as seguintes etapas se desejar configurar o aplicativo no modo iniciado pelo **IdP**:</span><span class="sxs-lookup"><span data-stu-id="8a187-155">On the **iLMS Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurar o logon único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url.png)

    <span data-ttu-id="8a187-157">a.</span><span class="sxs-lookup"><span data-stu-id="8a187-157">a.</span></span> <span data-ttu-id="8a187-158">Na caixa de texto **Identificador**, cole o valor do **Identificador** copiado da seção **Provedor de Serviços** das configurações do SAML no portal de administração do iLMS.</span><span class="sxs-lookup"><span data-stu-id="8a187-158">In the **Identifier** textbox, paste the **Identifier** value you copy from **Service Provider** section of SAML settings in iLMS admin portal.</span></span>

    <span data-ttu-id="8a187-159">b.</span><span class="sxs-lookup"><span data-stu-id="8a187-159">b.</span></span> <span data-ttu-id="8a187-160">Na caixa de texto **URL de Resposta**, cole o valor da **(URL) do Ponto de Extremidade** copiado da seção **Provedor de Serviços** das configurações do SAML no portal de administração do iLMS com o seguinte padrão `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span><span class="sxs-lookup"><span data-stu-id="8a187-160">In the **Reply URL** textbox, paste the **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal having the following pattern `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span></span>

    >[!Note]
    ><span data-ttu-id="8a187-161">“123456” é um valor de exemplo de identificador.</span><span class="sxs-lookup"><span data-stu-id="8a187-161">This '123456' is an example value of identifier.</span></span>

4. <span data-ttu-id="8a187-162">Marque **Mostrar configurações avançadas de URL**, se quiser configurar o aplicativo no modo iniciado em **SP**:</span><span class="sxs-lookup"><span data-stu-id="8a187-162">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurar o logon único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url1.png)

    <span data-ttu-id="8a187-164">Na caixa de texto **URL de Logon**, cole o valor da **(URL) do Ponto de Extremidade** copiado da seção **Provedor de Serviços** das configurações do SAML no portal de administração do iLMS como `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span><span class="sxs-lookup"><span data-stu-id="8a187-164">In the **Sign-on URL** textbox, paste the **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal as `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span></span>     

5. <span data-ttu-id="8a187-165">Para habilitar o provisionamento JIT, o aplicativo iLMS espera as declarações SAML em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="8a187-165">To enable JIT provisioning, iLMS application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="8a187-166">Configure as declarações a seguir para este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8a187-166">Configure the following claims for this application.</span></span> <span data-ttu-id="8a187-167">Você pode gerenciar os valores desses atributos da seção **Atributos de Usuário** na página de integração de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="8a187-167">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="8a187-168">A captura de tela a seguir mostra um exemplo disso.</span><span class="sxs-lookup"><span data-stu-id="8a187-168">The following screenshot shows an example for this.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-ilms-tutorial/4.png)
    
    <span data-ttu-id="8a187-170">Crie os atributos **Department, Region** e **Division** e adicione o nome desses atributos no iLMS.</span><span class="sxs-lookup"><span data-stu-id="8a187-170">Create **Department, Region** and **Division** attributes and add the name of these attributes in iLMS.</span></span> <span data-ttu-id="8a187-171">Todos esses atributos mostrados acima são necessários.</span><span class="sxs-lookup"><span data-stu-id="8a187-171">All these attributes shown above are required.</span></span>  

    > [!NOTE] 
    > <span data-ttu-id="8a187-172">Você precisa habilitar a opção **Criar Conta de Usuário Não Reconhecido** no iLMS para mapear esses atributos.</span><span class="sxs-lookup"><span data-stu-id="8a187-172">You have to enable **Create Un-recognized User Account** in iLMS to map these attributes.</span></span> <span data-ttu-id="8a187-173">Siga as instruções [aqui](http://support.inspiredelearning.com/customer/portal/articles/2204526) para ter uma ideia sobre a configuração de atributos.</span><span class="sxs-lookup"><span data-stu-id="8a187-173">Follow the instructions [here](http://support.inspiredelearning.com/customer/portal/articles/2204526) to get an idea on the attributes configuration.</span></span>

6. <span data-ttu-id="8a187-174">Na seção **Atributos do usuário**, na caixa de diálogo **Logon único**, configure o atributo do token SAML na imagem acima e siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="8a187-174">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="8a187-175">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="8a187-175">Attribute Name</span></span> | <span data-ttu-id="8a187-176">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="8a187-176">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="8a187-177">division</span><span class="sxs-lookup"><span data-stu-id="8a187-177">division</span></span> | <span data-ttu-id="8a187-178">user.department</span><span class="sxs-lookup"><span data-stu-id="8a187-178">user.department</span></span> |
    | <span data-ttu-id="8a187-179">region</span><span class="sxs-lookup"><span data-stu-id="8a187-179">region</span></span> | <span data-ttu-id="8a187-180">user.state</span><span class="sxs-lookup"><span data-stu-id="8a187-180">user.state</span></span> |
    | <span data-ttu-id="8a187-181">department</span><span class="sxs-lookup"><span data-stu-id="8a187-181">department</span></span> | <span data-ttu-id="8a187-182">user.jobtitle</span><span class="sxs-lookup"><span data-stu-id="8a187-182">user.jobtitle</span></span> |

    <span data-ttu-id="8a187-183">a.</span><span class="sxs-lookup"><span data-stu-id="8a187-183">a.</span></span> <span data-ttu-id="8a187-184">Clique em **Adicionar atributo** para abrir o diálogo **Adicionar Atributo**.</span><span class="sxs-lookup"><span data-stu-id="8a187-184">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_05.png)
    
    <span data-ttu-id="8a187-187">b.</span><span class="sxs-lookup"><span data-stu-id="8a187-187">b.</span></span> <span data-ttu-id="8a187-188">Na caixa de texto **Nome** , digite o nome do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="8a187-188">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="8a187-189">c.</span><span class="sxs-lookup"><span data-stu-id="8a187-189">c.</span></span> <span data-ttu-id="8a187-190">Na lista **Valor**, digite o valor do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="8a187-190">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="8a187-191">d.</span><span class="sxs-lookup"><span data-stu-id="8a187-191">d.</span></span> <span data-ttu-id="8a187-192">Clique em **Ok**</span><span class="sxs-lookup"><span data-stu-id="8a187-192">Click **Ok**</span></span>

7. <span data-ttu-id="8a187-193">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo XML em seu computador.</span><span class="sxs-lookup"><span data-stu-id="8a187-193">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_certificate.png) 

8. <span data-ttu-id="8a187-195">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="8a187-195">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-iLMS-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="8a187-197">Em outra janela do navegador da Web, faça logon no **portal de administração do iLMS** como administrador.</span><span class="sxs-lookup"><span data-stu-id="8a187-197">In a different web browser window, log in to your **iLMS admin portal** as an administrator.</span></span>

10. <span data-ttu-id="8a187-198">Clique em **SSO:SAML** na guia **Configurações** para abrir as configurações do SAML e realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="8a187-198">Click **SSO:SAML** under **Settings** tab to open SAML settings and perform the following steps:</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-ilms-tutorial/1.png) 

    <span data-ttu-id="8a187-200">a.</span><span class="sxs-lookup"><span data-stu-id="8a187-200">a.</span></span> <span data-ttu-id="8a187-201">Expanda a seção **Provedor de Serviços** e copie o valor do **Identificador** e da **(URL) do Ponto de Extremidade**.</span><span class="sxs-lookup"><span data-stu-id="8a187-201">Expand the **Service Provider** section and copy the **Identifier** and **Endpoint (URL)** value.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-ilms-tutorial/2.png) 

    <span data-ttu-id="8a187-203">b.</span><span class="sxs-lookup"><span data-stu-id="8a187-203">b.</span></span> <span data-ttu-id="8a187-204">Na seção **Provedor de Identidade**, clique em **Importar Metadados**.</span><span class="sxs-lookup"><span data-stu-id="8a187-204">Under **Identity Provider** section, click **Import Metadata**.</span></span>
    
    <span data-ttu-id="8a187-205">c.</span><span class="sxs-lookup"><span data-stu-id="8a187-205">c.</span></span> <span data-ttu-id="8a187-206">Selecione o arquivo de **Metadados** baixado no Portal do Azure na seção **Certificado de Autenticação do SAML**.</span><span class="sxs-lookup"><span data-stu-id="8a187-206">Select the **Metadata** file downloaded from Azure Portal from **SAML Signing Certificate** section.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig1.png) 

    <span data-ttu-id="8a187-208">d.</span><span class="sxs-lookup"><span data-stu-id="8a187-208">d.</span></span> <span data-ttu-id="8a187-209">Se você desejar habilitar o provisionamento JIT para criar contas do iLMS para cancelar o reconhecimento de usuários, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="8a187-209">If you want to enable JIT provisioning to create iLMS accounts for un-recognize users, follow below steps:</span></span>
        
       - <span data-ttu-id="8a187-210">Marque a opção **Criar Conta de Usuário Não Reconhecido**.</span><span class="sxs-lookup"><span data-stu-id="8a187-210">Check **Create Un-recognized User Account**.</span></span>
       
       ![Configurar o logon único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig2.png)

       -  <span data-ttu-id="8a187-212">Mapeie os atributos no Azure AD com os atributos no iLMS.</span><span class="sxs-lookup"><span data-stu-id="8a187-212">Map the attributes in Azure AD with the attributes in iLMS.</span></span> <span data-ttu-id="8a187-213">Na coluna de atributos, especifique o nome dos atributos ou o valor padrão.</span><span class="sxs-lookup"><span data-stu-id="8a187-213">In the attribute column, specify the attributes name or the default value.</span></span>

    <span data-ttu-id="8a187-214">e.</span><span class="sxs-lookup"><span data-stu-id="8a187-214">e.</span></span> <span data-ttu-id="8a187-215">Acesse a guia **Regras de Negócios** e realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="8a187-215">Go to **Business Rules** tab and perform the following steps:</span></span> 
        
       ![Configurar Logon Único](./media/active-directory-saas-ilms-tutorial/5.png)

       - <span data-ttu-id="8a187-217">Marque a opção **Criar Regiões, Divisões e Departamentos Não Reconhecidos** para criar Regiões, Divisões e Departamentos que ainda não existem no momento do Logon Único.</span><span class="sxs-lookup"><span data-stu-id="8a187-217">Check **Create Un-recognized Regions, Divisions and Departments** to create Regions, Divisions, and Departments that do not already exist at the time of Single Sign-on.</span></span>
        
       - <span data-ttu-id="8a187-218">Marque a opção **Atualizar Perfil de Usuário Durante a Conexão** para especificar se o perfil do usuário é atualizado a cada Logon Único.</span><span class="sxs-lookup"><span data-stu-id="8a187-218">Check **Update User Profile During Sign-in** to specify whether the user’s profile is updated with each Single Sign-on.</span></span> 
        
       - <span data-ttu-id="8a187-219">Se a opção **“Atualizar Valores em Branco para Campos Não Obrigatórios no Perfil de Usuário”** estiver marcada, os campos de perfil opcionais que estiverem em branco após a conexão também farão com que o perfil do iLMS do usuário contenha valores em branco nesses campos.</span><span class="sxs-lookup"><span data-stu-id="8a187-219">If the **“Update Blank Values for Non Mandatory Fields in User Profile”** option is checked, optional profile fields that are blank upon sign in will also cause the user’s iLMS profile to contain blank values for those fields.</span></span>
        
       - <span data-ttu-id="8a187-220">Marque a opção **Enviar Email de Notificação de Erro** e insira o email do usuário em que você deseja receber o email de notificação de erro.</span><span class="sxs-lookup"><span data-stu-id="8a187-220">Check **Send Error Notification Email** and enter the email of the user where you want to receive the error notification email.</span></span>

11. <span data-ttu-id="8a187-221">Clique no botão **Salvar** para salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="8a187-221">Click **Save** button to save the settings.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ilms-tutorial/save.png)

> [!TIP]
> <span data-ttu-id="8a187-223">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="8a187-223">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8a187-224">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="8a187-224">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8a187-225">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8a187-225">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
    
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8a187-226">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8a187-226">Creating an Azure AD test user</span></span>
<span data-ttu-id="8a187-227">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="8a187-227">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="8a187-229">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="8a187-229">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8a187-230">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8a187-230">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ilms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8a187-232">Vá para **usuários e grupos** e clique em **todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="8a187-232">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ilms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8a187-234">Na parte superior da caixa de diálogo clique **adicionar** para abrir o **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8a187-234">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ilms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8a187-236">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="8a187-236">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ilms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8a187-238">a.</span><span class="sxs-lookup"><span data-stu-id="8a187-238">a.</span></span> <span data-ttu-id="8a187-239">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="8a187-239">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8a187-240">b.</span><span class="sxs-lookup"><span data-stu-id="8a187-240">b.</span></span> <span data-ttu-id="8a187-241">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="8a187-241">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8a187-242">c.</span><span class="sxs-lookup"><span data-stu-id="8a187-242">c.</span></span> <span data-ttu-id="8a187-243">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="8a187-243">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8a187-244">d.</span><span class="sxs-lookup"><span data-stu-id="8a187-244">d.</span></span> <span data-ttu-id="8a187-245">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="8a187-245">Click **Create**.</span></span>
 
### <a name="creating-an-ilms-test-user"></a><span data-ttu-id="8a187-246">Criando um usuário de teste do iLMS</span><span class="sxs-lookup"><span data-stu-id="8a187-246">Creating an iLMS test user</span></span>

<span data-ttu-id="8a187-247">O aplicativo dá suporte ao provisionamento de usuário Just-In-Time e, após a autenticação, os usuários são criados no aplicativo automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8a187-247">Application supports Just in time user provisioning and after authentication users are created in the application automatically.</span></span> <span data-ttu-id="8a187-248">O JIT funcionará se você tiver clicado na caixa de seleção **Criar Conta de Usuário Não Reconhecido** durante a definição da configuração do SAML no portal de administração do iLMS.</span><span class="sxs-lookup"><span data-stu-id="8a187-248">JIT will work, if you have clicked the **Create Un-recognized User Account** checkbox during SAML configuration setting at iLMS admin portal.</span></span>

<span data-ttu-id="8a187-249">Se precisar criar um usuário manualmente, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="8a187-249">If you need to create an user manually, then follow below steps :</span></span>

1. <span data-ttu-id="8a187-250">Faça logon no site da empresa do iLMS como administrador.</span><span class="sxs-lookup"><span data-stu-id="8a187-250">Log in to your iLMS company site as an administrator.</span></span>

2. <span data-ttu-id="8a187-251">Clique em **“Registrar Usuário”** na guia **Usuários** para abrir a página **Registrar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="8a187-251">Click **“Register User”** under **Users** tab to open **Register User** page.</span></span> 
   
   ![Adicionar Funcionário](./media/active-directory-saas-ilms-tutorial/3.png)

3. <span data-ttu-id="8a187-253">Na página **“Registrar Usuário”**, realize as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="8a187-253">On the **“Register User”** page, perform the following steps.</span></span>

    ![Adicionar Funcionário](./media/active-directory-saas-ilms-tutorial/create_testuser_add.png)

    <span data-ttu-id="8a187-255">a.</span><span class="sxs-lookup"><span data-stu-id="8a187-255">a.</span></span> <span data-ttu-id="8a187-256">Na caixa de texto **Nome**, digite o nome Brenda.</span><span class="sxs-lookup"><span data-stu-id="8a187-256">In the **First Name** textbox, type the first name Britta.</span></span>
   
    <span data-ttu-id="8a187-257">b.</span><span class="sxs-lookup"><span data-stu-id="8a187-257">b.</span></span> <span data-ttu-id="8a187-258">Na caixa de texto **Sobrenome**, digite o sobrenome Fernandes.</span><span class="sxs-lookup"><span data-stu-id="8a187-258">In the **Last Name** textbox, type the last name Simon.</span></span>

    <span data-ttu-id="8a187-259">c.</span><span class="sxs-lookup"><span data-stu-id="8a187-259">c.</span></span> <span data-ttu-id="8a187-260">Na caixa de texto **ID de Email**, digite o endereço de email da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="8a187-260">In the **Email ID** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="8a187-261">d.</span><span class="sxs-lookup"><span data-stu-id="8a187-261">d.</span></span> <span data-ttu-id="8a187-262">Na lista suspensa **Região**, selecione o valor da região.</span><span class="sxs-lookup"><span data-stu-id="8a187-262">In the **Region** dropdown, select the value for region.</span></span>

    <span data-ttu-id="8a187-263">e.</span><span class="sxs-lookup"><span data-stu-id="8a187-263">e.</span></span> <span data-ttu-id="8a187-264">Na lista suspensa **Divisão**, selecione o valor da divisão.</span><span class="sxs-lookup"><span data-stu-id="8a187-264">In the **Division** dropdown, select the value for division.</span></span>

    <span data-ttu-id="8a187-265">f.</span><span class="sxs-lookup"><span data-stu-id="8a187-265">f.</span></span> <span data-ttu-id="8a187-266">Na lista suspensa **Departamento**, selecione o valor do departamento.</span><span class="sxs-lookup"><span data-stu-id="8a187-266">In the **Department** dropdown, select the value for department.</span></span>

    <span data-ttu-id="8a187-267">g.</span><span class="sxs-lookup"><span data-stu-id="8a187-267">g.</span></span> <span data-ttu-id="8a187-268">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="8a187-268">Click **Save**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8a187-269">Você pode enviar o email de registro para o usuário selecionando a caixa de seleção **Enviar Email de Registro**.</span><span class="sxs-lookup"><span data-stu-id="8a187-269">You can send registration mail to user by selecting **Send Registration Mail** checkbox.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8a187-270">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8a187-270">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8a187-271">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao iLMS.</span><span class="sxs-lookup"><span data-stu-id="8a187-271">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to iLMS.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="8a187-273">**Para atribuir Brenda Fernandes ao iLMS, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="8a187-273">**To assign Britta Simon to iLMS, perform the following steps:**</span></span>

1. <span data-ttu-id="8a187-274">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="8a187-274">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="8a187-276">Na lista de aplicativos, selecione **iLMS**.</span><span class="sxs-lookup"><span data-stu-id="8a187-276">In the applications list, select **iLMS**.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_app.png) 

3. <span data-ttu-id="8a187-278">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="8a187-278">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="8a187-280">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="8a187-280">Click **Add** button.</span></span> <span data-ttu-id="8a187-281">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8a187-281">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="8a187-283">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="8a187-283">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8a187-284">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8a187-284">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8a187-285">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8a187-285">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8a187-286">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="8a187-286">Testing single sign-on</span></span>

<span data-ttu-id="8a187-287">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="8a187-287">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8a187-288">Ao clicar no bloco iLMS no Painel de Acesso, você deverá ser conectado automaticamente ao aplicativo iLMS.</span><span class="sxs-lookup"><span data-stu-id="8a187-288">When you click the iLMS tile in the Access Panel, you should get automatically signed-on to your iLMS application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8a187-289">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="8a187-289">Additional resources</span></span>

* [<span data-ttu-id="8a187-290">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="8a187-290">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8a187-291">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8a187-291">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_203.png

