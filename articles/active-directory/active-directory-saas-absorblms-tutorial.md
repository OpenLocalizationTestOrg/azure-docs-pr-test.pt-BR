---
title: "Tutorial: Integração do Azure Active Directory ao Absorb LMS | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e absorver LMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba9f1b3d-a4a0-4ff7-b0e7-428e0ed92142
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: a140a78a3a9474a6372a3ad4fb8251bd2452c990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-absorb-lms"></a><span data-ttu-id="866cd-103">Tutorial: Integração do Azure Active Directory ao Absorb LMS</span><span class="sxs-lookup"><span data-stu-id="866cd-103">Tutorial: Azure Active Directory integration with Absorb LMS</span></span>

<span data-ttu-id="866cd-104">Neste tutorial, você aprenderá como toointegrate Absorb LMS com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="866cd-104">In this tutorial, you learn how toointegrate Absorb LMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="866cd-105">Integrando absorver LMS com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="866cd-105">Integrating Absorb LMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="866cd-106">Você pode controlar no AD do Azure que tenha acesso tooAbsorb LMS</span><span class="sxs-lookup"><span data-stu-id="866cd-106">You can control in Azure AD who has access tooAbsorb LMS</span></span>
- <span data-ttu-id="866cd-107">Você pode habilitar seu usuários tooautomatically get conectado tooAbsorb LMS (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="866cd-107">You can enable your users tooautomatically get signed-on tooAbsorb LMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="866cd-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="866cd-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="866cd-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte.</span><span class="sxs-lookup"><span data-stu-id="866cd-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="866cd-110">[O que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="866cd-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="866cd-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="866cd-111">Prerequisites</span></span>

<span data-ttu-id="866cd-112">tooconfigure integração do AD do Azure com absorver LMS, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="866cd-112">tooconfigure Azure AD integration with Absorb LMS, you need hello following items:</span></span>

- <span data-ttu-id="866cd-113">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="866cd-113">An Azure AD subscription</span></span>
- <span data-ttu-id="866cd-114">Uma assinatura do Absorb LMS com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="866cd-114">An Absorb LMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="866cd-115">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="866cd-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="866cd-116">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="866cd-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="866cd-117">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="866cd-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="866cd-118">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="866cd-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="866cd-119">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="866cd-119">Scenario description</span></span>
<span data-ttu-id="866cd-120">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="866cd-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="866cd-121">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="866cd-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="866cd-122">Adicionando absorver LMS da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="866cd-122">Adding Absorb LMS from hello gallery</span></span>
2. <span data-ttu-id="866cd-123">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="866cd-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-absorb-lms-from-hello-gallery"></a><span data-ttu-id="866cd-124">Adicionando absorver LMS da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="866cd-124">Adding Absorb LMS from hello gallery</span></span>
<span data-ttu-id="866cd-125">tooconfigure Olá integração de absorver LMS tooAzure AD, é necessário tooadd Absorb LMS na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="866cd-125">tooconfigure hello integration of Absorb LMS in tooAzure AD, you need tooadd Absorb LMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="866cd-126">**tooadd Absorb LMS da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="866cd-126">**tooadd Absorb LMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="866cd-127">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="866cd-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="866cd-129">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="866cd-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="866cd-130">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="866cd-130">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="866cd-132">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="866cd-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="866cd-134">Na caixa de pesquisa hello, digite **absorver LMS**, selecione **absorver LMS** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="866cd-134">In hello search box, type **Absorb LMS**, select **Absorb LMS** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Absorver LMS na lista de resultados de saudação](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="866cd-136">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="866cd-136">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="866cd-137">Nesta seção, você configurará e testará o logon único do Azure AD com o Absorb LMS, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="866cd-137">In this section, you configure and test Azure AD single sign-on with Absorb LMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="866cd-138">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no LMS absorver é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="866cd-138">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Absorb LMS is tooa user in Azure AD.</span></span> <span data-ttu-id="866cd-139">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em absorver LMS precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="866cd-139">In other words, a link relationship between an Azure AD user and hello related user in Absorb LMS needs toobe established.</span></span>

<span data-ttu-id="866cd-140">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em absorver LMS.</span><span class="sxs-lookup"><span data-stu-id="866cd-140">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Absorb LMS.</span></span>

<span data-ttu-id="866cd-141">tooconfigure e teste de logon único do AD do Azure com absorver LMS, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="866cd-141">tooconfigure and test Azure AD single sign-on with Absorb LMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="866cd-142">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="866cd-142">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="866cd-143">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="866cd-143">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="866cd-144">**[Criar um usuário de teste de absorver LMS](#create-an-absorb-lms-test-user)**  -toohave um equivalente do Britta Simon no LMS absorver que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="866cd-144">**[Create an Absorb LMS test user](#create-an-absorb-lms-test-user)** - toohave a counterpart of Britta Simon in Absorb LMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="866cd-145">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="866cd-145">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="866cd-146">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="866cd-146">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="866cd-147">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="866cd-147">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="866cd-148">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de absorver LMS.</span><span class="sxs-lookup"><span data-stu-id="866cd-148">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Absorb LMS application.</span></span>

<span data-ttu-id="866cd-149">**tooconfigure AD do Azure-logon único com LMS absorver, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="866cd-149">**tooconfigure Azure AD single sign-on with Absorb LMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="866cd-150">Em Olá portal do Azure, Olá **absorver LMS** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="866cd-150">In hello Azure portal, on hello **Absorb LMS** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="866cd-152">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="866cd-152">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_samlbase.png)

3. <span data-ttu-id="866cd-154">Em Olá **absorver LMS domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="866cd-154">On hello **Absorb LMS Domain and URLs** section, perform hello following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do Absorb LMS](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_url.png)

    <span data-ttu-id="866cd-156">a.</span><span class="sxs-lookup"><span data-stu-id="866cd-156">a.</span></span> <span data-ttu-id="866cd-157">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.myabsorb.com/Account/SAML`</span><span class="sxs-lookup"><span data-stu-id="866cd-157">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.myabsorb.com/Account/SAML`</span></span>

    <span data-ttu-id="866cd-158">b.</span><span class="sxs-lookup"><span data-stu-id="866cd-158">b.</span></span> <span data-ttu-id="866cd-159">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.myabsorb.com/Account/SAML`</span><span class="sxs-lookup"><span data-stu-id="866cd-159">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.myabsorb.com/Account/SAML`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="866cd-160">Esses valores não são Olá real.</span><span class="sxs-lookup"><span data-stu-id="866cd-160">These values are not hello real.</span></span> <span data-ttu-id="866cd-161">Atualize esses valores com URL de resposta e o identificador de real de saudação.</span><span class="sxs-lookup"><span data-stu-id="866cd-161">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="866cd-162">Entre em contato com [equipe de suporte de absorver LMS cliente](https://www.absorblms.com/support) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="866cd-162">Contact [Absorb LMS Client support team](https://www.absorblms.com/support) tooget these values.</span></span> 

4. <span data-ttu-id="866cd-163">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="866cd-163">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_certificate.png) 

6. <span data-ttu-id="866cd-165">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="866cd-165">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-absorblms-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="866cd-167">Em Olá **absorver LMS configuração** seção, clique em **configurar LMS absorver** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="866cd-167">On hello **Absorb LMS Configuration** section, click **Configure Absorb LMS** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="866cd-168">Saudação de cópia **URL de logout e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="866cd-168">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuração do Absorb LMS](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_configure.png) 

