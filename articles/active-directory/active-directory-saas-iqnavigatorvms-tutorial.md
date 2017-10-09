---
title: "Tutorial: Integração do Azure Active Directory ao IQNavigator VMS | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e IQNavigator VMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a8a09b25-dfa5-4c31-aea2-53bf1853b365
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 5a5a7dd3f427acfba2f0ae10552a7179db730118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-iqnavigator-vms"></a><span data-ttu-id="accd2-103">Tutorial: Integração do Azure Active Directory ao IQNavigator VMS</span><span class="sxs-lookup"><span data-stu-id="accd2-103">Tutorial: Azure Active Directory integration with IQNavigator VMS</span></span>

<span data-ttu-id="accd2-104">Neste tutorial, você aprenderá como toointegrate IQNavigator VMS com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="accd2-104">In this tutorial, you learn how toointegrate IQNavigator VMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="accd2-105">Integrando IQNavigator VMS com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="accd2-105">Integrating IQNavigator VMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="accd2-106">Você pode controlar no AD do Azure que tenha acesso tooIQNavigator VMS</span><span class="sxs-lookup"><span data-stu-id="accd2-106">You can control in Azure AD who has access tooIQNavigator VMS</span></span>
- <span data-ttu-id="accd2-107">Você pode habilitar seu usuários tooautomatically get conectado tooIQNavigator VMS (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="accd2-107">You can enable your users tooautomatically get signed-on tooIQNavigator VMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="accd2-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="accd2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="accd2-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="accd2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="accd2-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="accd2-110">Prerequisites</span></span>

<span data-ttu-id="accd2-111">tooconfigure integração do AD do Azure com IQNavigator VMS, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="accd2-111">tooconfigure Azure AD integration with IQNavigator VMS, you need hello following items:</span></span>

- <span data-ttu-id="accd2-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="accd2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="accd2-113">Uma assinatura habilitada para logon único do IQNavigator VMS</span><span class="sxs-lookup"><span data-stu-id="accd2-113">A IQNavigator VMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="accd2-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="accd2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="accd2-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="accd2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="accd2-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="accd2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="accd2-117">Caso não tenha um ambiente de avaliação do Azure AD, obtenha uma avaliação de um mês aqui: [oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="accd2-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="accd2-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="accd2-118">Scenario description</span></span>
<span data-ttu-id="accd2-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="accd2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="accd2-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="accd2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="accd2-121">Adicionando IQNavigator VMS da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="accd2-121">Adding IQNavigator VMS from hello gallery</span></span>
2. <span data-ttu-id="accd2-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="accd2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-iqnavigator-vms-from-hello-gallery"></a><span data-ttu-id="accd2-123">Adicionando IQNavigator VMS da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="accd2-123">Adding IQNavigator VMS from hello gallery</span></span>
<span data-ttu-id="accd2-124">integração de saudação tooconfigure IQNavigator VMs no Azure AD, é necessário tooadd IQNavigator VMS na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="accd2-124">tooconfigure hello integration of IQNavigator VMS into Azure AD, you need tooadd IQNavigator VMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="accd2-125">**tooadd IQNavigator VMS na Galeria de hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="accd2-125">**tooadd IQNavigator VMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="accd2-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="accd2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="accd2-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="accd2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="accd2-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="accd2-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="accd2-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="accd2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="accd2-133">Na caixa de pesquisa hello, digite **IQNavigator VMS**.</span><span class="sxs-lookup"><span data-stu-id="accd2-133">In hello search box, type **IQNavigator VMS**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_search.png)

5. <span data-ttu-id="accd2-135">No painel de resultados de saudação, selecione **IQNavigator VMS**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="accd2-135">In hello results panel, select **IQNavigator VMS**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="accd2-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="accd2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="accd2-138">Nesta seção, você configura e testa o logon único do Azure AD com o IQNavigator VMS, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="accd2-138">In this section, you configure and test Azure AD single sign-on with IQNavigator VMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="accd2-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá IQNavigator VMs é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="accd2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in IQNavigator VMS is tooa user in Azure AD.</span></span> <span data-ttu-id="accd2-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em VMS IQNavigator precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="accd2-140">In other words, a link relationship between an Azure AD user and hello related user in IQNavigator VMS needs toobe established.</span></span>

<span data-ttu-id="accd2-141">IQNavigator VMS, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="accd2-141">In IQNavigator VMS, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="accd2-142">tooconfigure e teste de logon único do AD do Azure com IQNavigator VMS, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="accd2-142">tooconfigure and test Azure AD single sign-on with IQNavigator VMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="accd2-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="accd2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="accd2-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="accd2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="accd2-145">**[Criar um usuário de teste de VMS IQNavigator](#creating-a-iqnavigator-vms-test-user)**  -toohave um equivalente de Britta Simon IQNavigator VMs que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="accd2-145">**[Creating a IQNavigator VMS test user](#creating-a-iqnavigator-vms-test-user)** - toohave a counterpart of Britta Simon in IQNavigator VMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="accd2-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="accd2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="accd2-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="accd2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="accd2-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="accd2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="accd2-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo IQNavigator VMS.</span><span class="sxs-lookup"><span data-stu-id="accd2-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your IQNavigator VMS application.</span></span>

<span data-ttu-id="accd2-150">**tooconfigure AD do Azure-logon único com IQNavigator VMS, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="accd2-150">**tooconfigure Azure AD single sign-on with IQNavigator VMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="accd2-151">Em Olá portal do Azure, Olá **IQNavigator VMS** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="accd2-151">In hello Azure portal, on hello **IQNavigator VMS** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="accd2-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="accd2-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_samlbase.png)

3. <span data-ttu-id="accd2-155">Em Olá **IQNavigator VMS domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="accd2-155">On hello **IQNavigator VMS Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_url.png)

    <span data-ttu-id="accd2-157">a.</span><span class="sxs-lookup"><span data-stu-id="accd2-157">a.</span></span> <span data-ttu-id="accd2-158">Em Olá **identificador** caixa de texto, digite a URL de saudação:`iqn.com`</span><span class="sxs-lookup"><span data-stu-id="accd2-158">In hello **Identifier** textbox, type hello URL:`iqn.com`</span></span>

    <span data-ttu-id="accd2-159">b.</span><span class="sxs-lookup"><span data-stu-id="accd2-159">b.</span></span> <span data-ttu-id="accd2-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.iqnavigator.com/security/login?client_name=https://sts.window.net/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="accd2-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.iqnavigator.com/security/login?client_name=https://sts.window.net/<instance name>`</span></span>

