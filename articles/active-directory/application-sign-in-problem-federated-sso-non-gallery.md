---
title: "logon único aaaProblems entrar no aplicativo de galeria não tooa configurado para federado | Microsoft Docs"
description: "Diretrizes para problemas específicos hello, que você pode encontrar ao entrar no aplicativo tooan configurado para baseado no SAML federado logon único com o Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 1243456695c097f404a66fc89893efa2afdaaf22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooa-non-gallery-application-configured-for-federated-single-sign-on"></a><span data-ttu-id="539e9-103">Problemas para entrar no aplicativo de galeria não tooa configurado para logon único federado</span><span class="sxs-lookup"><span data-stu-id="539e9-103">Problems signing in tooa non-gallery application configured for federated single sign-on</span></span>

<span data-ttu-id="539e9-104">tootroubleshoot seu problema, você precisa de configuração de aplicativo hello tooverify no AD do Azure como segue:</span><span class="sxs-lookup"><span data-stu-id="539e9-104">tootroubleshoot your problem, you need tooverify hello application configuration in Azure AD as follow:</span></span>

-   <span data-ttu-id="539e9-105">Você tiver seguido todas as etapas de configuração de saudação para Olá aplicativo da Galeria de AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="539e9-105">You have followed all hello configuration steps for hello Azure AD gallery application.</span></span>

-   <span data-ttu-id="539e9-106">Olá identificador e URL de resposta configurado no AAD correspondem a elas valores esperados no aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="539e9-106">hello Identifier and Reply URL configured in AAD match they expected values in hello application</span></span>

-   <span data-ttu-id="539e9-107">Você atribuiu usuários toohello aplicativo</span><span class="sxs-lookup"><span data-stu-id="539e9-107">You have assigned users toohello application</span></span>

## <a name="application-not-found-in-directory"></a><span data-ttu-id="539e9-108">Aplicativo não encontrado no diretório</span><span class="sxs-lookup"><span data-stu-id="539e9-108">Application not found in directory</span></span>

<span data-ttu-id="539e9-109">*Erro AADSTS70001: O aplicativo com identificador 'https://contoso.com' não foi encontrado no diretório Olá*.</span><span class="sxs-lookup"><span data-stu-id="539e9-109">*Error AADSTS70001: Application with Identifier ‘https://contoso.com’ was not found in hello directory*.</span></span>

<span data-ttu-id="539e9-110">**Possível causa**</span><span class="sxs-lookup"><span data-stu-id="539e9-110">**Possible cause**</span></span>

<span data-ttu-id="539e9-111">atributo de emissor Olá envia de saudação aplicativo tooAzure que AD na solicitação SAML Olá não corresponde o valor de identificador de saudação configurado no aplicativo de saudação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="539e9-111">hello Issuer attribute sends from hello application tooAzure AD in hello SAML request doesn’t match hello Identifier value configured in hello application Azure AD.</span></span>

<span data-ttu-id="539e9-112">**Resolução**</span><span class="sxs-lookup"><span data-stu-id="539e9-112">**Resolution**</span></span>

<span data-ttu-id="539e9-113">Verifique se esse atributo de emissor Olá na solicitação SAML Olá correspondentes Olá valor de identificador configurado no AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="539e9-113">Ensure that hello Issuer attribute in hello SAML request it’s matching hello Identifier value configured in Azure AD:</span></span>

1.  <span data-ttu-id="539e9-114">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="539e9-114">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="539e9-115">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="539e9-115">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="539e9-116">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="539e9-116">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="539e9-117">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="539e9-117">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="539e9-118">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="539e9-118">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="539e9-119">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="539e9-119">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="539e9-120">Selecione aplicativo hello deseja tooconfigure-logon único.</span><span class="sxs-lookup"><span data-stu-id="539e9-120">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="539e9-121">Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="539e9-121">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="539e9-122"><span id="_Hlk477190042" class="anchor"></span>Vá muito**domínio e URLs** seção.</span><span class="sxs-lookup"><span data-stu-id="539e9-122"><span id="_Hlk477190042" class="anchor"></span>Go too**Domain and URLs** section.</span></span> <span data-ttu-id="539e9-123">Verifique se o valor no hello identificador de caixa de texto é compatível com o valor Olá Olá identificador valor exibido no erro Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="539e9-123">Verify that hello value in hello Identifier textbox is matching hello value for hello identifier value displayed in hello error.</span></span>

