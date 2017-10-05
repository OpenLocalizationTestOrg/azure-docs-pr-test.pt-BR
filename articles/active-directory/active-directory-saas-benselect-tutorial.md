---
title: "Tutorial: Integração do Azure Active Directory com o BenSelect | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o BenSelect."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffa17478-3ea1-4356-a289-545b5b9a4494
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: f8caa023da05863372b7ef92b47a92168445d741
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benselect"></a><span data-ttu-id="08b0a-103">Tutorial: Integração do Azure Active Directory ao BenSelect</span><span class="sxs-lookup"><span data-stu-id="08b0a-103">Tutorial: Azure Active Directory integration with BenSelect</span></span>

<span data-ttu-id="08b0a-104">Neste tutorial, você aprenderá a integrar o BenSelect ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="08b0a-104">In this tutorial, you learn how to integrate BenSelect with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="08b0a-105">A integração do BenSelect ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="08b0a-105">Integrating BenSelect with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="08b0a-106">Você pode controlar no Azure AD quem tem acesso ao BenSelect</span><span class="sxs-lookup"><span data-stu-id="08b0a-106">You can control in Azure AD who has access to BenSelect</span></span>
- <span data-ttu-id="08b0a-107">Você pode permitir que os usuários façam logon automaticamente no BenSelect (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="08b0a-107">You can enable your users to automatically get signed-on to BenSelect (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="08b0a-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="08b0a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="08b0a-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="08b0a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="08b0a-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="08b0a-110">Prerequisites</span></span>

<span data-ttu-id="08b0a-111">Para configurar a integração do Azure AD ao BenSelect, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="08b0a-111">To configure Azure AD integration with BenSelect, you need the following items:</span></span>

- <span data-ttu-id="08b0a-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="08b0a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="08b0a-113">Uma assinatura habilitada para logon único do BenSelect</span><span class="sxs-lookup"><span data-stu-id="08b0a-113">A BenSelect single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="08b0a-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="08b0a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="08b0a-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="08b0a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="08b0a-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="08b0a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="08b0a-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="08b0a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="08b0a-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="08b0a-118">Scenario description</span></span>
<span data-ttu-id="08b0a-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="08b0a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="08b0a-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="08b0a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="08b0a-121">Adicionar BenSelect da galeria</span><span class="sxs-lookup"><span data-stu-id="08b0a-121">Adding BenSelect from the gallery</span></span>
2. <span data-ttu-id="08b0a-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="08b0a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-benselect-from-the-gallery"></a><span data-ttu-id="08b0a-123">Adicionar BenSelect da galeria</span><span class="sxs-lookup"><span data-stu-id="08b0a-123">Adding BenSelect from the gallery</span></span>
<span data-ttu-id="08b0a-124">Para configurar a integração do BenSelect ao Azure AD, você precisará adicionar o BenSelect à sua lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="08b0a-124">To configure the integration of BenSelect into Azure AD, you need to add BenSelect from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="08b0a-125">**Para adicionar o BenSelect da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="08b0a-125">**To add BenSelect from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="08b0a-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="08b0a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="08b0a-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="08b0a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="08b0a-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="08b0a-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="08b0a-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="08b0a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="08b0a-133">Na caixa de pesquisa, digite **BenSelect**.</span><span class="sxs-lookup"><span data-stu-id="08b0a-133">In the search box, type **BenSelect**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_search.png)

5. <span data-ttu-id="08b0a-135">No painel de resultados, selecione **BenSelect** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="08b0a-135">In the results panel, select **BenSelect**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="08b0a-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="08b0a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="08b0a-138">Nesta seção, você configura e testa o logon único do Azure AD com o BenSelect, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="08b0a-138">In this section, you configure and test Azure AD single sign-on with BenSelect based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="08b0a-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do BenSelect é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="08b0a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BenSelect is to a user in Azure AD.</span></span> <span data-ttu-id="08b0a-140">Em outras palavras, é necessário estabelecer uma relação de vinculação entre um usuário do Azure AD e o usuário relacionado no BenSelect.</span><span class="sxs-lookup"><span data-stu-id="08b0a-140">In other words, a link relationship between an Azure AD user and the related user in BenSelect needs to be established.</span></span>

<span data-ttu-id="08b0a-141">No BenSelect, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="08b0a-141">In BenSelect, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="08b0a-142">Para configurar e testar o logon único do Azure AD com o BenSelect, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="08b0a-142">To configure and test Azure AD single sign-on with BenSelect, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="08b0a-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="08b0a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="08b0a-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="08b0a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="08b0a-145">**[Criando um usuário de teste do BenSelect](#creating-a-benselect-test-user)** – para ter um equivalente de Brenda Fernandes no BenSelect que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="08b0a-145">**[Creating a BenSelect test user](#creating-a-benselect-test-user)** - to have a counterpart of Britta Simon in BenSelect that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="08b0a-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="08b0a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="08b0a-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="08b0a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="08b0a-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="08b0a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="08b0a-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo BenSelect.</span><span class="sxs-lookup"><span data-stu-id="08b0a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BenSelect application.</span></span>

<span data-ttu-id="08b0a-150">**Para configurar o logon único do Azure AD com o BenSelect, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="08b0a-150">**To configure Azure AD single sign-on with BenSelect, perform the following steps:**</span></span>

1. <span data-ttu-id="08b0a-151">No portal do Azure, na página de integração do aplicativo do **BenSelect**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="08b0a-151">In the Azure portal, on the **BenSelect** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="08b0a-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="08b0a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_samlbase.png)

3. <span data-ttu-id="08b0a-155">Na seção **Domínio e URLs do BenSelect**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="08b0a-155">On the **BenSelect Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_url.png)

    <span data-ttu-id="08b0a-157">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://www.benselect.com/enroll/login.aspx?Path=<tenant name>`</span><span class="sxs-lookup"><span data-stu-id="08b0a-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.benselect.com/enroll/login.aspx?Path=<tenant name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="08b0a-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="08b0a-158">This value is not real.</span></span> <span data-ttu-id="08b0a-159">Atualize esse valor com a URL de Resposta real.</span><span class="sxs-lookup"><span data-stu-id="08b0a-159">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="08b0a-160">Contate a [equipe de suporte do BenSelect](mailto:support@selerix.com) para obter esse valor.</span><span class="sxs-lookup"><span data-stu-id="08b0a-160">Contact [BenSelect support team](mailto:support@selerix.com) to get this value.</span></span>
 