4. <span data-ttu-id="accd2-161">Verificar **Mostrar configurações de URL avançadas**, executar Olá etapa a seguir:</span><span class="sxs-lookup"><span data-stu-id="accd2-161">Check **Show advanced URL settings**, perform hello following step:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_url1.png)

    <span data-ttu-id="accd2-163">Em Olá **estado de retransmissão** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.iqnavigator.com`</span><span class="sxs-lookup"><span data-stu-id="accd2-163">In hello **Relay state** textbox, type a URL using hello following pattern:`https://<subdomain>.iqnavigator.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="accd2-164">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="accd2-164">These values are not real.</span></span> <span data-ttu-id="accd2-165">Atualize esses valores com o estado real de URL de resposta e retransmissão hello.</span><span class="sxs-lookup"><span data-stu-id="accd2-165">Update these values with hello actual Reply URL and Relay state.</span></span> <span data-ttu-id="accd2-166">Entre em contato com [equipe de suporte do cliente de VMS IQNavigator](https://www.beeline.com/iqn-product-support/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="accd2-166">Contact [IQNavigator VMS Client support team](https://www.beeline.com/iqn-product-support/) tooget these values.</span></span> 

5. <span data-ttu-id="accd2-167">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="accd2-167">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="accd2-169">Olá toogenerate **metadados** url, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="accd2-169">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="accd2-170">a.</span><span class="sxs-lookup"><span data-stu-id="accd2-170">a.</span></span> <span data-ttu-id="accd2-171">Clique em **Registros do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="accd2-171">Click **App registrations**.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_appregistrations.png)
   
    <span data-ttu-id="accd2-173">b.</span><span class="sxs-lookup"><span data-stu-id="accd2-173">b.</span></span> <span data-ttu-id="accd2-174">Clique em **pontos de extremidade** tooopen **pontos de extremidade** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="accd2-174">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Configurar Logon Único](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_endpointicon.png)

    <span data-ttu-id="accd2-176">c.</span><span class="sxs-lookup"><span data-stu-id="accd2-176">c.</span></span> <span data-ttu-id="accd2-177">Clique em Olá cópia botão toocopy **documento de METADADOS de Federação** url e cole-o no bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="accd2-177">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_endpoint.png)
     
    <span data-ttu-id="accd2-179">d.</span><span class="sxs-lookup"><span data-stu-id="accd2-179">d.</span></span> <span data-ttu-id="accd2-180">Agora vá toohello a página de propriedades de **IQNavigator VMS** e cópia hello **Id do aplicativo** usando **cópia** botão e cole-o no bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="accd2-180">Now go toohello property page of **IQNavigator VMS** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_appid.png)

    <span data-ttu-id="accd2-182">e.</span><span class="sxs-lookup"><span data-stu-id="accd2-182">e.</span></span> <span data-ttu-id="accd2-183">Gerar Olá **URL de metadados** usando saudação padrão a seguir:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="accd2-183">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

7. <span data-ttu-id="accd2-184">IQNavigator aplicativo esperar que o valor de identificador de usuário exclusivo Olá na declaração do identificador de nome de saudação.</span><span class="sxs-lookup"><span data-stu-id="accd2-184">IQNavigator application expect hello unique user identifier value in hello Name Identifier claim.</span></span> <span data-ttu-id="accd2-185">Cliente pode mapear o valor correto de saudação de declaração do identificador de nome hello.</span><span class="sxs-lookup"><span data-stu-id="accd2-185">Customer can map hello correct value for hello Name Identifier claim.</span></span> <span data-ttu-id="accd2-186">Nesse caso Mapeamos usuário hello. UserPrincipalName para fins de demonstração de saudação.</span><span class="sxs-lookup"><span data-stu-id="accd2-186">In this case we have mapped hello user.UserPrincipalName for hello demo purpose.</span></span> <span data-ttu-id="accd2-187">Mas, de acordo com tooyour as configurações da organização você deve mapear valor correto Olá para ele.</span><span class="sxs-lookup"><span data-stu-id="accd2-187">But according tooyour organization settings you should map hello correct value for it.</span></span>   

    ![Configurar Logon Único](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_attribute.png)

