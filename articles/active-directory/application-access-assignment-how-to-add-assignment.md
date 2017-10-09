---
title: "aplicativo de tooan aaaHow tooassign usuários e grupos | Microsoft Docs"
description: "Atribuir usuários toohello aplicativo toogrant acesso"
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
ms.openlocfilehash: e039a26e4b8f88ad747354859f1071b8f74b6789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooassign-users-and-groups-tooan-application"></a><span data-ttu-id="95487-103">Como aplicativos de tooan de usuários e grupos tooassign</span><span class="sxs-lookup"><span data-stu-id="95487-103">How tooassign users and groups tooan application</span></span>

<span data-ttu-id="95487-104">Antes dos usuários podem fazer qualquer Olá abaixo de um aplicativo específico, você precisa toofirst **atribuí-los toohello aplicativo** toogrant a eles acesso:</span><span class="sxs-lookup"><span data-stu-id="95487-104">Before your users can do any of hello below for a specific application, you need toofirst **assign them toohello application** toogrant them access:</span></span>

-   <span data-ttu-id="95487-105">Acessar um aplicativo por **navegar diretamente o URL do aplicativo toohello** (também conhecido como iniciado por SP logon).</span><span class="sxs-lookup"><span data-stu-id="95487-105">Access an application by **navigating toohello application’s URL directly** (also known as SP-initiated sign-on).</span></span>

-   <span data-ttu-id="95487-106">Acessar um aplicativo usando Olá **URL de acesso do usuário** em um aplicativo **propriedades** página (também conhecido como iniciado pelo IDP logon).</span><span class="sxs-lookup"><span data-stu-id="95487-106">Access an application by using hello **User Access URL** on an application’s **Properties** page (also known as IDP-initiated sign on).</span></span>

