---
title: "Tutorial: integração do Azure Active Directory ao Lesson.ly | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Active Directory do Azure e o Lesson.ly."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8c9dc6e6-5d85-4553-8a35-c7137064b928
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: fc1e1b2de0a138dbe88d794f802b002321948ab8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lessonly"></a><span data-ttu-id="65bdc-103">Tutorial: integração do Active Directory do Azure com o Lesson.ly</span><span class="sxs-lookup"><span data-stu-id="65bdc-103">Tutorial: Azure Active Directory integration with Lesson.ly</span></span>

<span data-ttu-id="65bdc-104">Neste tutorial, você aprenderá a integrar o Lesson.ly ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="65bdc-104">In this tutorial, you learn how to integrate Lesson.ly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="65bdc-105">A integração do Lesson.ly com o Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="65bdc-105">Integrating Lesson.ly with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="65bdc-106">No AD do Azure, você pode controlar quem tem acesso ao Lesson.ly</span><span class="sxs-lookup"><span data-stu-id="65bdc-106">You can control in Azure AD who has access to Lesson.ly</span></span>
- <span data-ttu-id="65bdc-107">Você pode permitir que seus usuários façam logon automaticamente em Lesson.ly (Logon único) com as contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="65bdc-107">You can enable your users to automatically get signed-on to Lesson.ly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="65bdc-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="65bdc-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="65bdc-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="65bdc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65bdc-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="65bdc-110">Prerequisites</span></span>

<span data-ttu-id="65bdc-111">Para configurar a integração do AD do Azure ao Lesson.ly, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="65bdc-111">To configure Azure AD integration with Lesson.ly, you need the following items:</span></span>

- <span data-ttu-id="65bdc-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="65bdc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="65bdc-113">Uma assinatura habilitada para logon único do Lesson.ly</span><span class="sxs-lookup"><span data-stu-id="65bdc-113">A Lesson.ly single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="65bdc-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="65bdc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="65bdc-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="65bdc-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="65bdc-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="65bdc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="65bdc-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="65bdc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="65bdc-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="65bdc-118">Scenario description</span></span>
<span data-ttu-id="65bdc-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="65bdc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="65bdc-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="65bdc-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="65bdc-121">Adicionando o Lesson.ly da galeria</span><span class="sxs-lookup"><span data-stu-id="65bdc-121">Adding Lesson.ly from the gallery</span></span>
2. <span data-ttu-id="65bdc-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="65bdc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lessonly-from-the-gallery"></a><span data-ttu-id="65bdc-123">Adicionando o Lesson.ly da galeria</span><span class="sxs-lookup"><span data-stu-id="65bdc-123">Adding Lesson.ly from the gallery</span></span>
<span data-ttu-id="65bdc-124">Para configurar a integração do Lesson.ly ao AD do Azure, você precisa adicionar o Lesson.ly da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="65bdc-124">To configure the integration of Lesson.ly into Azure AD, you need to add Lesson.ly from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="65bdc-125">**Para adicionar o Lesson.ly da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="65bdc-125">**To add Lesson.ly from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="65bdc-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="65bdc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="65bdc-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="65bdc-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="65bdc-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="65bdc-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="65bdc-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="65bdc-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="65bdc-133">Na caixa de pesquisa, digite **Lesson.ly**.</span><span class="sxs-lookup"><span data-stu-id="65bdc-133">In the search box, type **Lesson.ly**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_search.png)

5. <span data-ttu-id="65bdc-135">No painel de resultados, selecione **Lesson.ly** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="65bdc-135">In the results panel, select **Lesson.ly**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="65bdc-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="65bdc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="65bdc-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Lesson.ly, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="65bdc-138">In this section, you configure and test Azure AD single sign-on with Lesson.ly based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="65bdc-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Lesson.ly é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65bdc-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lesson.ly is to a user in Azure AD.</span></span> <span data-ttu-id="65bdc-140">Em outras palavras, é necessário estabelecer uma relação de vinculação entre um usuário do Azure AD e o usuário relacionado do Lesson.ly.</span><span class="sxs-lookup"><span data-stu-id="65bdc-140">In other words, a link relationship between an Azure AD user and the related user in Lesson.ly needs to be established.</span></span>

