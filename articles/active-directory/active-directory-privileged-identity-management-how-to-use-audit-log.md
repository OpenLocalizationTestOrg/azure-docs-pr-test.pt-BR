---
title: "log de auditoria de saudação do aaaHow toouse no Azure AD Privileged Identity Management | Microsoft Docs"
description: "Saiba como log de auditoria de saudação de toouse na extensão do hello Privileged Identity Management do Azure."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 5d13a6dd-1fcb-4e76-82fb-cb2f4f0e4357
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 36987eaab9fe02c5dd7b4f4705e487299430745d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-audit-log-in-pim"></a><span data-ttu-id="486e9-103">Usando o log de auditoria Olá PIM</span><span class="sxs-lookup"><span data-stu-id="486e9-103">Using hello audit log in PIM</span></span>
<span data-ttu-id="486e9-104">Você pode usar toosee de log de auditoria de gerenciamento de identidade com privilégios (PIM) Olá todas as atribuições de saudação do usuário e ativações dentro de um determinado período de tempo.</span><span class="sxs-lookup"><span data-stu-id="486e9-104">You can use hello Privileged Identity Management (PIM) audit log toosee all hello user assignments and activations within a given time period.</span></span> <span data-ttu-id="486e9-105">Se você quiser toosee histórico de auditoria completa Olá da atividade em seu locatário, incluindo o administrador, o usuário final e a atividade de sincronização, você pode usar o hello [relatórios de acesso e uso do Active Directory do Azure.](active-directory-view-access-usage-reports.md)</span><span class="sxs-lookup"><span data-stu-id="486e9-105">If you want toosee hello full audit history of activity in your tenant, including administrator, end user, and synchronization activity, you can use hello [Azure Active Directory access and usage reports.](active-directory-view-access-usage-reports.md)</span></span>

