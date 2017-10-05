---
title: "Tutorial: Integração do Azure Active Directory ao RFPIO | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o RFPIO."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 87187076-7b50-4247-814f-f217b052703f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 26a8bb17dad5a01b401ce7f9b484f09822825cbf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rfpio"></a><span data-ttu-id="a5e63-103">Tutorial: Integração do Azure Active Directory ao RFPIO</span><span class="sxs-lookup"><span data-stu-id="a5e63-103">Tutorial: Azure Active Directory integration with RFPIO</span></span>

<span data-ttu-id="a5e63-104">Neste tutorial, você aprenderá a integrar o RFPIO ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="a5e63-104">In this tutorial, you learn how to integrate RFPIO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a5e63-105">A integração do RFPIO ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="a5e63-105">Integrating RFPIO with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a5e63-106">Você pode controlar no Azure AD quem tem acesso ao RFPIO.</span><span class="sxs-lookup"><span data-stu-id="a5e63-106">You can control who in Azure AD who has access to RFPIO.</span></span>
- <span data-ttu-id="a5e63-107">Você pode permitir que usuários façam logon automaticamente no RFPIO (Logon Único) com as respectivas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a5e63-107">You can enable your users to automatically get signed-on to RFPIO (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="a5e63-108">Você pode gerenciar suas contas em um único local: o novo Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a5e63-108">You can manage your accounts in one central location--the Azure portal.</span></span>

<span data-ttu-id="a5e63-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a5e63-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5e63-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a5e63-110">Prerequisites</span></span>

<span data-ttu-id="a5e63-111">Para configurar a integração do Azure AD ao RFPIO, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="a5e63-111">To configure Azure AD integration with RFPIO, you need the following items:</span></span>

- <span data-ttu-id="a5e63-112">Uma assinatura do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a5e63-112">An Azure AD subscription.</span></span>
- <span data-ttu-id="a5e63-113">Uma assinatura habilitada para logon único do RFPIO.</span><span class="sxs-lookup"><span data-stu-id="a5e63-113">A RFPIO single sign-on-enabled subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="a5e63-114">Não é recomendável que você use um ambiente de produção para testar as etapas neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="a5e63-114">We don't recommend that you use a production environment to test the steps in this tutorial.</span></span>

<span data-ttu-id="a5e63-115">Para testar as etapas neste tutorial, siga estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="a5e63-115">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="a5e63-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="a5e63-116">Do not use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="a5e63-117">Se não tiver um ambiente de avaliação do Azure AD, você pode obter uma [versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a5e63-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a5e63-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="a5e63-118">Scenario description</span></span>
<span data-ttu-id="a5e63-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="a5e63-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a5e63-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="a5e63-120">The scenario that's outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a5e63-121">Adicionar o RFPIO da galeria.</span><span class="sxs-lookup"><span data-stu-id="a5e63-121">Adding RFPIO from the gallery.</span></span>
2. <span data-ttu-id="a5e63-122">Configurar e testar o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a5e63-122">Configuring and testing Azure AD single sign-on.</span></span>

## <a name="add-rfpio-from-the-gallery"></a><span data-ttu-id="a5e63-123">Adicionar o RFPIO da galeria</span><span class="sxs-lookup"><span data-stu-id="a5e63-123">Add RFPIO from the gallery</span></span>
<span data-ttu-id="a5e63-124">Para configurar a integração do RFPIO ao Azure AD, você precisará adicionar o RFPIO da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="a5e63-124">To configure the integration of RFPIO into Azure AD, you need to add RFPIO from the gallery to your list of managed SaaS apps.</span></span>

### <a name="to-add-rfpio-from-the-gallery"></a><span data-ttu-id="a5e63-125">Para adicionar o RFPIO da galeria</span><span class="sxs-lookup"><span data-stu-id="a5e63-125">To add RFPIO from the gallery</span></span>