<span data-ttu-id="65bdc-141">No Lesson.ly, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="65bdc-141">In Lesson.ly, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="65bdc-142">Para configurar e testar o logon único do AD do Azure com o Lesson.ly, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="65bdc-142">To configure and test Azure AD single sign-on with Lesson.ly, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="65bdc-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="65bdc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="65bdc-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="65bdc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="65bdc-145">**[Criar um usuário de teste do Lesson.ly](#creating-a-lessonly-test-user)**: para ter um equivalente de Brenda Fernandes no Lesson.ly que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65bdc-145">**[Creating a Lesson.ly test user](#creating-a-lessonly-test-user)** - to have a counterpart of Britta Simon in Lesson.ly that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="65bdc-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="65bdc-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="65bdc-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="65bdc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="65bdc-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="65bdc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="65bdc-149">Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único no aplicativo Lesson.ly.</span><span class="sxs-lookup"><span data-stu-id="65bdc-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lesson.ly application.</span></span>

<span data-ttu-id="65bdc-150">**Para configurar o logon único do AD do Azure com o Lesson.ly, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="65bdc-150">**To configure Azure AD single sign-on with Lesson.ly, perform the following steps:**</span></span>

1. <span data-ttu-id="65bdc-151">No Portal do Azure, na página de integração de aplicativos do **Lesson.ly**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="65bdc-151">In the Azure portal, on the **Lesson.ly** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="65bdc-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="65bdc-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_samlbase.png)

3. <span data-ttu-id="65bdc-155">Na seção **Domínio e URLs do Lesson.ly**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="65bdc-155">On the **Lesson.ly Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_url.png)

    <span data-ttu-id="65bdc-157">a.</span><span class="sxs-lookup"><span data-stu-id="65bdc-157">a.</span></span> <span data-ttu-id="65bdc-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="65bdc-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.lesson.ly/signin`|
    | `https://<companyname>.lessonly.com/signin`|

    >[!NOTE]
    ><span data-ttu-id="65bdc-159">Ao referenciar um nome genérico, **companyname** precisará ser substituído por um nome real.</span><span class="sxs-lookup"><span data-stu-id="65bdc-159">When referencing a generic name that **companyname** needs to be replaced by an actual name.</span></span>
    
    <span data-ttu-id="65bdc-160">b.</span><span class="sxs-lookup"><span data-stu-id="65bdc-160">b.</span></span> <span data-ttu-id="65bdc-161">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="65bdc-161">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.lesson.ly/auth/saml/metadata`|
    | `https://<companyname>.lessonly.com/auth/saml/metadata`|

    > [!NOTE] 
    > <span data-ttu-id="65bdc-162">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="65bdc-162">These values are not real.</span></span> <span data-ttu-id="65bdc-163">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="65bdc-163">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="65bdc-164">Contate a [equipe de suporte do Cliente Lesson.ly](mailto:dev@lessonly.com) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="65bdc-164">Contact [Lesson.ly Client support team](mailto:dev@lessonly.com) to get these values.</span></span> 

4. <span data-ttu-id="65bdc-165">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="65bdc-165">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_certificate.png)

5. <span data-ttu-id="65bdc-167">O aplicativo Lesson.ly espera as declarações do SAML em um formato específico, o que exige que você adicione mapeamentos de atributo personalizados à sua configuração de **Atributos do Token SAML**. A seguinte captura de tela mostra um exemplo disso.</span><span class="sxs-lookup"><span data-stu-id="65bdc-167">The Lesson.ly application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **SAML Token Attributes** configuration.The following screenshot shows an example for this.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lessonly-tutorial/tutorial_lessonly_06.png)
           
