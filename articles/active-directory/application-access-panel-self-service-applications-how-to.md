---
title: acesso de aplicativo de autoatendimento toouse aaaHow | Microsoft Docs
description: "Habilitar o aplicativo de autoatendimento acesso tooallow usuários toofind seus próprios aplicativos"
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
ms.openlocfilehash: 03a44c20d544a6232fa802bcffaf70e5030ad3ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-self-service-application-access"></a><span data-ttu-id="f904b-103">Como acessar o aplicativo de autoatendimento toouse</span><span class="sxs-lookup"><span data-stu-id="f904b-103">How toouse self-service application access</span></span>

<span data-ttu-id="f904b-104">Antes dos usuários podem descobrir automaticamente aplicativos do seu painel de acesso, é necessário tooenable **acesso de aplicativo de autoatendimento** tooany aplicativos que você deseja tooallow usuários tooself-descobrir e solicitar acesso a.</span><span class="sxs-lookup"><span data-stu-id="f904b-104">Before your users can self-discover applications from their access panel, you need tooenable **Self-service application access** tooany applications that you wish tooallow users tooself-discover and request access to.</span></span>

<span data-ttu-id="f904b-105">Esse recurso é uma ótima maneira de toosave tempo e dinheiro como um grupo de TI e é altamente recomendável como parte de uma implantação de aplicativos modernos com o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="f904b-105">This feature is a great way for you toosave time and money as an IT group, and is highly recommended as part of a modern applications deployment with Azure Active Directory.</span></span>

<span data-ttu-id="f904b-106">Usando esse recurso, você pode:</span><span class="sxs-lookup"><span data-stu-id="f904b-106">Using this feature, you can:</span></span>

