---
title: "Tutorial: Integração do Azure Active Directory com o SAP NetWeaver | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o SAP NetWeaver."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1b9e59e3-e7ae-4e74-b16c-8c1a7ccfdef3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: ad4140eb1183094a67822ad92eabcd35101360b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-netweaver"></a><span data-ttu-id="61b51-103">Tutorial: Integração do Azure Active Directory com o SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="61b51-103">Tutorial: Azure Active Directory integration with SAP NetWeaver</span></span>

<span data-ttu-id="61b51-104">Neste tutorial, você aprenderá a integrar o SAP NetWeaver ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="61b51-104">In this tutorial, you learn how to integrate SAP NetWeaver with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="61b51-105">A integração do SAP NetWeaver ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="61b51-105">Integrating SAP NetWeaver with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="61b51-106">Você pode controlar no Azure AD que tem acesso ao SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="61b51-106">You can control in Azure AD who has access to SAP NetWeaver</span></span>
- <span data-ttu-id="61b51-107">Você pode permitir que seus usuários façam logon automaticamente no SAP NetWeaver (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="61b51-107">You can enable your users to automatically get signed-on to SAP NetWeaver (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="61b51-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="61b51-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="61b51-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="61b51-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="61b51-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="61b51-110">Prerequisites</span></span>

<span data-ttu-id="61b51-111">Para configurar a integração do Azure AD ao SAP NetWeaver, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="61b51-111">To configure Azure AD integration with SAP NetWeaver, you need the following items:</span></span>

- <span data-ttu-id="61b51-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="61b51-112">An Azure AD subscription</span></span>
- <span data-ttu-id="61b51-113">Uma assinatura habilitada para logon único do SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="61b51-113">An SAP NetWeaver single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="61b51-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="61b51-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="61b51-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="61b51-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="61b51-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="61b51-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="61b51-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="61b51-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="61b51-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="61b51-118">Scenario description</span></span>
<span data-ttu-id="61b51-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="61b51-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="61b51-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="61b51-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="61b51-121">Adicionar SAP NetWeaver da galeria</span><span class="sxs-lookup"><span data-stu-id="61b51-121">Adding SAP NetWeaver from the gallery</span></span>
2. <span data-ttu-id="61b51-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="61b51-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-netweaver-from-the-gallery"></a><span data-ttu-id="61b51-123">Adicionar SAP NetWeaver da galeria</span><span class="sxs-lookup"><span data-stu-id="61b51-123">Adding SAP NetWeaver from the gallery</span></span>
<span data-ttu-id="61b51-124">Para configurar a integração do SAP NetWeaver ao Azure AD, você precisará adicionar o SAP NetWeaver da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="61b51-124">To configure the integration of SAP NetWeaver into Azure AD, you need to add SAP NetWeaver from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="61b51-125">**Para adicionar o SAP NetWeaver da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="61b51-125">**To add SAP NetWeaver from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="61b51-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="61b51-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="61b51-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="61b51-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="61b51-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="61b51-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="61b51-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="61b51-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="61b51-133">Na caixa de pesquisa, digite **SAP NetWeaver**.</span><span class="sxs-lookup"><span data-stu-id="61b51-133">In the search box, type **SAP NetWeaver**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_search.png)

5. <span data-ttu-id="61b51-135">No painel de resultados, selecione **SAP NetWeaver** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="61b51-135">In the results panel, select **SAP NetWeaver**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="61b51-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="61b51-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="61b51-138">Nesta seção, você configurará e testará o logon único do Azure AD com o SAP NetWeaver, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="61b51-138">In this section, you configure and test Azure AD single sign-on with SAP NetWeaver based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="61b51-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do SAP NetWeaver é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="61b51-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP NetWeaver is to a user in Azure AD.</span></span> <span data-ttu-id="61b51-140">Em outras palavras, é necessário estabelecer uma relação de vinculação entre um usuário do Azure AD e o usuário relacionado no SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="61b51-140">In other words, a link relationship between an Azure AD user and the related user in SAP NetWeaver needs to be established.</span></span>

<span data-ttu-id="61b51-141">Essa relação de vínculo é estabelecida atribuindo o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** no SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="61b51-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SAP NetWeaver.</span></span>

<span data-ttu-id="61b51-142">Para configurar e testar o logon único do Azure AD com o SAP NetWeaver, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="61b51-142">To configure and test Azure AD single sign-on with SAP NetWeaver, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="61b51-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="61b51-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="61b51-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="61b51-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="61b51-145">**[Criação de um usuário de teste do SAP NetWeaver](#creating-an-sap-netweaver-test-user)** – para ter um equivalente de Brenda Fernandes no SAP NetWeaver que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="61b51-145">**[Creating an SAP NetWeaver test user](#creating-an-sap-netweaver-test-user)** - to have a counterpart of Britta Simon in SAP NetWeaver that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="61b51-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="61b51-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="61b51-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="61b51-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="61b51-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="61b51-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="61b51-149">Nesta seção, você habilitará o logon único do Azure AD no portal do Azure e configurará o logon único em seu aplicativo do SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="61b51-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAP NetWeaver application.</span></span>

<span data-ttu-id="61b51-150">**Para configurar o logon único do Azure AD com o SAP NetWeaver, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="61b51-150">**To configure Azure AD single sign-on with SAP NetWeaver, perform the following steps:**</span></span>

1. <span data-ttu-id="61b51-151">No portal do Azure, na página de integração do aplicativo **SAP NetWeaver**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="61b51-151">In the Azure portal, on the **SAP NetWeaver** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="61b51-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="61b51-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_samlbase.png)

3. <span data-ttu-id="61b51-155">Na seção **URLs e Domínio do SAP NetWeaver**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="61b51-155">On the **SAP NetWeaver Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_url.png)

    <span data-ttu-id="61b51-157">a.</span><span class="sxs-lookup"><span data-stu-id="61b51-157">a.</span></span> <span data-ttu-id="61b51-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<your company instance of SAP NetWeaver>`</span><span class="sxs-lookup"><span data-stu-id="61b51-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<your company instance of SAP NetWeaver>`</span></span>

    <span data-ttu-id="61b51-159">b.</span><span class="sxs-lookup"><span data-stu-id="61b51-159">b.</span></span> <span data-ttu-id="61b51-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<your company instance of SAP NetWeaver>`</span><span class="sxs-lookup"><span data-stu-id="61b51-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<your company instance of SAP NetWeaver>`</span></span>

    <span data-ttu-id="61b51-161">c.</span><span class="sxs-lookup"><span data-stu-id="61b51-161">c.</span></span> <span data-ttu-id="61b51-162">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<your company instance of SAP NetWeaver>/sap/saml2/sp/acs/100`</span><span class="sxs-lookup"><span data-stu-id="61b51-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<your company instance of SAP NetWeaver>/sap/saml2/sp/acs/100`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="61b51-163">Esses não são os valores reais.</span><span class="sxs-lookup"><span data-stu-id="61b51-163">These values are not the real.</span></span> <span data-ttu-id="61b51-164">Atualize esses valores com o Identificador, a URL de Resposta e a URL de Logon reais.</span><span class="sxs-lookup"><span data-stu-id="61b51-164">Update these values with the actual Identifier and Reply URL and Sign-On URL.</span></span> <span data-ttu-id="61b51-165">Aqui, sugerimos que você use o valor exclusivo de cadeia de caracteres no Identificador.</span><span class="sxs-lookup"><span data-stu-id="61b51-165">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="61b51-166">Contate a [equipe de suporte do cliente SAP NetWeaver](https://www.sap.com/support.html) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="61b51-166">Contact [SAP NetWeaver Client support team](https://www.sap.com/support.html) to get these values.</span></span> 

4. <span data-ttu-id="61b51-167">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo XML em seu computador.</span><span class="sxs-lookup"><span data-stu-id="61b51-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_certificate.png) 

5. <span data-ttu-id="61b51-169">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="61b51-169">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="61b51-171">Na seção **Configuração do SAP NetWeaver**, clique em **Configurar SAP NetWeaver** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="61b51-171">On the **SAP NetWeaver Configuration** section, click **Configure SAP NetWeaver** to open **Configure sign-on** window.</span></span> <span data-ttu-id="61b51-172">Copie a **ID da Entidade SAML** da **seção Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="61b51-172">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_configure.png) 