6. <span data-ttu-id="65bdc-169">Na seção **Atributos de Usuário** da caixa de diálogo **Logon único**, configure o atributo do token SAML, conforme mostrado na imagem anterior e realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="65bdc-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span></span>

    | <span data-ttu-id="65bdc-170">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="65bdc-170">Attribute Name</span></span>   | <span data-ttu-id="65bdc-171">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="65bdc-171">Attribute Value</span></span> |
    | ---------------  | ----------------|
    | <span data-ttu-id="65bdc-172">urn: oid:2.5.4.42</span><span class="sxs-lookup"><span data-stu-id="65bdc-172">urn:oid:2.5.4.42</span></span> |<span data-ttu-id="65bdc-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="65bdc-173">user.givenname</span></span> |
    | <span data-ttu-id="65bdc-174">urn: oid:2.5.4.4</span><span class="sxs-lookup"><span data-stu-id="65bdc-174">urn:oid:2.5.4.4</span></span>  |<span data-ttu-id="65bdc-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="65bdc-175">user.surname</span></span> |
    | <span data-ttu-id="65bdc-176">urn:oid:0.9.2342.19200300.1001.3</span><span class="sxs-lookup"><span data-stu-id="65bdc-176">urn:oid:0.9.2342.19200300.1001.3</span></span> |<span data-ttu-id="65bdc-177">user.mail</span><span class="sxs-lookup"><span data-stu-id="65bdc-177">user.mail</span></span> |

    <span data-ttu-id="65bdc-178">a.</span><span class="sxs-lookup"><span data-stu-id="65bdc-178">a.</span></span> <span data-ttu-id="65bdc-179">Clique em **Adicionar atributo** para abrir o diálogo **Adicionar Atributo**.</span><span class="sxs-lookup"><span data-stu-id="65bdc-179">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-lessonly-tutorial/tutorial_attribute_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-lessonly-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="65bdc-182">b.</span><span class="sxs-lookup"><span data-stu-id="65bdc-182">b.</span></span> <span data-ttu-id="65bdc-183">Na caixa de texto **Nome** , digite o nome do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="65bdc-183">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="65bdc-184">c.</span><span class="sxs-lookup"><span data-stu-id="65bdc-184">c.</span></span> <span data-ttu-id="65bdc-185">Na lista **Valor**, digite o valor do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="65bdc-185">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="65bdc-186">d.</span><span class="sxs-lookup"><span data-stu-id="65bdc-186">d.</span></span> <span data-ttu-id="65bdc-187">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="65bdc-187">Click **Ok**.</span></span>     

7. <span data-ttu-id="65bdc-188">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="65bdc-188">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lessonly-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="65bdc-190">Na seção **Configuração do Lesson.ly**, clique em **Configurar o Lesson.ly** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="65bdc-190">On the **Lesson.ly Configuration** section, click **Configure Lesson.ly** to open **Configure sign-on** window.</span></span> <span data-ttu-id="65bdc-191">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="65bdc-191">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_configure.png)

9. <span data-ttu-id="65bdc-193">Para configurar o logon único no lado do **Lesson.ly**, é necessário enviar o **Certificado (Base64)** baixado, a **URL de Saída, ID da Entidade SAML e URL do Serviço de Logon Único SAML** para a [equipe de suporte do Lesson.ly](mailto:dev@lessonly.com).</span><span class="sxs-lookup"><span data-stu-id="65bdc-193">To configure single sign-on on **Lesson.ly** side, you need to send the downloaded **Certificate(Base64)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Lesson.ly support team](mailto:dev@lessonly.com).</span></span>

