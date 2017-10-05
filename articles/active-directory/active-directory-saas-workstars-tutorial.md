---
title: "Tutorial: integração do Azure Active Directory com o Workstars | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Workstars."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 51a4a4e4-ff60-4971-b3f8-a0367b70d220
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: e17c85689fa3aebf00ebf559185032b90103b4a5
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workstars"></a><span data-ttu-id="94053-103">Tutorial: integração do Azure Active Directory com o Workstars</span><span class="sxs-lookup"><span data-stu-id="94053-103">Tutorial: Azure Active Directory integration with Workstars</span></span>

<span data-ttu-id="94053-104">Neste tutorial, você aprenderá a integrar o Workstars ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="94053-104">In this tutorial, you learn how to integrate Workstars with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="94053-105">A integração do Workstars ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="94053-105">Integrating Workstars with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="94053-106">No Azure AD, é possível controlar quem tem acesso ao Workstars.</span><span class="sxs-lookup"><span data-stu-id="94053-106">You can control in Azure AD who has access to Workstars.</span></span>
- <span data-ttu-id="94053-107">Você pode permitir que os usuários façam logon automaticamente no Workstars (logon único) com as respectivas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="94053-107">You can enable your users to automatically get signed-on to Workstars (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="94053-108">Você pode gerenciar suas contas em um único local central – o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="94053-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="94053-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="94053-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94053-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="94053-110">Prerequisites</span></span>

<span data-ttu-id="94053-111">Para configurar a integração do Azure AD ao Workstars, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="94053-111">To configure Azure AD integration with Workstars, you need the following items:</span></span>

- <span data-ttu-id="94053-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="94053-112">An Azure AD subscription</span></span>
- <span data-ttu-id="94053-113">Uma assinatura do Workstars habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="94053-113">A Workstars single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="94053-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="94053-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="94053-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="94053-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="94053-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="94053-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="94053-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="94053-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="94053-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="94053-118">Scenario description</span></span>
<span data-ttu-id="94053-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="94053-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="94053-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="94053-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="94053-121">Adicionar o Workstars da galeria</span><span class="sxs-lookup"><span data-stu-id="94053-121">Adding Workstars from the gallery</span></span>
2. <span data-ttu-id="94053-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="94053-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workstars-from-the-gallery"></a><span data-ttu-id="94053-123">Adicionar o Workstars da galeria</span><span class="sxs-lookup"><span data-stu-id="94053-123">Adding Workstars from the gallery</span></span>
<span data-ttu-id="94053-124">Para configurar a integração do Workstars ao Azure AD, você precisará adicionar o Workstars da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="94053-124">To configure the integration of Workstars into Azure AD, you need to add Workstars from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="94053-125">**Para adicionar o Workstars da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="94053-125">**To add Workstars from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="94053-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="94053-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="94053-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="94053-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="94053-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="94053-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="94053-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="94053-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="94053-133">Na caixa de pesquisa, digite **Workstars**, selecione **Workstars** no painel de resultados e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="94053-133">In the search box, type **Workstars**, select **Workstars** from result panel then click **Add** button to add the application.</span></span>

    ![Workstars na lista de resultados](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="94053-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="94053-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="94053-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Workstars, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="94053-136">In this section, you configure and test Azure AD single sign-on with Workstars based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="94053-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Workstars é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="94053-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Workstars is to a user in Azure AD.</span></span> <span data-ttu-id="94053-138">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Workstars.</span><span class="sxs-lookup"><span data-stu-id="94053-138">In other words, a link relationship between an Azure AD user and the related user in Workstars needs to be established.</span></span>

<span data-ttu-id="94053-139">No Workstars, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="94053-139">In Workstars, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="94053-140">Para configurar e testar o logon único do Azure AD com o Workstars, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="94053-140">To configure and test Azure AD single sign-on with Workstars, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="94053-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="94053-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="94053-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="94053-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="94053-143">**[Criar um usuário de teste do Workstars](#create-a-workstars-test-user)** – para ter um equivalente de Brenda Fernandes no Workstars vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="94053-143">**[Create a Workstars test user](#create-a-workstars-test-user)** - to have a counterpart of Britta Simon in Workstars that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="94053-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="94053-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="94053-145">**[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="94053-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="94053-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="94053-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="94053-147">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo Workstars.</span><span class="sxs-lookup"><span data-stu-id="94053-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workstars application.</span></span>

<span data-ttu-id="94053-148">**Para configurar o logon único do Azure AD com o Workstars, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="94053-148">**To configure Azure AD single sign-on with Workstars, perform the following steps:**</span></span>

1. <span data-ttu-id="94053-149">No Portal do Azure, na página de integração de aplicativos do **Workstars**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="94053-149">In the Azure portal, on the **Workstars** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="94053-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="94053-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_samlbase.png)

3. <span data-ttu-id="94053-153">Na seção **Domínio e URLs do Workstars**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="94053-153">On the **Workstars Domain and URLs** section, perform the following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_url.png)

    <span data-ttu-id="94053-155">a.</span><span class="sxs-lookup"><span data-stu-id="94053-155">a.</span></span> <span data-ttu-id="94053-156">Na caixa de texto **Identificador**, digite a URL: `https://workstars.com`</span><span class="sxs-lookup"><span data-stu-id="94053-156">In the **Identifier** textbox, type the URL: `https://workstars.com`</span></span>

    <span data-ttu-id="94053-157">b.</span><span class="sxs-lookup"><span data-stu-id="94053-157">b.</span></span> <span data-ttu-id="94053-158">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<subdomain>.workstars.com/saml/login_check`</span><span class="sxs-lookup"><span data-stu-id="94053-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.workstars.com/saml/login_check`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="94053-159">O valor não é real.</span><span class="sxs-lookup"><span data-stu-id="94053-159">The value is not real.</span></span> <span data-ttu-id="94053-160">Atualize o valor com a URL de Resposta real.</span><span class="sxs-lookup"><span data-stu-id="94053-160">Update the value with the actual Reply URL.</span></span> <span data-ttu-id="94053-161">Contate a [equipe de suporte do Workstars](https://support.workstars.com) para obter o valor.</span><span class="sxs-lookup"><span data-stu-id="94053-161">Contact [Workstars support team](https://support.workstars.com) to get the value.</span></span>
 
4. <span data-ttu-id="94053-162">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="94053-162">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_certificate.png) 

5. <span data-ttu-id="94053-164">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="94053-164">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-workstars-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="94053-166">Na seção **Configuração do Workstars**, clique em **Configurar o Workstars** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="94053-166">On the **Workstars Configuration** section, click **Configure Workstars** to open **Configure sign-on** window.</span></span> <span data-ttu-id="94053-167">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="94053-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuração do Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_configure.png) 

7. <span data-ttu-id="94053-169">Em outra janela do navegador, entre em seu site de empresa do Workstars como administrador.</span><span class="sxs-lookup"><span data-stu-id="94053-169">In another browser window, sign on to your Workstars company site as an administrator.</span></span>

8. <span data-ttu-id="94053-170">Na barra de ferramentas principal, clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="94053-170">In the main toolbar, click **Settings**.</span></span>

    ![Configurações do Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_sett.png)

9. <span data-ttu-id="94053-172">Vá para **Logon** > **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="94053-172">Go to **Sign On** > **Settings**.</span></span>

    ![Logon do Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_signon.png)

    ![Configurações do Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_settings.png)

10. <span data-ttu-id="94053-175">Na página **Configurações de Logon Único (SAML) – Configurações**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="94053-175">On the **Single Sign On (SAML) - Settings** page, perform the following steps:</span></span>
    
    ![SAML do Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_saml.png)

    <span data-ttu-id="94053-177">a.</span><span class="sxs-lookup"><span data-stu-id="94053-177">a.</span></span> <span data-ttu-id="94053-178">Na caixa de texto **Nome do Provedor de Identidade**, digite **Office 365**.</span><span class="sxs-lookup"><span data-stu-id="94053-178">In **Identity Provider Name** textbox, type **Office 365**.</span></span>

    <span data-ttu-id="94053-179">b.</span><span class="sxs-lookup"><span data-stu-id="94053-179">b.</span></span> <span data-ttu-id="94053-180">Na caixa de texto **ID da Entidade do Provedor de Identidade**, cole o valor da **ID da Entidade SAML** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="94053-180">In the **Identity Provider Entity ID** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="94053-181">c.</span><span class="sxs-lookup"><span data-stu-id="94053-181">c.</span></span> <span data-ttu-id="94053-182">Copie o conteúdo do arquivo de certificado baixado no bloco de notas e então cole-o na caixa de texto **Certificado x509**.</span><span class="sxs-lookup"><span data-stu-id="94053-182">Copy the content of the downloaded certificate file in notepad, and then paste it into the **x509 Certificate** textbox.</span></span> 

    <span data-ttu-id="94053-183">d.</span><span class="sxs-lookup"><span data-stu-id="94053-183">d.</span></span> <span data-ttu-id="94053-184">Na caixa de texto **URL do SSO do SAML**, cole o valor da **URL de Serviço de Logon Único do SAML** que você copiou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="94053-184">In the **SAML SSO URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="94053-185">e.</span><span class="sxs-lookup"><span data-stu-id="94053-185">e.</span></span> <span data-ttu-id="94053-186">Na caixa de texto **URL de Logoff Remoto**, cole o valor da **URL de Saída** que você copiou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="94053-186">In the **Remote Logout URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="94053-187">f.</span><span class="sxs-lookup"><span data-stu-id="94053-187">f.</span></span> <span data-ttu-id="94053-188">Selecione **ID de Nome** como **Email (Padrão)**.</span><span class="sxs-lookup"><span data-stu-id="94053-188">select **Name ID** as **Email (Default)**.</span></span>

    <span data-ttu-id="94053-189">g.</span><span class="sxs-lookup"><span data-stu-id="94053-189">g.</span></span> <span data-ttu-id="94053-190">Clique em **Confirmar**.</span><span class="sxs-lookup"><span data-stu-id="94053-190">Click **Confirm**.</span></span>
    
> [!TIP]
> <span data-ttu-id="94053-191">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="94053-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="94053-192">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="94053-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="94053-193">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="94053-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="94053-194">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="94053-194">Create an Azure AD test user</span></span>

<span data-ttu-id="94053-195">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="94053-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="94053-197">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="94053-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="94053-198">No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="94053-198">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-workstars-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="94053-200">Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="94053-200">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-workstars-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="94053-202">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.</span><span class="sxs-lookup"><span data-stu-id="94053-202">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![O botão Adicionar](./media/active-directory-saas-workstars-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="94053-204">Na caixa de diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="94053-204">In the **User** dialog box, perform the following steps:</span></span>

    ![A caixa de diálogo Usuário](./media/active-directory-saas-workstars-tutorial/create_aaduser_04.png)

    <span data-ttu-id="94053-206">a.</span><span class="sxs-lookup"><span data-stu-id="94053-206">a.</span></span> <span data-ttu-id="94053-207">Na caixa **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="94053-207">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="94053-208">b.</span><span class="sxs-lookup"><span data-stu-id="94053-208">b.</span></span> <span data-ttu-id="94053-209">Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="94053-209">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="94053-210">c.</span><span class="sxs-lookup"><span data-stu-id="94053-210">c.</span></span> <span data-ttu-id="94053-211">Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.</span><span class="sxs-lookup"><span data-stu-id="94053-211">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="94053-212">d.</span><span class="sxs-lookup"><span data-stu-id="94053-212">d.</span></span> <span data-ttu-id="94053-213">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="94053-213">Click **Create**.</span></span>
  
### <a name="create-a-workstars-test-user"></a><span data-ttu-id="94053-214">Criar um usuário de teste do Workstars</span><span class="sxs-lookup"><span data-stu-id="94053-214">Create a Workstars test user</span></span>

<span data-ttu-id="94053-215">Nesta seção, você criará uma usuária chamada Brenda Fernandes no Workstars.</span><span class="sxs-lookup"><span data-stu-id="94053-215">In this section, you create a user called Britta Simon in Workstars.</span></span> <span data-ttu-id="94053-216">Trabalhe com a [equipe de suporte do Workstars](https://support.workstars.com) para adicionar os usuários na plataforma do Workstars.</span><span class="sxs-lookup"><span data-stu-id="94053-216">Work with [Workstars support team](https://support.workstars.com) to add the users in the Workstars platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="94053-217">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="94053-217">Assign the Azure AD test user</span></span>

<span data-ttu-id="94053-218">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Workstars.</span><span class="sxs-lookup"><span data-stu-id="94053-218">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workstars.</span></span>

![Atribuir a função de usuário][200] 

<span data-ttu-id="94053-220">**Para atribuir Brenda Fernandes ao Workstars, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="94053-220">**To assign Britta Simon to Workstars, perform the following steps:**</span></span>

1. <span data-ttu-id="94053-221">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="94053-221">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="94053-223">Na lista de aplicativos, selecione **Workstars**.</span><span class="sxs-lookup"><span data-stu-id="94053-223">In the applications list, select **Workstars**.</span></span>

    ![O link do Workstars na lista de Aplicativos](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_app.png)  

3. <span data-ttu-id="94053-225">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="94053-225">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202]

4. <span data-ttu-id="94053-227">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="94053-227">Click **Add** button.</span></span> <span data-ttu-id="94053-228">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="94053-228">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="94053-230">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="94053-230">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="94053-231">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="94053-231">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="94053-232">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="94053-232">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="94053-233">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="94053-233">Test single sign-on</span></span>

<span data-ttu-id="94053-234">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="94053-234">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="94053-235">Quando você clica no bloco Workstars no Painel de Acesso, você deve fazer logon automaticamente no seu aplicativo Workstars.</span><span class="sxs-lookup"><span data-stu-id="94053-235">When you click the Workstars tile in the Access Panel, you should get automatically signed-on to your Workstars application.</span></span>
<span data-ttu-id="94053-236">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="94053-236">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="94053-237">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="94053-237">Additional resources</span></span>

* [<span data-ttu-id="94053-238">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="94053-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="94053-239">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="94053-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_203.png