7. <span data-ttu-id="61b51-174">Para configurar o logon único no lado do **SAP NetWeaver**, é necessário enviar o **XML de Metadados** baixado e a **ID da Entidade SAML** para o [suporte do SAP NetWeaver](https://www.sap.com/support.html).</span><span class="sxs-lookup"><span data-stu-id="61b51-174">To configure single sign-on on **SAP NetWeaver** side, you need to send the downloaded **Metadata XML** and **SAML Entity ID** to [SAP NetWeaver support](https://www.sap.com/support.html).</span></span> 

> [!TIP]
> <span data-ttu-id="61b51-175">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="61b51-175">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="61b51-176">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="61b51-176">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="61b51-177">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="61b51-177">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="61b51-178">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="61b51-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="61b51-179">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="61b51-179">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="61b51-181">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="61b51-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="61b51-182">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="61b51-182">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="61b51-184">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="61b51-184">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="61b51-186">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="61b51-186">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="61b51-188">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="61b51-188">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="61b51-190">a.</span><span class="sxs-lookup"><span data-stu-id="61b51-190">a.</span></span> <span data-ttu-id="61b51-191">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="61b51-191">In the **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="61b51-192">b.</span><span class="sxs-lookup"><span data-stu-id="61b51-192">b.</span></span> <span data-ttu-id="61b51-193">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="61b51-193">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="61b51-194">c.</span><span class="sxs-lookup"><span data-stu-id="61b51-194">c.</span></span> <span data-ttu-id="61b51-195">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="61b51-195">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="61b51-196">d.</span><span class="sxs-lookup"><span data-stu-id="61b51-196">d.</span></span> <span data-ttu-id="61b51-197">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="61b51-197">Click **Create**.</span></span>
 
### <a name="creating-an-sap-netweaver-test-user"></a><span data-ttu-id="61b51-198">Criação de um usuário de teste do SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="61b51-198">Creating an SAP NetWeaver test user</span></span>

<span data-ttu-id="61b51-199">Nesta seção, você criará uma usuária chamada Brenda Fernandes no SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="61b51-199">In this section, you create a user called Britta Simon in SAP NetWeaver.</span></span> <span data-ttu-id="61b51-200">Trabalhe com seu [suporte do SAP NetWeaver](https://www.sap.com/support.html) para adicionar os usuários à plataforma SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="61b51-200">Work with your [SAP NetWeaver support](https://www.sap.com/support.html) to add the users in the SAP NetWeaver platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="61b51-201">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="61b51-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="61b51-202">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="61b51-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP NetWeaver.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="61b51-204">**Para atribuir Britta Simon ao SAP NetWeaver, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="61b51-204">**To assign Britta Simon to SAP NetWeaver, perform the following steps:**</span></span>

1. <span data-ttu-id="61b51-205">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="61b51-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="61b51-207">Na lista de aplicativos, selecione **SAP NetWeaver**.</span><span class="sxs-lookup"><span data-stu-id="61b51-207">In the applications list, select **SAP NetWeaver**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_app.png) 

3. <span data-ttu-id="61b51-209">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="61b51-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="61b51-211">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="61b51-211">Click **Add** button.</span></span> <span data-ttu-id="61b51-212">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="61b51-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="61b51-214">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="61b51-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="61b51-215">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="61b51-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="61b51-216">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="61b51-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="61b51-217">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="61b51-217">Testing single sign-on</span></span>

<span data-ttu-id="61b51-218">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="61b51-218">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="61b51-219">Ao clicar no bloco do SAP NetWeaver no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo do SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="61b51-219">When you click the SAP NetWeaver tile in the Access Panel, you should get automatically signed-on to your SAP NetWeaver application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="61b51-220">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="61b51-220">Additional resources</span></span>

* [<span data-ttu-id="61b51-221">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="61b51-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="61b51-222">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="61b51-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_203.png