8. <span data-ttu-id="866cd-170">Em uma janela de navegador web diferente, faça logon no site da empresa absorver LMS tooyour como um administrador.</span><span class="sxs-lookup"><span data-stu-id="866cd-170">In a different web browser window, log in tooyour Absorb LMS company site as an administrator.</span></span>

9. <span data-ttu-id="866cd-171">Clique em Olá **ícone conta** na interface de administração de saudação.</span><span class="sxs-lookup"><span data-stu-id="866cd-171">Click hello **Account Icon** on hello admin interface.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-absorblms-tutorial/1.png)

10. <span data-ttu-id="866cd-173">Clique em **Configurações do Portal**.</span><span class="sxs-lookup"><span data-stu-id="866cd-173">Click **Portal Settings**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-absorblms-tutorial/2.png)
    
11. <span data-ttu-id="866cd-175">Clique em Olá **usuários** guia.</span><span class="sxs-lookup"><span data-stu-id="866cd-175">Click hello **Users** tab.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-absorblms-tutorial/3.png)

12. <span data-ttu-id="866cd-177">Execute Olá etapas tooaccess Olá logon único nos campos de configuração a seguir:</span><span class="sxs-lookup"><span data-stu-id="866cd-177">Perform hello following steps tooaccess hello Single Sign-On configuration fields:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-absorblms-tutorial/4.png)

    <span data-ttu-id="866cd-179">a.</span><span class="sxs-lookup"><span data-stu-id="866cd-179">a.</span></span> <span data-ttu-id="866cd-180">Selecione Olá apropriado **modo**.</span><span class="sxs-lookup"><span data-stu-id="866cd-180">Select hello appropriate **Mode**.</span></span>

    <span data-ttu-id="866cd-181">b.</span><span class="sxs-lookup"><span data-stu-id="866cd-181">b.</span></span> <span data-ttu-id="866cd-182">Abra Olá certificado que você baixou do hello portal do Azure no bloco de notas, remova Olá **---iniciar certificado---** e **---concluir certificado---** marca e cole Olá restantes conteúdo Olá **chave** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="866cd-182">Open hello Certificate that you have downloaded from hello Azure portal in notepad, remove hello **---BEGIN CERTIFICATE---** and **---END CERTIFICATE---** tag and then paste hello remaining content in hello **Key** textbox.</span></span>
    
    <span data-ttu-id="866cd-183">c.</span><span class="sxs-lookup"><span data-stu-id="866cd-183">c.</span></span> <span data-ttu-id="866cd-184">Em Olá **propriedade Id**, selecione Olá atributo apropriado que você tenha configurado como Olá identificador de usuário no hello AD do Azure (por exemplo, se userprinciplename Olá for selecionado no AD do Azure, em seguida, o nome de usuário deve ser selecionado.)</span><span class="sxs-lookup"><span data-stu-id="866cd-184">In hello **Id Property**, select hello appropriate attribute which you have configured as hello user identifier in hello Azure AD (For example, If hello userprinciplename is selected in Azure AD, then Username would be selected here.)</span></span>

    <span data-ttu-id="866cd-185">d.</span><span class="sxs-lookup"><span data-stu-id="866cd-185">d.</span></span> <span data-ttu-id="866cd-186">Em Olá **URL de logon**, cole Olá **"Single Sign-On URL do serviço SAML"** valor que você copiou de saudação **configurar o logon** janela de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="866cd-186">In hello **Login URL**, paste hello **“SAML Single Sign-On Service URL”** value you have copied from hello **Configure sign-on** window of hello Azure portal.</span></span>

    <span data-ttu-id="866cd-187">e.</span><span class="sxs-lookup"><span data-stu-id="866cd-187">e.</span></span> <span data-ttu-id="866cd-188">Em Olá **URL de Logout**, cole Olá **"URL de logout"** valor que você copiou de saudação **configurar o logon** janela de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="866cd-188">In hello **Logout URL**, paste hello **“Sign-Out URL”** value you have copied from hello **Configure sign-on** window of hello Azure portal.</span></span>