<span data-ttu-id="539e9-124">Depois que você atualizou o valor do identificador Olá no AD do Azure e sua correspondência Olá valor envia por aplicativo hello na solicitação SAML hello, você deve ser capaz de toosign no aplicativo toohello.</span><span class="sxs-lookup"><span data-stu-id="539e9-124">After you have updated hello Identifier value in Azure AD and it’s matching hello value sends by hello application in hello SAML request, you should be able toosign in toohello application.</span></span>

## <a name="hello-reply-address-does-not-match-hello-reply-addresses-configured-for-hello-application"></a><span data-ttu-id="539e9-125">endereço de resposta de saudação não coincide com os endereços de resposta de saudação configurados para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="539e9-125">hello reply address does not match hello reply addresses configured for hello application.</span></span> 

<span data-ttu-id="539e9-126">*Erro AADSTS50011: o endereço de resposta de saudação 'https://contoso.com' não coincide com os endereços de resposta de saudação configurados para o aplicativo hello*</span><span class="sxs-lookup"><span data-stu-id="539e9-126">*Error AADSTS50011: hello reply address ‘https://contoso.com’ does not match hello reply addresses configured for hello application*</span></span> 

<span data-ttu-id="539e9-127">**Possível causa**</span><span class="sxs-lookup"><span data-stu-id="539e9-127">**Possible cause**</span></span> 

<span data-ttu-id="539e9-128">Olá AssertionConsumerServiceURL valor na solicitação SAML Olá não coincide com o padrão configurado no AD do Azure ou valor de URL de resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="539e9-128">hello AssertionConsumerServiceURL value in hello SAML request doesn't match hello Reply URL value or pattern configured in Azure AD.</span></span> <span data-ttu-id="539e9-129">Olá AssertionConsumerServiceURL valor na solicitação SAML Olá é a URL de saudação consulte erro hello.</span><span class="sxs-lookup"><span data-stu-id="539e9-129">hello AssertionConsumerServiceURL value in hello SAML request is hello URL you see in hello error.</span></span> 

<span data-ttu-id="539e9-130">**Resolução**</span><span class="sxs-lookup"><span data-stu-id="539e9-130">**Resolution**</span></span> 

<span data-ttu-id="539e9-131">Verifique se esse valor de AssertionConsumerServiceURL Olá na solicitação SAML Olá sua correspondência Olá valor de URL de resposta configurado no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="539e9-131">Ensure that hello AssertionConsumerServiceURL value in hello SAML request it's matching hello Reply URL value configured in Azure AD.</span></span> 
 
1.  <span data-ttu-id="539e9-132">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="539e9-132">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span> 

2.  <span data-ttu-id="539e9-133">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="539e9-133">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span> 

3.  <span data-ttu-id="539e9-134">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="539e9-134">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span> 

4.  <span data-ttu-id="539e9-135">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="539e9-135">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span> 

5.  <span data-ttu-id="539e9-136">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="539e9-136">click **All Applications** tooview a list of all your applications.</span></span> 

  * <span data-ttu-id="539e9-137">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="539e9-137">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and       set hello **Show** option too**All Applications.**</span></span>
  
