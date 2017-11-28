---
title: aaaProblem usando o acesso do aplicativo de autoatendimento | Microsoft Docs
description: "Solucionar problemas de acesso do aplicativo de serviço tooself relacionada de problemas"
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
ms.reviewer: japere
ms.openlocfilehash: 2487be1df191a4e7fd0bcc0ebbe4ea62fae0fd5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-using-self-service-application-access"></a><span data-ttu-id="bd322-103">Problema ao usar o acesso de aplicativo de autoatendimento</span><span class="sxs-lookup"><span data-stu-id="bd322-103">Problem using self-service application access</span></span>

<span data-ttu-id="bd322-104">Acesso de aplicativo de autoatendimento é tooself de usuários de tooallow uma ótima maneira-descobrir aplicativos, se desejar permitir Olá business grupo tooapprove acesso toothose aplicativos.</span><span class="sxs-lookup"><span data-stu-id="bd322-104">Self-service application access is a great way tooallow users tooself-discover applications, optionally allow hello business group tooapprove access toothose applications.</span></span> <span data-ttu-id="bd322-105">Você pode permitir credenciais de Olá Olá business grupo toomanage atribuído toothose usuários para a direita da senha de logon único em aplicativos de seus painéis de acesso.</span><span class="sxs-lookup"><span data-stu-id="bd322-105">You can allow hello business group toomanage hello credentials assigned toothose users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="bd322-106">Antes dos usuários podem descobrir automaticamente aplicativos do seu painel de acesso, é necessário tooenable **acesso de aplicativo de autoatendimento** tooany aplicativos que você deseja tooallow usuários tooself-descobrir e solicitar acesso a.</span><span class="sxs-lookup"><span data-stu-id="bd322-106">Before your users can self-discover applications from their access panel, you need tooenable **Self-service application access** tooany applications that you wish tooallow users tooself-discover and request access to.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="bd322-107">Geral emite toocheck primeiro</span><span class="sxs-lookup"><span data-stu-id="bd322-107">General issues toocheck first</span></span>

-   <span data-ttu-id="bd322-108">Verifique se o acesso do aplicativo de autoatendimento está configurado corretamente.</span><span class="sxs-lookup"><span data-stu-id="bd322-108">Make sure self-service application access is configured correctly.</span></span> <span data-ttu-id="bd322-109">Consulte "Como acessar o aplicativo de autoatendimento tooconfigure".</span><span class="sxs-lookup"><span data-stu-id="bd322-109">See “How tooconfigure self-service application access”.</span></span>

-   <span data-ttu-id="bd322-110">Certifique-se de saudação usuário ou grupo tiver sido habilitado toorequest acesso ao aplicativo de autoatendimento.</span><span class="sxs-lookup"><span data-stu-id="bd322-110">Make sure hello user or group has been enabled toorequest self-service application access.</span></span>

