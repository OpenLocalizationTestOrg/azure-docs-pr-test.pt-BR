---
title: "Tutorial: integração do Azure Active Directory com o Cisco Spark | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Cisco Spark."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c47894b1-f5df-4755-845d-f12f4c602dc4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: a0a221622afe1c801a331e2319f3a7ace3111dad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-spark"></a><span data-ttu-id="8628e-103">Tutorial: Integração do Azure Active Directory ao Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="8628e-103">Tutorial: Azure Active Directory integration with Cisco Spark</span></span>

<span data-ttu-id="8628e-104">Neste tutorial, você aprenderá como integrar o Cisco Spark ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="8628e-104">In this tutorial, you learn how to integrate Cisco Spark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8628e-105">A integração do Cisco Spark ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="8628e-105">Integrating Cisco Spark with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8628e-106">Você pode controlar no Azure AD quem tem acesso ao Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="8628e-106">You can control in Azure AD who has access to Cisco Spark</span></span>
- <span data-ttu-id="8628e-107">Você pode permitir que os usuários sejam automaticamente conectados ao Cisco Spark (Logon Único) com as respectivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="8628e-107">You can enable your users to automatically get signed-on to Cisco Spark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8628e-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8628e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8628e-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8628e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8628e-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8628e-110">Prerequisites</span></span>

<span data-ttu-id="8628e-111">Para configurar a integração do Azure AD ao Cisco Spark, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="8628e-111">To configure Azure AD integration with Cisco Spark, you need the following items:</span></span>

- <span data-ttu-id="8628e-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8628e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8628e-113">Uma assinatura habilitada para logon único do Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="8628e-113">A Cisco Spark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8628e-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="8628e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8628e-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="8628e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8628e-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="8628e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8628e-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8628e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8628e-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="8628e-118">Scenario description</span></span>
<span data-ttu-id="8628e-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="8628e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8628e-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="8628e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8628e-121">Adicionando o Cisco Spark da galeria</span><span class="sxs-lookup"><span data-stu-id="8628e-121">Adding Cisco Spark from the gallery</span></span>
2. <span data-ttu-id="8628e-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8628e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cisco-spark-from-the-gallery"></a><span data-ttu-id="8628e-123">Adicionando o Cisco Spark da galeria</span><span class="sxs-lookup"><span data-stu-id="8628e-123">Adding Cisco Spark from the gallery</span></span>
<span data-ttu-id="8628e-124">Para configurar a integração do Cisco Spark ao Azure AD, você precisa adicionar o Cisco Spark da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="8628e-124">To configure the integration of Cisco Spark into Azure AD, you need to add Cisco Spark from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8628e-125">**Para adicionar o Cisco Spark da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="8628e-125">**To add Cisco Spark from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8628e-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8628e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8628e-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="8628e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8628e-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="8628e-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="8628e-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8628e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="8628e-133">Na caixa de pesquisa, digite **Cisco Spark**.</span><span class="sxs-lookup"><span data-stu-id="8628e-133">In the search box, type **Cisco Spark**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_search.png)

5. <span data-ttu-id="8628e-135">No painel de resultados, selecione **Cisco Spark** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8628e-135">In the results panel, select **Cisco Spark**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8628e-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8628e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8628e-138">Nesta seção, você configura e testa o logon único do Azure AD com o Cisco Spark com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="8628e-138">In this section, you configure and test Azure AD single sign-on with Cisco Spark based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8628e-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Cisco Spark é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8628e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cisco Spark is to a user in Azure AD.</span></span> <span data-ttu-id="8628e-140">Em outras palavras, é necessário estabelecer uma relação de vinculação entre um usuário do Azure AD e o usuário relacionado do Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="8628e-140">In other words, a link relationship between an Azure AD user and the related user in Cisco Spark needs to be established.</span></span>