6.  <span data-ttu-id="539e9-138">Selecionar aplicativo hello deseja tooconfigure-logon único</span><span class="sxs-lookup"><span data-stu-id="539e9-138">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="539e9-139">Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="539e9-139">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="539e9-140">Vá muito**domínio e URLs** seção.</span><span class="sxs-lookup"><span data-stu-id="539e9-140">Go too**Domain and URLs** section.</span></span> <span data-ttu-id="539e9-141">Verifique ou atualize o valor de saudação na caixa de texto toomatch Olá AssertionConsumerServiceURL valor na solicitação SAML de saudação do hello URL de resposta.</span><span class="sxs-lookup"><span data-stu-id="539e9-141">Verify or update hello value in hello Reply URL textbox toomatch hello AssertionConsumerServiceURL value in hello SAML request.</span></span>

  * <span data-ttu-id="539e9-142">Se você não vir o texto da URL de resposta de saudação, selecione Olá **Mostrar configurações de URL avançadas** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="539e9-142">If you don't see hello Reply URL textbox, select hello **Show advanced URL settings** checkbox.</span></span> 

<span data-ttu-id="539e9-143">Depois que você atualizou o valor de URL de resposta Olá no AD do Azure e tem correspondência do valor de saudação envia por aplicativo hello em Olá solicitação SAML, você deve ser capaz de toosign no aplicativo toohello.</span><span class="sxs-lookup"><span data-stu-id="539e9-143">After you have updated hello Reply URL value in Azure AD and it’s matching hello value sends by hello application in hello SAML request, you should be able toosign in toohello application.</span></span>

## <a name="user-not-assigned-a-role"></a><span data-ttu-id="539e9-144">Usuário não atribuído a uma função</span><span class="sxs-lookup"><span data-stu-id="539e9-144">User not assigned a role</span></span>

<span data-ttu-id="539e9-145">*Erro AADSTS50105: Olá usuário conectado 'brian@contoso.com' não está atribuído a função tooa para o aplicativo hello*</span><span class="sxs-lookup"><span data-stu-id="539e9-145">*Error AADSTS50105: hello signed in user 'brian@contoso.com' is not assigned tooa role for hello application*</span></span>

<span data-ttu-id="539e9-146">**Possível causa**</span><span class="sxs-lookup"><span data-stu-id="539e9-146">**Possible cause**</span></span>

<span data-ttu-id="539e9-147">saudação de usuário não recebeu acesso toohello aplicativo no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="539e9-147">hello user has not been granted access toohello application in Azure AD.</span></span>

<span data-ttu-id="539e9-148">**Resolução**</span><span class="sxs-lookup"><span data-stu-id="539e9-148">**Resolution**</span></span>

<span data-ttu-id="539e9-149">tooassign um ou mais aplicativos de tooan usuários diretamente, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="539e9-149">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="539e9-150">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="539e9-150">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="539e9-151">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="539e9-151">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="539e9-152">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="539e9-152">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="539e9-153">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="539e9-153">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="539e9-154">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="539e9-154">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="539e9-155">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="539e9-155">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="539e9-156">Selecione o aplicativo hello deseja tooassign uma lista de saudação do usuário toofrom.</span><span class="sxs-lookup"><span data-stu-id="539e9-156">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="539e9-157">Depois que o aplicativo hello carrega, clique em **usuários e grupos** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="539e9-157">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="539e9-158">Clique Olá **adicionar** botão na parte superior Olá **usuários e grupos** Olá de tooopen lista **Adicionar atribuição** folha.</span><span class="sxs-lookup"><span data-stu-id="539e9-158">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="539e9-159">Clique em Olá **usuários e grupos** seletor de saudação **Adicionar atribuição** folha.</span><span class="sxs-lookup"><span data-stu-id="539e9-159">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="539e9-160">Tipo de saudação **nome completo** ou **endereço de email** do usuário Olá que lhe interessam atribuindo em Olá **pesquisar por nome ou endereço de email** caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="539e9-160">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="539e9-161">Passe o mouse sobre Olá **usuário** em Olá lista tooreveal um **caixa de seleção**.</span><span class="sxs-lookup"><span data-stu-id="539e9-161">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="539e9-162">Clique em tooadd de foto ou logotipo de perfil do Olá caixa de seleção próxima toohello usuário seu usuário toohello **selecionados** lista.</span><span class="sxs-lookup"><span data-stu-id="539e9-162">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="539e9-163">**Opcional:** se você gostaria que muito**adicionar mais de um usuário**, tipo em outro **nome completo** ou **endereço de email** em Olá **pesquisar por nome endereço de email ou** caixa de pesquisa e, em seguida, clique em tooadd de caixa de seleção Olá esse usuário toohello **selecionados** lista.</span><span class="sxs-lookup"><span data-stu-id="539e9-163">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="539e9-164">Quando você terminar de selecionar usuários, clique em Olá **selecione** botão tooadd-los toohello lista de usuários e grupos toobe atribuído toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="539e9-164">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="539e9-165">**Opcional:** clique Olá **Selecionar função** seletor de saudação **Adicionar atribuição** folha tooselect uma função tooassign toohello usuários selecionados.</span><span class="sxs-lookup"><span data-stu-id="539e9-165">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="539e9-166">Clique em Olá **atribuir** botão tooassign Olá aplicativo toohello selecionado de usuários.</span><span class="sxs-lookup"><span data-stu-id="539e9-166">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="539e9-167">Após um curto período de tempo, usuários de saudação selecionado ser capaz de toolaunch esses aplicativos usando Olá métodos descritos na seção de descrição de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="539e9-167">After a short period of time, hello users you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span>

