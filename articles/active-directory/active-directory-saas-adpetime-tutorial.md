---
title: "Tutorial: integração do Azure Active Directory com o ADP eTime | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o ADP eTime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a3e9f0be-19ed-4b99-a180-619e7624fc26
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 31fed307a32e629d00aab7cc9d5167ee16d83936
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adp-etime"></a><span data-ttu-id="893ad-103">Tutorial: integração do Azure Active Directory ao ADP eTime</span><span class="sxs-lookup"><span data-stu-id="893ad-103">Tutorial: Azure Active Directory integration with ADP eTime</span></span>

<span data-ttu-id="893ad-104">Neste tutorial, você aprende a integrar o ADP eTime ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="893ad-104">In this tutorial, you learn how to integrate ADP eTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="893ad-105">A integração do ADP eTime ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="893ad-105">Integrating ADP eTime with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="893ad-106">Você pode controlar no Azure AD quem tem acesso ao ADP eTime</span><span class="sxs-lookup"><span data-stu-id="893ad-106">You can control in Azure AD who has access to ADP eTime</span></span>
- <span data-ttu-id="893ad-107">É possível permitir que seus usuários façam logon automaticamente no ADP eTime (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="893ad-107">You can enable your users to automatically get signed-on to ADP eTime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="893ad-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="893ad-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="893ad-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="893ad-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="893ad-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="893ad-110">Prerequisites</span></span>

<span data-ttu-id="893ad-111">Para configurar a integração do Azure AD com o ADP eTime, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="893ad-111">To configure Azure AD integration with ADP eTime, you need the following items:</span></span>

- <span data-ttu-id="893ad-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="893ad-112">An Azure AD subscription</span></span>
- <span data-ttu-id="893ad-113">Uma assinatura habilitada para logon único do ADP eTime</span><span class="sxs-lookup"><span data-stu-id="893ad-113">An ADP eTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="893ad-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="893ad-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="893ad-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="893ad-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="893ad-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="893ad-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="893ad-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="893ad-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="893ad-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="893ad-118">Scenario description</span></span>
<span data-ttu-id="893ad-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="893ad-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="893ad-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="893ad-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="893ad-121">Adição do ADP eTime a partir da galeria</span><span class="sxs-lookup"><span data-stu-id="893ad-121">Adding ADP eTime from the gallery</span></span>
2. <span data-ttu-id="893ad-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="893ad-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adp-etime-from-the-gallery"></a><span data-ttu-id="893ad-123">Adição do ADP eTime a partir da galeria</span><span class="sxs-lookup"><span data-stu-id="893ad-123">Adding ADP eTime from the gallery</span></span>
<span data-ttu-id="893ad-124">Para configurar a integração do ADP eTime com o Azure AD, você precisa adicionar o ADP eTime à sua lista de aplicativos SaaS gerenciados a partir da galeria.</span><span class="sxs-lookup"><span data-stu-id="893ad-124">To configure the integration of ADP eTime into Azure AD, you need to add ADP eTime from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="893ad-125">**Para adicionar o ADP eTime a partir da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="893ad-125">**To add ADP eTime from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="893ad-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="893ad-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="893ad-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="893ad-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="893ad-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="893ad-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="893ad-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="893ad-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="893ad-133">Na caixa de pesquisa, digite **ADP eTime**.</span><span class="sxs-lookup"><span data-stu-id="893ad-133">In the search box, type **ADP eTime**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_search.png)

5. <span data-ttu-id="893ad-135">No painel de resultados, selecione **ADP eTime** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="893ad-135">In the results panel, select **ADP eTime**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="893ad-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="893ad-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="893ad-138">Nesta seção, você configura e testa o logon único do Azure AD com o ADP eTime, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="893ad-138">In this section, you configure and test Azure AD single sign-on with ADP eTime based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="893ad-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do ADP eTime é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="893ad-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ADP eTime is to a user in Azure AD.</span></span> <span data-ttu-id="893ad-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="893ad-140">In other words, a link relationship between an Azure AD user and the related user in ADP eTime needs to be established.</span></span>

<span data-ttu-id="893ad-141">Essa relação de vinculação é estabelecida por meio da atribuição do valor de **nome de usuário** no Azure AD como o valor de **Nome de Usuário** no ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="893ad-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ADP eTime.</span></span>

<span data-ttu-id="893ad-142">Para configurar e testar o logon único do Azure AD com o ADP eTime, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="893ad-142">To configure and test Azure AD single sign-on with ADP eTime, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="893ad-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="893ad-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="893ad-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="893ad-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="893ad-145">**[Criando um usuário de teste do ADP eTime](#creating-an-adp-etime-test-user)** – para ter um equivalente de Brenda Fernandes no ADP eTime que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="893ad-145">**[Creating an ADP eTime test user](#creating-an-adp-etime-test-user)** - to have a counterpart of Britta Simon in ADP eTime that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="893ad-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="893ad-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="893ad-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="893ad-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="893ad-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="893ad-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="893ad-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="893ad-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ADP eTime application.</span></span>

<span data-ttu-id="893ad-150">**Para configurar o logon único do Azure AD com o ADP eTime, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="893ad-150">**To configure Azure AD single sign-on with ADP eTime, perform the following steps:**</span></span>

1. <span data-ttu-id="893ad-151">No portal do Azure, na página de integração do aplicativo do **ADP eTime**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="893ad-151">In the Azure portal, on the **ADP eTime** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="893ad-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="893ad-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_samlbase.png)