1. <span data-ttu-id="a5e63-126">No **[Portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo, selecione o ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a5e63-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation pane, select the **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a5e63-128">Selecione **Aplicativos da empresa**, em seguida, selecione **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a5e63-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="a5e63-130">Para adicionar um novo aplicativo, selecione o botão **Novo aplicativo** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a5e63-130">To add a new application, select the **New application** button on the top of dialog box.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="a5e63-132">Na caixa de pesquisa, digite **RFPIO**.</span><span class="sxs-lookup"><span data-stu-id="a5e63-132">In the search box, type **RFPIO**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_search.png)

5. <span data-ttu-id="a5e63-134">No painel de resultados, selecione **RFPIO** e selecione o botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a5e63-134">In the results panel, select **RFPIO**, and then select the **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a5e63-136">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5e63-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="a5e63-137">Nesta seção, você configurará e testará o logon único do Azure AD com o RFPIO, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="a5e63-137">In this section, you configure and test Azure AD single sign-on with RFPIO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a5e63-138">Para que o logon único funcione, o Azure AD precisa saber qual é a relação entre o usuário do RFPIO equivalente e um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a5e63-138">For single sign-on to work, Azure AD needs to know what the relationship is between counterpart user in RFPIO and a user in Azure AD.</span></span> <span data-ttu-id="a5e63-139">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do RFPIO.</span><span class="sxs-lookup"><span data-stu-id="a5e63-139">In other words, a link relationship between an Azure AD user and the related user in RFPIO needs to be established.</span></span>

<span data-ttu-id="a5e63-140">No RFPIO, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="a5e63-140">In RFPIO, assign the value of **user name** in Azure AD as the value of  **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a5e63-141">Para configurar e testar o logon único do Azure AD com o RFPIO, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="a5e63-141">To configure and test Azure AD single sign-on with RFPIO, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a5e63-142">**[Configurar o logon único do Azure AD](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="a5e63-142">**[Configure Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**--to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a5e63-143">**[Criar um usuário de teste do Azure AD](#creating-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="a5e63-143">**[Create an Azure AD test user](#creating-an-azure-ad-test-user)**-- to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a5e63-144">**[Criar um usuário de teste do RFPIO](#creating-a-rfpio-test-user)** – para ter um equivalente de Brenda Fernandes no RFPIO que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a5e63-144">**[Create a RFPIO test user](#creating-a-rfpio-test-user)** --to have a counterpart of Britta Simon in RFPIO that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a5e63-145">**[Atribuir o usuário de teste do Azure AD](#assigning-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a5e63-145">**[Assign the Azure AD test user](#assigning-the-azure-ad-test-user)**--to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a5e63-146">**[Testar o logon único](#testing-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="a5e63-146">**[Test Single Sign-On](#testing-single-sign-on)** --to verify if the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a5e63-147">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5e63-147">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a5e63-148">Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único no aplicativo RFPIO.</span><span class="sxs-lookup"><span data-stu-id="a5e63-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RFPIO application.</span></span>

<span data-ttu-id="a5e63-149">**Para configurar o logon único do Azure AD com o RFPIO, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a5e63-149">**To configure Azure AD single sign-on with RFPIO, perform the following steps:**</span></span>

1. <span data-ttu-id="a5e63-150">No Portal do Azure, na página de integração de aplicativos do **RFPIO**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="a5e63-150">In the Azure portal, on the **RFPIO** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="a5e63-152">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="a5e63-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_samlbase.png)

3. <span data-ttu-id="a5e63-154">Na seção **Domínio e URLs do RFPIO**, se você desejar configurar o aplicativo em modo iniciado pelo **IDP**:</span><span class="sxs-lookup"><span data-stu-id="a5e63-154">On the **RFPIO Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url.png)

    <span data-ttu-id="a5e63-156">a.</span><span class="sxs-lookup"><span data-stu-id="a5e63-156">a.</span></span> <span data-ttu-id="a5e63-157">Na caixa de texto **Identificador**, digite a URL: `https://www.rfpio.com`</span><span class="sxs-lookup"><span data-stu-id="a5e63-157">In the **Identifier** textbox, type the URL: `https://www.rfpio.com`</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url1.png)

    <span data-ttu-id="a5e63-159">b.</span><span class="sxs-lookup"><span data-stu-id="a5e63-159">b.</span></span> <span data-ttu-id="a5e63-160">Marque **Mostrar configurações de URL avançadas**.</span><span class="sxs-lookup"><span data-stu-id="a5e63-160">Check **Show advanced URL settings**.</span></span>

    <span data-ttu-id="a5e63-161">c.</span><span class="sxs-lookup"><span data-stu-id="a5e63-161">c.</span></span> <span data-ttu-id="a5e63-162">Na caixa de texto **Estado de Retransmissão** insira um valor de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="a5e63-162">In the **Relay State** textbox enter a string value.</span></span> <span data-ttu-id="a5e63-163">Entre em contato com a [equipe de suporte do RFPIO](https://www.rfpio.com/contact/) para obter esse valor.</span><span class="sxs-lookup"><span data-stu-id="a5e63-163">Contact [RFPIO support team](https://www.rfpio.com/contact/) to get this value.</span></span> 

4. <span data-ttu-id="a5e63-164">Marque **Mostrar configurações de URL avançadas**.</span><span class="sxs-lookup"><span data-stu-id="a5e63-164">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="a5e63-165">Se quiser configurar o aplicativo no modo iniciado em **SP**:</span><span class="sxs-lookup"><span data-stu-id="a5e63-165">If you wish to configure the application in **SP** initiated mode:</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url2.png)

    <span data-ttu-id="a5e63-167">Na caixa de texto **URL de Entrada**, digite a URL: `https://www.app.rfpio.com`</span><span class="sxs-lookup"><span data-stu-id="a5e63-167">In the **Sign on URL** textbox, type the URL: `https://www.app.rfpio.com`</span></span>

5. <span data-ttu-id="a5e63-168">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="a5e63-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_certificate.png) 

6. <span data-ttu-id="a5e63-170">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="a5e63-170">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="a5e63-172">Em outra janela do navegador da Web, faça logon no site do **RFPIO** como administrador.</span><span class="sxs-lookup"><span data-stu-id="a5e63-172">In a different web browser window, login to the **RFPIO** website as an administrator.</span></span>

8. <span data-ttu-id="a5e63-173">Clique no menu suspenso de canto inferior esquerdo.</span><span class="sxs-lookup"><span data-stu-id="a5e63-173">Click on the bottom left corner dropdown.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/app1.png)

