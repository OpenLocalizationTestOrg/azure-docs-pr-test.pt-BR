---
title: Como usar o log de auditoria no Azure AD Privileged Identity Management | Microsoft Docs
description: "Saiba como usar o log de auditoria na extensão do Privileged Identity Management do Azure."
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
ms.openlocfilehash: 7d9a5255a64d46c1388d328a606b3f297d61262b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-audit-log-in-pim"></a><span data-ttu-id="df9cb-103">Usar o log de auditoria no PIM</span><span class="sxs-lookup"><span data-stu-id="df9cb-103">Using the audit log in PIM</span></span>
<span data-ttu-id="df9cb-104">Você pode usar o log de auditoria do PIM (Privileged Identity Management) para ver todas as ativações e atribuições de usuário dentro de um determinado período de tempo.</span><span class="sxs-lookup"><span data-stu-id="df9cb-104">You can use the Privileged Identity Management (PIM) audit log to see all the user assignments and activations within a given time period.</span></span> <span data-ttu-id="df9cb-105">Se você quiser ver o histórico completo de auditoria da atividade em seu locatário, incluindo o administrador, usuário final e atividade de sincronização, use os [Relatórios de acesso e uso do Azure Active Directory.](active-directory-view-access-usage-reports.md)</span><span class="sxs-lookup"><span data-stu-id="df9cb-105">If you want to see the full audit history of activity in your tenant, including administrator, end user, and synchronization activity, you can use the [Azure Active Directory access and usage reports.](active-directory-view-access-usage-reports.md)</span></span>

