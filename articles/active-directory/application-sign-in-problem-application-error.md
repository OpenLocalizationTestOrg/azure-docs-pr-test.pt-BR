---
title: "aaaError na página do aplicativo depois de entrar no | Microsoft Docs"
description: "Como tooresolve problemas com o Azure AD de conexão ao próprio aplicativo hello emite um erro"
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
ms.openlocfilehash: 317b6f8e6417520ead80ae4e26c591ba6b134683
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="error-on-an-applications-page-after-signing-in"></a><span data-ttu-id="822e0-103">Erro em uma página de aplicativo após a entrada</span><span class="sxs-lookup"><span data-stu-id="822e0-103">Error on an application's page after signing in</span></span>

<span data-ttu-id="822e0-104">Nesse cenário, AD do Azure tem assinado usuário hello, mas aplicativo hello está exibindo um erro não permitindo Olá usuário toosuccessfully término hello entrada no fluxo.</span><span class="sxs-lookup"><span data-stu-id="822e0-104">In this scenario, Azure AD has signed hello user in, but hello application is displaying an error not allowing hello user toosuccessfully finish hello sign in flow.</span></span> <span data-ttu-id="822e0-105">Nesse cenário, o aplicativo hello não está aceitando problema de resposta de saudação pelo AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="822e0-105">In this scenario, hello application is not accepting hello response issue by Azure AD.</span></span>

<span data-ttu-id="822e0-106">Há alguns possíveis motivos por que o aplicativo hello não aceitou resposta de saudação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="822e0-106">There are some possible reasons why hello application didn’t accept hello response from Azure AD.</span></span> <span data-ttu-id="822e0-107">Se Olá erro no aplicativo hello tooknow limpar suficiente o que está faltando na resposta Olá, então:</span><span class="sxs-lookup"><span data-stu-id="822e0-107">If hello error in hello application is not clear enough tooknow what is missing in hello response, then:</span></span>

-   <span data-ttu-id="822e0-108">Se aplicativo hello Galeria de saudação do AD do Azure, verifique se você tiver seguido todas as etapas de saudação artigo Olá [como toodebug baseado no SAML único logon tooapplications no Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).</span><span class="sxs-lookup"><span data-stu-id="822e0-108">If hello application is hello Azure AD Gallery, verify you have followed all hello steps in hello article [How toodebug SAML-based single sign-on tooapplications in Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).</span></span>