9. <span data-ttu-id="a5e63-175">Clique em **Configurações da Organização**.</span><span class="sxs-lookup"><span data-stu-id="a5e63-175">Click on the **Organization Settings**.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/app2.png)

10. <span data-ttu-id="a5e63-177">Clique no **RECURSOS E INTEGRAÇÃO**.</span><span class="sxs-lookup"><span data-stu-id="a5e63-177">Click on the **FEATURES & INTEGRATION**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/app4.png)

11. <span data-ttu-id="a5e63-179">Em **Configuração de SSO de SAML**, clique **Editar**.</span><span class="sxs-lookup"><span data-stu-id="a5e63-179">In the **SAML SSO Configuration** Click **Edit**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/app3.png)

12. <span data-ttu-id="a5e63-181">Nesta seção, execute as seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="a5e63-181">In this Section perform following actions:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/app5.png)
    
    <span data-ttu-id="a5e63-183">a.</span><span class="sxs-lookup"><span data-stu-id="a5e63-183">a.</span></span> <span data-ttu-id="a5e63-184">Copie o conteúdo do **XML de Metadados baixado** e cole-o no campo de **configuração de identidade**.</span><span class="sxs-lookup"><span data-stu-id="a5e63-184">Copy the content of the **Downloaded Metadata XML** and paste it into the **identity configuration** field.</span></span>

    > [!NOTE]
    ><span data-ttu-id="a5e63-185">Para copiar o conteúdo do **XML de Metadados** baixado, use o **Notepad++** ou o **Editor XML** adequado.</span><span class="sxs-lookup"><span data-stu-id="a5e63-185">To copy the content of downloaded **Metadata XML** Use **Notepad++** or proper **XML Editor**.</span></span> 

    <span data-ttu-id="a5e63-186">b.</span><span class="sxs-lookup"><span data-stu-id="a5e63-186">b.</span></span> <span data-ttu-id="a5e63-187">Clique em **Validar**.</span><span class="sxs-lookup"><span data-stu-id="a5e63-187">Click **Validate**.</span></span>

    <span data-ttu-id="a5e63-188">c.</span><span class="sxs-lookup"><span data-stu-id="a5e63-188">c.</span></span> <span data-ttu-id="a5e63-189">Depois de clicar em **Validar**, inverta **SAML (Habilitado)** para ativado.</span><span class="sxs-lookup"><span data-stu-id="a5e63-189">After Clicking **Validate**, Flip **SAML(Enabled)** to on.</span></span>

    <span data-ttu-id="a5e63-190">d.</span><span class="sxs-lookup"><span data-stu-id="a5e63-190">d.</span></span> <span data-ttu-id="a5e63-191">Clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="a5e63-191">Click **Submit**.</span></span>