13. <span data-ttu-id="866cd-189">Habilitar **"Permitir apenas logon SSO"**.</span><span class="sxs-lookup"><span data-stu-id="866cd-189">Enable **‘Only Allow SSO Login’**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-absorblms-tutorial/5.png)

14. <span data-ttu-id="866cd-191">Clique em **"Salvar".**</span><span class="sxs-lookup"><span data-stu-id="866cd-191">Click **"Save."**</span></span>

> [!TIP]
> <span data-ttu-id="866cd-192">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="866cd-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="866cd-193">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="866cd-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="866cd-194">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="866cd-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="866cd-195">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="866cd-195">Create an Azure AD test user</span></span>

<span data-ttu-id="866cd-196">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="866cd-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="866cd-198">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="866cd-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="866cd-199">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="866cd-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-absorblms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="866cd-201">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="866cd-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-absorblms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="866cd-203">Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="866cd-203">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![botão Adicionar de saudação](./media/active-directory-saas-absorblms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="866cd-205">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="866cd-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-absorblms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="866cd-207">a.</span><span class="sxs-lookup"><span data-stu-id="866cd-207">a.</span></span> <span data-ttu-id="866cd-208">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="866cd-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="866cd-209">b.</span><span class="sxs-lookup"><span data-stu-id="866cd-209">b.</span></span> <span data-ttu-id="866cd-210">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="866cd-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="866cd-211">c.</span><span class="sxs-lookup"><span data-stu-id="866cd-211">c.</span></span> <span data-ttu-id="866cd-212">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="866cd-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="866cd-213">d.</span><span class="sxs-lookup"><span data-stu-id="866cd-213">d.</span></span> <span data-ttu-id="866cd-214">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="866cd-214">Click **Create**.</span></span>

### <a name="create-an-absorb-lms-test-user"></a><span data-ttu-id="866cd-215">Criar um usuário de teste do Absorb LMS</span><span class="sxs-lookup"><span data-stu-id="866cd-215">Create an Absorb LMS test user</span></span>

<span data-ttu-id="866cd-216">tooenable AD do Azure usuários toolog em tooAbsorb LMS, eles devem ser provisionados no tooAbsorb LMS.</span><span class="sxs-lookup"><span data-stu-id="866cd-216">tooenable Azure AD users toolog in tooAbsorb LMS, they must be provisioned in tooAbsorb LMS.</span></span>  
<span data-ttu-id="866cd-217">Para o Absorb LMS, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="866cd-217">For Absorb LMS, provisioning is a manual task.</span></span>

<span data-ttu-id="866cd-218">**tooprovision uma conta de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="866cd-218">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="866cd-219">Faça logon tooyour site da empresa de absorver LMS como um administrador.</span><span class="sxs-lookup"><span data-stu-id="866cd-219">Log in tooyour Absorb LMS company site as an administrator.</span></span>

2. <span data-ttu-id="866cd-220">Clique na guia **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="866cd-220">Click **Users** tab.</span></span>

    ![Convidar Pessoas](./media/active-directory-saas-absorblms-tutorial/absorblms_users.png)

3. <span data-ttu-id="866cd-222">Clique em **usuários** em Olá **usuários** guia.</span><span class="sxs-lookup"><span data-stu-id="866cd-222">Click **Users** under hello **Users** tab.</span></span>

    ![Convidar Pessoas](./media/active-directory-saas-absorblms-tutorial/absorblms_userssub.png)

4.  <span data-ttu-id="866cd-224">Selecione **Usuário** da lista suspensa **Adicionar Novo**.</span><span class="sxs-lookup"><span data-stu-id="866cd-224">Select **User** from **Add New** drop-down.</span></span>

    ![Convidar Pessoas](./media/active-directory-saas-absorblms-tutorial/absorblms_createuser.png)

5. <span data-ttu-id="866cd-226">Em Olá **adicionar usuário** página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="866cd-226">On hello **Add User** page, perform hello following steps:</span></span>

    ![Convidar Pessoas](./media/active-directory-saas-absorblms-tutorial/user.png)

    <span data-ttu-id="866cd-228">a.</span><span class="sxs-lookup"><span data-stu-id="866cd-228">a.</span></span> <span data-ttu-id="866cd-229">Em Olá **nome** caixa de texto Nome do tipo hello primeiro como Britta.</span><span class="sxs-lookup"><span data-stu-id="866cd-229">In hello **First Name** textbox, type hello first name like Britta.</span></span>

    <span data-ttu-id="866cd-230">b.</span><span class="sxs-lookup"><span data-stu-id="866cd-230">b.</span></span> <span data-ttu-id="866cd-231">Em Olá **Sobrenome** caixa de texto, digite Olá sobrenome como Simon.</span><span class="sxs-lookup"><span data-stu-id="866cd-231">In hello **Last Name** textbox, type hello last name like Simon.</span></span>
    
    <span data-ttu-id="866cd-232">c.</span><span class="sxs-lookup"><span data-stu-id="866cd-232">c.</span></span> <span data-ttu-id="866cd-233">Em Olá **Username** caixa de texto, nome de usuário do tipo hello como Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="866cd-233">In hello **Username** textbox, type hello user name like Britta Simon.</span></span>

    <span data-ttu-id="866cd-234">d.</span><span class="sxs-lookup"><span data-stu-id="866cd-234">d.</span></span> <span data-ttu-id="866cd-235">Em Olá **senha** caixa de texto, digite a senha de saudação do Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="866cd-235">In hello **Password** textbox, type hello password of Britta Simon.</span></span>

    <span data-ttu-id="866cd-236">e.</span><span class="sxs-lookup"><span data-stu-id="866cd-236">e.</span></span> <span data-ttu-id="866cd-237">Em Olá **Confirmar senha** caixa de texto, Olá tipo mesma senha.</span><span class="sxs-lookup"><span data-stu-id="866cd-237">In hello **Confirm Password** textbox, type hello same password.</span></span>
    
    <span data-ttu-id="866cd-238">f.</span><span class="sxs-lookup"><span data-stu-id="866cd-238">f.</span></span> <span data-ttu-id="866cd-239">Torne-a **ATIVA**.</span><span class="sxs-lookup"><span data-stu-id="866cd-239">Make it as **ACTIVE**.</span></span>   

6. <span data-ttu-id="866cd-240">Clique em **"Salvar".**</span><span class="sxs-lookup"><span data-stu-id="866cd-240">Click **"Save."**</span></span>
 
### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="866cd-241">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="866cd-241">Assign hello Azure AD test user</span></span>

<span data-ttu-id="866cd-242">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooAbsorb LMS.</span><span class="sxs-lookup"><span data-stu-id="866cd-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAbsorb LMS.</span></span>

![Atribuir função de usuário Olá][200]

<span data-ttu-id="866cd-244">**tooassign Britta Simon tooAbsorb LMS, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="866cd-244">**tooassign Britta Simon tooAbsorb LMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="866cd-245">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="866cd-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="866cd-247">Na lista de aplicativos hello, selecione **absorver LMS**.</span><span class="sxs-lookup"><span data-stu-id="866cd-247">In hello applications list, select **Absorb LMS**.</span></span>

    ![Olá absorver LMS link na lista de aplicativos Olá](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_app.png) 

3. <span data-ttu-id="866cd-249">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="866cd-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202] 

4. <span data-ttu-id="866cd-251">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="866cd-251">Click **Add** button.</span></span> <span data-ttu-id="866cd-252">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="866cd-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="866cd-254">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="866cd-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="866cd-255">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="866cd-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="866cd-256">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="866cd-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="866cd-257">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="866cd-257">Test single sign-on</span></span>

<span data-ttu-id="866cd-258">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="866cd-258">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="866cd-259">Clique em Olá absorver LMS lado a lado no hello painel de acesso, você obterá tooyour automaticamente conectado no aplicativo de absorver LMS.</span><span class="sxs-lookup"><span data-stu-id="866cd-259">Click hello Absorb LMS tile in hello Access Panel, you will get automatically signed-on tooyour Absorb LMS application.</span></span> <span data-ttu-id="866cd-260">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="866cd-260">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="866cd-261">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="866cd-261">Additional resources</span></span>

* [<span data-ttu-id="866cd-262">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="866cd-262">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="866cd-263">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="866cd-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_203.png