## <a name="not-a-valid-saml-request"></a><span data-ttu-id="539e9-168">Não é uma solicitação SAML válida</span><span class="sxs-lookup"><span data-stu-id="539e9-168">Not a valid SAML Request</span></span>

<span data-ttu-id="539e9-169">*Erro AADSTS75005: solicitação de Olá não é uma mensagem de protocolo Saml2 válida.*</span><span class="sxs-lookup"><span data-stu-id="539e9-169">*Error AADSTS75005: hello request is not a valid Saml2 protocol message.*</span></span>

<span data-ttu-id="539e9-170">**Possível causa**</span><span class="sxs-lookup"><span data-stu-id="539e9-170">**Possible cause**</span></span>

<span data-ttu-id="539e9-171">AD do Azure não oferece suporte a saudação SAML solicitação enviada pelo aplicativo hello para logon único.</span><span class="sxs-lookup"><span data-stu-id="539e9-171">Azure AD doesn’t support hello SAML Request sent by hello application for Single Sign-on.</span></span> <span data-ttu-id="539e9-172">Alguns problemas comuns são:</span><span class="sxs-lookup"><span data-stu-id="539e9-172">Some common issues are:</span></span>

-   <span data-ttu-id="539e9-173">Faltando campos obrigatórios na solicitação SAML Olá</span><span class="sxs-lookup"><span data-stu-id="539e9-173">Missing required fields in hello SAML request</span></span>

-   <span data-ttu-id="539e9-174">Método codificado de solicitação SAML</span><span class="sxs-lookup"><span data-stu-id="539e9-174">SAML request encoded method</span></span>

<span data-ttu-id="539e9-175">**Resolução**</span><span class="sxs-lookup"><span data-stu-id="539e9-175">**Resolution**</span></span>

1.  <span data-ttu-id="539e9-176">Capturar solicitação SAML.</span><span class="sxs-lookup"><span data-stu-id="539e9-176">Capture SAML request.</span></span> <span data-ttu-id="539e9-177">Siga o tutorial Olá [como toodebug baseado no SAML único logon tooapplications no AD do Azure](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) toolearn como solicitar toocapture Olá SAML.</span><span class="sxs-lookup"><span data-stu-id="539e9-177">follow hello tutorial on [how toodebug SAML-based single sign-on tooapplications in Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) toolearn how toocapture hello SAML request.</span></span>