> [!TIP]
> <span data-ttu-id="a5e63-192">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="a5e63-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a5e63-193">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="a5e63-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a5e63-194">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a5e63-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a5e63-195">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5e63-195">Create an Azure AD test user</span></span>
<span data-ttu-id="a5e63-196">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="a5e63-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="a5e63-198">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a5e63-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a5e63-199">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a5e63-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rfpio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a5e63-201">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="a5e63-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rfpio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a5e63-203">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a5e63-203">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rfpio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a5e63-205">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="a5e63-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rfpio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a5e63-207">a.</span><span class="sxs-lookup"><span data-stu-id="a5e63-207">a.</span></span> <span data-ttu-id="a5e63-208">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="a5e63-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a5e63-209">b.</span><span class="sxs-lookup"><span data-stu-id="a5e63-209">b.</span></span> <span data-ttu-id="a5e63-210">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="a5e63-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a5e63-211">c.</span><span class="sxs-lookup"><span data-stu-id="a5e63-211">c.</span></span> <span data-ttu-id="a5e63-212">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="a5e63-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a5e63-213">d.</span><span class="sxs-lookup"><span data-stu-id="a5e63-213">d.</span></span> <span data-ttu-id="a5e63-214">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a5e63-214">Click **Create**.</span></span>
 
### <a name="create-a-rfpio-test-user"></a><span data-ttu-id="a5e63-215">Criar um usuário de teste do RFPIO</span><span class="sxs-lookup"><span data-stu-id="a5e63-215">Create a RFPIO test user</span></span>

<span data-ttu-id="a5e63-216">Para permitir que os usuários do Azure AD façam logon no RFPIO, eles devem ser provisionados no RFPIO.</span><span class="sxs-lookup"><span data-stu-id="a5e63-216">To enable Azure AD users to log in to RFPIO, they must be provisioned into RFPIO.</span></span>  
<span data-ttu-id="a5e63-217">No caso do RFPIO, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="a5e63-217">In the case of RFPIO, provisioning is a manual task.</span></span>

<span data-ttu-id="a5e63-218">**Para provisionar uma conta de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a5e63-218">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="a5e63-219">Faça logon no site da empresa do RFPIO como administrador.</span><span class="sxs-lookup"><span data-stu-id="a5e63-219">Log in to your RFPIO company site as an administrator.</span></span>

2. <span data-ttu-id="a5e63-220">Clique no menu suspenso de canto inferior esquerdo.</span><span class="sxs-lookup"><span data-stu-id="a5e63-220">Click on the bottom left corner dropdown.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/app1.png)

3. <span data-ttu-id="a5e63-222">Clique em **Configurações da Organização**.</span><span class="sxs-lookup"><span data-stu-id="a5e63-222">Click on the **Organization Settings**.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/app2.png)