3. <span data-ttu-id="893ad-155">Na seção **Domínio e URLs do ADP eTime**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="893ad-155">On the **ADP eTime Domain and URLs** section, perform the following step:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_url.png)

    <span data-ttu-id="893ad-157">a.</span><span class="sxs-lookup"><span data-stu-id="893ad-157">a.</span></span> <span data-ttu-id="893ad-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<servername>.adp.com`</span><span class="sxs-lookup"><span data-stu-id="893ad-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<servername>.adp.com`</span></span>

    <span data-ttu-id="893ad-159">b.</span><span class="sxs-lookup"><span data-stu-id="893ad-159">b.</span></span> <span data-ttu-id="893ad-160">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer`</span><span class="sxs-lookup"><span data-stu-id="893ad-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer`</span></span> 
 
    > [!NOTE] 
    > <span data-ttu-id="893ad-161">Esses não são os valores reais.</span><span class="sxs-lookup"><span data-stu-id="893ad-161">These values are not the real.</span></span> <span data-ttu-id="893ad-162">Atualize esses valores com a URL de Resposta e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="893ad-162">Update these values with the actual Reply URL and Identifier.</span></span> <span data-ttu-id="893ad-163">Contate a [equipe de suporte do ADP eTime](https://www.adp.com/contact-us/overview.aspx) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="893ad-163">Contact [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) to get these values.</span></span>

4. <span data-ttu-id="893ad-164">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo XML em seu computador.</span><span class="sxs-lookup"><span data-stu-id="893ad-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_certificate.png) 

5. <span data-ttu-id="893ad-166">O aplicativo ADP eTime espera as declarações do SAML em um formato específico, o que exige a adição de mapeamentos de atributo personalizados para a configuração de atributos do token SAML.</span><span class="sxs-lookup"><span data-stu-id="893ad-166">The ADP eTime application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="893ad-167">A captura de tela a seguir mostra um exemplo disso.</span><span class="sxs-lookup"><span data-stu-id="893ad-167">The following screenshot shows an example for this.</span></span> <span data-ttu-id="893ad-168">O nome da declaração sempre será **"PersonImmutableID"** e o valor que mapeamos para ExtensionAttribute2 que contém o EmployeeID do usuário.</span><span class="sxs-lookup"><span data-stu-id="893ad-168">The claim name will always be **"PersonImmutableID"** and the value of which we have mapped to ExtensionAttribute2 which contains the EmployeeID of the user.</span></span> 

    <span data-ttu-id="893ad-169">Aqui, o mapeamento de usuário do Azure AD para o ADP eTime será feito na EmployeeID, mas isso pode ser mapeado para um valor diferente também baseado nas configurações do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="893ad-169">Here the user mapping from Azure AD to ADP eTime will be done on the EmployeeID but you can map this to a different value also based on your application settings.</span></span> <span data-ttu-id="893ad-170">Portanto, trabalhe com a [equipe de suporte do ADP eTime](https://www.adp.com/contact-us/overview.aspx) primeiro para usar o identificador correto de um usuário e mapear esse valor com a declaração **“PersonImmutableID”**.</span><span class="sxs-lookup"><span data-stu-id="893ad-170">So please work with [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) first to use the correct identifier of a user and map that value with the **"PersonImmutableID"** claim.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_attribute.png)

6. <span data-ttu-id="893ad-172">Na seção **Atributos do Usuário**, na caixa de diálogo **Logon único**, configure o atributo do token SAML como mostra a imagem e execute as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="893ad-172">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="893ad-173">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="893ad-173">Attribute Name</span></span> | <span data-ttu-id="893ad-174">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="893ad-174">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="893ad-175">PersonImmutableID</span><span class="sxs-lookup"><span data-stu-id="893ad-175">PersonImmutableID</span></span> | <span data-ttu-id="893ad-176">user.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="893ad-176">user.extensionattribute2</span></span> |
    
    <span data-ttu-id="893ad-177">a.</span><span class="sxs-lookup"><span data-stu-id="893ad-177">a.</span></span> <span data-ttu-id="893ad-178">Clique em **Adicionar atributo** para abrir o diálogo **Adicionar Atributo**.</span><span class="sxs-lookup"><span data-stu-id="893ad-178">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="893ad-181">b.</span><span class="sxs-lookup"><span data-stu-id="893ad-181">b.</span></span> <span data-ttu-id="893ad-182">Na caixa de texto **Nome** , digite o nome do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="893ad-182">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="893ad-183">c.</span><span class="sxs-lookup"><span data-stu-id="893ad-183">c.</span></span> <span data-ttu-id="893ad-184">Na lista **Valor**, digite o valor do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="893ad-184">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="893ad-185">d.</span><span class="sxs-lookup"><span data-stu-id="893ad-185">d.</span></span> <span data-ttu-id="893ad-186">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="893ad-186">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="893ad-187">Antes de configurar a declaração SAML, é necessário contatar a [equipe de suporte do ADP eTime](https://www.adp.com/contact-us/overview.aspx) e solicitar o valor do atributo de identificador exclusivo para seu locatário.</span><span class="sxs-lookup"><span data-stu-id="893ad-187">Before you can configure the SAML assertion, you need to contact your [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) and request the value of the unique identifier attribute for your tenant.</span></span> <span data-ttu-id="893ad-188">Você precisa desse valor para configurar a declaração personalizada para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="893ad-188">You need this value to configure the custom claim for your application.</span></span> 

7. <span data-ttu-id="893ad-189">Na seção **Configuração do ADP eTime**, clique em **Configurar o ADP eTime** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="893ad-189">On the **ADP eTime Configuration** section, click **Configure ADP eTime** to open **Configure sign-on** window.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_configure.png) 

8. <span data-ttu-id="893ad-191">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="893ad-191">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adpetime-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="893ad-193">Para configurar o logon único no lado do **ADP eTime**, é necessário enviar o **XML de Metadados** baixado para a [equipe de suporte do ADP eTime](https://www.adp.com/contact-us/overview.aspx).</span><span class="sxs-lookup"><span data-stu-id="893ad-193">To configure single sign-on on **ADP eTime** side, you need to send the downloaded **Metadata XML** to [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx).</span></span> 

> [!TIP]
> <span data-ttu-id="893ad-194">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="893ad-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="893ad-195">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="893ad-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="893ad-196">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="893ad-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="893ad-197">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="893ad-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="893ad-198">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="893ad-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="893ad-200">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="893ad-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="893ad-201">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="893ad-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adpetime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="893ad-203">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="893ad-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adpetime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="893ad-205">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="893ad-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adpetime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="893ad-207">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="893ad-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adpetime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="893ad-209">a.</span><span class="sxs-lookup"><span data-stu-id="893ad-209">a.</span></span> <span data-ttu-id="893ad-210">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="893ad-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="893ad-211">b.</span><span class="sxs-lookup"><span data-stu-id="893ad-211">b.</span></span> <span data-ttu-id="893ad-212">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="893ad-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="893ad-213">c.</span><span class="sxs-lookup"><span data-stu-id="893ad-213">c.</span></span> <span data-ttu-id="893ad-214">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="893ad-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="893ad-215">d.</span><span class="sxs-lookup"><span data-stu-id="893ad-215">d.</span></span> <span data-ttu-id="893ad-216">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="893ad-216">Click **Create**.</span></span>
 
### <a name="creating-an-adp-etime-test-user"></a><span data-ttu-id="893ad-217">Criando um usuário de teste do ADP eTime</span><span class="sxs-lookup"><span data-stu-id="893ad-217">Creating an ADP eTime test user</span></span>

<span data-ttu-id="893ad-218">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="893ad-218">The objective of this section is to create a user called Britta Simon in ADP eTime.</span></span> <span data-ttu-id="893ad-219">Trabalhe com a [equipe de suporte do ADP eTime](https://www.adp.com/contact-us/overview.aspx) para adicionar os usuários à conta do ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="893ad-219">Work with [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) to add the users in the ADP eTime account.</span></span> 
   
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="893ad-220">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="893ad-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="893ad-221">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="893ad-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ADP eTime.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="893ad-223">**Para atribuir Brenda Fernandes ao ADP eTime, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="893ad-223">**To assign Britta Simon to ADP eTime, perform the following steps:**</span></span>

1. <span data-ttu-id="893ad-224">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="893ad-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="893ad-226">Na lista de aplicativos, escolha **ADP eTime**.</span><span class="sxs-lookup"><span data-stu-id="893ad-226">In the applications list, select **ADP eTime**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_app.png) 

3. <span data-ttu-id="893ad-228">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="893ad-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="893ad-230">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="893ad-230">Click **Add** button.</span></span> <span data-ttu-id="893ad-231">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="893ad-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="893ad-233">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="893ad-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="893ad-234">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="893ad-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="893ad-235">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="893ad-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="893ad-236">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="893ad-236">Testing single sign-on</span></span>

<span data-ttu-id="893ad-237">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="893ad-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="893ad-238">Ao clicar no bloco do ADP eTime no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo do ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="893ad-238">When you click the ADP eTime tile in the Access Panel, you should get automatically signed-on to your ADP eTime application.</span></span>
<span data-ttu-id="893ad-239">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="893ad-239">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="893ad-240">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="893ad-240">Additional resources</span></span>

* [<span data-ttu-id="893ad-241">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="893ad-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="893ad-242">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="893ad-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_203.png

