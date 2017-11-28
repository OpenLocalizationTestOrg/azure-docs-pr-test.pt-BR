---
title: "Tutorial: integração do Azure Active Directory ao Coupa | Microsoft Docs"
description: "Saiba como toouse Coupa com o Active Directory do Azure tooenable única de logon, o provisionamento automatizado e muito mais!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 47f27746-9057-4b9c-991e-3abf77710f73
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 87e98573718d27d408c886466a374a987f58faa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-coupa"></a><span data-ttu-id="d548b-103">Tutorial: integração do Active Directory do Azure ao Coupa</span><span class="sxs-lookup"><span data-stu-id="d548b-103">Tutorial: Azure Active Directory integration with Coupa</span></span>
<span data-ttu-id="d548b-104">Olá objetivo deste tutorial é tooshow integração de saudação do Azure e do Coupa.</span><span class="sxs-lookup"><span data-stu-id="d548b-104">hello objective of this tutorial is tooshow hello integration of Azure and Coupa.</span></span>  
<span data-ttu-id="d548b-105">cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="d548b-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="d548b-106">Uma assinatura válida do Azure</span><span class="sxs-lookup"><span data-stu-id="d548b-106">A valid Azure subscription</span></span>
* <span data-ttu-id="d548b-107">Uma assinatura habilitada para SSO (logon único) do Coupa</span><span class="sxs-lookup"><span data-stu-id="d548b-107">A Coupa single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="d548b-108">Após concluir este tutorial, os usuários de saudação do Azure AD atribuídos tooCoupa será toosingle capaz de usar o logon no aplicativo hello usando Olá [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d548b-108">After completing this tutorial, hello Azure AD users you have assigned tooCoupa will be able toosingle sign into hello application using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="d548b-109">cenário de saudação descrito neste tutorial consiste em Olá blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="d548b-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

* <span data-ttu-id="d548b-110">Habilitando a integração de aplicativos Olá para o Coupa</span><span class="sxs-lookup"><span data-stu-id="d548b-110">Enabling hello application integration for Coupa</span></span>
* <span data-ttu-id="d548b-111">Configurando o logon único</span><span class="sxs-lookup"><span data-stu-id="d548b-111">Configuring single sign-on</span></span>
* <span data-ttu-id="d548b-112">Configurando o provisionamento de usuários</span><span class="sxs-lookup"><span data-stu-id="d548b-112">Configuring user provisioning</span></span>
* <span data-ttu-id="d548b-113">Atribuindo usuários</span><span class="sxs-lookup"><span data-stu-id="d548b-113">Assigning users</span></span>

<span data-ttu-id="d548b-114">![Cenário](./media/active-directory-saas-coupa-tutorial/IC791897.png "Cenário")</span><span class="sxs-lookup"><span data-stu-id="d548b-114">![Scenario](./media/active-directory-saas-coupa-tutorial/IC791897.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-coupa"></a><span data-ttu-id="d548b-115">Habilitar a integração de aplicativos Olá para o Coupa</span><span class="sxs-lookup"><span data-stu-id="d548b-115">Enable hello application integration for Coupa</span></span>
<span data-ttu-id="d548b-116">Olá objetivo desta seção é toooutline como integração de aplicativos tooenable Olá para o Coupa.</span><span class="sxs-lookup"><span data-stu-id="d548b-116">hello objective of this section is toooutline how tooenable hello application integration for Coupa.</span></span>

<span data-ttu-id="d548b-117">**integração do aplicativo hello tooenable para o Coupa, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d548b-117">**tooenable hello application integration for Coupa, perform hello following steps:**</span></span>

1. <span data-ttu-id="d548b-118">No hello portal clássico do Azure, no painel de navegação esquerdo hello, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d548b-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="d548b-119">![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="d548b-119">![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="d548b-120">De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.</span><span class="sxs-lookup"><span data-stu-id="d548b-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="d548b-121">Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="d548b-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="d548b-122">![Aplicativos](./media/active-directory-saas-coupa-tutorial/IC700994.png "Aplicativos")</span><span class="sxs-lookup"><span data-stu-id="d548b-122">![Applications](./media/active-directory-saas-coupa-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="d548b-123">Clique em **adicionar** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="d548b-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="d548b-124">![Adicionar aplicativo](./media/active-directory-saas-coupa-tutorial/IC749321.png "Adicionar aplicativo")</span><span class="sxs-lookup"><span data-stu-id="d548b-124">![Add application](./media/active-directory-saas-coupa-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="d548b-125">Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo da Galeria Olá**.</span><span class="sxs-lookup"><span data-stu-id="d548b-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="d548b-126">![Adicionar um aplicativo da galeria](./media/active-directory-saas-coupa-tutorial/IC749322.png "Adicionar um aplicativo da galeria")</span><span class="sxs-lookup"><span data-stu-id="d548b-126">![Add an application from gallerry](./media/active-directory-saas-coupa-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="d548b-127">Em Olá **caixa de pesquisa**, tipo **Coupa**.</span><span class="sxs-lookup"><span data-stu-id="d548b-127">In hello **search box**, type **Coupa**.</span></span>
   
   <span data-ttu-id="d548b-128">![Galeria de Aplicativos](./media/active-directory-saas-coupa-tutorial/IC791898.png "Galeria de Aplicativos")</span><span class="sxs-lookup"><span data-stu-id="d548b-128">![Application Gallery](./media/active-directory-saas-coupa-tutorial/IC791898.png "Application Gallery")</span></span>
7. <span data-ttu-id="d548b-129">No painel de resultados de saudação, selecione **Coupa**e, em seguida, clique em **concluir** aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="d548b-129">In hello results pane, select **Coupa**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="d548b-130">![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span><span class="sxs-lookup"><span data-stu-id="d548b-130">![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="d548b-131">Configurar o logon único</span><span class="sxs-lookup"><span data-stu-id="d548b-131">Configure single sign-on</span></span>

<span data-ttu-id="d548b-132">Olá objetivo desta seção é toooutline como tooenable usuários tooauthenticate tooCoupa com suas contas no AD do Azure usando federação com base no protocolo SAML de saudação.</span><span class="sxs-lookup"><span data-stu-id="d548b-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooCoupa with their account in Azure AD using federation based on hello SAML protocol.</span></span>  

<span data-ttu-id="d548b-133">Configurar logon único para o Coupa exige que você tooretrieve um valor de impressão digital de um certificado.</span><span class="sxs-lookup"><span data-stu-id="d548b-133">Configuring single sign-on for Coupa requires you tooretrieve a thumbprint value from a certificate.</span></span> <span data-ttu-id="d548b-134">Se você não estiver familiarizado com esse procedimento, consulte [como tooretrieve o valor de impressão digital do certificado](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="d548b-134">If you are not familiar with this procedure, see [How tooretrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>

<span data-ttu-id="d548b-135">**tooconfigure o logon único, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d548b-135">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="d548b-136">Faça logon no tooyour site da empresa Coupa como administrador.</span><span class="sxs-lookup"><span data-stu-id="d548b-136">Sign on tooyour Coupa company site as an administrator.</span></span>
2. <span data-ttu-id="d548b-137">Vá muito**instalação \> controle de segurança**.</span><span class="sxs-lookup"><span data-stu-id="d548b-137">Go too**Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="d548b-138">![Controles de Segurança](./media/active-directory-saas-coupa-tutorial/IC791900.png "Controles de Segurança")</span><span class="sxs-lookup"><span data-stu-id="d548b-138">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
3. <span data-ttu-id="d548b-139">Clique em computador toodownload Olá Coupa metadados arquivo tooyour, **baixar e importar metadados de SP**.</span><span class="sxs-lookup"><span data-stu-id="d548b-139">toodownload hello Coupa metadata file tooyour computer, click **Download and import SP metadata**.</span></span>
   
   <span data-ttu-id="d548b-140">![Metadados SP do Coupa](./media/active-directory-saas-coupa-tutorial/IC791901.png "Metadados SP do Coupa")</span><span class="sxs-lookup"><span data-stu-id="d548b-140">![Coupa SP metadata](./media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa SP metadata")</span></span>
4. <span data-ttu-id="d548b-141">Em uma janela de navegador diferente, faça logon no toohello portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="d548b-141">In a different browser window, sign on toohello Azure classic portal.</span></span>
5. <span data-ttu-id="d548b-142">Em Olá **Coupa** página de integração de aplicativos, clique em **configurar logon único** tooopen Olá **configurar logon único** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d548b-142">On hello **Coupa** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="d548b-143">![Configurar Logon Único](./media/active-directory-saas-coupa-tutorial/IC791902.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="d548b-143">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791902.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="d548b-144">Em Olá **como você gostaria usuários toosign em tooCoupa** página, selecione **AD do Microsoft Azure Single Sign-On**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="d548b-144">On hello **How would you like users toosign on tooCoupa** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="d548b-145">![Configurar Logon Único](./media/active-directory-saas-coupa-tutorial/IC791903.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="d548b-145">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791903.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="d548b-146">Em Olá **configurar URL do aplicativo** página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d548b-146">On hello **Configure App URL** page, perform hello following steps:</span></span>
   
   <span data-ttu-id="d548b-147">![Configurar URL do Aplicativo](./media/active-directory-saas-coupa-tutorial/IC791904.png "Configurar URL do Aplicativo")</span><span class="sxs-lookup"><span data-stu-id="d548b-147">![Configure App URL](./media/active-directory-saas-coupa-tutorial/IC791904.png "Configure App URL")</span></span>   
   1. <span data-ttu-id="d548b-148">Em Olá **URL de logon** caixa de texto, digite a URL usada pelo seu toosign usuários em tooyour aplicativo Coupa (por exemplo: "*http://company.Coupa.com*").</span><span class="sxs-lookup"><span data-stu-id="d548b-148">In hello **Sign On URL** textbox, type URL used by your users toosign on tooyour Coupa application (e.g.: “*http://company.Coupa.com*”).</span></span>
   2. <span data-ttu-id="d548b-149">Abra o arquivo de metadados do Coupa baixado e copie Olá **índice/URL AssertionConsumerService**.</span><span class="sxs-lookup"><span data-stu-id="d548b-149">Open your downloaded Coupa metadata file, and then copy hello **AssertionConsumerService index/URL**.</span></span>
   3. <span data-ttu-id="d548b-150">Em Olá **URL de resposta do Coupa** caixa de texto, colar Olá **índice/URL AssertionConsumerService** valor.</span><span class="sxs-lookup"><span data-stu-id="d548b-150">In hello **Coupa Reply URL** textbox, paste hello **AssertionConsumerService index/URL** value.</span></span>
   4. <span data-ttu-id="d548b-151">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="d548b-151">Click **Next**.</span></span>
8. <span data-ttu-id="d548b-152">Em Olá **configurar logon único no Coupa** página, toodownload o arquivo de metadados, clique em **baixar metadados**e, em seguida, salve o arquivo de saudação localmente no seu computador.</span><span class="sxs-lookup"><span data-stu-id="d548b-152">On hello **Configure single sign-on at Coupa** page, toodownload your metadata file, click **Download metadata**, and then save hello file locally on your computer.</span></span>
   
   <span data-ttu-id="d548b-153">![Configurar Logon Único](./media/active-directory-saas-coupa-tutorial/IC791905.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="d548b-153">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791905.png "Configure Single Sign-On")</span></span>
9. <span data-ttu-id="d548b-154">No site da empresa Olá Coupa, vá muito**instalação \> controle de segurança**.</span><span class="sxs-lookup"><span data-stu-id="d548b-154">On hello Coupa company site, go too**Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="d548b-155">![Controles de Segurança](./media/active-directory-saas-coupa-tutorial/IC791900.png "Controles de Segurança")</span><span class="sxs-lookup"><span data-stu-id="d548b-155">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
10. <span data-ttu-id="d548b-156">Em Olá **efetuar login usando credenciais de Coupa** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d548b-156">In hello **Log in using Coupa credentials** section, perform hello following steps:</span></span>  

   <span data-ttu-id="d548b-157">![Logon usando as credenciais do Coupa](./media/active-directory-saas-coupa-tutorial/IC791906.png "Logon usando as credenciais do Coupa")</span><span class="sxs-lookup"><span data-stu-id="d548b-157">![Log in using Coupa credentials](./media/active-directory-saas-coupa-tutorial/IC791906.png "Log in using Coupa credentials")</span></span> 
   1. <span data-ttu-id="d548b-158">Selecione **Fazer logon usando o SAML**.</span><span class="sxs-lookup"><span data-stu-id="d548b-158">Select **Log in using SAML**.</span></span>
   2. <span data-ttu-id="d548b-159">Clique em **procurar** tooupload seu arquivo de metadados baixado ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="d548b-159">Click **Browse** tooupload your downloaded Azure Active metadata file.</span></span>
   3. <span data-ttu-id="d548b-160">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="d548b-160">Click **Save**.</span></span>
11. <span data-ttu-id="d548b-161">Em Olá portal clássico do Azure, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **concluir** tooclose Olá **configurar logon único** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d548b-161">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
    
   <span data-ttu-id="d548b-162">![Configurar Logon Único](./media/active-directory-saas-coupa-tutorial/IC791907.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="d548b-162">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791907.png "Configure Single Sign-On")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="d548b-163">Configurar provisionamento do usuário</span><span class="sxs-lookup"><span data-stu-id="d548b-163">Configure user provisioning</span></span>

<span data-ttu-id="d548b-164">Ordem tooenable AD do Azure usuários toolog no Coupa, eles devem ser provisionados no Coupa.</span><span class="sxs-lookup"><span data-stu-id="d548b-164">In order tooenable Azure AD users toolog into Coupa, they must be provisioned into Coupa.</span></span>  

* <span data-ttu-id="d548b-165">No caso de saudação do Coupa, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="d548b-165">In hello case of Coupa, provisioning is a manual task.</span></span>

<span data-ttu-id="d548b-166">**tooconfigure provisionamento de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d548b-166">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="d548b-167">Faça logon no tooyour **Coupa** site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="d548b-167">Log in tooyour **Coupa** company site as administrator.</span></span>
2. <span data-ttu-id="d548b-168">No menu de saudação na parte superior de saudação, clique em **instalação**e, em seguida, clique em **usuários**.</span><span class="sxs-lookup"><span data-stu-id="d548b-168">In hello menu on hello top, click **Setup**, and then click **Users**.</span></span>
   
   <span data-ttu-id="d548b-169">![Usuários](./media/active-directory-saas-coupa-tutorial/IC791908.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="d548b-169">![Users](./media/active-directory-saas-coupa-tutorial/IC791908.png "Users")</span></span>
3. <span data-ttu-id="d548b-170">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d548b-170">Click **Create**.</span></span>
   
   <span data-ttu-id="d548b-171">![Criar Usuários](./media/active-directory-saas-coupa-tutorial/IC791909.png "Criar Usuários")</span><span class="sxs-lookup"><span data-stu-id="d548b-171">![Create Users](./media/active-directory-saas-coupa-tutorial/IC791909.png "Create Users")</span></span>
4. <span data-ttu-id="d548b-172">Em Olá **usuário criar** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d548b-172">In hello **User Create** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="d548b-173">![Detalhes do Usuário](./media/active-directory-saas-coupa-tutorial/IC791910.png "Detalhes do Usuário")</span><span class="sxs-lookup"><span data-stu-id="d548b-173">![User Details](./media/active-directory-saas-coupa-tutorial/IC791910.png "User Details")</span></span>
   
   1. <span data-ttu-id="d548b-174">Saudação de tipo **Login**, **nome**, **Sobrenome**, **ID de logon único**, **Email** atributos de um conta válida do Active Directory do Azure que você deseja tooprovision em Olá relacionados caixas de texto.</span><span class="sxs-lookup"><span data-stu-id="d548b-174">Type hello **Login**, **First name**, **Last Name**, **Single Sign-On ID**, **Email** attributes of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>
   2. <span data-ttu-id="d548b-175">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d548b-175">Click **Create**.</span></span>   
   >[!NOTE]
   ><span data-ttu-id="d548b-176">proprietário de conta do Active Directory do Azure Olá receberá um email com uma conta de saudação do link tooconfirm antes de se tornar ativa.</span><span class="sxs-lookup"><span data-stu-id="d548b-176">hello Azure Active Directory account holder will get an email with a link tooconfirm hello account before it becomes active.</span></span> 
   > 

>[!NOTE]
><span data-ttu-id="d548b-177">Você pode usar qualquer ferramenta de criação outros Coupa usuário conta ou APIs fornecidas pelo Coupa tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="d548b-177">You can use any other Coupa user account creation tools or APIs provided by Coupa tooprovision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="d548b-178">Atribuir usuários</span><span class="sxs-lookup"><span data-stu-id="d548b-178">Assign users</span></span>
<span data-ttu-id="d548b-179">tootest sua configuração, você precisa toogrant usuários de saudação do AD do Azure que você deseja tooallow usando seu tooit de acesso do aplicativo, atribuindo a eles.</span><span class="sxs-lookup"><span data-stu-id="d548b-179">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="d548b-180">**tooassign usuários tooCoupa, executar Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d548b-180">**tooassign users tooCoupa, perform hello following steps:**</span></span>

1. <span data-ttu-id="d548b-181">No hello portal clássico do Azure, crie uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="d548b-181">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="d548b-182">Em hello * * Coupa * * página de integração de aplicativos, clique em **atribuir usuários**.</span><span class="sxs-lookup"><span data-stu-id="d548b-182">On hello **Coupa **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="d548b-183">![Atribuir Usuários](./media/active-directory-saas-coupa-tutorial/IC791911.png "Atribuir Usuários")</span><span class="sxs-lookup"><span data-stu-id="d548b-183">![Assign Users](./media/active-directory-saas-coupa-tutorial/IC791911.png "Assign Users")</span></span>
3. <span data-ttu-id="d548b-184">Selecione seu usuário de teste, clique em **atribuir**e, em seguida, clique em **Sim** tooconfirm sua atribuição.</span><span class="sxs-lookup"><span data-stu-id="d548b-184">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="d548b-185">![Sim](./media/active-directory-saas-coupa-tutorial/IC767830.png "Sim")</span><span class="sxs-lookup"><span data-stu-id="d548b-185">![Yes](./media/active-directory-saas-coupa-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="d548b-186">Se você quiser tootest suas configurações de logon único, abra Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="d548b-186">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="d548b-187">Para obter mais detalhes sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d548b-187">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