<span data-ttu-id="8628e-141">No Cisco Spark, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="8628e-141">In Cisco Spark, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8628e-142">Para configurar e testar o logon único do Azure AD com o Cisco Spark, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="8628e-142">To configure and test Azure AD single sign-on with Cisco Spark, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8628e-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="8628e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8628e-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="8628e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8628e-145">**[Como criar um usuário de teste do Cisco Spark](#creating-a-cisco-spark-test-user)** – para ter um equivalente de Brenda Fernandes no Cisco Spark que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8628e-145">**[Creating a Cisco Spark test user](#creating-a-cisco-spark-test-user)** - to have a counterpart of Britta Simon in Cisco Spark that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8628e-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="8628e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8628e-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="8628e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8628e-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="8628e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8628e-149">Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único em seu aplicativo Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="8628e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cisco Spark application.</span></span>

<span data-ttu-id="8628e-150">**Para configurar o logon único do Azure AD com o Cisco Spark, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="8628e-150">**To configure Azure AD single sign-on with Cisco Spark, perform the following steps:**</span></span>

1. <span data-ttu-id="8628e-151">No portal do Azure, na página de integração de aplicativos do **Cisco Spark**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="8628e-151">In the Azure portal, on the **Cisco Spark** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="8628e-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="8628e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_samlbase.png)