2.  <span data-ttu-id="539e9-178">Entre em contato com o fornecedor do aplicativo hello e compartilhamento:</span><span class="sxs-lookup"><span data-stu-id="539e9-178">Contact hello application vendor and share:</span></span>

    -   <span data-ttu-id="539e9-179">Solicitação SAML</span><span class="sxs-lookup"><span data-stu-id="539e9-179">SAML request</span></span>

    -   [<span data-ttu-id="539e9-180">Requisitos de protocolo SAML de logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="539e9-180">Azure AD Single Sign-on SAML protocol requirements</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)

<span data-ttu-id="539e9-181">Eles devem validar suporte a implementação do Azure AD SAML Olá para logon único.</span><span class="sxs-lookup"><span data-stu-id="539e9-181">They should validate they support hello Azure AD SAML implementation for Single Sign-on.</span></span>

## <a name="no-resource-in-requiredresourceaccess-list"></a><span data-ttu-id="539e9-182">Nenhum recurso na lista requiredResourceAccess</span><span class="sxs-lookup"><span data-stu-id="539e9-182">No resource in requiredResourceAccess list</span></span>

<span data-ttu-id="539e9-183">*Erro AADSTS65005: o aplicativo de cliente de saudação solicitou acesso tooresource ' 00000002-0000-0000-c000-000000000000'. A solicitação falhou porque o cliente Olá não especificou esse recurso em sua lista de requiredResourceAccess*.</span><span class="sxs-lookup"><span data-stu-id="539e9-183">*Error AADSTS65005: hello client application has requested access tooresource '00000002-0000-0000-c000-000000000000'. This request has failed because hello client has not specified this resource in its requiredResourceAccess list*.</span></span>

<span data-ttu-id="539e9-184">**Possível causa**</span><span class="sxs-lookup"><span data-stu-id="539e9-184">**Possible cause**</span></span>

<span data-ttu-id="539e9-185">objeto de aplicativo Hello está corrompido.</span><span class="sxs-lookup"><span data-stu-id="539e9-185">hello application object is corrupted.</span></span>

<span data-ttu-id="539e9-186">**Resolução**</span><span class="sxs-lookup"><span data-stu-id="539e9-186">**Resolution**</span></span>

<span data-ttu-id="539e9-187">problema de saudação toosolve, remover o aplicativo de saudação do diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="539e9-187">toosolve hello problem, remove hello application from hello directory.</span></span> <span data-ttu-id="539e9-188">Em seguida, adicione e reconfigurar o aplicativo hello, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="539e9-188">Then, add and reconfigure hello application, follow hello steps below:</span></span>

1.  <span data-ttu-id="539e9-189">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="539e9-189">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="539e9-190">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="539e9-190">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="539e9-191">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="539e9-191">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="539e9-192">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="539e9-192">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="539e9-193">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="539e9-193">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="539e9-194">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="539e9-194">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="539e9-195">Selecione aplicativo hello deseja tooconfigure-logon único.</span><span class="sxs-lookup"><span data-stu-id="539e9-195">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="539e9-196">Clique em **excluir** na parte superior esquerda Olá da aplicativo hello **visão geral** folha.</span><span class="sxs-lookup"><span data-stu-id="539e9-196">Click **Delete** at hello top-left of hello application **Overview** blade.</span></span>

8.  <span data-ttu-id="539e9-197">Atualizar o AD do Azure e adicionar o aplicativo hello da Galeria do AD do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="539e9-197">Refresh Azure AD and Add hello application from hello Azure AD gallery.</span></span> <span data-ttu-id="539e9-198">Em seguida, Configure o aplicativo hello novamente.</span><span class="sxs-lookup"><span data-stu-id="539e9-198">Then, Configure hello application again.</span></span>

<span data-ttu-id="539e9-199">Depois de reconfigurar o aplicativo hello, você deve ser capaz de toosign no aplicativo toohello.</span><span class="sxs-lookup"><span data-stu-id="539e9-199">After reconfiguring hello application, you should be able toosign in toohello application.</span></span>