4. <span data-ttu-id="08b0a-161">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Bruto)** e, em seguida, salve o arquivo de certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="08b0a-161">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_certificate.png) 

5. <span data-ttu-id="08b0a-163">O aplicativo BenSelect espera que as declarações SAML estejam em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="08b0a-163">BenSelect application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="08b0a-164">Configure as declarações a seguir para este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="08b0a-164">Configure the following claims for this application.</span></span> <span data-ttu-id="08b0a-165">Você pode gerenciar os valores desses atributos da seção **Atributos de Usuário** na página de integração de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="08b0a-165">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="08b0a-166">A captura de tela a seguir mostra um exemplo disso.</span><span class="sxs-lookup"><span data-stu-id="08b0a-166">The following screenshot shows an example for this.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_06.png)

6. <span data-ttu-id="08b0a-168">Na seção **Atributos de Usuário**, na caixa de diálogo **Logon único**:</span><span class="sxs-lookup"><span data-stu-id="08b0a-168">In the **User Attributes** section on the **Single sign-on** dialog:</span></span>

    <span data-ttu-id="08b0a-169">a.</span><span class="sxs-lookup"><span data-stu-id="08b0a-169">a.</span></span> <span data-ttu-id="08b0a-170">Na lista suspensa **Identificador de Usuário**, selecione **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="08b0a-170">In the **User Identifier** dropdown list, select **ExtractMailPrefix**.</span></span>

    <span data-ttu-id="08b0a-171">b.</span><span class="sxs-lookup"><span data-stu-id="08b0a-171">b.</span></span> <span data-ttu-id="08b0a-172">Na lista suspensa **Email**, selecione **user.userprincipalname**.</span><span class="sxs-lookup"><span data-stu-id="08b0a-172">In the **Mail** dropdown list, select **user.userprincipalname**.</span></span>

7. <span data-ttu-id="08b0a-173">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="08b0a-173">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-benselect-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="08b0a-175">Na seção **Configuração do BenSelect**, clique em **Configurar o BenSelect** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="08b0a-175">On the **BenSelect Configuration** section, click **Configure BenSelect** to open **Configure sign-on** window.</span></span> <span data-ttu-id="08b0a-176">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="08b0a-176">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_configure.png) 