-   <span data-ttu-id="95487-107">Ver um aplicativo em seu [Painel de Acesso do Aplicativo](https://myapps.microsoft.com/) ou aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="95487-107">See an application appear on their [Application Access Panel](https://myapps.microsoft.com/) or mobile application.</span></span>

-   <span data-ttu-id="95487-108">Ver um aplicativo em seu [Inicializador de Aplicativos do Office 365](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a).</span><span class="sxs-lookup"><span data-stu-id="95487-108">See an application appear on their [Office 365 Application Launcher](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a).</span></span>

## <a name="methods-tooassign-applications-with-azure-active-directory"></a><span data-ttu-id="95487-109">Aplicativos de tooassign de métodos com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="95487-109">Methods tooassign applications with Azure Active Directory</span></span> 

<span data-ttu-id="95487-110">Há três formas de atribuir aplicativos com o Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="95487-110">There are 3 ways you can assign applications with Azure Active Directory:</span></span>

-   [<span data-ttu-id="95487-111">Atribuir um usuário diretamente tooan aplicativo como um administrador</span><span class="sxs-lookup"><span data-stu-id="95487-111">Assign a user directly tooan application as an administrator</span></span>](#assign-a-user-directly-as-an-administrator)

-   [<span data-ttu-id="95487-112">Atribua um grupo diretamente tooan aplicativo como um administrador</span><span class="sxs-lookup"><span data-stu-id="95487-112">Assign a group directly tooan application as an administrator</span></span>](#assign-a-group-directly-to-an-application-as-an-administrator)

-   [<span data-ttu-id="95487-113">Habilitar o aplicativo de autoatendimento acesso tooallow usuários toofind seus próprios aplicativos</span><span class="sxs-lookup"><span data-stu-id="95487-113">Enable self-service application access tooallow users toofind their own applications</span></span>](#enable-self-service-application-access-to-allow-users-to-find-their-own-applications)

## <a name="assign-a-user-directly-as-an-administrator"></a><span data-ttu-id="95487-114">Atribuir um usuário diretamente como administrador</span><span class="sxs-lookup"><span data-stu-id="95487-114">Assign a user directly as an administrator</span></span>

<span data-ttu-id="95487-115">tooassign um ou mais aplicativos de tooan usuários diretamente, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="95487-115">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="95487-116">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="95487-116">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="95487-117">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="95487-117">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="95487-118">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="95487-118">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="95487-119">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="95487-119">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="95487-120">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="95487-120">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="95487-121">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="95487-121">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="95487-122">Selecione o aplicativo hello deseja tooassign uma lista de saudação do usuário toofrom.</span><span class="sxs-lookup"><span data-stu-id="95487-122">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="95487-123">Depois que o aplicativo hello carrega, clique em **usuários e grupos** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="95487-123">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="95487-124">Clique Olá **adicionar** botão na parte superior Olá **usuários e grupos** Olá de tooopen lista **Adicionar atribuição** folha.</span><span class="sxs-lookup"><span data-stu-id="95487-124">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="95487-125">Clique em Olá **usuários e grupos** seletor de saudação **Adicionar atribuição** folha.</span><span class="sxs-lookup"><span data-stu-id="95487-125">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="95487-126">Tipo de saudação **nome completo** ou **endereço de email** do usuário Olá que lhe interessam atribuindo em Olá **pesquisar por nome ou endereço de email** caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="95487-126">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="95487-127">Passe o mouse sobre Olá **usuário** em Olá lista tooreveal um **caixa de seleção**.</span><span class="sxs-lookup"><span data-stu-id="95487-127">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="95487-128">Clique em tooadd de foto ou logotipo de perfil do Olá caixa de seleção próxima toohello usuário seu usuário toohello **selecionados** lista.</span><span class="sxs-lookup"><span data-stu-id="95487-128">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="95487-129">**Opcional:** se você gostaria que muito**adicionar mais de um usuário**, tipo em outro **nome completo** ou **endereço de email** em Olá **pesquisar por nome endereço de email ou** caixa de pesquisa e, em seguida, clique em tooadd de caixa de seleção Olá esse usuário toohello **selecionados** lista.</span><span class="sxs-lookup"><span data-stu-id="95487-129">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="95487-130">Quando você terminar de selecionar usuários, clique em Olá **selecione** botão tooadd-los toohello lista de usuários e grupos toobe atribuído toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="95487-130">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="95487-131">**Opcional:** clique Olá **Selecionar função** seletor de saudação **Adicionar atribuição** folha tooselect uma função tooassign toohello usuários selecionados.</span><span class="sxs-lookup"><span data-stu-id="95487-131">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="95487-132">Clique em Olá **atribuir** botão tooassign Olá aplicativo toohello selecionado de usuários.</span><span class="sxs-lookup"><span data-stu-id="95487-132">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="95487-133">Após um curto período de tempo, usuários de saudação selecionado ser capaz de toolaunch esses aplicativos usando Olá métodos descritos na seção de descrição de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="95487-133">After a short period of time, hello users you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span>

## <a name="assign-a-group-directly-tooan-application-as-an-administrator"></a><span data-ttu-id="95487-134">Atribua um grupo diretamente tooan aplicativo como um administrador</span><span class="sxs-lookup"><span data-stu-id="95487-134">Assign a group directly tooan application as an administrator</span></span>

<span data-ttu-id="95487-135">tooassign um ou mais grupos de aplicativo tooan diretamente, siga Olá etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="95487-135">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="95487-136">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="95487-136">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="95487-137">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="95487-137">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="95487-138">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="95487-138">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="95487-139">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="95487-139">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="95487-140">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="95487-140">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="95487-141">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="95487-141">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="95487-142">Selecione o aplicativo hello deseja tooassign uma lista de saudação do usuário toofrom.</span><span class="sxs-lookup"><span data-stu-id="95487-142">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="95487-143">Depois que o aplicativo hello carrega, clique em **usuários e grupos** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="95487-143">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="95487-144">Clique Olá **adicionar** botão na parte superior Olá **usuários e grupos** Olá de tooopen lista **Adicionar atribuição** folha.</span><span class="sxs-lookup"><span data-stu-id="95487-144">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="95487-145">Clique em Olá **usuários e grupos** seletor de saudação **Adicionar atribuição** folha.</span><span class="sxs-lookup"><span data-stu-id="95487-145">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="95487-146">Tipo de saudação **nome completo do grupo** do grupo de saudação que lhe interessam atribuindo em Olá **pesquisar por nome ou endereço de email** caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="95487-146">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="95487-147">Passe o mouse sobre Olá **grupo** em Olá lista tooreveal um **caixa de seleção**.</span><span class="sxs-lookup"><span data-stu-id="95487-147">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="95487-148">Clique em tooadd de foto ou logotipo de perfil do Olá caixa de seleção próxima toohello grupo seu usuário toohello **selecionados** lista.</span><span class="sxs-lookup"><span data-stu-id="95487-148">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="95487-149">**Opcional:** se você gostaria que muito**adicionar mais de um grupo**, tipo em outro **nome completo do grupo** em Olá **pesquisar por nome ou endereço de email** caixa de pesquisa e clique em tooadd de caixa de seleção Olá esse grupo toohello **selecionados** lista.</span><span class="sxs-lookup"><span data-stu-id="95487-149">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="95487-150">Quando você terminar de selecionar os grupos, clique em Olá **selecione** botão tooadd-los toohello lista de usuários e grupos toobe atribuído toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="95487-150">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="95487-151">**Opcional:** clique Olá **Selecionar função** seletor de saudação **Adicionar atribuição** folha tooselect toohello de tooassign uma função grupos selecionados.</span><span class="sxs-lookup"><span data-stu-id="95487-151">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="95487-152">Clique em Olá **atribuir** grupos selecionados do botão tooassign Olá aplicativo toohello.</span><span class="sxs-lookup"><span data-stu-id="95487-152">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="95487-153">Após um curto período de tempo, usuários hello dentro de grupos de saudação selecionado ser capaz de toolaunch esses aplicativos usando Olá métodos descritos na seção de descrição de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="95487-153">After a short period of time, hello users within hello groups you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span> <span data-ttu-id="95487-154">Se esses grupos forem dinâmicos, pode haver algum atraso de processamento adicional nessas atribuições que aparecem para os usuários nesses grupos atribuídos.</span><span class="sxs-lookup"><span data-stu-id="95487-154">If these are dynamic groups, there may be some additional processing delay in these assignments appearing for users within these assigned groups.</span></span>

## <a name="enable-self-service-application-access-tooallow-users-toofind-their-own-applications"></a><span data-ttu-id="95487-155">Habilitar o aplicativo de autoatendimento acesso tooallow usuários toofind seus próprios aplicativos</span><span class="sxs-lookup"><span data-stu-id="95487-155">Enable self-service application access tooallow users toofind their own applications</span></span>

<span data-ttu-id="95487-156">Acesso de aplicativo de autoatendimento é tooself de usuários de tooallow uma ótima maneira-descobrir aplicativos, se desejar permitir Olá business grupo tooapprove acesso toothose aplicativos.</span><span class="sxs-lookup"><span data-stu-id="95487-156">Self-service application access is a great way tooallow users tooself-discover applications, optionally allow hello business group tooapprove access toothose applications.</span></span> <span data-ttu-id="95487-157">Você pode permitir credenciais de Olá Olá business grupo toomanage atribuído toothose usuários para a direita da senha de logon único em aplicativos de seus painéis de acesso.</span><span class="sxs-lookup"><span data-stu-id="95487-157">You can allow hello business group toomanage hello credentials assigned toothose users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="95487-158">tooenable autoatendimento acesso tooan aplicativo, siga Olá etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="95487-158">tooenable self-service application access tooan application, follow hello steps below:</span></span>

1.  <span data-ttu-id="95487-159">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="95487-159">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="95487-160">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="95487-160">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="95487-161">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="95487-161">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="95487-162">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="95487-162">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="95487-163">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="95487-163">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="95487-164">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="95487-164">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="95487-165">Selecione o aplicativo hello tooenable acesso de autoatendimento toofrom Olá lista.</span><span class="sxs-lookup"><span data-stu-id="95487-165">Select hello application you want tooenable Self-service access toofrom hello list.</span></span>

7.  <span data-ttu-id="95487-166">Depois que o aplicativo hello carrega, clique em **autoatendimento** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="95487-166">Once hello application loads, click **Self-service** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="95487-167">tooenable acesso de aplicativo de autoatendimento para este aplicativo, ativar Olá **permitir que os usuários aplicativos de toothis acesso toorequest?** alternar muito**Sim.**</span><span class="sxs-lookup"><span data-stu-id="95487-167">tooenable Self-service application access for this application, turn hello **Allow users toorequest access toothis application?** toggle too**Yes.**</span></span>

9.  <span data-ttu-id="95487-168">Em seguida, tooselect Olá toowhich os usuários do grupo que solicitam acesso toothis aplicativo deve ser adicionado, clique em rótulo Olá seletor de Avançar toohello **toowhich grupo devem ser atribuídas usuários adicionados?** e selecione um grupo.</span><span class="sxs-lookup"><span data-stu-id="95487-168">Next, tooselect hello group toowhich users who request access toothis application should be added, click hello selector next toohello label **toowhich group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="95487-169">**Opcional:** se desejar toorequire uma aprovação de negócios antes que os usuários têm permissão de acesso, definir Olá **exigir aprovação antes de conceder acesso toothis aplicativo?** alternar muito**Sim**.</span><span class="sxs-lookup"><span data-stu-id="95487-169">**Optional:** If you wish toorequire a business approval before users are allowed access, set hello **Require approval before granting access toothis application?** toggle too**Yes**.</span></span>

11. <span data-ttu-id="95487-170">**Opcional: para aplicativos usando a senha de logon único no somente** se desejar tooallow esses negócios aprovadores toospecify Olá as senhas que são enviadas toothis aplicativo para usuários aprovados, defina Olá **permitir que os aprovadores tooset senhas do usuário para este aplicativo?**  alternar muito**Sim**.</span><span class="sxs-lookup"><span data-stu-id="95487-170">**Optional: For applications using password single-sign on only,** if you wish tooallow those business approvers toospecify hello passwords that are sent toothis application for approved users, set hello **Allow approvers tooset user’s passwords for this application?** toggle too**Yes**.</span></span>

12. <span data-ttu-id="95487-171">**Opcional:** toospecify Olá business aprovadores são permitidos tooapprove aplicativos de toothis de acesso, clique em rótulo Olá seletor de Avançar toohello **quem tem permissão de aplicativo de toothis tooapprove access?** tooselect backup too10 aprovadores de negócio individuais.</span><span class="sxs-lookup"><span data-stu-id="95487-171">**Optional:** toospecify hello business approvers who are allowed tooapprove access toothis application, click hello selector next toohello label **Who is allowed tooapprove access toothis application?** tooselect up too10 individual business approvers.</span></span>

  >[!NOTE]
  ><span data-ttu-id="95487-172">Não há suporte para grupos.</span><span class="sxs-lookup"><span data-stu-id="95487-172">Groups are not supported.</span></span>
  >
  >

13. <span data-ttu-id="95487-173">**Opcional:** **para aplicativos que expõem as funções**, se desejar tooa função tooassign autoatendimento usuários aprovados clique Olá seletor próximo toohello **função toowhich devem ser atribuídos aos usuários nesta aplicativo?**  tooselect Olá função toowhich esses usuários devem ser atribuídos.</span><span class="sxs-lookup"><span data-stu-id="95487-173">**Optional:** **For applications which expose roles**, if you wish tooassign self-service approved users tooa role, click hello selector next toohello **toowhich role should users be assigned in this application?** tooselect hello role toowhich these users should be assigned.</span></span>

14. <span data-ttu-id="95487-174">Clique em Olá **salvar** botão na parte superior de saudação do hello toofinish de folha.</span><span class="sxs-lookup"><span data-stu-id="95487-174">Click hello **Save** button at hello top of hello blade toofinish.</span></span>

<span data-ttu-id="95487-175">Depois de concluir a configuração do aplicativo de autoatendimento, os usuários podem navegar tootheir [painel de acesso do aplicativo](https://myapps.microsoft.com/) e clique em Olá **+ adicionar** botão toofind Olá aplicativos toowhich você habilitou Acesso de autoatendimento.</span><span class="sxs-lookup"><span data-stu-id="95487-175">Once you complete Self-service application configuration, users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled Self-service access.</span></span> <span data-ttu-id="95487-176">Aprovadores de negócios também recebem uma notificação em seu [Painel de Acesso do Aplicativo](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="95487-176">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="95487-177">Você pode habilitar um email notificando-os quando um usuário solicitou o aplicativo de tooan de acesso que requer sua aprovação.</span><span class="sxs-lookup"><span data-stu-id="95487-177">You can enable an email notifying them when a user has requested access tooan application that requires their approval.</span></span> 

<span data-ttu-id="95487-178">Essas aprovações oferecem suporte a fluxos de trabalho de aprovação único apenas, indicando que se você especificar vários aprovadores, qualquer aprovador único aplicativo de toohello aprovador access.</span><span class="sxs-lookup"><span data-stu-id="95487-178">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approver access toohello application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="95487-179">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="95487-179">Next steps</span></span>
[<span data-ttu-id="95487-180">Fornecer aplicativos de tooyour de logon único com o Proxy de aplicativo</span><span class="sxs-lookup"><span data-stu-id="95487-180">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