> [!TIP]
> <span data-ttu-id="65bdc-194">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="65bdc-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="65bdc-195">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="65bdc-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="65bdc-196">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="65bdc-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="65bdc-197">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="65bdc-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="65bdc-198">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="65bdc-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="65bdc-200">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="65bdc-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="65bdc-201">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="65bdc-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lessonly-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="65bdc-203">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="65bdc-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lessonly-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="65bdc-205">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="65bdc-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lessonly-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="65bdc-207">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="65bdc-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lessonly-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="65bdc-209">a.</span><span class="sxs-lookup"><span data-stu-id="65bdc-209">a.</span></span> <span data-ttu-id="65bdc-210">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="65bdc-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="65bdc-211">b.</span><span class="sxs-lookup"><span data-stu-id="65bdc-211">b.</span></span> <span data-ttu-id="65bdc-212">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="65bdc-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="65bdc-213">c.</span><span class="sxs-lookup"><span data-stu-id="65bdc-213">c.</span></span> <span data-ttu-id="65bdc-214">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="65bdc-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="65bdc-215">d.</span><span class="sxs-lookup"><span data-stu-id="65bdc-215">d.</span></span> <span data-ttu-id="65bdc-216">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="65bdc-216">Click **Create**.</span></span>
 
### <a name="creating-a-lessonly-test-user"></a><span data-ttu-id="65bdc-217">Criar um usuário de teste Lesson.ly</span><span class="sxs-lookup"><span data-stu-id="65bdc-217">Creating a Lesson.ly test user</span></span>

<span data-ttu-id="65bdc-218">O objetivo desta seção é criar um usuário chamado Brenda Fernandes em Lesson.ly.</span><span class="sxs-lookup"><span data-stu-id="65bdc-218">The objective of this section is to create a user called Britta Simon in Lesson.ly.</span></span> <span data-ttu-id="65bdc-219">O Lesson.ly dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="65bdc-219">Lesson.ly supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="65bdc-220">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="65bdc-220">There is no action item for you in this section.</span></span> <span data-ttu-id="65bdc-221">Um novo usuário será criado durante uma tentativa de acessar o Lesson.ly, caso ele ainda não exista.</span><span class="sxs-lookup"><span data-stu-id="65bdc-221">A new user will be created during an attempt to access Lesson.ly if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="65bdc-222">Se precisar criar um usuário manualmente, entre em contato com a [equipe de suporte do Lesson.ly](mailto:dev@lessonly.com).</span><span class="sxs-lookup"><span data-stu-id="65bdc-222">If you need to create an user manually, you need to contact the [Lesson.ly support team](mailto:dev@lessonly.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="65bdc-223">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="65bdc-223">Assigning the Azure AD test user</span></span>

<span data-ttu-id="65bdc-224">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure ao conceder acesso ao Lesson.ly.</span><span class="sxs-lookup"><span data-stu-id="65bdc-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lesson.ly.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="65bdc-226">**Para atribuir Brenda Fernandes ao Lesson.ly, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="65bdc-226">**To assign Britta Simon to Lesson.ly, perform the following steps:**</span></span>

1. <span data-ttu-id="65bdc-227">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="65bdc-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="65bdc-229">Na lista de aplicativos, selecione **Lesson.ly**.</span><span class="sxs-lookup"><span data-stu-id="65bdc-229">In the applications list, select **Lesson.ly**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_app.png) 

3. <span data-ttu-id="65bdc-231">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="65bdc-231">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="65bdc-233">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="65bdc-233">Click **Add** button.</span></span> <span data-ttu-id="65bdc-234">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="65bdc-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="65bdc-236">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="65bdc-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="65bdc-237">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="65bdc-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="65bdc-238">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="65bdc-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="65bdc-239">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="65bdc-239">Testing single sign-on</span></span>

<span data-ttu-id="65bdc-240">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="65bdc-240">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="65bdc-241">Quando você clicar no bloco Lesson.ly no Painel de Acesso, deverá ser automaticamente conectado ao seu aplicativo Lesson.ly.</span><span class="sxs-lookup"><span data-stu-id="65bdc-241">When you click the Lesson.ly tile in the Access Panel, you should get automatically signed-on to your Lesson.ly application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="65bdc-242">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="65bdc-242">Additional resources</span></span>

* [<span data-ttu-id="65bdc-243">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="65bdc-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="65bdc-244">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="65bdc-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_203.png