-   <span data-ttu-id="822e0-109">Usar uma ferramenta como [Fiddler](http://www.telerik.com/fiddler) toocapture SAML de solicitação, resposta SAML e o token SAML.</span><span class="sxs-lookup"><span data-stu-id="822e0-109">Use a tool like [Fiddler](http://www.telerik.com/fiddler) toocapture SAML request, SAML response and SAML token.</span></span>

-   <span data-ttu-id="822e0-110">Compartilhe resposta SAML Olá com tooknow de fornecedor do aplicativo hello, o que está faltando.</span><span class="sxs-lookup"><span data-stu-id="822e0-110">Share hello SAML response with hello application vendor tooknow what is missing.</span></span>

## <a name="missing-attributes-in-hello-saml-response"></a><span data-ttu-id="822e0-111">Atributos ausentes em Olá resposta SAML</span><span class="sxs-lookup"><span data-stu-id="822e0-111">Missing attributes in hello SAML response</span></span>

<span data-ttu-id="822e0-112">tooadd um atributo em toobe de configuração do AD do Azure Olá enviado em resposta a saudação do AD do Azure, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="822e0-112">tooadd an attribute in hello Azure AD configuration toobe sent in hello Azure AD response, follow hello steps below:</span></span>

1.  <span data-ttu-id="822e0-113">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="822e0-113">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="822e0-114">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="822e0-114">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="822e0-115">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="822e0-115">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="822e0-116">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="822e0-116">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="822e0-117">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="822e0-117">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="822e0-118">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="822e0-118">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="822e0-119">Selecione aplicativo hello deseja tooconfigure-logon único.</span><span class="sxs-lookup"><span data-stu-id="822e0-119">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="822e0-120">Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="822e0-120">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="822e0-121">Clique em **exibir e editar os atributos de todos os outros usuários sob** Olá **atributos de usuário** Olá de tooedit seção atributos toobe enviado toohello aplicativo no token SAML hello quando o usuário entrar.</span><span class="sxs-lookup"><span data-stu-id="822e0-121">click **View and edit all other user attributes under** hello **User Attributes** section tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="822e0-122">um atributo de tooadd:</span><span class="sxs-lookup"><span data-stu-id="822e0-122">tooadd an attribute:</span></span>

   * <span data-ttu-id="822e0-123">clique em **Adicionar atributo**.</span><span class="sxs-lookup"><span data-stu-id="822e0-123">click **Add attribute**.</span></span> <span data-ttu-id="822e0-124">Digite hello **nome** e Olá Olá selecione **valor** na lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="822e0-124">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   * <span data-ttu-id="822e0-125">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="822e0-125">Click **Save.**</span></span> <span data-ttu-id="822e0-126">Você verá um novo atributo Olá na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="822e0-126">You see hello new attribute in hello table.</span></span>

9.  <span data-ttu-id="822e0-127">Salve a configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="822e0-127">Save hello configuration.</span></span>

<span data-ttu-id="822e0-128">Próxima vez que usuário Olá entra no aplicativo toohello, o AD do Azure enviar novo atributo de saudação em Olá resposta SAML.</span><span class="sxs-lookup"><span data-stu-id="822e0-128">Next time hello user signs in toohello application, Azure AD send hello new attribute in hello SAML response.</span></span>

## <a name="hello-application-expects-a-different-user-identifier-value-or-format"></a><span data-ttu-id="822e0-129">aplicativo Hello espera um valor de identificador de usuário diferente ou um formato</span><span class="sxs-lookup"><span data-stu-id="822e0-129">hello application expects a different User Identifier value or format</span></span>

<span data-ttu-id="822e0-130">aplicativo de entrada toohello Hello está falhando porque Olá resposta SAML tem atributos como funções ou porque o aplicativo hello está esperando um formato diferente para o atributo EntityID de saudação.</span><span class="sxs-lookup"><span data-stu-id="822e0-130">hello sign-in toohello application is failing because hello SAML response is missing attributes such as roles or because hello application is expecting a different format for hello EntityID attribute.</span></span>

## <a name="add-an-attribute-in-hello-azure-ad-application-configuration"></a><span data-ttu-id="822e0-131">Adicione um atributo na configuração de aplicativo do AD do Azure hello:</span><span class="sxs-lookup"><span data-stu-id="822e0-131">Add an attribute in hello Azure AD application configuration:</span></span>

<span data-ttu-id="822e0-132">Olá toochange valor de identificador de usuário, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="822e0-132">toochange hello User Identifier value, follow hello steps below:</span></span>

1.  <span data-ttu-id="822e0-133">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="822e0-133">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="822e0-134">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="822e0-134">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="822e0-135">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="822e0-135">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="822e0-136">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="822e0-136">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="822e0-137">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="822e0-137">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="822e0-138">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="822e0-138">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="822e0-139">Selecione aplicativo hello deseja tooconfigure-logon único.</span><span class="sxs-lookup"><span data-stu-id="822e0-139">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="822e0-140">Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="822e0-140">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="822e0-141">Em Olá **atributos de usuário**, selecione Olá identificador exclusivo para os usuários no hello **identificador de usuário** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="822e0-141">Under hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

## <a name="change-entityid-user-identifier-format"></a><span data-ttu-id="822e0-142">Alterar o formato EntityID (Identificador de Usuário)</span><span class="sxs-lookup"><span data-stu-id="822e0-142">Change EntityID (User Identifier) format</span></span>

<span data-ttu-id="822e0-143">Se o aplicativo hello espera outro formato para o atributo EntityID de saudação.</span><span class="sxs-lookup"><span data-stu-id="822e0-143">If hello application expects another format for hello EntityID attribute.</span></span> <span data-ttu-id="822e0-144">Em seguida, você não será tooselect capaz de formato de ID (identificador de usuário) de saudação AD do Azure envia toohello aplicativo em resposta Olá após a autenticação do usuário.</span><span class="sxs-lookup"><span data-stu-id="822e0-144">Then, you won’t be able tooselect hello EntityID (User Identifier) format that Azure AD sends toohello application in hello response after user authentication.</span></span>

<span data-ttu-id="822e0-145">Azure AD Olá selecione formato Olá NameID atributo (identificador de usuário) com base no valor de saudação selecionado ou Olá formato solicitado pelo aplicativo hello em Olá AuthRequest SAML.</span><span class="sxs-lookup"><span data-stu-id="822e0-145">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="822e0-146">Para obter mais informações, visite o artigo de saudação [protocolo SAML de logon único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) em Olá seção NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="822e0-146">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>

## <a name="hello-application-expects-a-different-signature-method-for-hello-saml-response"></a><span data-ttu-id="822e0-147">aplicativo Hello espera um método de assinatura diferente para Olá resposta SAML</span><span class="sxs-lookup"><span data-stu-id="822e0-147">hello application expects a different signature method for hello SAML response</span></span>

<span data-ttu-id="822e0-148">toochange quais partes do token SAML Olá são assinados digitalmente pelo Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="822e0-148">toochange what parts of hello SAML token are digitally signed by Azure Active Directory.</span></span> <span data-ttu-id="822e0-149">Siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="822e0-149">Follow hello steps below:</span></span>

1.  <span data-ttu-id="822e0-150">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="822e0-150">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="822e0-151">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="822e0-151">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="822e0-152">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="822e0-152">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="822e0-153">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="822e0-153">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="822e0-154">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="822e0-154">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="822e0-155">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="822e0-155">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="822e0-156">Selecione aplicativo hello deseja tooconfigure-logon único.</span><span class="sxs-lookup"><span data-stu-id="822e0-156">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="822e0-157">Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="822e0-157">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="822e0-158">Clique em **Mostrar configurações de assinatura de certificado avançadas** em Olá **o certificado de autenticação SAML** seção.</span><span class="sxs-lookup"><span data-stu-id="822e0-158">click **Show advanced certificate signing settings** under hello **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="822e0-159">Selecione Olá apropriado **opção assinatura** esperado pelo aplicativo hello:</span><span class="sxs-lookup"><span data-stu-id="822e0-159">Select hello appropriate **Signing Option** expected by hello application:</span></span>

  * <span data-ttu-id="822e0-160">Assinar resposta SAML</span><span class="sxs-lookup"><span data-stu-id="822e0-160">Sign SAML response</span></span>

  * <span data-ttu-id="822e0-161">Assinar resposta SAML e declaração</span><span class="sxs-lookup"><span data-stu-id="822e0-161">Sign SAML response and assertion</span></span>

  * <span data-ttu-id="822e0-162">Assinar declaração SAML</span><span class="sxs-lookup"><span data-stu-id="822e0-162">Sign SAML assertion</span></span>

<span data-ttu-id="822e0-163">Próxima vez que usuário Olá entra no aplicativo toohello, logon do AD do Azure Olá parte da resposta SAML Olá selecionada.</span><span class="sxs-lookup"><span data-stu-id="822e0-163">Next time hello user signs in toohello application, Azure AD sign hello part of hello SAML response selected.</span></span>

## <a name="hello-application-expects-hello-signing-algorithm-toobe-sha-1"></a><span data-ttu-id="822e0-164">aplicativo Hello espera Olá assinatura toobe algoritmo SHA-1</span><span class="sxs-lookup"><span data-stu-id="822e0-164">hello application expects hello signing algorithm toobe SHA-1</span></span>

<span data-ttu-id="822e0-165">Por padrão, o AD do Azure assina token SAML hello usando Olá algoritmo de segurança mais.</span><span class="sxs-lookup"><span data-stu-id="822e0-165">By default, Azure AD signs hello SAML token using hello most security algorithm.</span></span> <span data-ttu-id="822e0-166">Não é recomendável alterar o algoritmo de entrada hello tooSHA-1, a menos que exigido pelo aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="822e0-166">Changing hello sign algorithm tooSHA-1 is not recommended unless required by hello application.</span></span>

<span data-ttu-id="822e0-167">toochange Olá algoritmo de assinatura, execute as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="822e0-167">toochange hello signing algorithm, follow hello steps below:</span></span>

1.  <span data-ttu-id="822e0-168">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="822e0-168">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="822e0-169">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="822e0-169">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="822e0-170">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="822e0-170">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="822e0-171">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="822e0-171">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="822e0-172">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="822e0-172">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="822e0-173">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="822e0-173">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="822e0-174">Selecione aplicativo hello deseja tooconfigure-logon único.</span><span class="sxs-lookup"><span data-stu-id="822e0-174">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="822e0-175">Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="822e0-175">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="822e0-176">Clique em **Mostrar configurações de assinatura de certificado avançadas** em Olá **o certificado de autenticação SAML** seção.</span><span class="sxs-lookup"><span data-stu-id="822e0-176">click **Show advanced certificate signing settings** under hello **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="822e0-177">Selecione SHA-1, em Olá **algoritmo de assinatura**.</span><span class="sxs-lookup"><span data-stu-id="822e0-177">Select SHA-1, in hello **Signing Algorithm**.</span></span>

<span data-ttu-id="822e0-178">Próxima vez Olá usuário se autentica no aplicativo toohello, logon do AD do Azure Olá token SAML usando o algoritmo SHA-1.</span><span class="sxs-lookup"><span data-stu-id="822e0-178">Next time hello user signs in toohello application, Azure AD sign hello SAML token using SHA-1 algorithm.</span></span>

## <a name="next-steps"></a><span data-ttu-id="822e0-179">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="822e0-179">Next steps</span></span>
[<span data-ttu-id="822e0-180">Como toodebug baseado no SAML único logon tooapplications no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="822e0-180">How toodebug SAML-based single sign-on tooapplications in Azure Active Directory</span></span>](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging)