3. <span data-ttu-id="8628e-155">Na seção **URLs e Domínio do Cisco Spark**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="8628e-155">On the **Cisco Spark Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_url.png)

    <span data-ttu-id="8628e-157">a.</span><span class="sxs-lookup"><span data-stu-id="8628e-157">a.</span></span> <span data-ttu-id="8628e-158">Na caixa de texto **URL de Logon**, digite uma URL como: `https://web.ciscospark.com/#/signin`</span><span class="sxs-lookup"><span data-stu-id="8628e-158">In the **Sign-on URL** textbox, type a URL as: `https://web.ciscospark.com/#/signin`</span></span>

    <span data-ttu-id="8628e-159">b.</span><span class="sxs-lookup"><span data-stu-id="8628e-159">b.</span></span> <span data-ttu-id="8628e-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://idbroker.webex.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="8628e-160">In the **Identifier** textbox, type a URL using the following pattern: `https://idbroker.webex.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8628e-161">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="8628e-161">This value is not real.</span></span> <span data-ttu-id="8628e-162">Atualize esse valor com o Identificador real.</span><span class="sxs-lookup"><span data-stu-id="8628e-162">Update this value with the actual Identifier.</span></span> <span data-ttu-id="8628e-163">Entre em contato com a [equipe de suporte ao Cliente do Cisco Spark](https://support.ciscospark.com/) para obter esse valor.</span><span class="sxs-lookup"><span data-stu-id="8628e-163">Contact [Cisco Spark Client support team](https://support.ciscospark.com/) to get this value.</span></span> 
 
4. <span data-ttu-id="8628e-164">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="8628e-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_certificate.png) 

5. <span data-ttu-id="8628e-166">O aplicativo Cisco Spark espera que as asserções SAML contenham atributos específicos.</span><span class="sxs-lookup"><span data-stu-id="8628e-166">Cisco Spark application expects the SAML assertions to contain specific attributes.</span></span> <span data-ttu-id="8628e-167">Configure as atribuições a seguir para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8628e-167">Configure the following attributes  for this application.</span></span> <span data-ttu-id="8628e-168">Você pode gerenciar os valores desses atributos da seção **Atributos de Usuário** na página de integração de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="8628e-168">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="8628e-169">A captura de tela a seguir mostra um exemplo disso.</span><span class="sxs-lookup"><span data-stu-id="8628e-169">The following screenshot shows an example for this.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_07.png) 

6. <span data-ttu-id="8628e-171">Na seção **Atributos do usuário**, na caixa de diálogo **Logon único**, configure o atributo do token SAML na imagem acima e siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="8628e-171">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="8628e-172">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="8628e-172">Attribute Name</span></span>  | <span data-ttu-id="8628e-173">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="8628e-173">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    |   <span data-ttu-id="8628e-174">uid</span><span class="sxs-lookup"><span data-stu-id="8628e-174">uid</span></span>    | <span data-ttu-id="8628e-175">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="8628e-175">user.userprincipalname</span></span> |   

    <span data-ttu-id="8628e-176">a.</span><span class="sxs-lookup"><span data-stu-id="8628e-176">a.</span></span> <span data-ttu-id="8628e-177">Clique em **Adicionar atributo** para abrir o diálogo **Adicionar Atributo**.</span><span class="sxs-lookup"><span data-stu-id="8628e-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="8628e-180">b.</span><span class="sxs-lookup"><span data-stu-id="8628e-180">b.</span></span> <span data-ttu-id="8628e-181">Na caixa de texto **Nome** , digite o nome do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="8628e-181">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="8628e-182">c.</span><span class="sxs-lookup"><span data-stu-id="8628e-182">c.</span></span> <span data-ttu-id="8628e-183">Na lista **Valor**, digite o valor do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="8628e-183">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="8628e-184">d.</span><span class="sxs-lookup"><span data-stu-id="8628e-184">d.</span></span> <span data-ttu-id="8628e-185">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="8628e-185">Click **Ok**.</span></span>

7. <span data-ttu-id="8628e-186">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="8628e-186">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="8628e-188">Entre no [Gerenciamento de Colaboração de Nuvem da Cisco](https://admin.ciscospark.com/) com suas credenciais completas de administrador.</span><span class="sxs-lookup"><span data-stu-id="8628e-188">Sign in to [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>

9. <span data-ttu-id="8628e-189">Escolha **Configurações** e, na seção **Autenticação**, clique em **Modificar**.</span><span class="sxs-lookup"><span data-stu-id="8628e-189">Select **Settings** and under the **Authentication** section, click **Modify**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_10.png)
    
10. <span data-ttu-id="8628e-191">Escolha **Integrar um provedor de identidade de terceiros. (Avançado)** e vá para a próxima tela.</span><span class="sxs-lookup"><span data-stu-id="8628e-191">Select **Integrate a 3rd-party identity provider. (Advanced)** and go to the next screen.</span></span>

11. <span data-ttu-id="8628e-192">Na página **Importar Metadados Idp**, arrastre e solte o arquivo de metadados do Azure AD na página ou use a opção de navegador de arquivos para localizar e carregar o arquivo de metadados do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8628e-192">On the **Import Idp Metadata** page, either drag and drop the Azure AD metadata file onto the page or use the file browser option to locate and upload the Azure AD metadata file.</span></span> <span data-ttu-id="8628e-193">Em seguida, escolha **Exigir certificado assinado por uma autoridade de certificação em Metadados (mais seguro)** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="8628e-193">Then, select **Require certificate signed by a certificate authority in Metadata (more secure)** and click **Next**.</span></span> 
    
    ![Configurar Logon Único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_11.png)

12. <span data-ttu-id="8628e-195">Escolha **Testar Conexão SSO** e, quando uma nova guia do navegador for aberta, autentique-se com o Azure AD conectando-se.</span><span class="sxs-lookup"><span data-stu-id="8628e-195">Select **Test SSO Connection**, and when a new browser tab opens, authenticate with Azure AD by signing in.</span></span>

13. <span data-ttu-id="8628e-196">Volte para a guia do navegador **Gerenciamento de Colaboração de Nuvem da Cisco**.</span><span class="sxs-lookup"><span data-stu-id="8628e-196">Return to the **Cisco Cloud Collaboration Management** browser tab.</span></span> <span data-ttu-id="8628e-197">Se o teste tiver sido bem-sucedido, escolha a opção **Este teste foi executado com êxito. Habilitar Logon Único** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="8628e-197">If the test was successful, select **This test was successful. Enable Single Sign-On option** and click **Next**.</span></span>

> [!TIP]
> <span data-ttu-id="8628e-198">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="8628e-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8628e-199">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="8628e-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8628e-200">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8628e-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8628e-201">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8628e-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="8628e-202">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="8628e-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="8628e-204">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="8628e-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8628e-205">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8628e-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8628e-207">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="8628e-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8628e-209">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8628e-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8628e-211">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="8628e-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8628e-213">a.</span><span class="sxs-lookup"><span data-stu-id="8628e-213">a.</span></span> <span data-ttu-id="8628e-214">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="8628e-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8628e-215">b.</span><span class="sxs-lookup"><span data-stu-id="8628e-215">b.</span></span> <span data-ttu-id="8628e-216">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="8628e-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8628e-217">c.</span><span class="sxs-lookup"><span data-stu-id="8628e-217">c.</span></span> <span data-ttu-id="8628e-218">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="8628e-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8628e-219">d.</span><span class="sxs-lookup"><span data-stu-id="8628e-219">d.</span></span> <span data-ttu-id="8628e-220">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="8628e-220">Click **Create**.</span></span>
 
### <a name="creating-a-cisco-spark-test-user"></a><span data-ttu-id="8628e-221">Criando um usuário de teste do Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="8628e-221">Creating a Cisco Spark test user</span></span>

<span data-ttu-id="8628e-222">Nesta seção, você criará um usuário chamado Brenda Fernandes no Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="8628e-222">In this section, you create a user called Britta Simon in Cisco Spark.</span></span> <span data-ttu-id="8628e-223">Nesta seção, você criará um usuário chamado Brenda Fernandes no Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="8628e-223">In this section, you create a user called Britta Simon in Cisco Spark.</span></span>

1. <span data-ttu-id="8628e-224">Acesse o [Gerenciamento de Colaboração de Nuvem da Cisco](https://admin.ciscospark.com/) com suas credenciais completas de administrador.</span><span class="sxs-lookup"><span data-stu-id="8628e-224">Go to the [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>

2. <span data-ttu-id="8628e-225">Clique em **Usuários** e em **Gerenciar Usuários**.</span><span class="sxs-lookup"><span data-stu-id="8628e-225">Click **Users** and then **Manage Users**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_12.png) 

3. <span data-ttu-id="8628e-227">Na janela **Gerenciar Usuário**, escolha **Adicionar ou modificar usuários manualmente** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="8628e-227">In the **Manage User** window, select **Manually add or modify users** and click **Next**.</span></span>

4. <span data-ttu-id="8628e-228">Escolha **Nomes e Endereço de email**.</span><span class="sxs-lookup"><span data-stu-id="8628e-228">Select **Names and Email address**.</span></span> <span data-ttu-id="8628e-229">Em seguida, preencha a caixa de texto como se segue:</span><span class="sxs-lookup"><span data-stu-id="8628e-229">Then, fill out the textbox as follows:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_13.png) 
    
    <span data-ttu-id="8628e-231">a.</span><span class="sxs-lookup"><span data-stu-id="8628e-231">a.</span></span> <span data-ttu-id="8628e-232">Na caixa de texto **Nome**, digite **Brenda**.</span><span class="sxs-lookup"><span data-stu-id="8628e-232">In the **First Name** textbox, type **Britta**.</span></span> 
    
    <span data-ttu-id="8628e-233">b.</span><span class="sxs-lookup"><span data-stu-id="8628e-233">b.</span></span> <span data-ttu-id="8628e-234">Na caixa de texto **Sobrenome**, digite **Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="8628e-234">In the **Last Name** textbox, type **Simon**.</span></span>
    
    <span data-ttu-id="8628e-235">c.</span><span class="sxs-lookup"><span data-stu-id="8628e-235">c.</span></span> <span data-ttu-id="8628e-236">Na caixa de texto **Endereço de email**, digite **britta.simon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="8628e-236">In the **Email address** textbox, type **britta.simon@contoso.com**.</span></span>