## <a name="navigate-to-the-audit-log"></a><span data-ttu-id="df9cb-106">Navegar até o log de auditoria</span><span class="sxs-lookup"><span data-stu-id="df9cb-106">Navigate to the audit log</span></span>
<span data-ttu-id="df9cb-107">No painel do [portal do Azure](https://portal.azure.com) , selecione o aplicativo **Azure AD Privileged Identity Management** .</span><span class="sxs-lookup"><span data-stu-id="df9cb-107">From the [Azure portal](https://portal.azure.com) dashboard, select the **Azure AD Privileged Identity Management** app.</span></span> <span data-ttu-id="df9cb-108">Aqui, acesse o log de auditoria clicando em **Gerenciar funções privilegiadas** > **Histórico de auditoria** no painel do PIM.</span><span class="sxs-lookup"><span data-stu-id="df9cb-108">From there, access the audit log by clicking **Manage privileged roles** > **Audit history** in the PIM dashboard.</span></span>

## <a name="the-audit-log-graph"></a><span data-ttu-id="df9cb-109">O gráfico do log de auditoria</span><span class="sxs-lookup"><span data-stu-id="df9cb-109">The audit log graph</span></span>
<span data-ttu-id="df9cb-110">Você pode usar o log de auditoria para exibir, em um gráfico de linha, o total de ativações, o número máximo de ativações diárias e a média diária de ativações.</span><span class="sxs-lookup"><span data-stu-id="df9cb-110">You can use the audit log to view the total activations, max activations per day, and average activations per day in a line graph.</span></span>  <span data-ttu-id="df9cb-111">Você também pode filtrar os dados por função se houver mais de uma função no histórico de auditoria.</span><span class="sxs-lookup"><span data-stu-id="df9cb-111">You can also filter the data by role if there is more than one role in the audit history.</span></span>

<span data-ttu-id="df9cb-112">Use os botões de **tempo**, **ação** e **função** para classificar o log.</span><span class="sxs-lookup"><span data-stu-id="df9cb-112">Use the **time**, **action**, and **role** buttons to sort the log.</span></span>

## <a name="the-audit-log-list"></a><span data-ttu-id="df9cb-113">A lista de logs de auditoria</span><span class="sxs-lookup"><span data-stu-id="df9cb-113">The audit log list</span></span>
<span data-ttu-id="df9cb-114">As colunas na lista de logs de auditoria são:</span><span class="sxs-lookup"><span data-stu-id="df9cb-114">The columns in the audit log list are:</span></span>

* <span data-ttu-id="df9cb-115">**Solicitante** : o usuário que solicitou a ativação ou alteração da função.</span><span class="sxs-lookup"><span data-stu-id="df9cb-115">**Requestor** - the user who requested the role activation or change.</span></span>  <span data-ttu-id="df9cb-116">Se o valor for "Sistema Azure", verifique o log de auditoria do Azure para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="df9cb-116">If the value is "Azure System", check the Azure audit log for more information.</span></span>
* <span data-ttu-id="df9cb-117">**Usuário** : o usuário que está ativando ou está atribuído a uma função.</span><span class="sxs-lookup"><span data-stu-id="df9cb-117">**User** - the user who is activating or assigned to a role.</span></span>
* <span data-ttu-id="df9cb-118">**Função** : a função atribuída ou ativada pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="df9cb-118">**Role** - the role assigned or activated by the user.</span></span>
* <span data-ttu-id="df9cb-119">**Ação** : as ações tomadas pelo solicitante.</span><span class="sxs-lookup"><span data-stu-id="df9cb-119">**Action** - the actions taken by the requestor.</span></span> <span data-ttu-id="df9cb-120">Isso pode incluir a atribuição, o cancelamento da atribuição, a ativação ou a desativação.</span><span class="sxs-lookup"><span data-stu-id="df9cb-120">This can include assignment, unassignment, activation, or deactivation.</span></span>
* <span data-ttu-id="df9cb-121">**Tempo** - quando a ação aconteceu.</span><span class="sxs-lookup"><span data-stu-id="df9cb-121">**Time** - when the action occurred.</span></span>
* <span data-ttu-id="df9cb-122">**Raciocínio** -se qualquer texto foi digitado no campo de motivo durante a ativação, ele será mostrado aqui.</span><span class="sxs-lookup"><span data-stu-id="df9cb-122">**Reasoning** - if any text was entered into the reason field during activation, it will show up here.</span></span>
* <span data-ttu-id="df9cb-123">**Expiração** : relevante apenas para a ativação de funções.</span><span class="sxs-lookup"><span data-stu-id="df9cb-123">**Expiration** - only relevant for activation of roles.</span></span>

## <a name="filter-the-audit-log"></a><span data-ttu-id="df9cb-124">Filtrar o log de auditoria</span><span class="sxs-lookup"><span data-stu-id="df9cb-124">Filter the audit log</span></span>
<span data-ttu-id="df9cb-125">Você pode filtrar as informações que aparecem no log de auditoria clicando no botão **Filtrar** .</span><span class="sxs-lookup"><span data-stu-id="df9cb-125">You can filter the information that shows up in the audit log by clicking the **Filter** button.</span></span>  <span data-ttu-id="df9cb-126">A **folha Atualizar parâmetros do gráfico** será exibida.</span><span class="sxs-lookup"><span data-stu-id="df9cb-126">The **Update chart parameters blade** will appear.</span></span>

<span data-ttu-id="df9cb-127">Depois de definir os filtros, clique em **Atualizar** para filtrar os dados no log.</span><span class="sxs-lookup"><span data-stu-id="df9cb-127">After you set the filters, click **Update** to filter the data in the log.</span></span>  <span data-ttu-id="df9cb-128">Se os dados não aparecerem imediatamente, atualize a página.</span><span class="sxs-lookup"><span data-stu-id="df9cb-128">If the data doesn't appear right away, refresh the page.</span></span>

### <a name="change-the-date-range"></a><span data-ttu-id="df9cb-129">Alterar o intervalo de data</span><span class="sxs-lookup"><span data-stu-id="df9cb-129">Change the date range</span></span>
<span data-ttu-id="df9cb-130">Use os botões **Hoje**, **Última semana**, **Mês Passado** ou **Personalizar** para alterar o intervalo de tempo do log de auditoria.</span><span class="sxs-lookup"><span data-stu-id="df9cb-130">Use the **Today**, **Past Week**, **Past Month**, or **Custom** buttons to change the time range of the audit log.</span></span>

<span data-ttu-id="df9cb-131">Quando você escolher o botão **Personalizar**, terá um campo de data **De** e um campo de data **Até** para especificar um intervalo de datas para o log.</span><span class="sxs-lookup"><span data-stu-id="df9cb-131">When you choose the **Custom** button, you will be given a **From** date field and a **To** date field to specify a range of dates for the log.</span></span>  <span data-ttu-id="df9cb-132">Você pode digitar as datas no formato DD/MM/AAAA, ou clique no ícone **calendário** e escolha a data em um calendário.</span><span class="sxs-lookup"><span data-stu-id="df9cb-132">You can either enter the dates in MM/DD/YYYY format or click on the **calendar** icon and choose the date from a calendar.</span></span>

### <a name="change-the-roles-included-in-the-log"></a><span data-ttu-id="df9cb-133">Alterar as funções incluídas no log</span><span class="sxs-lookup"><span data-stu-id="df9cb-133">Change the roles included in the log</span></span>
<span data-ttu-id="df9cb-134">Marque ou desmarque a caixa de seleção **Função** ao lado de cada função para incluí-la ou excluí-la do log.</span><span class="sxs-lookup"><span data-stu-id="df9cb-134">Check or uncheck the **Role** checkbox next to each role to include or exclude it from the log.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="df9cb-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="df9cb-135">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