8. <span data-ttu-id="accd2-189">Em Olá **IQNavigator VMS configuração** seção, clique em **configurar VMS de IQNavigator** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="accd2-189">On hello **IQNavigator VMS Configuration** section, click **Configure IQNavigator VMS** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="accd2-190">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="accd2-190">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_configure.png) 

9. <span data-ttu-id="accd2-192">tooconfigure logon único no **IQNavigator VMS** lado, você precisa Olá toosend **URL de metadados**, **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** muito [Equipe de suporte de VMS IQNavigator](https://www.beeline.com/iqn-product-support/).</span><span class="sxs-lookup"><span data-stu-id="accd2-192">tooconfigure single sign-on on **IQNavigator VMS** side, you need toosend hello **Metadata URL**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[IQNavigator VMS support team](https://www.beeline.com/iqn-product-support/).</span></span> <span data-ttu-id="accd2-193">Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="accd2-193">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="accd2-194">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="accd2-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="accd2-195">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="accd2-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="accd2-196">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="accd2-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="accd2-197">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="accd2-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="accd2-198">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="accd2-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="accd2-200">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="accd2-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="accd2-201">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="accd2-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="accd2-203">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="accd2-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="accd2-205">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="accd2-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="accd2-207">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="accd2-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="accd2-209">a.</span><span class="sxs-lookup"><span data-stu-id="accd2-209">a.</span></span> <span data-ttu-id="accd2-210">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="accd2-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="accd2-211">b.</span><span class="sxs-lookup"><span data-stu-id="accd2-211">b.</span></span> <span data-ttu-id="accd2-212">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="accd2-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="accd2-213">c.</span><span class="sxs-lookup"><span data-stu-id="accd2-213">c.</span></span> <span data-ttu-id="accd2-214">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="accd2-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="accd2-215">d.</span><span class="sxs-lookup"><span data-stu-id="accd2-215">d.</span></span> <span data-ttu-id="accd2-216">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="accd2-216">Click **Create**.</span></span>
 
### <a name="creating-a-iqnavigator-vms-test-user"></a><span data-ttu-id="accd2-217">Criando um usuário de teste do IQNavigator VMS</span><span class="sxs-lookup"><span data-stu-id="accd2-217">Creating a IQNavigator VMS test user</span></span>

<span data-ttu-id="accd2-218">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon IQNavigator VMs.</span><span class="sxs-lookup"><span data-stu-id="accd2-218">hello objective of this section is toocreate a user called Britta Simon in IQNavigator VMS.</span></span> <span data-ttu-id="accd2-219">Trabalhar com [equipe de suporte de VMS IQNavigator](https://www.beeline.com/iqn-product-support/) tooadd usuários Olá Olá conta IQNavigator VMS.</span><span class="sxs-lookup"><span data-stu-id="accd2-219">Work with  [IQNavigator VMS support team](https://www.beeline.com/iqn-product-support/) tooadd hello users in hello IQNavigator VMS account.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="accd2-220">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="accd2-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="accd2-221">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooIQNavigator VMS.</span><span class="sxs-lookup"><span data-stu-id="accd2-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIQNavigator VMS.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="accd2-223">**tooassign Britta Simon tooIQNavigator VMS, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="accd2-223">**tooassign Britta Simon tooIQNavigator VMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="accd2-224">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="accd2-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="accd2-226">Na lista de aplicativos hello, selecione **IQNavigator VMS**.</span><span class="sxs-lookup"><span data-stu-id="accd2-226">In hello applications list, select **IQNavigator VMS**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_app.png) 

3. <span data-ttu-id="accd2-228">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="accd2-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="accd2-230">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="accd2-230">Click **Add** button.</span></span> <span data-ttu-id="accd2-231">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="accd2-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="accd2-233">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="accd2-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="accd2-234">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="accd2-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="accd2-235">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="accd2-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="accd2-236">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="accd2-236">Testing single sign-on</span></span>

<span data-ttu-id="accd2-237">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="accd2-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="accd2-238">Quando você clica em Olá lado a lado no painel de acesso de saudação IQNavigator VMS, você deve obter tooyour automaticamente conectado no aplicativo IQNavigator VMS.</span><span class="sxs-lookup"><span data-stu-id="accd2-238">When you click hello IQNavigator VMS tile in hello Access Panel, you should get automatically signed-on tooyour IQNavigator VMS application.</span></span>
<span data-ttu-id="accd2-239">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="accd2-239">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="accd2-240">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="accd2-240">Additional resources</span></span>

* [<span data-ttu-id="accd2-241">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="accd2-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="accd2-242">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="accd2-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_203.png