4. <span data-ttu-id="a5e63-224">Clique em **MEMBROS DA EQUIPE**.</span><span class="sxs-lookup"><span data-stu-id="a5e63-224">Click **TEAM MEMBERS**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/app6.png)

5. <span data-ttu-id="a5e63-226">Clique em **ADICIONAR MEMBROS**.</span><span class="sxs-lookup"><span data-stu-id="a5e63-226">Click on **ADD MEMBERS**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/app7.png)

6. <span data-ttu-id="a5e63-228">Na seção **Adicionar Novos Membros**.</span><span class="sxs-lookup"><span data-stu-id="a5e63-228">In the **Add New Members** section.</span></span> <span data-ttu-id="a5e63-229">Execute as seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="a5e63-229">Perform following actions:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/app8.png)

    <span data-ttu-id="a5e63-231">a.</span><span class="sxs-lookup"><span data-stu-id="a5e63-231">a.</span></span> <span data-ttu-id="a5e63-232">Insira **Endereço de email** no campo **Inserir um email por linha**.</span><span class="sxs-lookup"><span data-stu-id="a5e63-232">Enter **Email address** in the **Enter one email per line** field.</span></span>

    <span data-ttu-id="a5e63-233">b.</span><span class="sxs-lookup"><span data-stu-id="a5e63-233">b.</span></span> <span data-ttu-id="a5e63-234">Selecione **Função** de acordo com seus requisitos.</span><span class="sxs-lookup"><span data-stu-id="a5e63-234">Plese select **Role** according your requirements.</span></span>

    <span data-ttu-id="a5e63-235">c.</span><span class="sxs-lookup"><span data-stu-id="a5e63-235">c.</span></span> <span data-ttu-id="a5e63-236">Clique em **ADICIONAR MEMBROS**.</span><span class="sxs-lookup"><span data-stu-id="a5e63-236">Click **ADD MEMBERS**.</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="a5e63-237">O titular da conta do Azure Active Directory receberá um email e seguirá um link para confirmar a conta antes que ela se torne ativa.</span><span class="sxs-lookup"><span data-stu-id="a5e63-237">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="a5e63-238">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5e63-238">Assign the Azure AD test user</span></span>

<span data-ttu-id="a5e63-239">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo acesso ao RFPIO.</span><span class="sxs-lookup"><span data-stu-id="a5e63-239">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RFPIO.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="a5e63-241">**Para atribuir Brenda Fernandes ao RFPIO, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a5e63-241">**To assign Britta Simon to RFPIO, perform the following steps:**</span></span>

1. <span data-ttu-id="a5e63-242">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a5e63-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="a5e63-244">Na lista de aplicativos, selecione **RFPIO**.</span><span class="sxs-lookup"><span data-stu-id="a5e63-244">In the applications list, select **RFPIO**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_app.png) 

3. <span data-ttu-id="a5e63-246">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="a5e63-246">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="a5e63-248">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a5e63-248">Click **Add** button.</span></span> <span data-ttu-id="a5e63-249">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a5e63-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="a5e63-251">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="a5e63-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a5e63-252">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a5e63-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a5e63-253">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a5e63-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a5e63-254">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="a5e63-254">Test single sign-on</span></span>

<span data-ttu-id="a5e63-255">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="a5e63-255">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="a5e63-256">Quando você clicar no bloco RFPIO no Painel de Acesso, deverá fazer logon automaticamente no seu aplicativo RFPIO.</span><span class="sxs-lookup"><span data-stu-id="a5e63-256">When you click the RFPIO tile in the Access Panel, you should get automatically signed-on to your RFPIO application.</span></span>
<span data-ttu-id="a5e63-257">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a5e63-257">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a5e63-258">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="a5e63-258">Additional resources</span></span>

* [<span data-ttu-id="a5e63-259">Lista de tutoriais sobre como integrar aplicativos SaaS com o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a5e63-259">List of tutorials about how to integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a5e63-260">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a5e63-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_203.png