-   <span data-ttu-id="f904b-107">Permitir que os usuários a descobrir automaticamente os aplicativos de saudação [painel de acesso do aplicativo](https://myapps.microsoft.com/) sem incomodar Olá IT grupo.</span><span class="sxs-lookup"><span data-stu-id="f904b-107">Let users self-discover applications from hello [Application Access Panel](https://myapps.microsoft.com/) without bothering hello IT group.</span></span>

-   <span data-ttu-id="f904b-108">Adicione esses grupo pré-configurado de tooa de usuários para que possa ver quem tem acesso solicitado, remover o acesso e gerenciar funções hello atribuídas toothem.</span><span class="sxs-lookup"><span data-stu-id="f904b-108">Add those users tooa pre-configured group so you can see who has requested access, remove access, and manage hello roles assigned toothem.</span></span>

-   <span data-ttu-id="f904b-109">Se desejar permitir um aprovador de negócios tooapprove solicitações de acesso de aplicativo Olá, equipe de TI precisa.</span><span class="sxs-lookup"><span data-stu-id="f904b-109">Optionally allow a business approver tooapprove application access requests so hello IT group doesn’t have to.</span></span>

-   <span data-ttu-id="f904b-110">Configure opcionalmente os indivíduos too10 que podem aprovar acesso toothis aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f904b-110">Optionally configure up too10 individuals who may approve access toothis application.</span></span>

-   <span data-ttu-id="f904b-111">Permitir opcionalmente um aprovador business senhas de saudação tooset esses usuários poderão usar toosign no aplicativo toohello, à direita do aprovador de negócios Olá [painel de acesso do aplicativo](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="f904b-111">Optionally allow a business approver tooset hello passwords those users can use toosign in toohello application, right from hello business approver’s [Application Access Panel](https://myapps.microsoft.com/).</span></span>

-   <span data-ttu-id="f904b-112">Opcionalmente, automaticamente atribua a função de aplicativo de tooan de autoatendimento usuários atribuídos diretamente.</span><span class="sxs-lookup"><span data-stu-id="f904b-112">Optionally automatically assign self-service assigned users tooan application role directly.</span></span>

## <a name="enable-self-service-application-access-tooallow-users-toofind-their-own-applications"></a><span data-ttu-id="f904b-113">Habilitar o aplicativo de autoatendimento acesso tooallow usuários toofind seus próprios aplicativos</span><span class="sxs-lookup"><span data-stu-id="f904b-113">Enable self-service application access tooallow users toofind their own applications</span></span>

<span data-ttu-id="f904b-114">Acesso de aplicativo de autoatendimento é tooself de usuários de tooallow uma ótima maneira-descobrir aplicativos, se desejar permitir Olá business grupo tooapprove acesso toothose aplicativos.</span><span class="sxs-lookup"><span data-stu-id="f904b-114">Self-service application access is a great way tooallow users tooself-discover applications, optionally allow hello business group tooapprove access toothose applications.</span></span> <span data-ttu-id="f904b-115">Você pode permitir credenciais de Olá Olá business grupo toomanage atribuído toothose usuários para a direita da senha de logon único em aplicativos de seus painéis de acesso.</span><span class="sxs-lookup"><span data-stu-id="f904b-115">You can allow hello business group toomanage hello credentials assigned toothose users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="f904b-116">tooenable autoatendimento acesso tooan aplicativo, siga Olá etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="f904b-116">tooenable self-service application access tooan application, follow hello steps below:</span></span>

1.  <span data-ttu-id="f904b-117">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="f904b-117">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="f904b-118">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="f904b-118">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f904b-119">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="f904b-119">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f904b-120">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="f904b-120">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="f904b-121">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="f904b-121">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="f904b-122">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="f904b-122">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="f904b-123">Selecione o aplicativo hello tooenable acesso de autoatendimento toofrom Olá lista.</span><span class="sxs-lookup"><span data-stu-id="f904b-123">Select hello application you want tooenable Self-service access toofrom hello list.</span></span>

7.  <span data-ttu-id="f904b-124">Depois que o aplicativo hello carrega, clique em **autoatendimento** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="f904b-124">Once hello application loads, click **Self-service** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="f904b-125">tooenable acesso de aplicativo de autoatendimento para este aplicativo, ativar Olá **permitir que os usuários aplicativos de toothis acesso toorequest?** alternar muito**Sim.**</span><span class="sxs-lookup"><span data-stu-id="f904b-125">tooenable Self-service application access for this application, turn hello **Allow users toorequest access toothis application?** toggle too**Yes.**</span></span>

9.  <span data-ttu-id="f904b-126">Em seguida, tooselect Olá toowhich os usuários do grupo que solicitam acesso toothis aplicativo deve ser adicionado, clique em rótulo Olá seletor de Avançar toohello **toowhich grupo devem ser atribuídas usuários adicionados?** e selecione um grupo.</span><span class="sxs-lookup"><span data-stu-id="f904b-126">Next, tooselect hello group toowhich users who request access toothis application should be added, click hello selector next toohello label **toowhich group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="f904b-127">**Opcional:** se desejar toorequire uma aprovação de negócios antes que os usuários têm permissão de acesso, definir Olá **exigir aprovação antes de conceder acesso toothis aplicativo?** alternar muito**Sim**.</span><span class="sxs-lookup"><span data-stu-id="f904b-127">**Optional:** If you wish toorequire a business approval before users are allowed access, set hello **Require approval before granting access toothis application?** toggle too**Yes**.</span></span>

11. <span data-ttu-id="f904b-128">**Opcional: para aplicativos usando a senha de logon único no somente** se desejar tooallow esses negócios aprovadores toospecify Olá as senhas que são enviadas toothis aplicativo para usuários aprovados, defina Olá **permitir que os aprovadores tooset senhas do usuário para este aplicativo?**  alternar muito**Sim**.</span><span class="sxs-lookup"><span data-stu-id="f904b-128">**Optional: For applications using password single-sign on only,** if you wish tooallow those business approvers toospecify hello passwords that are sent toothis application for approved users, set hello **Allow approvers tooset user’s passwords for this application?** toggle too**Yes**.</span></span>

12. <span data-ttu-id="f904b-129">**Opcional:** toospecify Olá business aprovadores são permitidos tooapprove aplicativos de toothis de acesso, clique em rótulo Olá seletor de Avançar toohello **quem tem permissão de aplicativo de toothis tooapprove access?** tooselect backup too10 aprovadores de negócio individuais.</span><span class="sxs-lookup"><span data-stu-id="f904b-129">**Optional:** toospecify hello business approvers who are allowed tooapprove access toothis application, click hello selector next toohello label **Who is allowed tooapprove access toothis application?** tooselect up too10 individual business approvers.</span></span>

   * <span data-ttu-id="f904b-130">Não há suporte para grupos.</span><span class="sxs-lookup"><span data-stu-id="f904b-130">Groups are not supported.</span></span>

13. <span data-ttu-id="f904b-131">**Opcional:** **para aplicativos que expõem as funções**, se desejar tooa função tooassign autoatendimento usuários aprovados clique Olá seletor próximo toohello **função toowhich devem ser atribuídos aos usuários nesta aplicativo?**  tooselect Olá função toowhich esses usuários devem ser atribuídos.</span><span class="sxs-lookup"><span data-stu-id="f904b-131">**Optional:** **For applications which expose roles**, if you wish tooassign self-service approved users tooa role, click hello selector next toohello **toowhich role should users be assigned in this application?** tooselect hello role toowhich these users should be assigned.</span></span>

14. <span data-ttu-id="f904b-132">Clique em Olá **salvar** botão na parte superior de saudação do hello toofinish de folha.</span><span class="sxs-lookup"><span data-stu-id="f904b-132">Click hello **Save** button at hello top of hello blade toofinish.</span></span>

<span data-ttu-id="f904b-133">Depois de concluir a configuração do aplicativo de autoatendimento, os usuários podem navegar tootheir [painel de acesso do aplicativo](https://myapps.microsoft.com/) e clique em Olá **+ adicionar** botão toofind Olá aplicativos toowhich você habilitou Acesso de autoatendimento.</span><span class="sxs-lookup"><span data-stu-id="f904b-133">Once you complete Self-service application configuration, users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled Self-service access.</span></span> <span data-ttu-id="f904b-134">Aprovadores de negócios também recebem uma notificação em seu [Painel de Acesso do Aplicativo](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="f904b-134">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="f904b-135">Você pode habilitar um email notificando-os quando um usuário solicitou o aplicativo de tooan de acesso que requer sua aprovação.</span><span class="sxs-lookup"><span data-stu-id="f904b-135">You can enable an email notifying them when a user has requested access tooan application that requires their approval.</span></span> 

<span data-ttu-id="f904b-136">Suportam a essas aprovações única aprovação fluxos de trabalho, que significa que, se você especificar vários aprovadores, qualquer aprovador único pode aprovar acesso toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f904b-136">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approve access toohello application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f904b-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f904b-137">Next steps</span></span>
[<span data-ttu-id="f904b-138">Configuração do Azure Active Directory para gerenciamento de grupo de autoatendimento</span><span class="sxs-lookup"><span data-stu-id="f904b-138">Setting up Azure Active Directory for self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