## <a name="navigate-toohello-audit-log"></a><span data-ttu-id="486e9-106">Navegue toohello log de auditoria</span><span class="sxs-lookup"><span data-stu-id="486e9-106">Navigate toohello audit log</span></span>
<span data-ttu-id="486e9-107">De saudação [portal do Azure](https://portal.azure.com) dashboard, selecione Olá **do Azure AD Privileged Identity Management** aplicativo.</span><span class="sxs-lookup"><span data-stu-id="486e9-107">From hello [Azure portal](https://portal.azure.com) dashboard, select hello **Azure AD Privileged Identity Management** app.</span></span> <span data-ttu-id="486e9-108">A partir daí, acessar o log de auditoria Olá clicando **gerenciar funções privilegiadas** > **histórico de auditoria** no painel PIM hello.</span><span class="sxs-lookup"><span data-stu-id="486e9-108">From there, access hello audit log by clicking **Manage privileged roles** > **Audit history** in hello PIM dashboard.</span></span>

## <a name="hello-audit-log-graph"></a><span data-ttu-id="486e9-109">gráfico de log de auditoria de saudação</span><span class="sxs-lookup"><span data-stu-id="486e9-109">hello audit log graph</span></span>
<span data-ttu-id="486e9-110">Você pode usar o hello audit log tooview Olá total de ativações, ativações máx por dia e ativações médias por dia em um gráfico de linha.</span><span class="sxs-lookup"><span data-stu-id="486e9-110">You can use hello audit log tooview hello total activations, max activations per day, and average activations per day in a line graph.</span></span>  <span data-ttu-id="486e9-111">Você também pode filtrar dados saudação pela função se houver mais de uma função no histórico de auditoria de saudação.</span><span class="sxs-lookup"><span data-stu-id="486e9-111">You can also filter hello data by role if there is more than one role in hello audit history.</span></span>

<span data-ttu-id="486e9-112">Saudação de uso **tempo**, **ação**, e **função** botões toosort Olá log.</span><span class="sxs-lookup"><span data-stu-id="486e9-112">Use hello **time**, **action**, and **role** buttons toosort hello log.</span></span>

## <a name="hello-audit-log-list"></a><span data-ttu-id="486e9-113">lista de log de auditoria de saudação</span><span class="sxs-lookup"><span data-stu-id="486e9-113">hello audit log list</span></span>
<span data-ttu-id="486e9-114">Olá colunas na lista de log de auditoria de saudação são:</span><span class="sxs-lookup"><span data-stu-id="486e9-114">hello columns in hello audit log list are:</span></span>

* <span data-ttu-id="486e9-115">**Solicitante** -usuário Olá que solicitou a ativação da função hello ou alterar.</span><span class="sxs-lookup"><span data-stu-id="486e9-115">**Requestor** - hello user who requested hello role activation or change.</span></span>  <span data-ttu-id="486e9-116">Se o valor de saudação é "Azure sistema", verifique o log de auditoria do Azure de saudação para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="486e9-116">If hello value is "Azure System", check hello Azure audit log for more information.</span></span>
* <span data-ttu-id="486e9-117">**Usuário** -usuário Olá que está sendo ativado ou tooa função atribuída.</span><span class="sxs-lookup"><span data-stu-id="486e9-117">**User** - hello user who is activating or assigned tooa role.</span></span>
* <span data-ttu-id="486e9-118">**Função** -função hello atribuídos ou ativado pelo usuário hello.</span><span class="sxs-lookup"><span data-stu-id="486e9-118">**Role** - hello role assigned or activated by hello user.</span></span>
* <span data-ttu-id="486e9-119">**Ação** - ações de saudação solicitante hello.</span><span class="sxs-lookup"><span data-stu-id="486e9-119">**Action** - hello actions taken by hello requestor.</span></span> <span data-ttu-id="486e9-120">Isso pode incluir a atribuição, o cancelamento da atribuição, a ativação ou a desativação.</span><span class="sxs-lookup"><span data-stu-id="486e9-120">This can include assignment, unassignment, activation, or deactivation.</span></span>
* <span data-ttu-id="486e9-121">**Tempo** - quando a ação de saudação ocorreu.</span><span class="sxs-lookup"><span data-stu-id="486e9-121">**Time** - when hello action occurred.</span></span>
* <span data-ttu-id="486e9-122">**Raciocínio** -se que qualquer texto foi inserido no campo de razão de saudação durante a ativação, ele aparecerá aqui.</span><span class="sxs-lookup"><span data-stu-id="486e9-122">**Reasoning** - if any text was entered into hello reason field during activation, it will show up here.</span></span>
* <span data-ttu-id="486e9-123">**Expiração** : relevante apenas para a ativação de funções.</span><span class="sxs-lookup"><span data-stu-id="486e9-123">**Expiration** - only relevant for activation of roles.</span></span>

## <a name="filter-hello-audit-log"></a><span data-ttu-id="486e9-124">Log de auditoria de saudação do filtro</span><span class="sxs-lookup"><span data-stu-id="486e9-124">Filter hello audit log</span></span>
<span data-ttu-id="486e9-125">Você pode filtrar as informações de saudação que aparece no log de auditoria Olá clicando Olá **filtro** botão.</span><span class="sxs-lookup"><span data-stu-id="486e9-125">You can filter hello information that shows up in hello audit log by clicking hello **Filter** button.</span></span>  <span data-ttu-id="486e9-126">Olá **folha de parâmetros de gráfico de atualização** será exibida.</span><span class="sxs-lookup"><span data-stu-id="486e9-126">hello **Update chart parameters blade** will appear.</span></span>

<span data-ttu-id="486e9-127">Depois de definir filtros de saudação, clique em **atualização** dados de saudação toofilter no log de saudação.</span><span class="sxs-lookup"><span data-stu-id="486e9-127">After you set hello filters, click **Update** toofilter hello data in hello log.</span></span>  <span data-ttu-id="486e9-128">Se dados saudação não aparecem imediatamente, atualize a página de saudação.</span><span class="sxs-lookup"><span data-stu-id="486e9-128">If hello data doesn't appear right away, refresh hello page.</span></span>

### <a name="change-hello-date-range"></a><span data-ttu-id="486e9-129">Alterar o intervalo de datas Olá</span><span class="sxs-lookup"><span data-stu-id="486e9-129">Change hello date range</span></span>
<span data-ttu-id="486e9-130">Saudação de uso **hoje**, **semana passada**, **último mês**, ou **personalizado** botões toochange intervalo de tempo de saudação do log de auditoria de saudação.</span><span class="sxs-lookup"><span data-stu-id="486e9-130">Use hello **Today**, **Past Week**, **Past Month**, or **Custom** buttons toochange hello time range of hello audit log.</span></span>

<span data-ttu-id="486e9-131">Quando você escolhe Olá **personalizado** botão, você terá um **de** campo de data e um **para** toospecify campo um intervalo de datas para o log de saudação de data.</span><span class="sxs-lookup"><span data-stu-id="486e9-131">When you choose hello **Custom** button, you will be given a **From** date field and a **To** date field toospecify a range of dates for hello log.</span></span>  <span data-ttu-id="486e9-132">Você pode inserir datas de saudação no formato DD/MM/AAAA ou clique em Olá **calendário** ícone e escolha a data de saudação de um calendário.</span><span class="sxs-lookup"><span data-stu-id="486e9-132">You can either enter hello dates in MM/DD/YYYY format or click on hello **calendar** icon and choose hello date from a calendar.</span></span>

### <a name="change-hello-roles-included-in-hello-log"></a><span data-ttu-id="486e9-133">Alterar funções hello incluídas no log de saudação</span><span class="sxs-lookup"><span data-stu-id="486e9-133">Change hello roles included in hello log</span></span>
<span data-ttu-id="486e9-134">Marque ou desmarque Olá **função** caixa de seleção próxima tooeach função tooinclude ou exclusão de saudação de log.</span><span class="sxs-lookup"><span data-stu-id="486e9-134">Check or uncheck hello **Role** checkbox next tooeach role tooinclude or exclude it from hello log.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="486e9-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="486e9-135">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