-   <span data-ttu-id="bd322-111">Verifique se o usuário hello está visitando o local correto de saudação para acesso ao aplicativo de autoatendimento.</span><span class="sxs-lookup"><span data-stu-id="bd322-111">Make sure hello user is visiting hello correct place for self-service application access.</span></span> <span data-ttu-id="bd322-112">os usuários podem navegar tootheir [painel de acesso do aplicativo](https://myapps.microsoft.com/) e clique em Olá **+ adicionar** botão toofind Olá aplicativos toowhich você habilitou o acesso de autoatendimento.</span><span class="sxs-lookup"><span data-stu-id="bd322-112">users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled self-service access.</span></span>

-   <span data-ttu-id="bd322-113">Se o acesso de aplicativo de autoatendimento foi configurado recentemente, tente toosign e sair novamente no painel de acesso do usuário Olá após toosee de alguns minutos se as alterações de acesso de autoatendimento Olá apareceu.</span><span class="sxs-lookup"><span data-stu-id="bd322-113">If self-service application access was just recently configured, try toosign in and out again into hello user’s Access Panel after a few minutes toosee if hello self-service access changes have appeared.</span></span>

## <a name="how-tooconfigure-self-service-application-access"></a><span data-ttu-id="bd322-114">Como acessar o aplicativo de autoatendimento tooconfigure</span><span class="sxs-lookup"><span data-stu-id="bd322-114">How tooconfigure self-service application access</span></span>

<span data-ttu-id="bd322-115">tooenable autoatendimento acesso tooan aplicativo, siga Olá etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="bd322-115">tooenable self-service application access tooan application, follow hello steps below:</span></span>

1.  <span data-ttu-id="bd322-116">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="bd322-116">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="bd322-117">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="bd322-117">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bd322-118">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="bd322-118">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bd322-119">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="bd322-119">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="bd322-120">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="bd322-120">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="bd322-121">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="bd322-121">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="bd322-122">Selecione o aplicativo hello tooenable acesso de autoatendimento toofrom Olá lista.</span><span class="sxs-lookup"><span data-stu-id="bd322-122">Select hello application you want tooenable Self-service access toofrom hello list.</span></span>

7.  <span data-ttu-id="bd322-123">Depois que o aplicativo hello carrega, clique em **autoatendimento** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="bd322-123">Once hello application loads, click **Self-service** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="bd322-124">tooenable acesso de aplicativo de autoatendimento para este aplicativo, ativar Olá **permitir que os usuários aplicativos de toothis acesso toorequest?** alternar muito**Sim.**</span><span class="sxs-lookup"><span data-stu-id="bd322-124">tooenable Self-service application access for this application, turn hello **Allow users toorequest access toothis application?** toggle too**Yes.**</span></span>

9.  <span data-ttu-id="bd322-125">Em seguida, tooselect Olá toowhich os usuários do grupo que solicitam acesso toothis aplicativo deve ser adicionado, clique em rótulo Olá seletor de Avançar toohello **toowhich grupo devem ser atribuídas usuários adicionados?** e selecione um grupo.</span><span class="sxs-lookup"><span data-stu-id="bd322-125">Next, tooselect hello group toowhich users who request access toothis application should be added, click hello selector next toohello label **toowhich group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="bd322-126">**Opcional:** se desejar toorequire uma aprovação de negócios antes que os usuários têm permissão de acesso, definir Olá **exigir aprovação antes de conceder acesso toothis aplicativo?** alternar muito**Sim**.</span><span class="sxs-lookup"><span data-stu-id="bd322-126">**Optional:** If you wish toorequire a business approval before users are allowed access, set hello **Require approval before granting access toothis application?** toggle too**Yes**.</span></span>

11. <span data-ttu-id="bd322-127">**Opcional: para aplicativos usando a senha de logon único no somente** se desejar tooallow esses negócios aprovadores toospecify Olá as senhas que são enviadas toothis aplicativo para usuários aprovados, defina Olá **permitir que os aprovadores tooset senhas do usuário para este aplicativo?**  alternar muito**Sim**.</span><span class="sxs-lookup"><span data-stu-id="bd322-127">**Optional: For applications using password single-sign on only,** if you wish tooallow those business approvers toospecify hello passwords that are sent toothis application for approved users, set hello **Allow approvers tooset user’s passwords for this application?** toggle too**Yes**.</span></span>

12. <span data-ttu-id="bd322-128">**Opcional:** toospecify Olá business aprovadores são permitidos tooapprove aplicativos de toothis de acesso, clique em rótulo Olá seletor de Avançar toohello **quem tem permissão de aplicativo de toothis tooapprove access?** tooselect backup too10 aprovadores de negócio individuais.</span><span class="sxs-lookup"><span data-stu-id="bd322-128">**Optional:** toospecify hello business approvers who are allowed tooapprove access toothis application, click hello selector next toohello label **Who is allowed tooapprove access toothis application?** tooselect up too10 individual business approvers.</span></span>

 >[!NOTE]
 > <span data-ttu-id="bd322-129">Não há suporte para grupos.</span><span class="sxs-lookup"><span data-stu-id="bd322-129">Groups are not supported.</span></span>
 >
 >

13. <span data-ttu-id="bd322-130">**Opcional:** **para aplicativos que expõem as funções**, se desejar tooa função tooassign autoatendimento usuários aprovados clique Olá seletor próximo toohello **função toowhich devem ser atribuídos aos usuários nesta aplicativo?**  tooselect Olá função toowhich esses usuários devem ser atribuídos.</span><span class="sxs-lookup"><span data-stu-id="bd322-130">**Optional:** **For applications which expose roles**, if you wish tooassign self-service approved users tooa role, click hello selector next toohello **toowhich role should users be assigned in this application?** tooselect hello role toowhich these users should be assigned.</span></span>

14. <span data-ttu-id="bd322-131">Clique em Olá **salvar** botão na parte superior de saudação do hello toofinish de folha.</span><span class="sxs-lookup"><span data-stu-id="bd322-131">Click hello **Save** button at hello top of hello blade toofinish.</span></span>

<span data-ttu-id="bd322-132">Depois de concluir a configuração do aplicativo de autoatendimento, os usuários podem navegar tootheir [painel de acesso do aplicativo](https://myapps.microsoft.com/) e clique em Olá **+ adicionar** botão toofind Olá aplicativos toowhich você habilitou Acesso de autoatendimento.</span><span class="sxs-lookup"><span data-stu-id="bd322-132">Once you complete Self-service application configuration, users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled Self-service access.</span></span> <span data-ttu-id="bd322-133">Aprovadores de negócios também recebem uma notificação em seu [Painel de Acesso do Aplicativo](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="bd322-133">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="bd322-134">Você pode habilitar um email notificando-os quando um usuário solicitou o aplicativo de tooan de acesso que requer sua aprovação.</span><span class="sxs-lookup"><span data-stu-id="bd322-134">You can enable an email notifying them when a user has requested access tooan application that requires their approval.</span></span> 

<span data-ttu-id="bd322-135">Suportam a essas aprovações única aprovação fluxos de trabalho, que significa que, se você especificar vários aprovadores, qualquer aprovador único pode aprovar acesso toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bd322-135">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approve access toohello application.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a><span data-ttu-id="bd322-136">Se essas etapas de solução de problemas não resolver o problema de saudação</span><span class="sxs-lookup"><span data-stu-id="bd322-136">If these troubleshooting steps do not resolve hello issue</span></span> 

<span data-ttu-id="bd322-137">Abra um tíquete de suporte com hello informações a seguir se disponíveis:</span><span class="sxs-lookup"><span data-stu-id="bd322-137">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="bd322-138">ID de erro de correlação</span><span class="sxs-lookup"><span data-stu-id="bd322-138">Correlation error ID</span></span>

-   <span data-ttu-id="bd322-139">UPN (endereço de email de usuário)</span><span class="sxs-lookup"><span data-stu-id="bd322-139">UPN (user email address)</span></span>

-   <span data-ttu-id="bd322-140">TenantID</span><span class="sxs-lookup"><span data-stu-id="bd322-140">TenantID</span></span>

-   <span data-ttu-id="bd322-141">Tipo de navegador</span><span class="sxs-lookup"><span data-stu-id="bd322-141">Browser type</span></span>

-   <span data-ttu-id="bd322-142">Fuso horário e hora/cronograma durante o erro</span><span class="sxs-lookup"><span data-stu-id="bd322-142">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="bd322-143">Rastreamentos do Fiddler</span><span class="sxs-lookup"><span data-stu-id="bd322-143">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd322-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bd322-144">Next steps</span></span>
[<span data-ttu-id="bd322-145">Configuração do Azure Active Directory para gerenciamento de grupo de autoatendimento</span><span class="sxs-lookup"><span data-stu-id="bd322-145">Setting up Azure Active Directory for self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