5. <span data-ttu-id="8628e-237">Clique no sinal de mais para adicionar Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="8628e-237">Click the plus sign to add Britta Simon.</span></span> <span data-ttu-id="8628e-238">Em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="8628e-238">Then, click **Next**.</span></span>

6. <span data-ttu-id="8628e-239">Na janela **Adicionar Serviços para Usuários**, clique em **Salvar** e em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="8628e-239">In the **Add Services for Users** window, click **Save** and then **Finish**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8628e-240">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8628e-240">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8628e-241">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo acesso ao Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="8628e-241">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cisco Spark.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="8628e-243">**Para atribuir Brenda Fernandes ao Cisco Spark, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="8628e-243">**To assign Britta Simon to Cisco Spark, perform the following steps:**</span></span>

1. <span data-ttu-id="8628e-244">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="8628e-244">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="8628e-246">Na lista de aplicativos, escolha **Cisco Spark**.</span><span class="sxs-lookup"><span data-stu-id="8628e-246">In the applications list, select **Cisco Spark**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_app.png) 

3. <span data-ttu-id="8628e-248">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="8628e-248">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="8628e-250">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="8628e-250">Click **Add** button.</span></span> <span data-ttu-id="8628e-251">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8628e-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="8628e-253">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="8628e-253">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8628e-254">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8628e-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8628e-255">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8628e-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8628e-256">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="8628e-256">Testing single sign-on</span></span>

<span data-ttu-id="8628e-257">O objetivo desta seção é testar sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="8628e-257">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="8628e-258">Ao clicar no bloco Cisco Spark no Painel de Acesso, você deverá ser conectado automaticamente ao aplicativo Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="8628e-258">When you click the Cisco Spark tile in the Access Panel, you should get automatically signed-on to your Cisco Spark application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8628e-259">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="8628e-259">Additional resources</span></span>

* [<span data-ttu-id="8628e-260">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="8628e-260">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8628e-261">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8628e-261">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_060.png
[100]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_203.png