9. <span data-ttu-id="08b0a-178">Para configurar o logon único no lado do **BenSelect**, é necessário enviar o **Certificado (Bruto)** baixado, a **URL de Saída, ID da Entidade SAML e URL do Serviço de Logon Único SAML** para a [equipe de suporte do BenSelect](mailto:support@selerix.com).</span><span class="sxs-lookup"><span data-stu-id="08b0a-178">To configure single sign-on on **BenSelect** side, you need to send the downloaded **Certificate(Raw)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [BenSelect support team](mailto:support@selerix.com).</span></span>

   >[!NOTE]
   ><span data-ttu-id="08b0a-179">Você precisa mencionar que essa integração requer o algoritmo SHA256 (não há suporte para SHA1) para definir o SSO no servidor apropriado, como app2101 etc.</span><span class="sxs-lookup"><span data-stu-id="08b0a-179">You need to mention that this integration requires the SHA256 algorithm (SHA1 is not supported) to set the SSO on the appropriate server like app2101 etc.</span></span> 
   
> [!TIP]
> <span data-ttu-id="08b0a-180">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="08b0a-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="08b0a-181">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="08b0a-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="08b0a-182">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="08b0a-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="08b0a-183">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="08b0a-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="08b0a-184">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="08b0a-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="08b0a-186">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="08b0a-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="08b0a-187">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="08b0a-187">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-benselect-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="08b0a-189">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="08b0a-189">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-benselect-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="08b0a-191">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="08b0a-191">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-benselect-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="08b0a-193">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="08b0a-193">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-benselect-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="08b0a-195">a.</span><span class="sxs-lookup"><span data-stu-id="08b0a-195">a.</span></span> <span data-ttu-id="08b0a-196">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="08b0a-196">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="08b0a-197">b.</span><span class="sxs-lookup"><span data-stu-id="08b0a-197">b.</span></span> <span data-ttu-id="08b0a-198">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="08b0a-198">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="08b0a-199">c.</span><span class="sxs-lookup"><span data-stu-id="08b0a-199">c.</span></span> <span data-ttu-id="08b0a-200">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="08b0a-200">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="08b0a-201">d.</span><span class="sxs-lookup"><span data-stu-id="08b0a-201">d.</span></span> <span data-ttu-id="08b0a-202">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="08b0a-202">Click **Create**.</span></span>
 
### <a name="creating-a-benselect-test-user"></a><span data-ttu-id="08b0a-203">Criando um usuário de teste do BenSelect</span><span class="sxs-lookup"><span data-stu-id="08b0a-203">Creating a BenSelect test user</span></span>

<span data-ttu-id="08b0a-204">O objetivo desta seção é criar uma usuária chamada Brenda Fernandes no BenSelect.</span><span class="sxs-lookup"><span data-stu-id="08b0a-204">The objective of this section is to create a user called Britta Simon in BenSelect.</span></span> <span data-ttu-id="08b0a-205">Trabalhe com a [equipe de suporte do BenSelect](mailto:support@selerix.com) para adicionar os usuários à conta do BenSelect.</span><span class="sxs-lookup"><span data-stu-id="08b0a-205">Work with [BenSelect support team](mailto:support@selerix.com) to add the users in the BenSelect account.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="08b0a-206">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="08b0a-206">Assigning the Azure AD test user</span></span>

<span data-ttu-id="08b0a-207">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao BenSelect.</span><span class="sxs-lookup"><span data-stu-id="08b0a-207">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BenSelect.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="08b0a-209">**Para atribuir Brenda Fernandes ao BenSelect, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="08b0a-209">**To assign Britta Simon to BenSelect, perform the following steps:**</span></span>

1. <span data-ttu-id="08b0a-210">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="08b0a-210">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="08b0a-212">Na lista de aplicativos, escolha **BenSelect**.</span><span class="sxs-lookup"><span data-stu-id="08b0a-212">In the applications list, select **BenSelect**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_app.png) 

3. <span data-ttu-id="08b0a-214">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="08b0a-214">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="08b0a-216">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="08b0a-216">Click **Add** button.</span></span> <span data-ttu-id="08b0a-217">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="08b0a-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="08b0a-219">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="08b0a-219">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="08b0a-220">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="08b0a-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="08b0a-221">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="08b0a-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="08b0a-222">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="08b0a-222">Testing single sign-on</span></span>

<span data-ttu-id="08b0a-223">Nesta seção, você testará sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="08b0a-223">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="08b0a-224">Ao clicar no bloco BenSelect no Painel de Acesso, você deverá ser conectado automaticamente ao aplicativo BenSelect.</span><span class="sxs-lookup"><span data-stu-id="08b0a-224">When you click the BenSelect tile in the Access Panel, you should get automatically signed-on to your BenSelect application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="08b0a-225">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="08b0a-225">Additional resources</span></span>

* [<span data-ttu-id="08b0a-226">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="08b0a-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="08b0a-227">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="08b0a-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_203.png