## <a name="certificate-or-key-not-configured"></a><span data-ttu-id="539e9-200">Chave ou certificado não configurado</span><span class="sxs-lookup"><span data-stu-id="539e9-200">Certificate or key not configured</span></span>

<span data-ttu-id="539e9-201">Erro AADSTS50003: nenhuma chave de assinatura configurada.</span><span class="sxs-lookup"><span data-stu-id="539e9-201">Error AADSTS50003: No signing key configured.</span></span>

<span data-ttu-id="539e9-202">**Possível causa**</span><span class="sxs-lookup"><span data-stu-id="539e9-202">**Possible cause**</span></span>

<span data-ttu-id="539e9-203">objeto de aplicativo Hello está corrompido e o AD do Azure não reconhece o certificado de saudação configurado para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="539e9-203">hello application object is corrupted and Azure AD doesn’t recognize hello certificate configured for hello application.</span></span>

<span data-ttu-id="539e9-204">**Resolução**</span><span class="sxs-lookup"><span data-stu-id="539e9-204">**Resolution**</span></span>

<span data-ttu-id="539e9-205">toodelete e criar um novo certificado, execute as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="539e9-205">toodelete and create a new certificate, follow hello steps below:</span></span>

1.  <span data-ttu-id="539e9-206">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="539e9-206">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="539e9-207">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="539e9-207">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="539e9-208">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="539e9-208">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="539e9-209">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="539e9-209">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="539e9-210">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="539e9-210">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="539e9-211">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="539e9-211">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="539e9-212">Selecione aplicativo hello deseja tooconfigure-logon único.</span><span class="sxs-lookup"><span data-stu-id="539e9-212">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="539e9-213">Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="539e9-213">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="539e9-214">Clique em **criar novo certificado** em Olá **SAML certificado de assinatura** seção.</span><span class="sxs-lookup"><span data-stu-id="539e9-214">click **Create new certificate** under hello **SAML signing Certificate** section.</span></span>

9.  <span data-ttu-id="539e9-215">Selecione a data de validade.</span><span class="sxs-lookup"><span data-stu-id="539e9-215">Select Expiration date.</span></span> <span data-ttu-id="539e9-216">Em seguida, clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="539e9-216">Then, click **Save.**</span></span>

10. <span data-ttu-id="539e9-217">Verificar **ativar o novo certificado** certificado do active toooverride hello.</span><span class="sxs-lookup"><span data-stu-id="539e9-217">Check **Make new certificate active** toooverride hello active certificate.</span></span> <span data-ttu-id="539e9-218">Em seguida, clique em **salvar** na parte superior de saudação da folha de saudação e aceitar o certificado de substituição tooactivate hello.</span><span class="sxs-lookup"><span data-stu-id="539e9-218">Then, click **Save** at hello top of hello blade and accept tooactivate hello rollover certificate.</span></span>

11. <span data-ttu-id="539e9-219">Em Olá **o certificado de autenticação SAML** seção, clique em **remover** tooremove Olá **não utilizado** certificado.</span><span class="sxs-lookup"><span data-stu-id="539e9-219">Under hello **SAML Signing Certificate** section, click **remove** tooremove hello **Unused** certificate.</span></span>

## <a name="problem-when-customizing-hello-saml-claims-sent-tooan-application"></a><span data-ttu-id="539e9-220">Problema ao personalizar Olá SAML declarações enviadas tooan aplicativo</span><span class="sxs-lookup"><span data-stu-id="539e9-220">Problem when customizing hello SAML claims sent tooan application</span></span>

<span data-ttu-id="539e9-221">toolearn como declarações de atributo toocustomize Olá SAML enviado tooyour aplicativo, consulte [declarações mapeamento no Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="539e9-221">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="539e9-222">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="539e9-222">Next steps</span></span>
[<span data-ttu-id="539e9-223">Requisitos de protocolo SAML de logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="539e9-223">Azure AD Single Sign-on SAML protocol requirements</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)
